#Load Data Using the Custom Object Import Wizard#

**Duration:** 5–10 minutes

Most organizations keep important data in all sorts of places, including documents and spreadsheets. In this tutorial, you learn how to load data that currently lives in a personal spreadsheet into the Warehouse app, where everyone in your organization can view and manage the data.

There are several ways to load data, and this tutorial shows you only one method, using a the Custom Object Import Wizard. This wizard uses a CSV file as its source. A CSV file is a plain text file with each field separated by commas—thus the name “comma-separated values.”

**Prerequisites**

Text Editor

This tutorial requires a text editor and the ability to upload a file from your computer. If you’re using a tablet or mobile device, you may not be able to complete this tutorial depending on the capability of the device.

**Step 1: Create the Data File**

The first step is to make a simple data file that you can use for this tutorial.

1. To save you time, download the necessary CSV-formatted text file, from this URL. [https://raw.github.com/joshbirk/workshop2013/master/files/Merchandise.csv](https://raw.github.com/joshbirk/workshop2013/master/files/Merchandise.csv)
2. Right-click and save the file locally. It should look like:"Merchandise Name","Price","Quantity"
3. "17 Inch Monitor",99,200
4. "21 Inch Monitor",129,200
5. "25 Inch Monitor",179,200  

**Tell Me More....**

Some things to notice in the CSV file include that:

- The field names are on the first line. These names exactly match the labels for fields in the Merchandise object.
- Text fields are delimited by quotes. Doing so allows you to include spaces and special characters inside a text field. Fields that have a number data type don’t require quotes.

##Step 2: Load the Data##

Loading data from a CSV file into a custom object is simple using the Custom Object Import Wizard.

1. From Setup, in the Quick Find field, type import and then click **Import Custom Objects**
2. At the bottom of the page, click **Start the Import Wizard!**
3. When the wizard starts, select Merchandise, then click **Next**.
4. Select No, and then click **Next**.
5. Select None, and then click **Next**.
6. Click **Choose File** or **Browse...** and select the data file you created earlier, then click **Next**.
7. Notice on the Field Mapping step you can match headings in your CSV file to field names in Salesforce. That was already done in the CSV file, so you can click **Next**. 
8. Click **Import Now** and then **Finish**.

**Tell Me More....**

Once you finish the wizard, the platform queues the data load. For large sets of data, it may take a while for the data load to happen, and you’ll be notified by email when the data load completes. If you want to monitor this process more closely, in Setup, click **Imports**.

 
##Step 3: Try Out the App##

Once the data load is completed, go back to your app and confirm that the new Merchandise records are in place.

1. Click the Merchandise tab.
2. Next to the View drop-down list, make sure All is selected and click **Go!**

