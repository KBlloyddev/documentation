---
layout: default
title: Teams to Teams
grand_parent: Migration Project Guides
parent: O365
nav_order: 3
has_children: false
has_toc: false

---

## Teams to Teams
{: .no_toc }

Before starting your migration project, make sure you have setup both <a href="https://cloudm-migrate.github.io/documentation/Endpoint-Configuration-Guides/O365Tenant.html">O365</a> endpoints using the configuration guides. Be sure to validate both tenants have passed their connectivity tests with no errors. 

When doing a Teams to Teams migration it's recommmend to have already created the users on the destination tenant. If this is not done it's possible for a channel to be created without the correct Team Owner. 

<a name="top"></a>
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Standard Migration 
{: .no_toc }

This process assumes that the destinaton tenant contains all the users and have already had mailboxes provisioned. A first migration pass is performed followed by a Delta with a Finalize Migration switch to make the Teams instance available to end users.

### First Migration Pass

In CloudM Migrate go to **Step 3** and use the **Filter** option to select **Microsoft Teams** under Export Type. Select the selection column header and choose **Select All From Filter**. Select **Create Batch** and name it MS Teams under **Configuration Name**.

To validate only Teams are in the batch, select Export and verify the ExportObjectType column only lists Microsoft Teams. 

To migrate the Teams, validate the following item columns are selected:

- Mail 
- Calendar 
- OneDrive
- Conversations

Select **Step 1** for the **Source Configuration** and then select **Advanced Settings**. Navigate to **Microsoft Teams/Groups** and turn on the option **Migrate Team Channel Tabs**. 

Select **Step 2** for the **Destination Configuration** and then select **Advanced Settings**. Navigate to **Microsoft Teams/Groups** and turn on the option **Teams Direct Migration**. Validate that the **Rehydrate Teams Private Chats** is off as these are done in the Delta Pass to avoid duplication. 

1 to 1 chats are stored in a folder in the users mailbox and are completed during the first pass. 

**NOTE:** The **Teams Direct Migration** option will create the Teams on the distination in MigrationMode. This restricts visiblity and access to the Team on the destination. If the Team already exists and this option in enabled, the migration will fail as an exiting Team can't be set to MigrationMode. To migrate to an existing Team disable the Team Direct Migration option. 

Validate the **Finalize Teams Direct Migration** is set to Disabled. 

Execute the migration by selecting the paper airplane on the left and then selecting **Start**. 

### Delta Pass and Finalizing 

After the first pass is completed you can set a date for the destination Teams to go live for your users. To do so, go to the batch perviously created for the first pass and then go to **Step 2**. Select **Advanced Settings** and set the option **Finalize Teams Direct Migration** to Enabled. 

CloudM Migrate has the option to rehydrate the last ten messages of users 1 to 1 chats. It's recommended to do this during the Delta Pass to avoid duplication. To set this feature go to **Step 2** and expand the **Advanced Settings**. Navigate to **Microsoft Teams/Groups** and enable the **Rehydrate Teams Private Chats** option. 

Execute the migration by selecting the paper airplane on the left and then selecting Start. When this pass is completed, the Teams will be live on the destination.



