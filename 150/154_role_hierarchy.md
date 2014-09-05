#Share Records Using a Role Hierarchy#

**Duration:** 5–10 minutes

In the last tutorial you saw that private record access can get in the way of managers seeing what their employees are up to. You need to open up that record access to managers, but not necessarily _all_ managers. Ideally managers should be able to see all invoices owned by salespeople that they manage. In this tutorial, you learn how to set up and use a role hierarchy to automatically open up private records in an organization's org chart.

**Step 1: Create a Role Hierarchy**

To create a role hierarchy:

1. Switch back to the browser with your administrator login.
2. From Setup, **Manage Users** | **Roles**.Notice there’s a drop-down list of sample role hierarchies you can choose. Click through the options and notice the differences.
3. Chose Territory-based Sample and click **Set Up Roles**.
4. Under CEO, click **Add Role**.
5. For Label, enter Sales Manager and click **Save & New**.
6. For Label, enter Salesperson.
7. For This role reports to, use the lookup to select **Sales Manager**.
8. Click **Save**.
9. Now go back to the Creating the Role Hierarchy page (under **Administration Setup** | **Manage Users** | **Roles**. Expand the node for Sales Manager, and you can see the subordinate Salesperson role.

**Tell Me More....**

There are a lot of extra roles defined based on the sample template you started with. You can delete them if you want, it won’t make any difference for this set of tutorials. Note that DE orgs come only with two users, so unfortunately you can’t continue to add users.

**Step 2: Assign Users to Roles**

1. You should still be on the Creating the Role Hierarchy page, if not, navigate to Setup and click **Manage Users** | **Roles**.
2. Next to Sales Manager role, click **Assign**.
3. Add Sales Manager to the Selected list, then click **Save**.
4. Repeat the process to assign the Sales Person user to the Salesperson role.

**Step 3: Test Record Access**

Again, it's time to test the effects of your most recent security configuration changes.

1. Switch back to the browser that's logged in as the Sales Manager, then click the Invoices tab.
2. Click **Go!** next to View: All.
3. Notice that the Sales Manager user can now work with the invoice owned by the Sales Person user. That's because the role hierarchy shares private records up the role hierarchy.

**Tell Me More....**

A role hierarchy is just one option for sharing access to private records. For example, organizations often need to share sets of private records that are related by ownership or other criteria with particular users. For such requirements, you can use _groups_. All that you need to do is create a group and your _sharing rules_ using a few more clicks.

