#Build your first Angular.js App on Visualforce

##Slide introduction
[[slides]]

##Getting your own Dev org
We'll be using a developer org to create our Angular.js App. If you don't already have access to a new, or lightly used developer org follow these steps:

1. __Visit__ [http://goo.gl/CfYHVR](http://goo.gl/CfYHVR) 
2. __Email:__ Any email address you can currently reach
3. __Username:__ Anything in the form of an email _(Example: Tessa-AngularOnVf@example.com)_
4. Check your email. You'll be getting an activation link you need to click to set your password.

##Installing Resources
Angular.js is an application framework, and as such doesn't provide things like styling or icons. As a result there are numerous files we need to get setup. The link below will install an *unmanaged* package in your development org that contains all the files we need to get up and running. 

[Click this to install the unmanaged package from http://sforce.co/VOpT83](http://sforce.co/VOpT83)

##Editing Javascript
1. login to your developer org, and navigate to:
	- setup â†’ develop â†’ static resources
2. Click on the "app" static resource
3. Click "view file" to download the zip file to your computer.
4. Find where your computer has downloaded the file, and unzip it.

This zip file contains all the javascript, css and image resources needed to bootstrap an AngularJs app in visualforce. It is effectively a "seed" of a project. 

##Creating the Visualforce page
Our application's view templates will be visualforce pages, and we'll need to create a visualforce page to host our angular app. 

1. In your Developer org, open up the Dev console by navigating to: 
	- Name Menu â†’ Developer Console
2. We'll be doing some of our work here in the developer console, so don't close this window.
3. Use the file â†’ new menu and select "visualforce page"
4. When prompted, provide the name "MasterApp" for the name.
5. Alter the opening Apex:page tag to include the following attributes:
	- ```showHeader="false"```
	- ```sidebar="false"```
	- ```standardStylesheets="false"```
	- ```docType="html-5.0"```
6. Quick save your page. (cmd-s / ctrl-s)
7. The unmanaged package installed earlier installed a couple of custom visualforce components. Those components handle loading all the various JS files for us. Include those by putting this between the apex:page tags
	- ```<c:ngApp>```
	- ```<c:ngForce/>```

##The ng-app directive
As we talked about during the slideshow, Angular activates when it fines the attribute ```ng-app="app_name_here"``` on a container element (div, body, etc.) We'll need to create a div to contain our Angular app and include the ```ng-app``` attribute to active angular.

1. In your "MasterApp" visualforce page create a new blank line after the ```<c:ngForce/> tag
2. Create a div tag, and include the ```ng-app="df14"``` attribute. Or copy this code into place:

```html
<div ng-app="df14" class="container-fluid ui-view-container">
  <div class="ui-view" id="master-ui-view" style="padding-top: 70px;">
    <!-- our main content will go here -->
  </div>
</div>
```

At this point, our basic Angular app is almost complete, but it doesn't do anything.

In your dev org, visit [instance.salesforce.com/apex/masterApp](instance.salesforce.com/apex/masterApp) making sure you replace instance with the naX prefix present in your current URL.

This is your AngularJs app, running inside visualforce.

Open the javascript console and observe the errors.

##Accessing Salesforce Records
We want our Angular app to be able to create, display, edit and delete salesforce records. To do this, we'll need to create a controller, and use the ngForce library to access Salesforce data.

1. With your favorite code editor, open up the directory where you unzipped our static resource file.
2. Open the resources â†’ controllers â†’ masterAppPageCtrl.js file
3. About half way down you'll find a soql query. Add the word "Account" to the query, and save the file.
4. Using your OS's built in zip function zip up the resources folder and upload to Salesforce by navigating to:
	- setup â†’ develop â†’ static resources â†’ app
	- clicking the edit button
	- clicking the choose file button
	- select your new resources.zip file and click "choose"
	- click the "Save" button
5. Reload your MasterApp page in another window. The javascript errors are gone -- because the query is valid now. However, we still don't see any account information.
6. In the Developer Console, open up the visualforce page named "df14_nav" by:
	- Clicking file â†’ Open â†’ selecting the "df14_nav" page
7. Create a unordered list tag ```<ul>``` and create a single ```<li>``` element within it. 
8. Add an Angular repeat ```ng-repeat``` attribute to the ```<li>``` element with the expression ```acct in accounts``` Your ```<ul>``` block should look like this:

```html
<ul>
  <li ng-repeat="acct in accounts" >
	
  </li>
</ul>
```
between the ```<li>``` tags you can use angular merge syntax ```{{ expression }} ``` to merge in data from our $Scope variable on the controller. Go ahead and add in the account Name between the ```<li>``` tags like this:
``` {{acct.Name}} ``` 

Note that we'll use the iteration variable acct, created by Angular when we said 'acct in accounts'  

##Conclusion

You've now created an Angular.js app on visualforce, complete with a controller and a couple of views. You've integrated it to Salesforce and are displaying account names as an unordered list in your app! 
