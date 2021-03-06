#Create a Warehouse App#

**Level:** Beginner; **Duration:** 5–10 minutes

Running apps in the cloud is great because there is no server to configure, no software to install, and no ongoing maintenance of your infrastructure. This tutorial teaches you how to build a cloud app.

At the heart of this app is what you want to sell: merchandise. When you create an app, you automatically create a data object that keeps track of all the elements of a particular merchandise item, such as its name, description, and price. On the Salesforce platform, these data objects are called _custom objects_. If you’re familiar with databases, you can think of them as a table.

An object comes with standard fields and screens that allow you to list, view, and edit information about the object. But you can also add your own fields to track or list just about anything you can think of. When you complete this tutorial, you’ll have a working app with its own menu, a tab, and a custom object that tracks the name, description, and price of all your merchandise, as well as screens that allow you to view and edit all of this information.

##Step 1: Build a Cloud App and Database##

You can create an app with just a few clicks. In this tutorial, you use the App Quick Start wizard to create an app that can help you manage merchandise records in a warehouse.

1. Launch your browser and go to [https://login.salesforce.com](https://login.salesforce.com/).
2. Enter your username (in the form of an email address) and password.
3. From the Force.com Setup page, click **Add App** in the Getting Started section. (If you’re starting from somewhere else, look in the upper right corner, and click **Setup**.)
4. Fill in the form as follows:
    - For the App, type Warehouse.
    - For the Label, type Merchandise.
    - For the Plural Label, type Merchandise.
![app_quick_start](https://cloud.githubusercontent.com/assets/1034381/4133229/287eac46-335c-11e4-95e0-4ff2950687a8.png)
6. Click **Create** and you see right away some of the functionality that’s automatically added.
![all_set](https://cloud.githubusercontent.com/assets/1034381/4133227/287cd59c-335c-11e4-9dd2-cc278b381d63.png)
7. Click **Go To My App** to see your new app.
![app_first_view](https://cloud.githubusercontent.com/assets/1034381/4133226/28792bcc-335c-11e4-8c0e-3853fee55af7.png)
8. Click **Start Tour** and follow along for a quick overview of your app’s built-in user interface.

1. **Force.com app menu**—Shows the apps that are available to you. The app you just created is selected.
2. **Tabs**—Provide an easy way to find and organize objects and records. In the Merchandise tab, which is open, you can create, view, and edit records. The other tabs are the standard feature tabs that are included with every app.
3. **Create records**—Click **New** to add records to your custom object. If you click this button now, you see only one data entry field in the object, but you’ll create more in the following steps.
4. **Force.com Quick Access menu**—Quickly jump to relevant app customization features. It’s available from any object list view page and record detail page, but only for users with the “Customize Application” permission.

###Tell Me More….###

An app is composed of tabs, but the tabs don’t have to be related to each other. In fact, you can modify custom apps to group all of your most frequently used tabs together in one place. For example, if you refer to the Accounts tab a lot, you can add that to the Warehouse app. You can switch between apps you created, bought, or installed by selecting them from the menu.

##Step 2: Try Out the App##

Your app doesn’t do much yet, but you can start using it right away.

1. To try out your new app, click **New** to create a new Merchandise record.
![new_merch](https://cloud.githubusercontent.com/assets/1034381/4133245/28adf05a-335c-11e4-8b2c-3450b977ceaf.png)
2. Add a new merchandise record for Laptop and click **Save**.
![new_merch_laptop](https://cloud.githubusercontent.com/assets/1034381/4133243/28a77068-335c-11e4-94a2-859ae4c5d6da.png)

##Step 3: Explore the App##

Building a simple app is really fast! But don’t let this basic app fool you. Salesforce is a powerful platform that lets you build much more sophisticated apps just as easily, and without code. Look closely around the screen to see all of the functionality included by default.
![try_out_app](https://cloud.githubusercontent.com/assets/1034381/4133252/28c044da-335c-11e4-8aec-8baf6b36e927.png)

1. Every app has full-text search functionality for all text fields of an object and Chatter feeds.
2. Every object in Salesforce automatically has an attached "feed," called Chatter, that lets authorized app users socialize about and collaborate on the object. Using Chatter, users can post updates in an object’s feed, comment on posts, and follow (subscribe to) the feed to get pushed updates when they happen. For example, on a Merchandise record, one user might post a question about the record, to which followers and other users can comment in reply.
3. Every DE org has a recycle bin that you can use to view and restore deleted records.
4. Every record in Salesforce has an "owner," which serves as the basis for a powerful security system that supports ownership-based record sharing.
5. You can also manage activities related to a record from the Open Activities and Activity History related lists. Activities include tasks to perform (making phone calls or sending email), calendar events, and requested meetings.
6. Every DE org has a Chat window that lets users interact with one another.
