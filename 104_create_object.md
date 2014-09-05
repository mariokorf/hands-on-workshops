#Create a New Object#

**Level:** Beginner; **Duration:** 10–15 minutes

To make the Warehouse app more realistic, you need invoices to track orders going in and out of the warehouse. In this tutorial, you learn how to extend the app further by:

- Creating another custom object, for keeping track of invoices. This object needs a Status field to track whether the invoice is open, closed, or somewhere in-between.
- Adding a tab to the app so users can work with invoices.
- Reordering tabs for easier navigation.

##Step 1: Create the Invoice Object Using the Wizard##

An invoice is required to move inventory into or out of the warehouse. In this step, you create an invoice object that allows you to create multiple invoice statements, each with a unique number, status, and description.

1. Return to Setup, and click **Create** | **Objects**.
2. Click **New Custom Object**.
3. Fill in the custom object definition.
    - In the Label field, type Invoice.
    - In the Plural Label field, type Invoices.
    - Select Starts with vowel sound.
    - In the Record Name field, type Invoice Number (replace Name with Number).
    - For Data Type, select Auto Number.
    - In the Display Format field, type INV–{0000}. (Note there are no spaces.)
    - In the Starting Number field, type 0.

4.  
5. In the Optional Features section, select Allow Reports (in case you create reports later).
6. Select Launch New Custom Tab Wizard after saving this custom object.
7. Click **Save**.

**Tell Me More....**

- The checkbox for vowel sounds ensures that the correct article is used: “a” or “an.”
- The Auto Number data type tells the platform to automatically assign a number to each new record that is created, beginning with the starting number you specify. Because of the display format you chose, the invoice numbers will be INV-0000, INV-0001, and so on.
- You could have started invoices at any number, but this tutorial starts invoices at INV-0000 to remind you that the platform is zero-based.

##Step 2: Add an Invoice Tab to the App##

When you click the Merchandise tab, a list of Merchandise records appears. Similarly, you need to create a tab that displays Invoices.

1. Because you selected **Launch New Custom Tab Wizard...** in the previous step, you should now be looking at that wizard (if you’re not, click **Setup** | **Create** | **Tabs**, and then click **New** in the Custom Object Tabs section). Choose your Invoice object.
2. In the Tab Style lookup, choose **Form** and click **Next** and then **Next** again.
3. It makes sense to display this new tab for the Warehouse app. On the Add to Custom Apps page, clear the checkbox next to all apps except **Warehouse** and click **Save**.

##Step 3: Reorder Tabs in the App##

Take a look at the tabs across the top of your screen and you see the new Merchandise tab isn’t next to the Invoice tab. You can put tabs in any order you like, so go ahead and put them next to each other.

1. The Setup menu on the left should already be open, so click **Create** | **Apps** and click **Edit** next to your Warehouse app.
2. In the Selected Tabs list, select Invoices and use the up arrow to move it under Merchandise.
3. Click **Save** and then take a look at the tabs.

##Step 4: Add a Status Field to the Invoice Object##

If you try to create an invoice now, you won’t be impressed. There are no fields that you can modify because they are all standard, auto-managed fields. In this step, you extend the Invoice object to add a new Status picklist field to track the status of each invoice (for example, open or closed).

1. In the Setup area, click **Create** | **Objects** and then click **Invoice**.
2. Scroll down to the Custom Fields & Relationships related list and click **New**.
3. For Data Type, select Picklist and click **Next**.
4. Fill in the custom field details.
    1. Field Label: Status
    2. Type the following picklist values in the box provided, with each entry on its own line. Open  
Closed  
Negotiating  
Pending
    3. Select Use first value as default value.
    4. In the Help Text field, type Choose a value from the drop-down list.

5. Leave the defaults for the remaining fields and click **Next**, **Next**, and **Save**.

**Tell Me More....**

Before moving on to the next step, recall the Help text you added to the Status field. When users hover their pointer over the Status field, a pop-up bubble appears with whatever help text you specify. Although it’s beyond the scope of this tutorial, understand that you can easily create unique translations for app labels and help text so that the app supports multiple languages, again, without writing a single line of code. Very cool.

##Step 5: Try Out the App##

Although your app isn’t completely done yet, you can create invoices and save them. It’s not a problem that the invoice is still missing some fields. When you add more fields to the Invoice object, the new fields automatically appear on the records that already exist.

1. Click the Invoices tab.
2. Click **New**. Notice that you can choose a status for the invoice, but leave it as Open.
3. Click **Save**.
4. Click the Invoices tab again and notice there’s a new invoice, with the number INV-0000. Create another new invoice, this time with a Closed status.
5. Click the Invoices tab again and see your two invoices.

The database is starting to look better, but it’s still incomplete. An invoice is made up of line items that list what merchandise and how many are being ordered. In the next tutorial, you’ll add another object—Line Items—and then relate that object to the other ones we’ve created.

**Tell Me More....**

- You only have a few records so far, but how would the page look if you had hundreds of records? Thankfully, the default list view for a tab shows you only the most recent records you touched and lets you page through sets with standard navigation controls.
- Another built-in feature is _list views_. A list view is a customized presentation of data that shows only the fields you want, based on filters you define. For example, suppose you’re only interested in open invoices with a price greater than $1000. You can create a custom list view that shows exactly those records. This is covered in a later tutorial.
