#Modify a Page Layout#

**Level:** Beginner; **Duration:** 20-30 minutes

In [Create Views of Data](file:///Users/mkorf/Documents/Content/views_intro.htm) you learned how to create a customized view for _lists_ of data. However, you can also customize what's on the detail page for a particular record, or the _page layout_. Click an invoice and take a look at the default page layout for all invoices, which should look similar to the following:

This tutorial teaches you more about page layouts and how to modify them.

##Step 1: Open the Page Layout Editor##

Use one of the following ways to open the page layout editor.

- While on the record page that you want to modify:
    - Click **Edit Layout**.
    - Click the Quick Access menu on the right, and choose **Edit Layout**.

- From Setup, click **Create** | **Objects**, click the object you want to change the layout of, scroll down to the Page Layouts section, and then click **Edit** next to the layout you want edit.

##Step 2: Understand a Page Layout##

Notice that the editor itself has upper and lower sections. The upper section is a retractable toolbox called the _palette_ (highlighted in the following image), and the lower section is the preview pane. When you scroll down the page, notice that the palette moves with you, which makes it easy for you to edit longer pages.

In the page layout itself, notice that there are several sections that organize related information.

- The Highlights Panel is useful for displaying key information at the top of the page.
- The Publisher Actions is useful for customizing the actions that appear in the publisher.
- At the top of the Invoice Detail, notice the area for standard buttons (Edit, Delete, etc.) and custom buttons.
- Next comes the Invoice Detail, which has three default sections.
    - Information typically contains fields that users can manipulate at some point during the lifecycle of a record (creation and updates). By default, this section has two columns for fields.
    - System Information typically contains fields that the platform automatically maintains—fields that users cannot edit. This section is also a two-column layout.
    - Custom Links typically contains custom navigation links.

- Below Invoice Detail is a section for Mobile Cards. By default, this section is empty, but it’s important to know that mobile cards only appear in Salesforce1.
- Last on the page is a related list for related Line Items.

You can make many changes to the page layout.

1. Hover over a section title. Notice that the mouse pointer changes, indicating that you can drag the section to a new location relative to other sections.
2. Hover over the upper-right corner of any section. Notice that two buttons appear: one for removing the section (don't click it!) and another for editing its properties. Go ahead and click . Notice that you can now edit the name of the section (only for non-default sections), when to display the section header, the section layout (one or two columns), and the tab-key order among section fields. Click **Cancel**.

##Step 3: Rearrange Fields on a Page Layout##

In this step, make some simple changes to the Invoice Detail area of the page layout.

1. Click  for the Information section (see above if you forgot how to find this) and change the section layout to one column. Click **OK**.
2. Drag the Owner field above the Status field. When you’re done, the modified Invoice Detail area should look like this.


##Step 4: Add Fields to the Related List##

As it is now, the related list of Line Items is not very informative—it only has the line item numbers. In this step, improve the related list by adding some new fields.

1. Click **Related List Properties** (the wrench icon above the Line Items section), add Merchandise and Quantity to the Selected Fields list, then click **OK**. When you return to the page layout editor, the related list preview should now appear similar to the following screen.
2. That's it — you're done modifying the page layout. At the top of the page, in the toolbox, click **Save**.

##Step 5: Try Out the App##

Check out the results of your work.

1. Click the Invoices tab to return to your app, and then click an invoice that has at least one line item.
2. Notice the rearranged fields in the Invoice Detail area, as well as the new fields in the related Line Items section.

##Step 6: Edit a Mini Page Layout##

When you are in the Warehouse app, notice the Recent Items sidebar. Specifically, move over a recent invoice and notice that you get a mini page pop-up that previews the invoice information. See below — that's not very informative, is it?

It's easy to change this default mini page layout as well.

1. Return to the page layout editor for Invoice.
2. Click **Mini Page Layout** at the top of the palette.
3. Add Invoice Number, Owner, and Status to the list of selected fields, and then click **Save**. The improved pop up should look more like:
 
