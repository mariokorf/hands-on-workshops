#Create an Approval Process#

**Level:** Beginner; **Duration:** 10–15 minutes

An approval process specifies the steps necessary for a record to be approved and who must approve it at each step. A step can apply to all records included in the process or just records that have certain attributes. An approval process also specifies the actions to take when a record is first submitted for approval and that record is approved, rejected, or recalled.

##Step 1: Create an Approval Process##

To create an approval process, you start in Setup.

1. From Setup, click **Create** | **Workflow & Approvals** | **Approval Processes**.
2. In the Manage Approval Process For drop-down list, choose Line Item.
3. Click **Create New Approval Process** and then **Use Jump Start Wizard**.
4. In the Name field, enter Approve Unit Price Change
5. Click the drop-down list next to Use this approval process if the following, and choose Formula evaluates to true.
6. In the formula field, click **Insert Field**, select Line Item &gt; and then select Unit Price. Click **Insert**.
7. Click **Insert Operator** and select **&lt;&gt; Not Equal**.
8. Click **Insert Field**, select Line Item &gt;, select Merchandise &gt; and then Price. Click **Insert**. Before moving on, make sure your screen looks like:
9. Now you need to assign the approval to someone. For large companies where multiple people could have the ability to grant approval, you might assign this to a queue. In DE orgs there are only two users, so click the option for Automatically assign to approvers and choose Admin User. (If you’ve edited your profile, this will be your name, note that you may need to click the lookup icon if you don't’s see your name listed.)
10. Make sure your screen looks like this and then **Save** your work. 
11. Click **OK** in the pop-up, and then click** View Approval Process Detail Page**

##Step 2: Examine the Approval Process Detail Page##

The detail page of the approval process has a lot going on, and it's worth a minute to explore the user interface.

1. Edit every step of an approval process.
2. Clone or delete an approval process.
3. Activate and deactivate an approval process.
4. View an approval process diagram as a flow chart.
5. View general details of the approval process.

In addition, you can add new steps and actions (email alerts, field updates, and outbound messages) wherever you want.

##Step 3: Modify Approval Process Actions##

In this step you modify the approval process so that if the price change is rejected, the price reverts back.

1. In the Final Approval Actions section, click **Edit** next to Record Lock.
2. Choose **Unlock the record for editing**, and then click **Save**.
3. In the Final Rejection Actions section, click **Add New** and choose **Field Update**.
4. In the Name field, enter Reset Price.
5. In Field to Update, choose Unit Price.
6. Select Use a formula to set the new value.
7. Click **Show Formula Editor**.
8. Use the Formula Editor to select Line Item &gt;, then Merchandise &gt;, then Price.
9. Click **Insert**, and then click **Save**.

##Step 4: Activate the Approval Process##

Just like workflow rules, before you can use an approval process, you need to activate it. This might seem like an unnecessary step until you think about situations where you might not want an approval process to run. For example, let's say you want to run a special promotion and decrease the price of a certain laptop in all open invoices. This would fire off the approval process for every open invoice, creating a bottleneck to getting orders out the door. In a case like this, you'd want to deactivate the approval process before running the batch update. When you're finished, you'd activate the approval process again.

1. Click **Activate** and then click **OK** in the pop-up.
2. While you’re on the detail page, click **View Diagram** to get a visual representation of your approval process. You can click any of the nodes and get more information.

Before you can see how the approval process works, you need to make sure that your users will be able to submit the relevant records for approval. Otherwise, the approval process will never start! In this step, you add the Submit for Approval button to the Line Item page layout.

1. From Setup, click **Create** | **Objects**, and click **Line Item**.
2. In the Page Layouts related list, click **Edit** next to Line Item Layout.
3. From the Buttons category in the palette, drag the **Submit for Approval** button to the Standard Buttons area.
4. Click **Save**.

Now all users assigned to this page layout will be able to submit line items for approval.

##Step 5: Try Out the App##

Now it's time to try out the new approval process and simulate the workflow as both the submitter and approver of a change.

1. Click the Invoices tab, and choose an existing invoice.
2. Add a new item to the invoice.
3. Click **Edit** next to the new line item, reduce the value for Unit Price, and then click **Save**.
4. Click **Submit for Approval** and **OK**.
5. Notice that the record is locked, you get a default email, and in the Approval History related list the overall status is Pending.
6. Click the link you received in your email, add a comment, and then click **Approve**. Notice the record is unlocked and the overall status is Approved.
7. Repeat steps 1-6, but this time reject the price change. Notice that Unit Price reverts to the default merchandise price.

###Tell Me More….###

Approval processes are automatically included on your Home tab. If you click the Home tab, you can see the items you need to approve and reject right there.

##Step 6: Configure Approvals for Chatter and Salesforce1##

Approval processes have built-in support for Chatter posts, which means they can also show up on your mobile device.

1. In Setup, click **Customize** | **Chatter** | **Settings**.
2. Click **Edit**.
3. Select Allow Approvals, and then click **Save**.

Approval feed items will now show up on your users’ Chatter feed on the full site and in Salesforce1.
