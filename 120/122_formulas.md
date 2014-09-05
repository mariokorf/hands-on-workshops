#Add a Formula Field#

**Level:** Beginner; **Duration:** 5–10 minutes

Another thing that's missing from the Line Item object is a Line Item Total field that displays the product of each Line Item's Quantity and Unit Price. In this tutorial, you implement this common business logic by creating a new formula field in the Line Item object, again, without writing any code.

##Step 1: Calculate a Value for Each Line Item##

In the first step of this tutorial, you will add a new calculated field called Line Item Total to the line item. This field will multiply the number of items with the price and act as a total for each line item.

1. Click **Setup** | **Create** | **Objects**.
2. Click the **Line Item** object and in the Custom Fields & Relationships related list, and click **New**.
3. Choose Formula, and click **Next**.
4. For Field Label, enter Line Item Total.
5. For Formula Return Type, choose Currency and click **Next**.
6. Click the Insert Merge Field drop-down list, and choose **Unit Price**. You should now see Unit_Price__c in the text box.
7. Click the Insert Operator drop-down list and choose **Multiply**.
8. In the **Insert Merge Field** drop-down list, select **Quantity**. You should now see Unit_Price__c * Quantity__c in the text box. 
9. Click **Next**, **Next**, and then **Save**.

**Tell Me More....**

The Formula field type is great for automatically deriving field values from other values, as you have done here. The formula you entered was quite straightforward: a simple multiplication of two field values on the same record. There's also an Advanced Formula tab, which allows you to do much more with these formulas.

##Step 2: Try Out the App##

To see the new Line Item Total formula field in action, you’ll need to create a new line item.

1. Click the Invoices tab and then click an existing invoice.
2. Add a new line item, select a piece of merchandise, and enter a quantity.
3. Save the line item and you can see the formula field in action.


 
