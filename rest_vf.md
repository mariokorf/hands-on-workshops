#Building REST APIs with Apex

## Introduction

The fictional warehouse company we have previously built an app for wants to enable an API to allow resellers to use their warehouse. 
- They want to be able to get the number of items in stock for a particular piece of merchandise given its ID
- They want to be able to create an invoice for a particular piece of merchandise 
- They want to be able to delete a non-closed invoice

In this workshop you'll learn how to use Workbench and the REST Explorer to implement the GET, POST and DELETE verbs that correspond to the above scenarios. 

## Step 1 - Install the Warehouse App
Rather than build the app from scratch you can install a package that contains a pre-built Warehous app. 

7. Log into your DE org and then click the installation URL link: [https://login.salesforce.com/packaging/installPackage.apexp?p0=04ti0000000Pj8s](https://login.salesforce.com/packaging/installPackage.apexp?p0=04ti0000000Pj8s)
9. On the Package Installation Details page, click **Continue**.
10. Follow the instructions to install the pacakge. 
13. Once the installation completes, you can select the Warehouse app from the app picker in the upper right corner. Select the app.
14. Click the **Data** tab.
15. Click **Create Data**.

## Step 2 - Create a Class and the GET Method for the Web Service

Resellers need to be able to get the number of items in stock for a particular piece of merchandise given its ID. You do this by creating a GET method. 

1. Open the developer console by clicking your name in the top right hand corner of the screen and selecting **Developer Console**.
2. Create a new class by going to **File > New > Apex Class**. 
3. Name the class "WarehouseService".
3. Enter the following code to create the get method:

```Apex
@RestResource(urlmapping='/warehouse/*')
global class WarehouseService {
	@HttpGet
    global static Integer getAvailableMerchandise() {
        RestRequest req = RestContext.request;
		String merchId = req.requestURI.substring(req.requestURI.lastIndexOf('/')+1);
        Merchandise__c merch = [SELECT Id, Quantity__c FROM Merchandise__c WHERE Id = :merchId];
        if(merch != null) {
            return Integer.valueOf(merch.Quantity__c);
        }
        
        return 0;
    }
}
```
4. Select **File > Save** the file.
5. In the Merchanise tab of the Salesforce window select an item of merchandise and copy its Id.
6. In a new browser tab, navigate to [http://workbench.developerforce.com/restExplorer.php](http://workbench.developerforce.com/restExplorer.php)
7. Select "Developer Account" and API v 31. 
8. Click the checkbox to accept the terms and login using your Salesforce developer org credentials.
7. In the **Jump to** dropdown list, select REST Explorer and click **Select**.
8. In the input text area enter */services/apexrest/warehouse/{merchandiseId}* replacing the *{merchandiseId}* text with your merchandise Id you just retrieved.
9. Click **Execute** and a number should be returned (click the "Show Raw Response" link to view the number in a more readable format).

## Step 3 - Add the POST Method
Your company also wants resellers to be able to create an invoice for a particular piece of merchandise (merchandise ID and quantity). You can do this with a POST method. 

1. In the class you previously created, add the following code and save as before.
```Apex
@HttpPost
global static Id createNewInvoice(Id merchandiseId, Integer quantity) {
  Invoice__c inv = new Invoice__c();
  insert inv;
  Line_Item__c line = new Line_Item__c();
  line.Merchandise__c = merchandiseId;
  line.Quantity__c = quantity;
  line.Name = 'Line 1';
  line.Invoice__c = inv.Id;
  insert line;
  return inv.Id;
}
```
2. In the REST Explorer, select the **POST** checkbox and change the input area to be "/services/apexrest/warehouse/"
3. In the Request Body area enter:
```JSON
{"merchandiseId":"XXXXXX", "quantity":2}
```
and replace the XXXXXX with your merchandise Id (keeping it enclosed in quotes to form valid JSON).
4. Click **Execute**.
5. Click **Show Raw Response** and see that an Invoice Id has been returned which you can view in the browser.
6. Copy this Invoice Id.

## Step 4 - Add the DELETE Method
Finally, you resellers to have a way to delete a non-closed invoice. You do this with a DELETE method. 

1. In the WarehouseService class add the method code below:
```Apex
@HttpDelete
global static boolean deleteInvoice() {
  RestRequest req = RestContext.request;
  String invoiceId = req.requestURI.substring(req.requestURI.lastIndexOf('/')+1);
  Invoice__c inv = [SELECT Status__c, Id FROM Invoice__c WHERE Id = :invoiceId];
  if(inv.Status__c != 'Closed') {
    delete inv;
    return true;
  }
  return false;
}
```
2. In the REST Explorer select the **DELETE** checkbox and update the input area to be '/services/apexrest/warehouse/{invoiceId}' updating the {invoiceId} to be the Id of the invoice from before (or any invoice).
3. Click **Execute**.
4. Click **Show Raw Response** and see that a message of "true" is returned informing you that the invoice has been successfully deleted.

## Step 5 - Further Exercies 
You have now created a RESTful web service in Apex that uses 3 of the verbs; GET, POST and DELETE. You have tested that the code works using the REST Explorer tool and can see how you can allow customers to connect to your applications. 

Now try the following on your own:
- Create a method using PUT or PATCH to update a non-closed Invoice.
- Add error handling to the code and ensure that the "RestResponse" object is updated to return the correct status code.
- Write test methods for the code using the RestRequest and RestResponse objects in the RestContext system class instance.
