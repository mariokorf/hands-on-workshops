#Add a Roll-Up Summary Field#

**Level:** Beginner; **Duration:** 5–10 minutes

Another thing that's missing from the Invoice is a field that aggregates all of the line items into one big invoice total. This is easy to do if the objects are in a master-detail relationship, because you can use a _roll-up summary field_.

##Step 1: Calculate a Total With a Roll-Up Summary Field##

Now that you have the total for each line item, it makes sense to add them all to get the invoice total. Because the line items have a master-detail relationship with the invoice, you can use a roll-up summary field to calculate this value. Roll-up summary is a special type of field that lets you aggregate information about related detail (child) objects. In this case, you want to sum the value of each line item.

1. Navigate back to the Invoice custom object page from Setup by clicking **Create** | **Objects** and then clicking **Invoice**.
2. In the Custom Fields & Relationships related list click **New**.
3. Choose Roll-Up Summary as the data type, and click **Next**.
4. For the Field Label field, enter Invoice Total, and click **Next**.
5. In the Summarized Object list choose Line Items.
6. For Roll Up Type, select Sum.
7. In the Field to Aggregate list choose Line Item Total.
8. Verify that your screen looks like this. Then click **Next**, **Next** and **Save**. 

##Step 2: Try Out the App##

To see the new Invoice Total formula field in action, you only need to examine an invoice.

1. Click the Invoices tab and then click an existing invoice.
2. Notice the new Invoice Total field that “rolls up” all the values from the detail object’s Line Item Totals.
3. To get the Line Item Total field to appear on the detail page, you’ll have to edit the page layout. (If you haven’t done that yet, see [Modify a Page Layout](file:///Users/mkorf/Documents/Content/page_layout_intro.htm)). When you do, it should look like the following image.
