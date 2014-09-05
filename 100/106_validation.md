#Enforce a Business Rule#

**Level:** Beginner; **Duration:** 5–10 minutes

Typically, every business app enforces rules that prevent bad data from getting into the system. Without such rules, things can get really messy, really fast because users might not adhere to these rules on their own. In this tutorial, you learn how to enforce a basic business rule for the Warehouse app—you can’t order zero or negative items. To do this, you create and test a validation rule, all in just a couple of minutes without any coding.

##Step 1: Understand the Business Rule##

Before you begin, make sure you have a clear understanding of this particular business rule.

1. Log into your DE org (if necessary) and select the **Warehouse** app.
2. Click the Invoice tab, select an invoice, and look at a specific line item.
3. Play around with the quantity field for the line item. Notice that a value is required, but that you can set the value to any number: 0, -10, 3.14159. You don’t want users entering bad data (such as negative numbers), so this situation isn’t acceptable.

##Step 2: Create a Validation Rule##

Enforcing basic business rules is easy and doesn’t require any coding.

1. Click **Setup** | **Create** | **Objects** | **Line Item**, scroll down to the Validation Rules related list, and click **New**.
2. For Rule Name type Validate_Quantity.
3. Optionally fill out the Description field. It’s a good practice to document business logic so that other developers can easily understand the purpose of the rule. Also notice that there are handy links to help for the page.
4. In the Error Condition Formula area, you build a validation rule’s error condition formula to identify when the error condition evaluates to TRUE.
    1. Click **Insert Field** to open the Insert Field popup window.
    2. Select Line Item &gt; in the first column and Quantity in the second column.
    3. Click **Insert**.
    4. Type the less-than-or-equal-to symbol (&lt;=) so the formula looks like this:Quantity__c &lt;= 0  

5. Click **Check Syntax** to make sure there are no errors. If you do find errors, fix them before proceeding. 
6. In the Error Message field, type You must order at least one item.
7. For the Error Location, select Field, then choose Quantity from the drop-down list.
8. Click **Save**.

**Tell Me More....**

Take a quick look at the Validation Rule Detail page. Notice that the new validation rule is “Active” meaning that the platform is currently enforcing the rule. In certain situations, you might want to deactivate the rule temporarily (for example, before loading a bunch of data). This is easy to do by simply deselecting the **Active** box (but don’t do this now).

##Step 3: Try Out the App##

Now that the rule is in place and active, test it.

1. Click the **Invoices** tab and select an existing invoice.
2. Create a **New Line Item** and type a Quantity of –1.
3. Choose a merchandise item and **Save** and you see the error message that you set up for the rule.
4. Fix the error by entering a valid quantity and then **Save**.

**Tell Me More....**

- If you didn’t see the error message, check the validation formula again. You need to make the rule fire when the condition evaluates to TRUE.
- The formula in this tutorial is rather simple, but don’t let that fool you. The platform’s formula syntax empowers you to enforce a wide range of business rules that not only includes one object, but pulls in other related objects as well.

##Step 4: Modify the Validation Rule##

The Warehouse app already has a validation rule ensuring that a user must order at least one piece of merchandise. It would be even better if this rule also checked how many items are in stock, so that a person can’t order more items than are available.

1. Click **Setup** | **Create** | **Objects** | **Line Item**, scroll down to the Validation Rules related list, and edit the **Validate_Quantity** rule.
2. Edit the Description field to explain that it won’t allow users to order more items than are in stock.
3. In the Error Condition Formula area, start by putting some parentheses around the first rule, insert the logical OR operator, and then add another set of parentheses so that the error condition looks like the following:(Quantity__c &lt;= 0) || ()  

4. Click between the second set of parentheses and click **Insert Field** to open the Insert Field popup window.
5. Select Line Item &gt; in the first column, and Quantity in the second column, click **Insert**.
6. Type or insert the greater-than symbol (&gt;).
7. Click **Insert Field** and select Line Item &gt; in the first column, Merchandise &gt; in the second column, and Quantity in the third column.
8. Click **Insert** and verify the code looks like the following:(Quantity__c &lt;= 0) || (Quantity__c &gt; Merchandise__r.Quantity__c)  

9. Click **Check Syntax** to make sure there are no errors. If you do find errors, fix them before proceeding.
10. Click **Save**.

**Tell Me More....**

You can enter a formula directly into the Error Condition Formula area, but as you saw here, you can easily traverse the available objects and find the components you need for the formula. Let's analyze the formula you created.

- Mechandise__r—Because the Merchandise object is related to the Line Item object, the platform automatically provides a relationship field that lets you navigate from a Line Item record to a Merchandise record; that's what the Mechandise__r is doing.
- Quantity__c—This is the field you created to track the total amount of stock on a Merchandise record.
- Merchandise__r.Quantity__c—This tells the system to retrieve the value of Total Inventory field on the related Merchandise record.
- Quantity__c—This refers to the Quantity field on the current (Line Item) record.

Putting it all together, the formula checks that the total inventory on the related merchandise record is less than the number of units being sold. As indicated on the Error Condition Formula page, you need to provide a formula that is true if an error should be displayed, and this is just what you want: it will only be true when the total inventory is less than the units sold.

