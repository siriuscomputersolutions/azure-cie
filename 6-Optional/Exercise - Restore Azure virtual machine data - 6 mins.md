# Exercise - Restore Azure virtual machine data

* 6 minutes

A few days after your first Azure virtual machine backup was completed, the server had issues and it needs to be restored from a backup. You want to restore the virtual machine's disk and attach it to the problematic live server, and then track the restore to ensure that it has completed successfully.

In this exercise, you'll see how to restore a successful backup to replace a VM that has become corrupted, and monitor its progress.

## Login to the Azure Portal

1. Open the [Azure portal](https://portal.azure.com) in a browser.

2. Sign into Azure using the Microsoft account email address and password you created for this session.

## Restore a virtual machine in the Azure portal

### Create a storage account to use as a staging location

1. Select **All Services**, and then search for **storage accounts**. From the list, select **Storage accounts**.

    ![Select storage accounts](images/restorevms1.png)

2. Select **+ Add**, and then use the following information to create a storage account:

   **Resource Group**

    * Select **labvms-eastus**.

   **Storage account name**

    * Enter a unique name like **restorestagingYYYYMMDD**, where YYYYMMDD is replaced with today's date.

    **Location**

    * Select **East US** for the **Location**, from the list.

    **Note** - You **MUST** use **East US** for this lab, as future tasks in this lab depend on it.

    **Replication**

    * Select **Locally-redundant storage (LRS)** for **Replication**, from the list.

3. Confirm the Basics settings are correct and click **Review + create**.

     ![Specify storage account options](images/restorevms2.png)

4. On the **Create storage account** page, select **Create**.

5. Wait for the storage account to be deployed.

### Confirm the backup job has completed before proceeding

The backup job you started in a previous lab, must be completed, before you can proceed with the restore proceedure.

1. In the [Azure portal](https://portal.azure.com/), select **All resources** on the left side.

2. Select the **azure-backup-eastus** Recovery Services vault.

3. Select the **Backup Jobs** under **Monitoring** to see a summary of all the backup jobs and their current status.

    ![Screenshot of the Backup Jobs](images/restorevms3.png)

**Note** - Do not proceed with this lab unless the backup job is completed.

### Stop the VM to allow for the restore

A backup can't be restored if the VM is allocated and running. If you forget to stop the VM, you'll see an error that is similar to the following example.

![Screenshot showing the error details when a VM is running](images/restorevms4.png)

To prevent this error, use the following steps.

1. In the far left menu, select **Virtual machines**, and then select **test-win-vm1**.

    ![Screenshot of the VM overview page](images/restorevms5.png)

2. Select **Stop** to shut down the VM.

    ![Screenshot of stopping the VM](images/restorevms6.png)

3. In the **Stop this virtual machine** popup, select **OK**.

    ![Screenshot of stop this VM prompt](images/restorevms7.png)

### Restore the VM

The Recovery Services vaults are accessible at the subscription level. However, as you are already viewing the VM, Azure provides a quick link to the specific vault under **Operations**.

1. In the left menu, under **Operations**, select **Backup**.

    ![Screenshot of the Backup operation for a VM](images/restorevms8.png)

2. To restore the virtual machine, at the top select **Restore VM**.

    ![Screenshot of Restore VM](images/restorevms9.png)

3. Select the restore point to use for the recovery, then select **OK**.

    ![Screenshot showing selecting a restore point](images/restorevms10.png)

4. In the **Restore Configuration** window, select **Replace Existing** and use the following information to configure the restore:

   **Restore Type**

    * Select **Replace Disk(s)**, this is the restore point that will be used to replace the existing VM's disks.

    **Staging Location**

    * Select the storage account you created previously.

        ![Screenshot showing the restore configuration options](images/restorevms11.png)

5. Select **OK**.

6. On the confirmation screen, select **Restore**.

## Track a restore

1. At the top of the page, select **View all Jobs**.

    ![Screenshot of the restore progress](images/restorevms12.png)

2. Select the restore job, you can now monitor the progress of the VM restore:

    * **Job Progress**: Real-time percentage of the job as a whole
    * **Sub Tasks**: Shows the status of the current task within the job

Congratulations! With a few steps, you restored a VM in Azure.
