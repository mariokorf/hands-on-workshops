#Create New Users#

**Duration:** 5–10 minutes

Once you have profiles and permission sets in place, you can turn your attention to users. Every new org starts with a super-user administrator that can access and customize everything in the organization, including profiles, permission sets, and other users. You happen to be logged in as that super-user right now. Because you don’t want everyone to have that kind of power and access, you’ll want to restrict what people can do.

In this tutorial you create two new users that represent people that work in the warehouse: a manager and a salesperson. Yes, these are the same names for the profiles and permission sets you created earlier, but now you’ll assign them to people.

**Step 1: Create New Users**

Use the following steps to create a new user that serves a "sales manager." In the following steps, make sure to use an email address that you can access immediately:

1. In the Setup area, click **Manage Users** | **Users**.
2. Click **New User**.
3. Fill out the form as follows:
    - First Name:Sales
    - Last Name:Manager
    - Email: _enter your email address_
    - Username:_your username_.manager@_your domain_
    - Nickname: _your username_.manager
    - Role: Leave this field blank for now, you’ll assign roles later.
    - User License:Salesforce Platform
    - Profile:Warehouse App User
    - At the very bottom, clear the checkboxes for the newsletters, but make sure Generate new password and notify user immediately: is checked.

4. Click **Save**.

Repeat the process to create a new that serves as a "salesperson," with the following exceptions:

- First Name:Sales
- Last Name:Person
- Email: _enter your email address_
- Username:_your username_.sales@_your domain_
- Nickname: _your username_.sales
- Role: Leave this field blank for now, you’ll assign roles later.
- User License:Salesforce Platform
- Profile:Warehouse App User
- At the very bottom, clear the checkboxes for the newsletters, but make sure Generate new password and notify user immediately: is checked.

You now have two users, both using the Warehouse App User profile. Also, you should have two emails in your email inbox: activation emails for each new user.


**Step 2: Test Record Access**

The Warehouse App User profile is assigned to both of these new users, so while they can log into the DE org and start the Warehouse app, they can’t do much more. First, you’ll log in as the Sales Manager.

1. You should have an email in your inbox, click the link to log in as the Sales Manager.Note  

2. This is a good time to switch between browsers, as noted in the Prerequisites.  

3. Change your password and then you should see the Home tab.
4. Notice that the default app is Warehouse (if you don’t see Warehouse that’s OK, you just missed that setting in the profile, either edit the profile or select the Warehouse app now), but that you can't see the Merchandise or Invoices tabs. Why not? Because the user's profile doesn't provide the permissions necessary to access to the underlying objects that power the app.

**Step 3: Assign Permission Sets to Users**

To give the Sales Manager and Sales Person users access to the permissions they require, simply update each user with the appropriate permission set.

1. Switch back to the browser with your administrator login.
2. In the Setup area, click **Manage Users** | **Users**.
3. Click **Manager, Sales** to go to this user's detail page.
4. In the Permission Set Assignments section, click **Edit Assignments**.
5. Add both the Warehouse Merchandise Manager and Warehouse Sales Person permission sets to the user's list of Enabled Permission Sets and click **Save**.
6. Repeat the previous steps for the **Person, Sales** user, but this time, add _only_ the Warehouse Sales Person permission set to the user's list of permission sets.

**Step 4: Test Record Access**

Now it's time to see the effects of adding the permission sets to the two users.

1. Switch back to your other browser that's already logged into the DE org as the Sales Manager, refresh the page, and notice that the Merchandise and Invoices tabs are now available.
2. Click on the Merchandise tab.
3. Click **Go!** next to View: All to display all records.
4. Click on the Invoices tab and check those out, too.
5. Now log out and, using the activation link in your email, log in as the Salesperson (and change your password).
6. Confirm that the Salesperson can see the Invoices tab, but not the Merchandise tab, as governed by the user's permission sets.

**Tell Me More**

As you can see, it’s pretty easy to create profiles and permission sets and then assign them to different users.

