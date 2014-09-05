#Create a Profile and Permission Set#

**Duration:** 5–10 minutes

Before creating users, it’s best to create one or more profiles and permission sets. Profiles and permissions sets are collections of functional permissions and settings that control what a user can do. For example, profiles and permission sets control:

- System-level access, including time- and IP-based login restrictions as well as permissions that apply to different functions within an organization such as the ability to manage users
- Object-level access, including permissions to create, update, and delete records for each object in the database
- Field-level access, including the ability to read or edit fields in objects
- Access to invoke Apex classes and custom logic

So what's the difference between a profile and a permission set? Users can have exactly one profile, but could have a number of permission sets. Here’s how that might work; suppose you need to implement a security policy that has many types of users with similar yet varying privilege requirements. Rather than building and managing many profiles that differ only slightly, it’s more efficient to build one profile to manage the common permissions and then use permission sets to manage other specific sets of permissions.

Note

Before you get started creating profiles and permission sets, be aware that the available permissions you can configure for a profile or permission set depend on the user license you associate with it.

**Step 1: Create a Profile**

Complete the following steps to create a base profile for the Warehouse app:

1. From Setup, click **Manage Users** | **Profiles**.
2. Next to **Standard Platform User** click **Clone**.
3. Name the new profile Warehouse App User, then click **Save**.

**Tell Me More....**

The profile you clone is important to consider because it determines what type of user license to use. For example, in a DE org, you have three Salesforce Platform User licenses that these tutorials intend to use.

**Step 2: Edit a Profile**

Now edit the new profile so that it delivers the common permissions that all types of Warehouse app users need to do their work. Specifically, every Warehouse app user needs to be able to:

- Switch to the Warehouse app
- See the Invoices tab, but not necessarily the Merchandise tab
- Read Merchandise records because Merchandise is a lookup object

Complete the following steps to create the baseline profile for Warehouse app users:

1. On the Warehouse App User detail page, click **Edit**.
2. In the Custom App Settings section, select Visible and Default for the Warehouse app.
3. In the Tab Settings section, set Invoices to Default On and Merchandise to Tab Hidden.
4. In the Custom Object Permissions section, enable Read for the Merchandise object (see the following image) and then click **Save**.

 **Step 3: Create the Manager Permission Set**

In this step, you are going to configure security for two different types of Warehouse app users: managers and sales people. Both types of users can use the Warehouse App profile for their base permissions, but need different privileges thereafter. To handle this requirement, create two different permission sets.

Use the following steps to create the Warehouse Manager permission set:

1. From Setup, click **Manage Users** | **Permission Sets** and then **New**.
2. For Label, enter Warehouse Manager.
3. For User License, select Salesforce Platform and click **Save**.

Now modify the new permission set so that it provides access to create, update, and delete Merchandise object records, and view the Merchandise tab.

1. From the Warehouse Manager permission set detail page, click **Object Settings**.
2. Click **Merchandise**.
3. Click **Edit**.
4. In Tab Settings, enable Available and Visible.
5. In Object Permissions, enable all permissions.
6. Click **Save**.

**Step 4: Create the Salesperson Permission Set**

Use these steps to create the Warehouse Salesperson permission set:

1. From Setup, click **Manage Users** | **Permission Sets** and then **New**.
2. For Label, enter Warehouse Salesperson.
3. For User License, select Salesforce Platform and click **Save**.

Now modify the new permission set so that it provides access to create, update, and delete Invoice and Line Item object records, and view the Invoices tab.

1. From the Warehouse Salesperson permission set detail page, click **Object Settings**.
2. Click **Invoices** and then **Edit**.
3. In Tab Settings, enable Available and Visible.
4. In Object Permissions, enable these permissions: Read, Create, Edit, and Delete.
5. Click **Save**.
6. In the breadcrumb menu, click **Object Settings**.
7. Click **Line Items**.
8. Click **Edit**.
9. In Object Permissions, enable the following permissions: Read, Create, Edit, and Delete.
10. Click **Save**.

The Warehouse Salesperson permission set doesn’t give access to Merchandise, only Invoices and Line Items. You can see this on the Object Settings page for the permission set.
