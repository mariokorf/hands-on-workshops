#Relate Objects#

**Level:** Beginner; **Duration:** 10–15 minutes

In previous tutorials you created objects that stood on their own. The fields on the Merchandise object had no relation to the fields on the Invoice object. In this tutorial, you create a Line Item object, and what’s special about this new object is that its fields are related to both the Invoice and Merchandise objects.

- An invoice has one or more line items. In fact, you might say that a particular invoice “owns” its line items. That kind of relationship is called a _master-detail relationship_, where the detail records refer to a master record.
- Line items also relate to merchandise through another kind of relationship called a _lookup_. You already saw something similar in the Status field. When you create a new invoice, you can choose a status from the picklist. A lookup field is different because the values come dynamically from a custom object rather than statically from a picklist.

Master-detail relationships and lookups might seem confusing now, but once you implement them, it will all be very clear.

##Step 1: Create the Line Item Object##

Each invoice is made up of a number of invoice line items, which represent the number of merchandise items being sold at a particular price. You are first going to create the Line Item object, and then relate it to the Invoice and Merchandise objects.

1. From Setup, click **Create** | **Objects**.
2. Click **New Custom Object** and fill in the custom object definition.
    - Label: Line Item
    - Plural Label: Line Items
    - Record Name: Line Item Number
    - Data Type: Autonumber
    - In the Display Format field, type LI–{0000}. (Note there are no spaces.)
    - • In the Starting Number field, type 1.

3.  
4. In the Optional Features section, select Allow Reports, and click **Save**.

##Step 2: Add a Quantity Field##

Every line item needs to track the quantity ordered. So the next thing you need to do is add a Quantity field. Recall that the Merchandise object also has a Quantity field to track how many items are in stock, and the steps to create the field are the same.

1. On the Line Item detail page, scroll down to Custom Fields and Relationships and click **New**.
2. For Data Type, select Number and click **Next**.
3. Fill in the field details:
    - Field Label: Quantity
    - Select Required

4. Leave the defaults for the remaining fields, and click **Next**, **Next**, and then **Save**.

##Step 3: Relate Line Items to Invoice##

Now that you have all the objects representing the data model, you need to relate them to each other. Line items are related to both an invoice (an invoice is composed of a number of line items) and merchandise (a line item takes its price from the merchandise).

1. On the detail page of the Line Item object, scroll down to the Custom Fields & Relationships related list and click **New**.
2. For Data Type, select Master-Detail Relationship and click **Next**.
3. In the Related To field, select your Invoice custom object, and click **Next**.
4. For Field Label and Field Name enter Invoice.
5. Accept the defaults on the next three screens by clicking **Next**.
6. On the final screen click **Save & New**.

**Tell Me More....**

One way to think of this master-detail relationships is that an invoice now “owns” its line items. In other words, an invoice can now contain multiple line items. One of the neat things about master-detail relationships is that they support roll-up summary fields, allowing you to aggregate information about the child records. You’ll use that feature in a later tutorial.

##Step 4: Look Up Merchandise Items##

The other kind of relationship you need to create is called a _lookup_. As the name implies, the field gets its information by looking it up dynamically in another object. In the last step, you used **Save & New**, so you should already be on the New Custom Field dialog.

1. For Data Type field, select Lookup Relationship and click **Next**.
2. In the Related To field, select Merchandise and click **Next**.
3. For Field Label and Field Name enter Merchandise.
4. Verify your screen looks like the following image and then click **Next**.
5. Accept the defaults on the subsequent screens by clicking **Next**, and **Next** again.
6. On the final screen, deselect the checkboxes for Merchandise Layout and Append related list to users (you don’t want a list of line items on the Merchandise page), and click **Save**.

**Tell Me More....**

At this point you have two relationships, a master-detail relationship that allows an invoice record to contain many line items, and a lookup relationship that relates a particular line item to a piece of merchandise.

##Step 5: Try Out the App##

As you saw in the previous tutorial, the platform automatically generates a user interface for the objects you create, so that you can view, edit, delete, and update records. Because you also related the objects, the user interface provides a way of navigating between related records as well. You can see how all that works by creating another invoice record.

1. Click the Invoices tab and then **New** and **Save**.
2. Notice there’s a button to create a **New Line Item**. Click it.
3. For Line Item Number, type 1.
4. For Quantity, type 2.
5. In the Merchandise field, type the first few letters of laptop and click the Find icon. 
6. Click **Laptop** and then **Save**.

**Tell Me More....**

If you’re familiar with the products in your inventory, you can type the first few letters of a piece of merchandise and click **Save**. You don’t need to click the Find icon, the system automatically finds the merchandise and adds it when you save the record. There’s a lot of built-in functionality!

##Step 6: View the Schema##

You now have three custom objects, several fields, and two kinds of relationships. If you have all of that in your head, awesome. However, most people find this is an ideal time to use the old adage “a picture is worth a thousand words.”

1. From Setup, click **Schema Builder**.
2. In the left pane, click **Clear All** to remove the standard objects from the schema.
3. Select the checkboxes for Merchandise, Invoice, and Line Item.
4. Click **Auto-Layout** to arrange the objects, or manually adjust the layout if necessary.

The Schema Builder shows your objects, fields, and relationships in a standard entity-relationship diagram. In a relationship, the “crows feet” at the end of the line tell you which side is the “many” side of a one-to-many relationship (one invoice can contain multiple line items). When you’re done looking at the schema, click **Close**.

Note

Schema Builder isn't just for viewing your schema, it also supports drag-and-drop development for creating new objects and fields. However, unlike the wizards you used so far, fields added using Schema Builder are not automatically added to page layouts. You must configure page layouts before your new fields are visible to users. Field visibility and page layouts are covered in subsequent tutorials.

##Summary##

At this point, you have created three custom objects: Merchandise, Invoice, and Line Item. On each of those objects you created custom fields to represent text, numbers, and currency. Two of these fields have system-generated values: the Status picklist, which defaults to Open, and the Invoice Number field, which is automatically assigned by the Auto-number data type. You also created user-defined fields, such as the Quantity entered for each line item. Finally, you expanded on the basic data model by creating two fields that get their values from other objects; these are the relationship fields you created in this tutorial.

The master-detail relationship allows you to aggregate information, so that an invoice can contain multiple line items, and those line items can be aggregated. The lookup relationship allows you to pull in dynamic content, so that each piece of merchandise on a line item automatically gets a price. The relationships also provide additional benefits. You can add up the price of each invoice line item and create a sum total for the invoice, and you can navigate to the related records in a user interface. You’ll learn how to do those things declaratively in the next tutorial, and later in code as well. Onward!
