#Create a Dashboard#

**Level:** Beginner; **Duration:** 15 minutes

Dashboards in Salesforce are like a dashboard in your car, showing you important information at a glance. Dashboards can show data in charts, gauges, tables, metrics, or Visualforce pages. Naturally, you can customize dashboards to show exactly what you want.

In this tutorial, you create a new dashboard that's powered by the report you created in the previous tutorial.

##Step 1: Create a New Dashboard##

Create a new dashboard for the Warehouse app that's powered by the Merchandise in Stock report that you’ve created.

1. Click the Reports tab and then **New Dashboard**.
2. Click the editor's Components tab, then drag the Vertical Bar Chart component and drop it in the first column of the new dashboard.
3. Now click the editor's Data Sources tab, and under **Reports** | **Unfiled Public Reports**, drag your report and drop it on top of the new Vertical Bar Chart component that's in the dashboard.

##Step 2: Add a Pie Chart Component##

That was so easy. Why not play around with adding a different type of dashboard component, just for fun?

1. Repeat the previous steps, but this time use a Pie Chart component in the second column.
2. Then click Remove this column () in the header of the third column to remove the unused third column from the layout. When you are finished, the dashboard preview should look similar to the following.
3. Click **Save**, name the dashboard Merchandise Overview, and click **Save**.


##Step 3: Try Out the App##

1. **Close** the editor, and in the pop-up dialog, choose **Save and Close**. The dashboard then runs automatically when you leave the editor. Your dashboard should look similar to the following image.
2. To access the dashboard at any time, click the Reports or Dashboard tab in the Warehouse app.

**Tell Me More....**

- When you set a running user for a dashboard, it runs using the security settings of that single, specific user. All users with access to the dashboard see the same data, regardless of their own personal security settings. To set the running user, click  next to the View dashboard as field.
- Dashboards can be updated either manually or on a schedule, and they can be delivered through email and mobile.
- A dashboard won't automatically refresh unless it is set to do so. Each time you view a dashboard, it indicates in the upper-right corner when it was last refreshed. To update the data in the dashboard, click **Refresh**.
- Try adding a filter when editing the dashboard by clicking **Add Filter**. A filter lets you see different views of dashboard data based on filter conditions. You can add up to three filters per dashboard with up to ten conditions on a filter. Instead of filtering at the report level, you directly manipulate dashboard data.
