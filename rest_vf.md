#Building REST APIs with apex - letting others connect with your app

## Introduction
Begin with [slide deck here](https://docs.google.com/presentation/d/1-Gi56q7fealscnT7kD6fiGkBX--mh31hZ5Cu2A-3DHg/edit?usp=sharing) to obtain an overview of REST and see some comapnies who have used APIs to grow their business by integrating with Salesforce.com - you can do the same growing outwards as well. 

The warehousing company we have previously built an app for want to enable an API to allow resellers to use their warehouse
- They want to be able to get the number of items in stock for a particular piece of merchandise given its ID
- They want to be able to create an invoice for a particular piece of merchandise (merchandise ID and quantity)
- They want to be able to delete a non-closed invoice

## Step 1 - Sign Up for Developer Edition & Install the Warehouse App
These instructions are designed to be used with a Developer Edition organization, or DE org for short. DE orgs are multipurpose environments with all of the features and permissions that allow you to develop, package, test, and install apps.

1. In your browser, go to https://developer.salesforce.com/signup.
2. Fill in the fields about you and your company.
3. In the Email Address field, make sure to use a public address you can easily check from a Web browser.
4. Type a unique Username. Note that this field is also in the form of an email address, but it does not have to be the same as your email address, and in fact, itâ€™s usually better if they arenâ€™t the same. Your username is your login and your identity on developer.salesforce.com, so youâ€™re often better served by choosing a username such as firstname@lastname.com.
5. Read and then select the checkbox for the Master Subscription Agreement and then click Submit Registration.
6. In a moment youâ€™ll receive an email with a login link. Click the link and change your password.
7. Click the installation URL link: [https://login.salesforce.com/packaging/installPackage.apexp?p0=04ti0000000Pj8s](https://login.salesforce.com/packaging/installPackage.apexp?p0=04ti0000000Pj8s)
8. If you arenâ€™t logged in already, enter the username and password of your DE org.
9. On the Package Installation Details page, click Continue.
10. Click Next, and on the Security Level page click Next.
11. Click Install.
12. Click Deploy Now and then Deploy.
13. Once the installation completes, you can select the Warehouse app from the app picker in the upper right corner. Select the app.
14. Click the Data tab.
15. Click Create Data.

## Step 2 - Create a Class and the GET Method for the Web Service

1. Open the developer console by clicking your name in the top right hand corner of the screen and selecting "Developer Console"
2. Create a new class by going to File Ã¢â€ ' New Ã¢â€ ' Apex Class and entering "WarehouseService"
3. Enter the following code to create our get method:

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
4. Goto File Ã¢â€ ' Save to save the file in it's current format.
5. In the Merchanise tab of the Salesforce window select an item of merchandise and copy its Id.
6. In a new browser tab, navigate to http://workbench.developerforce.com/restExplorer.php, select "Developer Account" and API v 31, click the checkbox to accept the terms and login using your Salesforce developer org credentials.
7. Once Authenticated, if not already in the REST Explorer, select this option in the "Jump to" dropdown list and press the "Select" button.
8. In the input text area enter '/services/apexrest/warehouse/{merchandiseId}' replacing the {merchandiseId} text with your merchandise Id from before.
9. Press "Execute" and a number should be returned (click the "Show Raw Response" link to view the number in a more readable format).

## Step 3 - Add the POST Method
1. In the class we previously created, add the following code and save as before.
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
2. In the REST Explorer, select the "POST" checkbox and change the input area to be "/services/apexrest/warehouse/"
3. In the "Request Body" area enter:
```JSON
{"merchandiseId":"XXXXXX", "quantity":2}
```
and replace the XXXXXX with your merchandise Id (keeping it enclosed in quotes to form valid JSON).
4. Press "Execute"
5. Click "Show Raw Response" and see that an Invoice Id has been returned which you can view in the browser.
6. Copy this Invoice Id.

## Step 4 - Add the DELETE Method
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
2. In the REST Explorer select the "DELETE" checkbox and update the input area to be '/services/apexrest/warehouse/{invoiceId}' updating the {invoiceId} to be the Id of the invoice from before (or any invoice).
3. Press "Execute"
4. Click "Show Raw Response" and see that a message of "true" is returned informing you that the invoice has been successfully deleted.

## Step 5 - Further Study
You have now created a RESTful web service in Apex that uses 3 of the verbs; GET, POST and DELETE. You have tested the code works using the REST Explorer tool and can see how you can allow customers to connect to your applications. Try the following on your own:
- Create a method using PUT or PATCH to update a non-closed Invoice.
- Add error handling to the code and ensure that the "RestResponse" object is updated to return the correct status code.
- Write test methods for the code using the RestRequest and RestResponse objects in the RestContext system class instance.
