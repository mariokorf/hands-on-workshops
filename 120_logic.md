#Automate a Field Update Using Workflow#

**Level:** Beginner; **Duration:** 10–15 minutes

Your company can operate more efficiently with standardized internal procedures and automated business processes. In your Salesforce app, you can use workflow rules to automate your procedures and processes. Workflow rules can trigger actions (such as email alerts, tasks, field updates, and outbound messages) based on time triggers, criteria, and formulas.

Automatically populating a field with a default value is a common business rule. Recall that you did something similar already using a Lookup field on two related objects. A Line Item can “look up” merchandise and give the user a choice of which item they want. But what if, rather than having a user choose, populating the field was done automatically? That’s when you need a workflow rule, so that depending on different conditions, you the platform can automatically populate a field with the appropriate value, and without user intervention.

##Step 1: Examine the Line Item Detail Page##

To get started, quickly review the Invoice and Line Item objects from earlier tutorials.

1. In your DE org, click the Invoices tab.
2. Open any invoice, and then open the detail page for a line item. Notice there’s no price field for the line item.

In this tutorial, you create a new field for the Line Item object called Unit Price. You don’t want users creating their own price, and since the price is already stored in the Merchandise object, you can populate this field automatically using a neat feature called a _workflow rule_.

##Step 2: Create a Unit Price Field##

The steps for creating the new Unit Price field are essentially the same as when you created the Price field on the Merchandise object except this time name the field Unit Price.

1. From the Line Item tab or record, click the Quick Access menu (the tab that pops out from the right side of the window), hover over View Fields and click **New**. (If you aren't on the Line Item object already, in Setup click **Create** | **Objects**. Then click **Line Item**, and in the Custom Fields and Relationships section, click **New**.)
2. For the data type, select Currency and then click **Next**.
3. Fill in the custom field details as follows.
    - Field Label:Unit Price
    - Length:16
    - Decimal Places:2

4. Leave the defaults for the remaining fields by clicking **Next** on subsequent screens until you can **Save**.
5. Now go back to an existing Invoice and add a new Line Item. Notice there's a new field for Unit Price, but you have to populate that field manually. You want this field to populate automatically, so click **Cancel**, and add this new functionality.

##Step 3: Automatically Populate the Unit Price Field##

To automatically populate the new Unit Price field, create a workflow rule.

1. From Setup, click **Create** | **Workflow & Approvals** | **Workflow Rules**.
2. Optionally, read the brief introduction, click **Continue**, and then click **New Rule**.
3. Select the Line Item object, and click **Next**.
4. For the rule name, enter Populate Unit Price, and for the description enter something like Populates the Line Item object’s Unit Price field with the value of the Merchandise object’s Price field.
5. For evaluation criteria, select created.
6. For the first rule criteria row, for the field select Line Item: Quantity, for the operator select greater or equal, and for the value enter 1.
7. Click **Save & Next**.Note  

8. It makes sense to fire this workflow rule only for _new_ line item records because you are effectively assigning a default field value when creating a new record. Later on, users might need to adjust the price of merchandise in each line item (for example, to offer discounts).  

Continuing on, the next step is to assign an action to the workflow rule to update the Unit Price field automatically.

1. Click the drop-down list that reads Add Workflow Action and choose **New Field Update**.
2. In the Name field, enter Copy Unit Price.
3. In the Field to Update list, choose Line Item and then Unit Price.
4. Select the option to use a formula to set the new value. Before continuing, confirm that your screen matches the following.
5. Click **Show Formula Editor**, and then click **Insert Field**.
6. In the first column choose **Line Item &gt;**, in the second column choose **Merchandise &gt;**, and in the third column choose **Price**.
7. Confirm that your screen matches the following, and then click **Insert**.
8. Click **Save**, and then click **Done** to return to the detail page of the new workflow rule.

**Tell Me More...**

In the formula, notice some new syntax, namely "Merchandise__r". You’ve seen __c used already, so what’s with the __r? That’s the platform’s object notation for a field that’s related to another object. You can use related fields to traverse object relationships and access related fields. In this case, the formula uses the relationship between the Line Item record and Merchandise object to get the corresponding Merchandise record's value for Price.

##Step 4: Update Total Inventory When an Order is Placed##

The inventory of merchandise should be automatically maintained as orders are placed. When you create a new invoice ("Open" status), every new line item needs to decrease the total inventory by the number of units sold. Similarly, updates to an existing line item need to update the total inventory by the difference in units sold.

There are a few different ways you can make this update. You could do this in Apex code, or by creating a Flow, or by creating another workflow rule. For simplicity, you’ll stick with workflow for now, but there is one minor problem to fix first, which is that the workflow field update won’t work with a lookup relationship. So the first step is to change the lookup to a master-detail. Fortunately, the platform makes such changes very easy.

1. From Setup, click **Create** | **Objects**, and click **Line Item**.
2. Scroll down to Custom Fields and Relationships, and next to Merchandise click **Edit**.
3. Click **Change Field Type**, and then select Master-Detail Relationship.
4. Click **Next**, and then **Save**.

Now you can create the workflow rules.

1. From Setup, click **Create** | **Workflow & Approvals** | **Workflow Rules**
2. On the All Workflow Rules page, click **New Rule**.
3. Select Line Item as the object, and click **Next**.
4. In the Rule Name field, enter Line Item Updated.
5. For Evaluate the rule when a record is: select created, and every time it’s edited.
6. In the Rule Criteria field, leave criteria are met selected.
7. In the Field drop-down list, select Invoice: Status. In Operator, select equals. For Value, click the lookup icon and choose Open, and click **Insert Selected**.
8. Click **Save & Next**.
9. Click **Add Workflow Action** and choose **New Field Update**. The New Field Update wizard opens.
10. In the Name field, enter Update Stock Inventory.
11. In the first Field to Update drop-down list, select Merchandise. In the second, select Quantity.
12. Select Use a formula to set the new value.
13. Click **Show Formula Editor**.
14. Click **Insert Field** and choose **Line Item &gt;** | **Merchandise &gt;** | **Quantity**. Click **Insert** to add the field to the editor.
15. Click **Insert Operator** and choose **– Subtract**.
16. Click **Insert Field** and choose **Line Item &gt;** | **Quantity**. Click **Insert** to add the field to the editor. The completed formula should be Merchandise__r.Quantity__c - Quantity__c.
17. Click **Check Syntax**, and make corrections if necessary.
18. Click **Save** to close the New Field Update wizard and return to Step 3 of the Workflow wizard.
19. On the Specify Workflow Actions page, click **Done**.

 
##Step 5: Activate the Workflow Rule##

This is a tiny step, but it’s an important one. By default, workflow rules are not active.

1. In Setup click **Workflow & Approvals** | **Workflow Rules** to get to the All Workflow Rules page.
2. Next to Line Item Updated and Populate Unit Price, you’ll see an **Activate** link. Click the link next to each workflow rule.

**Tell Me More...**

Workflow rules are not activated by default, because you might turn off workflow rules when running bulk processes. For example, you might want to update a whole bunch of records at the same time, and firing the workflow rule each time wouldn’t invalidate your processes. Workflow rules can also do things like send email updates, and you might not want to send thousands of emails when you’re doing a simple price change.

##Step 6: Try Out the App##

Now try out the revised app and see how the new workflow rule implements your business logic.

1. Click the Invoices tab and either create a new Invoice or edit an existing Invoice.
2. Add a **New Line Item** and after you've chosen the Merchandise, click **Save**.
3. Click back into the detail page for the new Line Item and notice how the workflow rule automatically populated the Unit Price field by looking up the Price of the Merchandise that you selected. Sweet.


