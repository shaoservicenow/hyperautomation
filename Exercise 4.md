---
layout: default
title: Exercise 4 Process Automation Designer
nav_order: 5
---

# Exercise 4: Process Automation Designer

Even with automation, there are still activities that the Supplier Management team has to manually oversee which cannot be avoided. One of these processes is to check the ESG compliance of suppliers. In this exercise, we will be building on top of a playbook to assign a task to the ESG compliance team so that a suppliers commitments are tracked and accounted for.

## Building in Process Automation Designer

1. Navigate back to the main ServiceNow UI

1. Under **All**, search and navigate to **Process Automation Designer**

    ![relative](images/padnav.png)

1. In the **Multi-flow processes** list, click **Supplier License Verification**

    ![relative](images/openpad.png)

    > Note: For this lab, we have already implemented placeholder instructions based on the previous exercises. This is meant to be a quick start to add a new activity.

1. On a new column, click **Add lane**

1. On the right pop-up sidebar, enter **ESG assessment** under **Label** (2)

1. Enter **ESG assessment activities to be processed** under **Description** (2)

1. Click **Save and close**

    ![relative](images/padsteps.png)

1. Under the newly created **ESG assessment** lane, click **Add an activity**

1. In the pop-up, search **create task**, and click **Create Task** under **Commmon Activities**

    ![relative](images/createtask.png)

1. On the **Activity properties** side bar that appears, change the **Label** to **Assign ESG check**

1. Under **Description**, enter **Create a new task for the ESG team to conduct a ESG check for supplier** (1)

1. Click the **Automation** tab (2)

    ![relative](images/fillactivity.png)

1. Under the **Inputs** section, select **Abel Tuter** under **Assigned To**

1. Under **Short Description**, enter **Conduct ESG check on -** (1), then click the data pill picker (2), expand **Trigger - Business License** (3), expand **Business License Record** (4), click **Business name** (5)

    ![relative](images/dotwalk.png)

1. Your screen should look like the following

    ![relative](images/completeactivity.png)

1. On the top right of the screen, click **Activate**

    ![relative](images/activatepad.png)

This exercise was purely illustrative on how you can go further and build playbooks on these process to accelerate the organization's automation agenda. Process Automation Designer is a highly powerful tool that can orchestrate your business processes and flows across stakeholders, departments and more.

