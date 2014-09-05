#Create Views of Data#

**Level:** Beginner; **Duration:** 5 minutes

A custom object tab in an application is a navigational element that, when clicked, displays data for the corresponding object. For example, when you click on **Invoices** in the Warehouse app, you see a default list view of the most recent invoices that you've touched. This tutorial teaches you more about views and how to create custom views to meet specific needs.

**Step 1: View a List of Invoices**

Notice how the All view sorts records alphabetically and provides navigation controls for large lists. So, right out of the box, you have several default views that list invoices. But what if you need a custom view? No problem.

1. Select the Warehouse app and click the Invoices custom object tab. By default, the Recent Invoices view displays your most recently viewed records — notice the pick list in the upper right corner of the view. You can update the view display by changing the picklist to Recently Created and various other options.
2. Click **Go!** to switch from the Recent Invoices view and display a list of All invoices. Notice how the All view sorts records alphabetically and provides navigation controls for large lists.   

**Tell Me More....**

Right out of the box, you have several pre–built views that list invoices, with navigation and sorting. But what if you need a custom view, for example you wanted to see only closed invoices? No problem.

##Step 2: Create a New View##

In this step, you create a custom view that shows only invoices with a status of Closed.

1. On the Invoices tab, click **Create New View** and name it Closed Invoices.
2. Select All Invoices, and specify a filter criteria: Status equals Closed.
3. A custom view shows only the fields you select. Update the Selected Fields list with only Invoice Number, Status, and Last Modified Date.
4. Select Visible only to me and then click **Save**.

**Tell Me More....**

Notice that you restricted the visibility of this view. That's a really important feature because you can create views of data for everyone in your company, groups of people, or a view that only you can see.

##Step 3: Try Out the App##

In this step, you create a custom view that shows only invoices with a status of Closed.

1. To display the new Closed Invoices view from anywhere in the app, click the Invoices tab, select Closed Invoices, and click **Go!**
2. When your screen refreshes, you might not have any invoices in the new Closed Invoices view. If this is the case, edit one or more invoices and change the status to Closed. Now go back to your view of closed invoices and notice the power of custom views.

**Tell Me More....**

At this point, you might think that views are read-only displays of data for a custom object — not so. In the new Closed Invoices view, move over the Status field for a specific invoice. Notice that a pencil icon appears in the field, indicating that the field is editable inline, right from the view. Double-click the Status field and the app provides you a way to edit the field.
