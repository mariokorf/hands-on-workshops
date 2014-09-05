#Create a Report#

**Level:** Beginner; **Duration:** 15 minutes

The Warehouse app you created with the App Quick Start wizard includes a Reports tab, where you can create, edit, run, and schedule reports. Start by creating a simple report that tells you how much stock you have for each item in your warehouse. Then you’ll use groupings and filters to get the most out of the data in your report.

Try out buckets for on-the-fly grouping, and experiment with showing your report data graphically as a chart. And once you’ve got charts mastered, take a look at how you can provide users with valuable context by embedding charts in record detail pages.


##Step 1: Create a Simple Report##

In this step, you create a simple tabular report that shows the merchandise in your warehouse and how many pieces of each are in stock. Tabular reports present data in simple rows and columns, much like a spreadsheet. They can be used to show column summaries, like sum, average, maximum, and minimum.

1. From the Reports tab, click **New Report**.
2. In the Quick Find box, enter Merchandise, and in the **Other Reports** folder, choose **Merchandise**.
3. Click **Create**.
4. In the report builder, notice that the Merchandise Name field is already there. You only need one more field: the quantity of each item. From the Fields pane, drag Quantity onto the preview.
5. Click **Save**, and give your report a meaningful name, such as Merchandise in Stock.
6. In the Report Folder drop-down list, select Unfiled Public Reports, so everyone can access it. (If you didn’t want this report to be accessible to everyone, you’d create a folder and give different people different levels of access to it. More on that later.)
7. Click **Save and Run Report**.

That’s it. Your new report is ready to go!

You can get fancy with reports, but that's all you need from this one. And as you'll soon see, even this simple report gives you a lot of functionality.

- Use the Summarize Information by drop-down list to summarize the report based on any field on the Merchandise object. For example, you could summarize on Owner Name to see who entered each piece of merchandise, as well as the count.
- Use the Show drop-down list specify whether you want to see just your merchandise, your team's merchandise, or all merchandise.
- In the Time Frame section, you can choose to run this report based on the created, modified, or last activity date, as well as choose the date range for the data you want to see.
- Click **Run Report**, and choose to run the report now or on some future date. If you choose the latter, it takes only a few more clicks to have that report in your inbox every day—or however often you want it.
- If you’d rather see a summary than a bunch of details, click **Hide Details**.
- Click **Customize** to make changes to the report, and you'll return to the familiar drag-and-drop interface you used to create the report.
- And finally, you can export the report as a printed document, spreadsheet, or CSV file by clicking **Export Details**.

**Tell Me More....**

- Click the column headers to toggle between ascending and descending order. The Grand Totals indicates the record count as well as the summaries you chose. Click **Customize** to make additional changes to this report.
- You can click through to the data records that are being reported on, a characteristic found in all reports on Salesforce. For example, click the name of any merchandise record listed in the report to view its detail page.
- A report folder's sharing settings determine who can do what with reports in that folder. Click  next to the folder in the Reports tab and click **Share**. You can give people three levels of access: Viewer, Editor, or Manager. For more information, see Share a Report or Dashboard Folder.

##Step 2: Get More Information Out of Your Report#

The report builder gives you a lot of ways to view your data. Viewing data in groups usually helps make sense of what you’re looking at. In this case, grouping by item, price, or total units sold can be helpful.

First we’ll turn our simple tabular report into a slightly fancier summary report, and then we’ll give it a grouping.

1. Click **Customize**.
2. The default format is tabular, but we want a summary report. Click **Tabular Format** and choose Summary instead.
3. Find and drag the Price field to your report.
4. Click  next to Price, click **Summarize this Field**, select Average, and then click **Apply**.
5. Click  next to Quantity, click **Summarize this Field**, select Sum, and then click **Apply**.
6. Select the Merchandise Name field (either from Fields or Preview panel) and drag it to the area labeled **Drop a field here to create a grouping**. This aggregates data by the unique merchandise item.

The report is now grouped by merchandise, and it includes the sum of quantity and the average price for each level.

**Tell Me More...**

Try adding a _cross filter_ from the Add drop-down list in the Filters pane. A cross filter lets you filter on the report's child objects using a simple with or without condition. To learn more about cross filters, watch [Using Cross Filters in Reports](http://www.salesforce.com/_app/video/reports/help/cross_filters.jsp).


##Step 3: Add Buckets to Your Report##

_Bucketing_ lets you quickly group report records without creating a formula or a custom field. For example, say you also want to group by quantity into ranges. To do this, create a bucket field on Quantity and define the ranges.

First, create a bucket field based on Quantity with ranges for small, medium, and large. You'll use the bucket field to create the grouping.

1. Click  on Quantity and click **Bucket this Field**.
2. Enter a bucket field name, Quantity Range.
3. Define ranges as Small (500), Medium (between 500–1000), and Large (greater than 1000).
4. Click **OK**.
5. Grab the Quantity Range bucket field that's already on the report and make it the first-level grouping by dragging it onto the drop zone above Merchandise Name.

Now the report shows data grouped in two levels—first, by quantity range (small, medium or large), and second, by merchandise name.

**Tell Me More....**

You can filter a bucket field just like other fields in the report. For example, set a filter for Quantity Range not equal to Small to see only merchandise with quantities in the medium or large range.

To learn more about bucket fields, watch [Getting Started with Buckets](http://www.salesforce.com/_app/video/reports/help/bucketing.jsp).

##Step 4: Show Your Report Data as a Chart##

It’s often a good idea to give users a visual way to understand the data in your report. Let's add a combination chart to our report now.

1. In the Preview pane, click **Add Chart** to create a chart to represent your data. In the Chart Editor that appears, click the vertical bar chart.
2. In the Y-Axis drop-down list, leave Sum of Quantity selected.
3. In the X-Axis drop-down list, select Merchandise: Merchandise Name. Notice the bucket field, Quantity Range, is also available, as there are two groupings.
4. Select Plot additional values.
5. In the Display drop-down list, select Line.
6. Select Use second axis.
7. In the Value drop-down list, select Average of Price.
8. Click **OK**, then **Save**.

The combination chart shows merchandise in stock (bars) against average price (line).

##Step 5: Embed the Report Chart in a Record Page##

There are many ways to share reports once you’ve created them. One of the best is to embed the report’s chart on a record detail page, where users can see it as they do their work: no need to jump over to the Reports tab. In [Modify a Page Layout](file:///Users/mkorf/Documents/Content/page_layout_intro.htm#user_interface_intro), you learned how to customize what's on the detail page for a particular type of record. Now we’ll do that for merchandise records.

1. From Setup, click **Create** | **Objects**, then choose **Merchandise**.
2. Under the Page Layouts related list, click **Edit** next to Merchandise Layout.
3. Click **Report Charts** in the palette.  

4. Drag the **Section** element onto the preview pane and place it above the Mobile Cards area. Enter Charts for the section name, and select 1-column for the layout..
5. In the Quick Find box, type the name of the report and click  to find and select the report chart. (You can add two if you want.) You can browse up to 200 recently viewed reports. But you only see reports that already have charts.
6. Drag the **Merchandise In Stock** report chart onto the layout.
7. Click **Save** and go look at a merchandise record. It will look something like:  

Now users can quickly see how much merchandise is in stock, without leaving their record detail page! Notice that, by default, the chart is automatically filtered to show data that’s relevant to the particular record type you’re looking at. You can set different filters back on the page layout. Just click  on the chart to customize it.

To learn more about embedding report charts on record pages, watch [Embedding Charts Anywhere](http://www.salesforce.com/_app/video/reports/help/Showing_Report_Charts_on_Pages/).

**Tell Me More....**

Salesforce provides an Analytics API that lets you access your data remotely and build your own apps and visualizations. There’s an API resource for almost anything you can do with reports through the standard web interface. For example, say you’ve used Visualforce to build a custom app, and you want to give that app a Reports tab. Or your users need a special kind of chart that isn’t one of the out-of-the-box report builder options.

For a quick start on using the Salesforce Analytics API, see the [Analytics API Developer Guide](http://www.salesforce.com/us/developer/docs/api_analytics/salesforce_analytics_rest_api.pdf).
