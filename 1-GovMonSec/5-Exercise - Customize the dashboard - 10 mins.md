# Exercise - Customize the dashboard

* 10 minutes

Dashboards are a flexible tool for managing different aspects of Azure services through the Portal. They make it convenient to monitor the state of your services. Because they are shareable, they help ensure that everyone on your team sees the same data and stays aware of the state of your critical components. Let's create a new dashboard and add some tiles to it.

## Login to the Azure Portal

1. Open the [Azure portal](https://portal.azure.com) in a browser.

2. Sign into Azure using the Microsoft account email address and password you created for this session.

## Create a new dashboard

1. In the Azure portal, select **Dashboard** from the left navigation, then click the **New Dashboard** button at the top.

2. In the box saying **My Dashboard**, change the name to **Customer Dashboard**.

## Add and configure the Clock Tile

1. In the tile gallery, drag the clock onto the workspace. Place it on the top right of the available space.

2. On the **Edit clock** blade, change the Location to **Pacific Time (US & Canada)**.

3. Under **Time format**, click **24 hour**.

4. Click **Done**.

5. Repeat the preceding four steps, except select **Eastern Time (US & Canada)**. You should now have two clocks, one showing the time on the West Coast, the other on the East Coast.

## Resize a tile

1. In the **Tile Gallery** pane, click **All resources**, and then drop the tile onto the top left-hand side of the new dashboard workspace.

2. Click the tile, right-click the ellipsis, and then click **6x6**.

3. Click the gray corner on the bottom right-hand side of the tile, and resize the tile to 3.5 vertically by six horizontally. Note that when you finish resizing, it adjusts to 4x6.

4. In the Tile Gallery, click the **Resource Groups** tile, and drag it onto the workspace. Place it underneath the **All resources** tile.

5. In the Tile Gallery, click the **Service Health** tile, and drag it onto the workspace. Place it to the right of the **All resources** tile.

6. Continue to add the following tiles, rearranging them to fit:

    * Help + Support
    * Quick Tasks
    * Marketplace
    * What's New
7. When you have added these tiles, click **Done customizing**. The **Customer Dashboard** dashboard should appear.

## Clone a dashboard

You now want to create a very similar dashboard for some other customers.

1. Click the **Clone** button.

2. Rename the dashboard from **Clone of Customer Dashboard** to **Azure AD Admin Dashboard**.

3. On the **Resource Groups** tile, click the dustbin icon to delete this tile.

4. From the Tile Gallery, add the following tiles:

    * Organization Identity
    * Users and Groups
    * User Activity Summary
    * Welcome to the Azure AD Admin Center
5. Reposition the tiles as necessary, and then click **Done customizing**.

## Share a dashboard

You now want to make this dashboard available to other users. To do this, carry out the following steps:

1. From the Azure AD Admin dashboard, click the **Share** button at the top.

2. On the **Sharing and access control** panel that appears, verify that the **Publish to the 'dashboards' resource group** checkbox is checked.

3. Click **Publish**, and then close the **Sharing + access control** blade.

4. Use the dropdown at the top to navigate to the **Customer Dashboard**.

    Note that in **All resources**, a Shared dashboard resource has appeared.

5. Repeat steps 1 to 3 to share the Customer Dashboard.

## Edit a dashboard.json file

To show how you can download and edit a dashboard file, carry out the following steps:

1. Click **Download**.

2. Open Windows Explorer, and navigate to your Downloads folder.

3. Find the _Customer Dashboard.json_ file and double-click it.

4. In your file editor, look for the text _ClockPart_.

5. On the first occurrence of ClockPart, change the previous **rowSpan** value to 1.

6. On the second occurrence of Clockpart, also change the previous **rowSpan** value to 1.

7. On the second occurrence of Clockpart, change the Y value from 2 to 1.

8. Save the _Customer Dashboard.json_ file and close your code editor.

9. On the Azure dashboard, click **Upload**.

10. In the **Open** dialog box, browse to the Downloads folder, and double-click _Customer Dashboard.json_.

    Note that the clocks have resized to one row high, and the bottom clock has moved up one row.

## Select a shared dashboard

You've realized that you don't like the smaller clocks, and you want to return to the earlier shared version of the Customer Dashboard. You can do that either by editing the file and uploading it again or by accessing the shared version. To do that, carry out the following steps:

1. Click the down arrow next to **Customer Dashboard**.

2. Click **Browse all dashboards**.

3. On the **All dashboards** blade, under **TYPE**, select **Shared dashboards**.

4. Click **Customer Dashboard**.

5. Close the **All dashboards** blade.

    Note that the clocks have returned to their original size.

## Switch to full screen

1. Click the down arrow next to **Customer Dashboard**.

    Note that there is another Customer Dashboard, without the shared symbol next to it. Click that version of Customer Dashboard, and the clocks become small again.

2. Switch back to the shared Customer Dashboard.

3. Click the **Full Screen** button.

    Note that the browser menus and bars have all disappeared.

4. Click the **Exit Full Screen** to return to the standard screen.

## Unshare a dashboard

If you want to prevent a shared dashboard from being available for selection, you can _unshare_ it. To unshare a dashboard, carry out the following steps:

1. Click the **Unshare** button. The **Sharing + access control** blade appears.

2. Click the **Unpublish** button.

3. In the confirmation message box, click **OK**.

4. Click the down arrow next to **Customer Dashboard**.

5. Click **Browse all dashboards**.

6. On the **All dashboards** blade, under **TYPE**, select **Shared dashboards**.

    Note that **Customer Dashboard** no longer appears in the list of available dashboards.

7. Close the **All dashboards** blade.

## Delete a dashboard

1. Ensure that the **Azure AD Admin** dashboard is selected.

2. Click the **Delete** button.

3. In the **Confirmation** message box, select the checkbox to confirm that this dashboard will no longer be visible, and then click **OK**.

## Reset a dashboard

1. Ensure that **Customer Dashboard** is selected.

2. Click **Edit**.

3. Right-click on the workspace, and click **Reset to default state**.

4. In the **Reset dashboard to default state** message box, click **Yes**.

    Note that the Customer Dashboard has reset to its default tiles.

5. Click **Done customizing**.

Congratulations! You have now created and edited dashboards, shared them, altered them as **.JSON** files, unshared and finally, reset them to the default state. You should now be able to see what powerful tools dashboards can be and how you can use them to create efficient interfaces for differing roles within an organization.
