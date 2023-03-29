---
layout: default
title: Exercise 5 Testing
nav_order: 5
---

# Exercise 5: Testing what we built

In this final exercise, we will be testing what we built. We will be processing this inbound email attachment from Bluth Co.

![relative](images/licensesample.png)

1. Navigate to the main ServiceNow interface

1. Click **Workspaces**, then click **Supplier Management Workspace**

    ![relative](images/findworkspace.png)

1. You should land on the **Supplier Management Workspace**. This is a simple workspace to currently only handle the business licenses, but will be the starting point for all other Supplier Management applications as well.

    ![relative](images/supmgmtws.png)

1. Keep this workspace open, we will come back to it after triggering the workflow

1. You can skip the following steps if the App Engine Studio tab is still open

1. Under **All**, search and navigate to **App Engine Studio**

    ![relative](images/openaes.png)

1. In the **My recent apps** section, click **Supplier Management**

    ![relative](images/openapp.png)

1. Under **Logic and Automation**, click **Process Supplier Email** (If you cannot locate this flow, you might have to expand the list by clicking **See all** on the top right of the section)

    ![relative](images/openflow.png)

1. Within the **Process Supplier Email** flow screen, click **Test**

    ![relative](images/test.png)

1. For **Email Record**, click the field and search **business license**. You should see one result titled **Business license registration for Bluth Co**

    > This email record was originally sent in by the supplier, and contains the attachment from the email

1. Select it and click **Run Test**

    ![relative](images/bluth.png)

1. Quickly head back to the **Supplier Management Workspace** tab

1. The business license has already begun processing, if you were quick enough, you should be able to see 1 record under **Unprocessed Business Licenses** after clicking the **Refresh** icon

    ![relative](images/refreshworkspace.png)

1. Click **1** under **Unprocessed Business Licenses**

1. On the record list, click the record

    ![relative](images/recordlist.png)

1. On the next record screen, the fields (Business name, License number, Expiration date) should automatically be populated once the document has been processed (note: this can take up to 3 minutes to process)

1. Click the **Bluth Co Business License** attachment on the right

    ![relative](images/attscreen.png)

1. An overlay screen showing the attachment will appear. Check the details and close the screen on the top right

    ![relative](images/closeatta.png)

1. Click the **Playbook** icon on the far right of the screen, under attachments

    ![relative](images/clickpb.png)

1. The sidebar will load the playbook (You will have to expand the panel by dragging the divider all the way to the left)

    ![relative](images/dragdivider.png)

1. Recall how we designed this process in **Process Automation Designer** in Exercise 4

1. Click **Create Task** to assign the ESG check task to Abel Tuter

    ![relative](images/createtask2.png)

1. You can expand the new task to see the details of the task created

    ![relative](images/assessmentass.png)

Congratulations, you've completed the lab! What you've just experienced are some of the tools with the Hyperautomation toolbox on the ServiceNow platform. This is only the beginning on what's possible, and there are many more tools that you can explore to further automate processes, such as Process Optimization, Predictive Intelligence, Performance Analytics, Decision Builder, etc.

Where will your Hyperautomation journey take you next?




