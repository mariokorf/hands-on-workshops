#Add Fields to an Object#

**Level:** Beginner; **Duration:** 5–10 minutes

In the first tutorial, you created a cloud app for managing merchandise in a warehouse. Behind the scenes, the platform created a database for the app. This tutorial is the first of many that teach you how to continue building the database for your app. A _database_ organizes and manages data so that users can work with it efficiently. Traditional relational databases use tables to manage discrete, possibly related, collections of information, organized further into datatype-specific columns (attributes) and rows (records). In Salesforce, you refer to these as _objects_.

Your DE org comes with many _standard objects_ (for example, Accounts, Products, Tasks) that support pre-built apps. Any new objects you create are called _custom objects_. The Merchandise object is one such custom object. In this tutorial you add two new _custom fields_ (Price and Inventory) to supplement the _standard fields_ the object already has (Name, Owner, CreatedBy, LastModifiedBy).

The following image is a sneak peek of the data model you will be building, which allows you to view your objects, fields, and relationships.

![warehouse_schema](https://cloud.githubusercontent.com/assets/1034381/4133253/28c4fffc-335c-11e4-9f52-3f826737dd68.png)

##Step 1: Add the Price Field to the Merchandise Object##

A merchandise object should have fields that are used for tracking various information, such as how much individual units cost and how many units are in stock. You can add custom fields to list or track just about anything you can think of.

1. Click **Setup** | **Create** | **Objects**.
2. Click **Merchandise**, scroll down to Custom Fields and Relationships, and click **New**.
3. The wizard helps you quickly specify everything about a new field, including its name, labels to use for app pages, help information, and visibility and security settings. Create the Price field as follows:
    1. For Data Type, select **Currency**, and click **Next**.
    2. Fill in the custom field details:
        - Field Label: *Price*
        - Length: *16*
        - Decimal Places: *2*
        - Select the **Required** checkbox

    3. Leave the defaults for the remaining fields, and click **Next**.
    4. Click **Next** again to accept the default field visibility and security settings.
    5. Click **Save & New** to save the Price field and to return to the first step of the wizard.

##Step 2: Add the Quantity Field to the Merchandise Object##

You should already be in the New Custom Field wizard, so you can create the Quantity field in the same manner.

1. For Data Type, select **Number** and click **Next**.
2. Fill in the field details:
    - Field Label: *Quantity*
    - Select **Required**

3. Leave the defaults for the remaining fields, and click **Next** and **Next** again.
4. Click **Save**.

Take a look at the following image to familiarize yourself with the Merchandise custom object.

![merch_object_detail](https://cloud.githubusercontent.com/assets/1034381/4133242/28a04cc0-335c-11e4-99dd-f782dc1f2259.png)

1. **Merchandise detail page**—Shows you everything you need to know about your Merchandise custom object. Soon you’ll add relationships, validation rules, and other neat features to this object.
2. **API name**—When you created the Merchandise object, you didn’t specify an API name, but one was generated for you. This name is how the object is referenced programmatically. All custom objects end in __c, which differentiates them from standard objects.
3. **Standard fields**—Some fields are generated automatically; these are standard fields. For example, the Merchandise object has a standard field for Owner, which means it automatically tracks who created each record.
4. **Custom fields**—Includes the fields you just created in this step. Like custom objects, custom fields have API names that end in __c.

**Tell Me More....**

- The custom fields you created so far are nothing fancy, but you can do fancy! The platform has support for nearly any type of data you want to track, such as currency, email, geolocation, URLs, date/time, and so on. Fields don't just contain static values, they can be derived from formulas, or take their values from other objects.
- Why do you need an API name as well as the object and field label? A label is what the user sees, so it should be easy to read and may contain spaces. The API name is used internally in code, and can’t contain spaces or illegal characters. For example, a field labeled “Customer ph# :” would be named Customer_ph in the code (the system replaces spaces with underscores and removes the # and : characters).


##Step 3: Try Out the App##

At this point you have a nice representation of your warehouse items—each have a name, price, and quantity. Time to create some more inventory.

In the first tutorial, you created one Merchandise record with just a name (Laptop). In this tutorial you create a few more Merchandise records that include the new Price and Quantity fields.

1. Click the **Merchandise** tab to leave Setup and return to the app.
2. Click **Laptop** in the Merchandise listing.
3. Click **Edit**, and then specify the price and quantity as follows.
    - Price: *500*
    - Quantity: *1000*
5. Click **Save**
![merch_edit](https://cloud.githubusercontent.com/assets/1034381/4133240/289e5f0a-335c-11e4-85e5-7f90b934f7f8.jpg)
6. If you created the E-reader item in the mobile tutorial, edit that item in a similar manner. If not, create a new Merchandise record called E-reader with the following field values.
    - Price: *100*
    - Quantity: *1500*
7. Click **Save & New** and create a merchandise record for Desktop with these attributes.
    - Price: *1000*
    - Quantity: *500*
8. Click **Save & New**, and create a merchandise record for Tablet with these attributes.
    - Price: *300*
    - Quantity: *5000*
9. Click **Save**.

**Tell Me More....**

* Take note how the platform automatically added the new Price and Quantity fields to your Laptop record. When you add new fields through the wizards, the fields are added to your existing objects _and_ exposed automatically on your app’s user interface. Nice!
* Also look at one of your merchandise records. Notice the Owner, CreatedBy, and LastModifiedBy fields. These are _standard fields_ which the platform automatically manages. Users have the ability to edit the Name standard field, along with the custom fields Price and Quantity.
![merch_detail](https://cloud.githubusercontent.com/assets/1034381/4133239/289d0cd6-335c-11e4-940a-98b7d287d721.png)  
* Did you notice the Recent Items in the sidebar? This handy feature lets you view and navigate to the most recently changed records in your database. The linked names in this sidebar come from each object’s Name field.
 
