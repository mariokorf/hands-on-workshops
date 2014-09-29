TUTORIAL #3: UPDATE THE HEROKU APP

 

You now have two sides of an integration in place: one running a Java endpoint on Heroku, and another in Force.com which communicates with the endpoint when the appropriate changes take place. Now that you’ve got the connection in place, update the Heroku application to retrieve the pertinent information and display it to the user.

Step 1: Configure Your Connected App

Before moving on, let’s go back to your Salesforce organization so that we can configure your connected app. At a high level, we will:

- Add your app to the available connected apps in your organization. 
- Enable OAuth. External applications must authenticate remotely before they can access data. Force.com supports OAuth 2.0 (hereafter referred to as OAuth) as an authentication mechanism. Let’s go ahead and begin. 

1. From Setup, click **Create **&gt; **Apps**. 
2. In the Connected Apps section, click **New**. 
3. For **Connected App Name**, enter your app name. 
4. Enter the **API Name**, used when referring to your app from a program. It defaults to a version of the name without spaces. 
5. Provide your **Contact Email**. 
6. Under API (Enable OAuth Settings) select **Enable OAuth Settings**. 
7. For Callback URL, enter **_https://{appname}.herokuapp.com/_auth_**. 

Note: Be sure to replace _{appname} _with your actual Heroku app name.

1. In the **Selected OAuth Scopes **field, select **Full access (full) **and **Perform requests on your ****behalf at any time (refresh_token, offline_access)**, and then add them to the selected OAuth scopes. 
2. Click **Save**. 

Step 2: Update Your Application with a New Branch

While you were creating a new Apex trigger on your Force.com instance, other developers added new functionality to the original project and placed it into a specific branch on GitHub. Using this branch you can test out new features, specifically, your Heroku application’s ability to directly access your Salesforce records. It’s easy to add this branch, called “full,” to your codebase:

1. Return to the command line, and make sure you’re in the **spring-mvc-fulfillment-base **folder. 
2. Enter the following command to fetch the “full” branch and merge it with your master branch, all in one step: **   git pull origin full**
    1. Before continuing, go back to your org. 
    2. From Setup, click **Create **&gt; **Apps**. 
    3. In the Connected App Settings section, click your app name. 

1. Next to Consumer Secret, click **Click to reveal**. 
2. Use your keyboard controls to copy the number that appears. 

1. You need to set your Access keys to your Heroku application. Enter:  
**heroku config:add OAUTH_CLIENT_KEY=****_PUBLICKEY _****OAUTH_CLIENT_SECRET=****_PRIVATEKEY _ **Replace **PUBLICKEY **with the **Consumer Key **. Similarly, replace **PRIVATEKEY **with the **Consumer Secret **. It may be helpful to do this in a text editor before putting it on the command line. 
2. Execute the following command to push the local changes to Heroku: **git push heroku master **
3. In a browser tab or window, navigate to **https://****_{appname}_****.herokuapp.com **to see the changes (refresh your browser if needed). 

By adding an OAuth flow to your app, your app can request a user’s permission to work with session information without requiring the third-party server to handle the user’s credentials. With this functionality added to the project, the fulfillment application can use the Force.com REST API to access information directly from the user’s instance.

**Tell Me More...**

You can review all of the changes brought in by this branch on GitHub at: https://github.com/sbob-sfdc/spring-mvc-fulfillment-base/compare/master...full . Notice that

the changes use the Force.com REST API to manipulate invoice records. Look at InvoiceServiceImpl.java in particular to see how it creates, queries, retrieves and deletes invoices. This tutorial uses the findOrder() method only. The other methods are included for your reference.

Step 3: View the Invoice Information

In the previous steps you added brand new functionality by merging a branch into your local code. The application now understands how to use OAuth and how to access data from the Force.com platform. Now let’s view the invoice fields in your fulfillment app.

1. Navigate to your fulfillment app in the browser, and then refresh the page. 
2. Click an order. 

Notice that, given an ID, this code retrieves the corresponding invoice record. Because there might be mock ID's in the database that are not in Force.com, the app handles the corresponding exception by showing default data. Adding the invoice to the model makes it available to view. Now when you test the fulfillment application, it will show the invoice information currently in your Force.com instance by grabbing the information via the REST API using the record ID. Your order detail page might look something like:

**Tell Me More...**

 

Notice that the Web service call from Force.com to create orders is not secured. Securing the call goes beyond the scope of this workbook, but a simple solution would be to set up a shared secret between the Force.com app and the fulfillment app. The Force.com app would create an HMAC signature from the parameters in the request, using the secret, and the fulfillment app would verify the signature.

Summary

Congratulations! Your fulfillment app now retrieves invoice information via the Force.com REST API and displays it to the user. You configured your app in Salesforce to use OAuth for authentication, and you added OAuth credentials to your app hosted on Heroku. You can further modify your app to manipulate invoice information however you want.

