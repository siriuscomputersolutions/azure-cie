# Exercise - Use the Azure portal

* 10 minutes

In this lab, you will learn about features and services available in the Azure portal user interface (UI).

## Login to the Azure Portal

1. Open the [Azure portal](https://portal.azure.com) in a browser.

2. Sign into Azure using the Microsoft account email address and password you created for this session.

## Toolbar

The Azure portal has several features and services available; let's look at some of the more common areas you'll tend to use. First, take a moment to hover your mouse pointer over each of the icons in the top menu bar for a few seconds each. You should see a tooltip label pop-up for each one. This is the name of the menu item. You will use these icons later.

![Screenshot of the Azure portal icon bar](images/azureportal1.png)

## Services blade

1. In the left-hand pane, click **All services**. Take a couple of minutes to scroll down the list to see how many services Azure offers.

    ![Screenshot of all the services blade](images/azureportal2.png)

2. You can search for services through the _filter_ box.

3. Select **Virtual machines**. If you don't see it, use the filter box. The **Virtual Machines** blade appears. There is nothing currently showing because you have not defined any virtual machines.

4. Click the **+ Add** button. The **Create a virtual machine** blade appears, as in the previous exercise.

5. Click the **X** in the top right-hand corner to close the **Create a virtual machine** blade.

6. Click the **X** in the top right-hand corner to close the **Virtual machines** blade.

7. You should now be back at the Dashboard page. If not, you can always click on **Dashboard** in the left-most pane.

## Notifications blade

1. On the icon bar menu bar, click the **Notifications** (bell) icon. This will list any pending notifications.

    ![Screenshot of the notifications blade](images/azureportal3.png)

2. If any notifications appear, hover your mouse over one of them. Click the **X** that appears in that notification to dismiss it.

3. Click **Dismiss all**. You should have no notifications showing.

4. Click the **X** in the top right-hand corner to close the **Notifications** pane.

## Azure Cloud Shell

![Icon representing the Azure Cloud Shell](images/azureportal4.png)

The Azure Cloud Shell allows you to use a command-line interface (CLI) to execute commands in your Azure subscription. You can access it by clicking the (`>_`) icon in the toolbar. However, it isn't available in the Sandbox environment - so you will only be able to do this in your own active subscriptions. You can also navigate to [https://shell.azure.com](https://shell.azure.com) to launch a Cloud Shell in the browser independent of the portal.

When you launch the shell, you will see a Welcome window. You can choose either a **Bash** or **PowerShell** environment, depending on your personal preferences. You can also change the shell at any time through the language drop-down on the left side of the shell.

Finally, there are a variety of management and programming tools included in the created environment.

* Azure command-line tools (Azure CLI, AzCopy, etc.)
* Languages / Frameworks including .NET Core, Python, and Java
* Container management support for Docker, Kubernetes, etc.
* Code editors such as vim, emacs, code, and nano
* Build tools (make, maven, npm, etc.)
* Database query tools such as `sqlcmd`

## Settings

![Icon representing the settings panel](images/azureportal5.png)

1. Click the **Settings** (cog) icon to open the **Portal settings** pane.

2. Drop down the **Log me out when inactive** setting, and select **After one hour**.

3. Under **Choose a theme**, select the different colored themes and observe the changes to the portal UI. Leave it set to the one you like the best.

4. Under **High contrast theme**, try the three different options.

5. Disable Toast notifications. This means notifications will not appear as pop-up "toast"-style notifications, but will still show up in the Notifications (bell) icon as always.

6. Note the **Allow double-click on dashboard to change theme** setting, enabled by default. When enabled, you can use the mouse to cycle through the various color themes without opening this Settings menu by double-clicking the left mouse button in the Dashboard view's background area. Disable this option to avoid accidentally changing your color theme.

7. Click **Apply** to accept your changes.

8. Click the **Settings** (cog) icon in the top menu bar and, under **Language**, select **Español**, and then click the **Refresh** button. If a **Translate this page** dialog box appears, close the box. Note that the whole portal is now in Spanish.

9. Click the **Settings** (cog) icon in the top menu bar and, under **Idioma**, select **English**. Click the **Actualizar** button. The portal returns to English.

## Feedback blade

![Icon representing the feedback panel](images/azureportal6.png)

1. Click the **Feedback** (smiley face) icon to open the **Send us feedback** blade.

2. Type your impressions of Azure in the **Tell us about your experience** box, click the box that says **Microsoft can email you about your feedback**, and click **Submit Feedback**.

3. A **Feedback sent** message will appear, and then close. You should now be back at the Dashboard.

## Help blade

![Icon representing the feedback panel](images/azureportal7.png)

1. Click the **Help** (`?`) icon to show the **Help** blade.

2. Click the **Help + Support** button.

3. In the **Help + Support** blade, under **Support**, click **New support request**. To create a new support request, you would fill in the information in each of the following sections, and then click **Create** to lodge the issue.

    * **Basics:** the issue type
    * **Problem:** severity of the problem, a summary and description, and any additional information
    * **Contact information:** preferred contact method and the information associated with this contact method
4. You can view the status of your support requests by clicking on **All support requests**.

**Note**
Support requests can only be created using an active paid subscription. Creating support requests from a free Microsoft Learn sandbox is not supported.

### What's new and other information

1. Click the **Help** icon and click **What's new**.

2. Review the features that have recently been released. Also note and explore the other **Help** menu options, such as:

* Azure roadmap
* Launch guided tour
* Keyboard shortcuts
* Show diagnostics
* Privacy + terms

1. Click the **X** in the top right-hand corner to close the **Help** blade.

2. Close the **What's new** blade. You should now be back to the Dashboard.

## Directory and subscription

![Icon representing the subscription panel](images/azureportal8.png)

1. Click the **Directory + Subscription** (book and filter) icon to show the **Directory + subscription** blade.

    This is where you can switch between multiple subscriptions or directories. You should see the Concierge subscription here, and if you have an Azure account tied to the same email address, your own subscription.

    There is also a link to learn more about directories and subscriptions.

2. Click the **X** in the top right-hand corner to close the **Directory + subscription** blade.

## Profile settings

1. Click on your name in the top right-hand corner of the portal. Options include:

    * Sign in with another account, or sign out entirely
    * View your account profile, where you can change your password
    * Submit an idea
    * Check your permissions
    * View your bill
    * Update your contact information

    Note that some items do not appear unless you click the "..." icon.

2. Click "..." then **View my bill** to navigate to the **Cost Management + Billing - Invoices** page, which helps you analyze where Azure is generating costs.

3. If you're using your own account and not sandbox, you can select a subscription from the drop-down list.

4. Click a billing period.

5. Note the service costs and check them against what you expect for your current subscription.

6. Click the **X** in the top right-hand corner to close the **Costs by service** blade.

7. Click the **X** in the top right-hand corner to close the **Cost Management + Billing - Invoices** page.

8. You should now be back at the Dashboard.

Now that we've explored all the main areas of the Azure portal, let's look at one of the most useful features - Dashboards.
