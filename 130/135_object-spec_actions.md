**Tutorial 5: Create Related Records with Object-Specific Actions**

Object-specific actions let users create records that are automatically associated with related records. This example uses the Account and Case standard objects, which come in every Developer Edition org.

In this example, a mobile technician might want a way to create a new case while still on site with a customer. If you put a record create action on the Account object with Case as the target object, the technicians can browse to the customer account record on their mobile device, and log cases directly from there.

The overall steps for creating an object-specific action are the following:

1. **Create the object-specific action. **
2. **Choose which fields users see. Predefine required field values where possible. **
3. **Add the action to one or more of that object’s page layouts. **

**Step 1: Define an Object-Specific Action**

For this scenario, you create an invoice that’s associated with an existing account.

1. **In Setup, go to Customize &gt; Accounts &gt; Buttons, Links and Actions and click New Action. **
2. **For Action Type, select Create a Record. **
3. **For Target Object, select Case. **
4. **For Label, enter ****Create a Case ****and then Save.  
The action layout editor opens, which is where you can customize the fields assigned to the action. **
5. **Drag the ****Status ****field off the layout and back up into the palette and then Save. **
6. **You get a warning message about a required field. Click Yes, because you’ll fix that next. **

**Tell Me More....**

You just dragged a required field off the page layout. The platform gives you a warning message, as well it should, because users won’t be able to create a case from the mobile action! The reason for removing that field will become clear in the next step, when you predefine that field’s value.

**Step 2: Choose Fields and Predefine Values**

Objects can have many fields, and so when a user creates a record for that object, it can result in a long list that results in a lot of scrolling. So it’s important to choose which fields show up on the action layout. Additionally, you can predefine field values, and then remove them from the action layout.

For this example using a mobile technician, they are already on site logging the case. Rather than require them to choose a Status every time they create a case, you can predefine the field value. Then you can remove the required field from the action layout. Whenever a Create Case action is used, the status will automatically be set.

1. **In Setup, click Customize &gt; Accounts &gt; Buttons, Links, and Actions. **
2. **Click the Create a Case action you just created. **
3. **In the Predefined Values related list, click New. **
4. **From the Field Name drop-down list, select Status. **

**5. **Set its value to **Working **and then **Save**. **Tell Me More....**

Note that predefined values override default values. In the previous example, imagine that cases created on the full Salesforce site are typically new, and so whenever a case is created there, the default value is set to “Open”. But when a new case is created from a mobile device, it’s because there’s a mobile technician on site, and they are actually working on that case. New cases logged from the mobile device overrides the default value and predefines it as “Working”. As you can see, not only do predefined field values free up screen space, they can also be used to optimize for what people do when they are mobile.

**Step 3: Customize an Object-Specific Layout**

Before the action will show up either in the full Salesforce site, or in the Salesforce1 mobile app, it needs to be added to a page layout.

1. **In Setup, click Customize &gt; Accounts, and then click Page Layouts. **
2. **Next to Account Mobile Layout, click Edit.  
This is the layout you created earlier. Notice that the Publisher Actions section is empty, and there’s a message there telling you that any actions on this layout are being inherited from the global publisher layout. You don’t want that, you want to customize the actions on this layout to be pertinent to the work the mobile users need to do. **
3. **In the Publisher Actions section, click override the global publisher layout. **
4. **Click the Actions category in the palette, then drag Create a Case so that it’s the second item in the list.  
Notice there’s also a New Case item in the palette. The New Case item is a default action assigned to the Account object, but it’s not editable. You don’t want this default action, because you created a custom Create a Case action. **
5. **Click Save. The new Create a Case action will now show up in the feed on the Account detail page in the full Salesforce site, and in the publisher for the Salesforce1 mobile app for all profiles with this layout. **
6. **Now test it on your mobile device by navigating to an account. **
7. **On the detail page for an account, tap and tap Create a Case. **

You don’t see the required Status field for the case, but it’s there, and so is the association to this particular account. **Tell Me More....**

When you create object-specific layouts, put the most important ones first. Keep in mind that the first six actions in the list show up on the first page of the publisher in the Salesforce1 mobile app.
