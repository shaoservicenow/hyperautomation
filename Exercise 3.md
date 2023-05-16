---
layout: default
title: Exercise 3 Integration Hub
nav_order: 4
---

# Exercise 3: Integration Hub (30mins)

During the discovery interviews with the Supplier Management team, it was often mentioned that they spend a significant amount of time checking the supplier's business registration against the local business registries. This requires them to manually log into the business license portal and to pull out the license information and manually verify one by one. Fortunately, the business license registry offers an API to get information from each license number that we can use to make this process seamless, which we will use in Integration Hub.

![](images/licenselookupapi.png)

> In the lab, we will simulate calling a simulated API, which is modeled after an actual API provider: License Lookup. Check it out here: https://apis.licenselookup.org/business-license-search-api/

## Adding a new field to our custom table

We first have to add a field to our custom **Business License** table to mark whether the record has been verified.

1. Under **All**, search and navigate to **App Engine Studio**

    ![](images/openaes.png)

1. In the **My recent apps** section, click **Supplier Management**

    ![](images/openapp.png)

1. Under **Data**, click the **Business License** table

    ![](images/bltable.png)

1. In the Table Builder view, click **+ Add new field**

    ![](images/addnewfield.png)

1. Under **Column label**, enter **Registry verified** (1)

1. On the same row, under **Type**, change the value from **String** to **True/False** (2)

1. Click **Save** on the top right of Table Builder (3)

    ![](images/registryverified.png)

### ***Table builder comes standard in every Hyperautomation toolbox. Make sure you know how to use it effectively to construct the foundations of your applications.***

## Creating a custom action to connect via API

Now that we have the **Registry verified** field to indicate whether a record has been verified, we will use the Business License Search API to populate this field. We will first create a custom action to integrate with this API service, before using it in a flow.

1. Navigate back to the main ServiceNow UI

1. Under **All**, search and navigate to **Flow Designer**

    ![](images/fdopen.png)

1. Flow Designer will open in a new browser tab

1. On the top right of the screen, click **New**, then click **Action**

    ![](images/action.png)

1. Under **Action name**, enter **Lookup license details**

1. Leave **Application** as **Supplier Management**

1. Click **Submit**

    ![](images/actiondetails.png)

1. Click **Create Input** (1)

1. In the new row that appears, change Label to **License number** (2), the name column will automatically populate with **license_number**

1. Toggle **Mandatory** to true (3)

1. Click **Save** on the top right (4)

    ![](images/licnumaction.png)

1. Click **Add new step icon** on the left side of the screen, in between **Inputs** and **Error Evaluation**

    ![](images/addstep.png)

1. In the pop-up, search **rest**, and select the **REST** step

    ![](images/selectrest.png)

1. On the new REST step action screen, change **Connection** to **Define Connection Inline** (1)

1. Under **Base URL**, enter **https://my-json-server.typicode.com/shaoservicenow** (2)

    >Note: This is a mocked up API service that stores a database of license records

    ![](images/connectiondetails.png)

1. Under **Resource Path**, enter **/licenselookup/licenses/** (1)

1. From the right Data panel, drag and drop the **License number** data pill onto the end of the string, after **/licenselookup/licenses/** (2)

    ![](images/draglic.png)

1. Click **Save**

1. Click **Test**

1. In the pop-up modal, there should be one input field for **License number** as your defined in inputs. Enter the number **4828-19200-11024**

1. Click **Run Test**

    ![](images/testnumber.png)

1. Once the processing is complete, click **Your test has finished running. View the Action execution details.**

    ![](images/testok.png)

1. You should be directed to the **Execution Details** tab

1. Scroll down and expand **Steps**

    ![](images/expandsteps.png)

1. Scroll down until you see **Response Body**, then click on the return value

    ![](images/returnbody.png)

1. In the pop-up modal, select everything in the box and copy it to clipboard (Ctrl+c for PC or Cmd+c for Mac)

    ![](images/copyall.png)

1. Close this pop-up

1. Return to the **Lookup license details** tab by clicking on it

    ![](images/returntoaction.png)

1. Close the **Test action** pop-up

1. Click **Add new step icon** on the left side of the screen, in between **REST step** and **Error Evaluation**

    ![](images/resterror.png)

1. Search and click **JSON Parser**

    ![](images/parsestep.png)

1. Drag and drop **Response Body** from the right sidebar onto **Source data** field (1)

1. In the main section, paste the JSON object you copied from earlier (2)

1. Click **Generate Target** (3)

    ![](images/jsonstep.png)

1. Click **Save** on the top right of the screen

1. Click **Outputs** on the left of the screen (1)

1. Click **Create Output** (2)

    ![](images/output.png)

1. Change the Label **variable** to **Business name** (1)

1. Change the Name **variable** to **business_name** (2)

1. Click **Create Output**

    ![](images/output1.png)

1. For the new output, Label is **Expiration date** and Name is **expiration_date**, change **Type** to **Date** (1)

1. Click **Exit Edit Mode** (2)

    ![](images/exitedit.png)

1. Expand the **root** data pill under **JSON Parser step** on the right sidebar

1. Drag and drop the **business-name** data pill onto the **Business name** field

1. Do the same again with **expiration-date** onto **Expiration date** field

    ![](images/bned.png)

1. Click **Save**

1. Click **Test**

1. Enter the license number **4828-19200-11024**, then click **Run Test**

1. Click **Your test has finished running. View the Action execution details.**

1. In the **Execution Details** tab, do you see **Business name** and **Expiration date** populated under **Output Data**?

    ![](images/completetest.png)

1. Navigate back to the **Lookup license details** tab

1. Close the **Test Action** pop-up

1. Click **Publish**

    ![](images/pubaction.png)

## Create a flow to use the API action

1. Navigate back to App Engine Studio **App Home**

1. Click **Add** under **Logic and automation**

    ![](images/apphome.png)

1. Click **Flow**

    ![](images/createflow.png)

1. On the next screen, click **Build from scratch**

1. On the next screen form, under **Name**, enter **Verify business license**

1. Under **Description**, enter **Call the business license lookup API to verify a supplier business license**

    ![](images/verifylicenseflow.png)

1. Click **Continue**

1. Once the flow has finished being created, click **Edit this flow**

1. Close the **Getting Started** pop-up, if it appears

1. Click **Add a trigger**

    ![](images/addtrigger.png)

1. We want this flow to be triggered when a record on our Business License table is updated. Choose **Updated** under the **Record** section

    ![](images/clickupdate.png)

    > Our trigger condition would be whenever Document Intelligence has processed a document as we saw in Exercise 2. This would be where the Business License Number has been extracted from the attachment.

1. Search and select the **Business License [x_snc_supplier_m_0_business_license]** table under **Table** (1)

1. Click **Add filters** under **Condition** (2)

    > It's important that this flow only runs when the Business License number has successfully been extracted from the license document by Document Intelligence. Add a condition to only run when the License number is not empty.

1. In field selection, select **License number** (2)

1. In operator, select **is not empty** (3)

1. Click **Done** (4)

    ![](images/updatedetails.png)

1. Click **Save** on the top right (When working on a flow, save often!)

1. Click **Add an Action, Flow Logic, or Subflow**

1. Click **Action**

1. Search **lookup license details**

1. Click **Lookup license details** (this is the action we had just created)

    ![](images/liclookupapi.png)

1. From the right data panel, expand **Business License Record**, then drag and drop **License number** onto the **License number** field

    ![](images/poplic.png)

    > We are passing the license number from our Business License record into the API to retrieve information

1. Click **Done**

1. On the right data panel, examine the **1 - Lookup license details** data section. The two outputs, **Business name** and **Expiration date** were our outputs defined from the API call we created

    ![](images/outputaction.png)

    > From these outputs we would like to validate back against the business license that the supplier submitted. This is meant to be illustrative, but you can continue to build additional verification logic if you choose.

1. Click **Add an Action, Flow Logic, or Subflow**

1. Cick **Flow Logic**, then click **If**

    ![](images/iflogic.png)

1. Under **Condition Label**, enter **Business name match**

1. Expand the **Business License Record** data pill, then drag and drop **Business name** data pill onto **Condition 1** (1)

1. The operator should be left default as **is** (2)

    ![](images/biznamematch1.png)

1. From **1 - Business License Search**, drag and drop the **Business name** data pill onto the next field

    ![](images/namematch.png)

1. Click **Done**

1. Under the **If** branch, click **Action**

    ![](images/branchaction.png)

1. Search **update record**

1. Within the **ServiceNow Core** spoke, click **Update Record**

    ![](images/updaterecord.png)

1. Drag and drop the **Business License Record** data pill onto **Record** (1)

1. Click **Add field value**

1. Search and select **Registry verified** (2)

1. Check the box next to the **Registry verified** field to mark as true (3)

    ![](images/verifystep.png)

1. Click **Test** on the top right of the page

1. In the pop-up, click and select record **BSL001006**

    ![](images/1006.png)

1. Click the information icon

1. Click **Open Record**

    ![](images/openrecord.png)

1. The record will open in a new browser page (The business name should be **Cyberdyne Systems**) Keep the page open

1. Back on the flow designer screen, click **Run Test**

1. Switch back to the **Cyberdyne Systems** record page

1. The **Registry verified** checkbox should change to **true**

    ![](images/verifytrue.png)

1. Switch back the the flow designer screen

1. Close the pop-up, and on the top right of the form, click **Activate**

    ![](images/activateflow2.png)

> Challenge exercise: We did not create logic to show whenever the business name does not match. How would you deliver this scenario? Hint - you can create a new field to mark when a business license is not verified by the API, and then trigger an "else" rule that will populate that field. You can test it out with record BSL0001002.

Great job on making it to this point. In this exercise, we used a custom integration through Integration Hub to verify the business license. So far, we have successfully managed to automate the retrieval, extraction and verification of supplier business licenses without any manual intervention! What used to be a very repetitive, boring task, which took Nintech Co. hours of work each week is now an automated process that takes less than 2 mins. The Supplier Management team now has more time to focus on work that requires human creativity and personality, like Supplier Relationship Management and working with Suppliers to help meet Nintech Co. and their shared ESG goals.

[Previous exercise](https://shaoservicenow.github.io/hyperautomation/Exercise%202.html){: .btn .mr-4 }
[Next exercise](https://shaoservicenow.github.io/hyperautomation/Exercise%204.html){: .btn .btn-purple }