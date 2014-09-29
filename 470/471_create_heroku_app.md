##Tutorial #1: Create a New Heroku Application##
Heroku provides a powerful Platform as a Service for deploying applications in a multitude of languages, including Java. In this tutorial, you create a Web application using the Java Spring MVC framework to mimic handling fulfillment requests from our Warehouse application.
Familiarity with Java is helpful, but not required for this exercise. The tutorial starts with an application template to get you up and running. You then walk through the steps to securely integrate the application with the Force.com platform.

###Step 1: Clone the GitHub Project###

Git is a distributed source control system with an emphasis on speed and ease of use. Heroku integrates directly into Git, allowing for continuous deployment of your application by pushing changes into a Heroku repository. GitHub is a Web-based hosting service for Git repositories.

You start with a pre-existing Spring MVC-based application stored on GitHub. Then, as you make changes, deploy them into your Heroku account and see your updates available online via Heroku’s cloud framework.

1. Open a command line terminal. For Mac OS X users, this can be done by going to the Terminal program, under **Applications/Utilities **. For PC users, this can be done by going to the **Start Menu**, and typing **_cmd _**into the Run dialog. 
2. Once in the command line terminal, change to a directory where you want to download the example app. For example, if your directory is “development,” type **_cd development_**. 
3. Execute the following command:  
**git clone https://github.com/sbob-sfdc/spring-mvc-fulfillment-base **

Git downloads the existing project into a new folder, spring-mvc-fulfillment-base. 

###Step 2: Create a Heroku Project###

Now that you have the project locally, you need a place to deploy it that is accessible on the Web. In this step you deploy the app on Heroku.

1. In the command line terminal, change directory to the **spring-mvc-fulfillment-base **folder you created in the last step: **cd spring-mvc-fulfillment-base **
2. Execute the following command to log in to Heroku (followed by Heroku login credentials, if necessary): **heroku login **Heroku uses Git with SSH to deploy code. If you haven’t used SSH on this machine, you’ll need to create a public key after you provide your Heroku login credentials. On Microsoft Windows, you might need to add your Git directory to your system path before you can create a public key. 
3. Execute the following command to create a new application on Heroku: **heroku create **

###Step 3: Test the Application###

Heroku creates a local Git repository as well as a new repository on its hosting framework, where you can push applications, and adds the definition for that remote deployment for your local Git repository to understand. This makes it easy to leverage Git for source control, make local edits, and deploy your application to the Heroku cloud.

All application names on Heroku must be unique, so you’ll see messages like the following when Heroku creates a new app:

   Creating quiet-planet-3215... done

Important: The output above shows that the new application name is quiet-planet-3215 . You might want to copy and paste the generated name into a text file or otherwise make a note of it. Throughout this workbook, there are references to the application name that look like _{appname} _that should be replaced with your application name. So, if your application name is quiet-planet-3215, when a tutorial step prompts you to enter a URL with the format

https://_{appname}_.herokuapp.com/_auth, use: https://quiet-planet-3215.herokuapp.com/_auth .

1. To deploy the local code to Heroku, execute the following command: **git push heroku master **If prompted, select Yes to verify the authenticity of **heroku.com **. The deployment process will take a while as it copies files, grabs any required dependencies, compiles, and then deploys your application. 
2. Once the process is complete, you can preview the existing application by executing: **heroku open **You can also simply open **https://****_{appname}_****.herokuapp.com **in a browser. You now have a new Heroku application in the cloud. The first page should look like this: 

 

**Tell Me More...**

Scroll back through the terminal log to the git push command, and you’ll see some magic. Early on, Heroku detects that the push is a Spring MVC app, so it installs Maven, builds the app, and then gets it running for you, all with just a single command.

Step 3: Test the Application

This step shows you how to take your application for a quick test run to verify it’s working.

1. In a browser tab or window, navigate to **https://****_{appname}_****.herokuapp.com**. 
2. Click **Ajax @Controller Example**. 

1. In another browser tab or window, open the Warehouse application on your Force.com instance. 
2. Click **Invoices **and then select an existing invoice or create a new one if necessary. 
3. In the browser URL bar, select the invoice record ID, which is everything after **salesforce.com **in the URL. It should look something like **a01E0000000diKc**. Copy the ID to your clipboard. 
4. Return to the browser window or tab showing your Heroku application. 
5. Paste the invoice record ID into the field under **Id**. 
6. Click **Create**. An order is created with the Invoice ID. Note that this order is distinct from a Salesforce order record. 
7. Click **OK**. Your page looks something like: 

Summary

Heroku’s polyglot design lets you easily deploy your applications with industry-standard tools, such as Git. Typically, teams use local development environments, like Eclipse, and in fact Heroku has released an Eclipse plug-in for seamless integration with Eclipse. You can also interact with Heroku on the command line and directly access logs and performance tools for your applications.
