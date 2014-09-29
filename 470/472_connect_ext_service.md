##TUTORIAL #2: CONNECT THE WAREHOUSE APP WITH AN EXTERNAL SERVICE##

 

Force.com offers several ways to integrate with external systems. For example, without writing any code, you can declare workflow rules that send outbound messages. You can implement more complex scenarios programmatically with Apex code.

This tutorial teaches you how to create a Web service callout to integrate the Warehouse app with the fulfillment application you deployed in Tutorial 1. This fulfillment system, written in Java, is hosted on Heroku, but it could be any application with a Web service interface.

The following diagram illustrates the example scenario requirements: when an invoice’s status changes to Closed in your Force.com system, the system sends a JSON-formatted message to the order fulfillment service running on Heroku, which then returns an order ID to the Force.com system. The order ID is then added to the invoice.

###Step 1: Create an External ID Field on Invoice###

To start, create a custom field in the invoice custom object that can store the order ID returned by the Java app running on Heroku. The field is an index into an external system, so it makes sense to make it an External ID.

1. Log in to your Salesforce organization. 
2. Go to the Invoice Statement custom object from Setup by clicking **Create **&gt; **Objects **&gt; **Invoice**. 
3. Scroll down to **Custom Fields & Relationships**, and then click **New**. 
4. Select the **Text **field type, and then click **Next**. 
5. Enter **_OrderId _**as the field label, and then enter **_6 _**as the field length. Accept the default field name **_OrderId_**. 
6. Select the **External ID **checkbox, and then click **Next**. 
7. Click **Next **to accept the defaults, and then click **Save**. 

###Step 2: Create a Remote Site Record###

The Force.com platform implements very conservative security controls. By default, Force.com prohibits callouts to external sites. This step teaches you how to register the Heroku Java site in the Remote Site Settings page.

1. From Setup, click **Security Controls **&gt; **Remote Site Settings**. 
2. Click **New Remote Site**. 
3. In the Remote Site Name field, enter **_FulfillmentWebService _**(no spaces). 
4. In the Remote Site URL field, enter **_https://{appname}.herokuapp.com_**. 
5. Click **Save **to accept the remaining default values. 

Now any Apex code in your app can call the fulfillment Web service that you deployed in Tutorial 1.

Tell Me More...

Just for fun, you can delete this remote site record and create and test the callout in Step 3 and Step 4 below to observe the error message that is generated when an app attempts to call a URL without permission. Don’t forget to come back and add the remote site record again, though!

###Step 3: Create an Integration Apex Class###

Now that your app can access an external URL, it's time to implement the callout. Apex triggers are not permitted to make synchronous Web service calls. This restriction ensures that a long-running Web service doesn’t hold a lock on a record within your Force.com app.

The steps in this tutorial teach you how to build out the correct approach, which is to create an Apex class with an asynchronous method that uses the @future annotation, and then build a trigger to call the method as necessary. When the trigger calls the asynchronous method, Force.com queues the call, executes the trigger, and then releases any record locks. Eventually, when the asynchronous call reaches the top of the queue, Force.com executes the call and posts the invoice to the order fulfillment Web service running on Heroku.

Start by adding the code for the asynchronous method in a new Apex class.

1. From Setup, click **Develop **&gt; **Apex Classes**. 
2. Click **New **and paste in the following code: 

public class Integration {

    // The ExternalOrder class holds a string and integer

    // received from the external fulfillment system.

    public class ExternalOrder {

        public String id {get; set;}

        public Integer order_number {get; set;}

}

    // The postOrder method integrates the local Force.com invoicing system

    // with a remote fulfillment system; specifically, by posting data about

    // closed orders to the remote system. Functionally, the method 1) prepares

    // JSON-formatted data to send to the remote service, 2) makes an HTTP call

    // to send the prepared data to the remote service, and then 3) processes

    // any JSON-formatted data returned by the remote service to update the

    // local Invoices with the corresponding external IDs in the remote system.

    @future (callout=true) // indicates that this is an asynchronous call

    public static void postOrder(List&lt;Id&gt; invoiceIds) {

        // 1) see above

        // Create a JSON generator object

        JSONGenerator gen = JSON.createGenerator(true);

Step 3: Create an Integration Apex Class

// open the JSON generator

gen.writeStartArray();

// interate through the list of invoices passed in to the call

// writing each invoice ID to the array

for (Id invoiceId : invoiceIds) {

    gen.writeStartObject();

    gen.writeStringField('id', invoiceId);

    gen.writeEndObject();

}

// close the JSON generator

gen.writeEndArray();

// create a string from the JSON generator

String jsonOrders = gen.getAsString();

// debugging call, which you can check in debug logs

System.debug('jsonOrders: ' + jsonOrders);

// 2) see above

// create an HTTPrequest object

HttpRequest req = new HttpRequest();

// set up the HTTP request with a method, endpoint, header, and body

req.setMethod('POST');

// DON'T FORGET TO UPDATE THE FOLLOWING LINE WITH YOUR APP NAME

req.setEndpoint('https://{appname}.herokuapp.com/order');

req.setHeader('Content-Type', 'application/json');

req.setBody(jsonOrders);

// create a new HTTP object

Http http = new Http();

// create a new HTTP response for receiving the remote response

// then use it to send the configured HTTPrequest

HTTPResponse res = http.send(req);

// debugging call, which you can check in debug logs

System.debug('Fulfillment service returned '+ res.getBody());

// 3) see above

// Examine the status code from the HTTPResponse

// If status code != 200, write debugging information, done

if (res.getStatusCode() != 200) {

    System.debug('Error from ' + req.getEndpoint() + ' : ' +

      res.getStatusCode() + ' ' + res.getStatus());

}

// If status code = 200, update each Invoice

// with the external ID returned by the fulfillment service.

else {

    // Retrieve all of the Invoice records

    // originally passed into the method call to prep for update.

    List&lt;Invoice__c&gt; invoices =

      [SELECT Id FROM Invoice__c WHERE Id IN :invoiceIds];

    // Create a list of external orders by deserializing the

    // JSON data returned by the fulfillment service.

    List&lt;ExternalOrder&gt; orders =

      (List&lt;ExternalOrder&gt;)JSON.deserialize(res.getBody(),

        List&lt;ExternalOrder&gt;.class);

} }

    // Create a map of Invoice IDs from the retrieved

    // invoices list.

    Map&lt;Id, Invoice__c&gt; invoiceMap =

      new Map&lt;Id, Invoice__c&gt;(invoices);

    // Update the order numbers in the invoices

    for ( ExternalOrder order : orders ) {

      Invoice__c invoice = invoiceMap.get(order.id);

      invoice.OrderId__c = String.valueOf(order.order_number);

    }

    // Update all invoices in the database with a bulk update

    update invoices;

}

Don’t forget to replace _{appname} _with your Heroku application name. 
**3. **Click **Save**.

This code collects the necessary data for the remote service, makes the remote service HTTP call, and processes any data returned by the remote service to update local invoices with the corresponding external IDs. See the embedded comments in the code for details.

Step 4: Test the **@future **Method  
Before creating a trigger that calls an @future method, it’s best practice to interactively test the method by itself and validate that

the remote site settings are correctly configured. To test the method interactively, you can use the Developer Console.

1. Go to the Developer Console by clicking **_Your Name _**&gt; **Developer Console**. 
2. Click **Debug **&gt; **Open Execute Anonymous Window**, and then enter the following code. This small snippet of Apex code retrieves the ID for a single invoice and calls your **@future **method using this ID. 
3. Select the **Open Log **checkbox. 
4. Click **Execute**. You should see two entries in the logs at the bottom of the page. Double click the second line — it should have **Future Handler **as its operation and a status of **Success**. 

// Get an Invoice__c for testing

Invoice__c invoice = [SELECT ID FROM Invoice__c LIMIT 1];

// Call the postOrder method to test the asynchronous call

Integration.postOrder(new List&lt;Id&gt;{invoice.id});

**5. **Select the **Filter **checkbox under the Execution Log, above the Logs list, and then type _DEBUG _as the filter text. Scroll down and double click the last line of the execution log. You should see a popup window with the response from the fulfillment Web service that looks something like:

Now that you have a functional @future method that can call the fulfillment Web service, it's time to tie things together with a trigger. 

Step 5: Create a Trigger to Call the **@future **Method

To create a trigger on the invoice object that calls the Integration.postOrder method that was created in Step 3, complete the following steps:

1. Go to the invoice custom object from Setup by clicking **Create **&gt; **Objects **&gt; **Invoice**. 
2. Scroll down to **Triggers**, click **New**, and then paste the following code in place of the trigger skeleton: 

   

08:08:42:962 USER_DEBUG [58]|DEBUG|Fulfillment service returned

[{"order_number":2,"id":"a01E0000009RpppIAC"}]

 

trigger HandleOrderUpdate on Invoice__c (after update) {

    // Create a map of IDs to all of the *old* versions of records

    // updated by the call that fires the trigger.

    Map&lt;ID, Invoice__c&gt; oldMap =    new Map&lt;ID,

    Invoice__c&gt;(Trigger.old);

    // Create an empty list of IDs

    List&lt;Id&gt; invoiceIds = new List&lt;Id&gt;();

    // Iterate through all of the *new* versions of Invoice__c

    // records updated by the call that fires the trigger, adding

    // corresponding IDs to the invoiceIds list, but *only* when an

    // invoice's status changed from a non-"Closed" value to "Closed".

    for (Invoice__c invoice: Trigger.new) {

        if (invoice.status__c == 'Closed' &&  oldMap.get(invoice.Id).status__c !=

'Closed'){

            invoiceIds.add(invoice.Id);

        }

    }

    // If the list of IDs is not empty, call Integration.postOrder

    // supplying the list of IDs for fulfillment.

    if (invoiceIds.size() &gt; 0) {

        Integration.postOrder(invoiceIds);

    }

}

**3. **Click **Save**.

The comments in the code explain what the code does. In particular, understand that Force.com triggers must be able to handle both single-row and bulk updates because of the varying types of calls that can fire them (single-row or bulk update calls). The trigger creates a list of invoice IDs that have been closed in this update, and then calls the @future method once, passing the list of IDs.

Step 6: Test the Complete Integration Path

With the trigger in place, test the integration by firing the trigger.

1. Select the Warehouse app. 
2. Click the **Invoices **tab. 
3. Click one of the recent invoices and notice that there is no OrderId for the invoice. 
4. If the Status is already Closed, double-click the word **Closed**, change it to **Open **and click **Save**. 
5. Double-click the **Status **value, change it to **Closed **and click **Save**. This triggers the asynchronous callout. 
6. Wait a few seconds and refresh the page in the browser. 
7. You should see an external order ID appear in the **OrderId **field. 

The following screen shows the Invoices tab before any changes have been made:

The following screen shows the Invoices tab after the asynchronous call has returned the new order ID:

Summary

Congratulations! Your app is sending invoices for fulfillment. You have successfully created an asynchronous Apex class that posted invoice details to your fulfillment app hosted on Heroku. Of course, your external application could reside anywhere as long as you have access via Web services. Your class uses open standards including JSON and REST to transmit data, and a trigger on invoices to execute the process.
