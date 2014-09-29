**Tutorial 4: Quickly Create Records Using Global Actions**

There are two kinds of publisher actions, global actions and object-specific actions. Global actions let users create records that aren’t related to any other record. Object-specific actions are created in the context of another record, and are automatically related to that record.

Another way to think of global actions are things that users want to do quickly, but not necessarily completely. For example, imagine one of your users works at a trade show and meets new people all day long. She needs a way to quickly add someone as a contact without navigating to a record or associating this person with any other information. That’s what a global action is for, quick things that users can follow up with later. In fact, there’s a built-in _global _action for creating a New Contact. There’s also a built-in _object-specific _action on the Account object. If you were to navigate to an account record and tap , you’d see there’s also a New Contact action there. If you create the new contact in the context of this account, the contact is already associated with the account. The names of the actions are the same, but they behave differently when called from different places.

You can include global actions on global publisher layouts, as well as page layouts for any supported object. In this tutorial you add the global action to the global publisher layout.

**Step 1: Create a Global Action**

In this step you create a global action that creates new lesson directly from the feed.

1. **In Setup, go to Create &gt; Global Actions &gt; Actions.  
Notice there are a number of actions to choose from; you’ve seen some of these already in the mobile app. **
2. **Click New Action. **
3. **For Action Type, select Create a Record. **
4. **For Target Object select Lesson. **
5. **For Label, enter ****Add Lesson****. **
6. **ClickSave. **

After saving, the action layout editor opens. Typically at this point you’d customize the fields that show up here, but there aren’t many fields on this object, so it’s not necessary yet.

**Tell Me More....**

At the bottom of the action layout editor there’s a section for predefined values. If you predefine a required field, you don’t need to show that field on the page. This is not only faster for the user, but it means there are fewer things on the screen. Predefining fields is a great way to customize the mobile experience, and you’ll learn about that in just a bit.

**Step 2: Customize the Global Publisher Layout**

Before the global action will show up either in the full Salesforce site, or in the Salesforce1 mobile app, you need to add it to the global publisher layout.

1. **In Setup, go to Create &gt; Global Actions &gt; Publisher Layouts. **
2. **Next to the Global Layout, click Edit. **

1. **In the editor, notice there are a number of items in the Publisher Actions area, such as Post, File, New Task, etc. Drag the Add Lesson action into the left side of the Publisher Actions section, between Post and File. **
2. **ClickSave. **
3. **Now try it out by opening the mobile app. Refresh the app by pulling down, then tap , and then tap Feed. **
4. **Tap and you’ll see the Add Lesson item in the publisher. **

**Tell Me More....**

- Global actions show up in the publisher on pages to which the global publisher layout applies: in Chatter and in any layout that hasn’t been overridden by a more specific publisher layout. 
- If you’ve used page layouts before, you know that page layouts can be assigned to user profiles. The global layout is assigned to all user profiles by default, so you don’t need to assign the layout to a profile in order to see the global action you created. But it’s useful to know that if you have different users that need different global layouts, it’s easy to change right here by clicking **Publisher Layout Assignment**. 
