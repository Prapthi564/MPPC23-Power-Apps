# 🚀 Lab 4: Enterprise Scale

## Lab 4 - Tasks

In this lab, you will go through only one task:

- Extend the previous pipeline with Approvals

### ☑️ Task: Extend the previous pipeline with Approvals

#### Task 1.1 : Extending the pipeline in the Deployment Pipeline Configuration App

In this task, you will learn how to extend the pipeline and add an approval before deploying to production.

1. Go to the [maker portal](https://make.powerapps.com).

2. Make sure you're in the **Prod** environment; if you're not, switch to it.

    ![](./assets/bs100.png)

3. Navigate to **Apps (1)** then hover on the **Deployment Pipeline Configuration (2)** app, and select the **Play (3)** button.

    ![](./assets/bs101.png)

4. This will open the **Deployment Pipeline Configuration** app and will enable you to modify your pipeline. Select the **My first pipeline** pipeline.

    ![](./assets/extend-pipeline-select-pipeline(1).png)

5. On the next screen, scroll down to the **Deployment Stages** and select the **Deploy to prod** deployment stage.

    ![](./assets/bs102.png)

6. Enable the check box in the **Pre-Deployment Step Required (1)** field and select the **Save & Close (2)** button in the command bar at the top.

    ![](./assets/extend-pipeline-enable-pre-deployment-step(1).png)

7. In the Deployment Stages subgrid, verify whether the **Pre-Deployment Step Required field** is set to **Yes**. If it is, the task is complete. If not, return to step 5 and try again.

    ![](./assets/extend-pipeline-enable-pre-deployment-step-saved(1).png)

#### Task 1.2 : Create a cloud flow that handles the approval

In this task, you will learn how to create an approval flow that will handle the approval before deploying to production.

1. Go to the [maker portal](https://make.powerapps.com).

1. Make sure you are in the **Prod** environment and if not, switch to that environment.

    ![](./assets/bs100.png)

1. Select **Flows (1)** from the left navigation pane, the select **New flow (2)** in the command bar at the top and select **Automated cloud flow (3)**.

    ![](./assets/extend-pipeline-create-automated-cloud-flow(1).png)

1. This will open a pop up where you can name your flow and configure a trigger. 

    - Name your flow as **My first pipeline production approval (1)**
    - Search for **action (2)**
    - Select the Microsoft Dataverse trigger  **When an action is performed (3)**
    - Select the **Create (4)** button 

      ![](./assets/extend-pipeline-cloud-flow-trigger(1).png)

1. If a small Microsoft Dataverse dialog appears, choose **OAuth (1)** as the Authentication Type and click on **Sign in (2)** using the same credentials you used for Power Apps.

    ![](./assets/bs103.png)

1. Configure the trigger inputs by making it look like the screenshot below.

    - Catalog: Select **Microsoft Dataverse Common (1)**
    - Category: Select **Power Platform Pipeline (2)**
    - Table name: Select **none (3)**
    - Action name: Select **OnPreDeploymentStarted (4)**

      ![](./assets/bs104.png)

1. Select the **ellipsis (...) (1)** at the top-right corner of the trigger and select **Settings (2)** to open up the trigger settings.

    ![](./assets/extend-pipeline-cloud-flow-trigger-open-settings(1).png)

1. Select the **Add** button below **trigger conditions** to add a trigger condition.

    ![](./assets/bs105.png)

1. Add the following trigger condition to make sure the cloud flow only triggers when the pipeline name is equal to **My first pipeline** **(1)** and then select **Add (2)** button.

    ```
    @equals(triggerOutputs()?['body/OutputParameters/DeploymentPipelineName'], 'My first pipeline')
    ```

     ![](./assets/bs106.png)    

1. Add the following trigger condition to make sure the cloud flow only triggers when the pipeline name is equal to **Deploy to prod**.

    ```
    @equals(triggerOutputs()?['body/OutputParameters/DeploymentStageName'], 'Deploy to prod')
    ```

1. Select the **Done** button at the bottom of the trigger card to save the trigger conditions.

    ![](./assets/extend-pipeline-cloud-flow-trigger-settings-save-condition(1).png)

1. Select the **+ New step** button to add an action to start and wait for an approval.

    ![](./assets/bs107.png)

1. Search for **approval (1)** and select the **Start and wait for an approval (2)** action.

    ![](./assets/extend-pipeline-cloud-flow-add-approval(1).png)

1. Configure the approval action as:  

    - In **Approval Type**, select **Approve/Reject - First to respond (1)** 

    - For title, add `Approval requested for`, select **ActionOutputs DeploymentPipelineName** from the `dynamic content` fields on the right, add ` - `, and select another dynamic content field from the right called **ActionOutputs DeploymentStageName** **(2)**  

    - For **Assigned to**, add the email address of your user **<inject key="AzureAdUserEmail"></inject> (3)**

      >**Note:** In production scenarios, this would be an admin that would approve deployments.  

    - For **Details**, add **# Deployment notes**, add a hard return, and select the **ActionOutputs DeploymentNotes** field from the `dynamic content` fields on the right **(4)**

    - For **Item link**, select the **ActionOutputs StageRunDetailsLink** field from the `dynamic content` fields on the right **(5)**

    - For **Item link description**, add **Stage Run Details** **(6)**  

      ![](./assets/bs108.png)

1. Click the **+ New step** button to insert a condition beneath the **Start and wait for an approval** action.

    ![](./assets/bs109.png)

1. Search for **Condition (1)** and add the **Condition (2)** action.

    ![](./assets/bs110.png)

1. In the first input field of the condition:

    - Click inside it. In the dynamic content panel, select **Outcome** under Start and wait for an approval.

      ![](./assets/bs111.png)    

1. Add **Approve** to the other input field of the condition.

    ![](./assets/extend-pipeline-cloud-flow-add-condition-details(2)(1).png)

1. In the **If yes** section of the condition,

    - Click **Add an action**

      ![](./assets/bs112.png)    

    - Search for **Perform an unbound action (1)** and then select **Perform an unbound action (2)** (from the Microsoft Dataverse connector)

      ![](./assets/bs113.png)     

1. Now configure the action fields:

    - Action Name: Select or type **UpdatePreDeploymentStepStatus (1)**  

    - Add **20 (2)** as the PreDeploymentStepStatus (20 is the status ID for approved).  

    - Add the **Response summary (3)** dynamic content field from the **Start and wait for an approval** action as Comments.  

      ![](./assets/bs114.png)     

    - Navigate to **Expression (1)** tab, add the following expression via the expression panel to the **Comments** field **(2)** and select the **OK (3)** button:

        ```
        first(outputs('Start_and_wait_for_an_approval')?['body/responses'])?['comments']
        ```  

        ![](./assets/bs115.png)

1. Add the `ActionInputs StageRunId` dynamic content field from the **When an action is performed** trigger as `StageRunId`.

    ![](./assets/bs116.png)

1. In the **If no** section of the condition,

    - Click **Add an action**

      ![](./assets/bs117.png)    

    - Search for **Perform an unbound action (1)** and selec**Perform an unbound action (2)** (from the Microsoft Dataverse connector)

      ![](./assets/bs118.png)    

1. Now configure the action fields: 
    
    - Action Name: Select or type **UpdatePreDeploymentStepStatus (1)**.

    - Add **30 (2)** as the **PreDeploymentStepStatus** (30 is the status ID for rejected).  

    - Add the **Response summary (3)** dynamic content field from the **Start and wait for an approval** action as Comments.  

    - Select **Expression (4)** tab, add the following expression via the expression panel to the **Comments** field **(5)** and select the blue **OK (6)** button:

        ```
        first(outputs('Start_and_wait_for_an_approval')?['body/responses'])?['comments']
        ```

        ![](./assets/bs120.png)  

1. Add the **ActionInputs StageRunId** dynamic content field from the **When an action is performed** trigger as StageRunId.  

    ![](./assets/bs121.png)

1. Click on **Save** to save the flow.

    ![](./assets/bs122.png)

#### Task 1.3 : Test and Execute "Deploy to Prod" with Approval Process

In this task, you are going to find out if the approval you configured in the last task actually works!

1. Go to the [maker portal](https://make.powerapps.com).

1. Ensure you're in the **Dev** environment; if you're not, switch to it.

    ![](./assets/bs123.png)

1. Go to **Solutions (1)** in the left menu. Select the **MPPC 23 (2)** solution.

    ![](./assets/run-first-pipeline-dev(1).png)

1. Click on the **hamburger (1)** icon and then select the **Pipelines (2)** from the left.

    ![](./assets/bs124.png)

1. Earlier in this lab, you have made a Pre-Deployment Step required. That means that now, there is an info box on the deploy to prod stage **(1)**. Select the purple **Deploy here (2)** button.

    ![](./assets/bs127.png)

1. This will open a new sidebar which will give you the option to start your deployment now or plan your deployment for later. Select the purple **Next** button to go to the next screen.

    ![](./assets/bs126.png)  

1. This will lead you to the next section called **Summary**. Here you can find a bunch of info about the solution you are about to deploy to the QA environment. It also shows an AI suggested solution overview.

    - Now the AI suggested solution overview is added in the **Deployment notes (1)** box

    - Select the **Deploy (2)** button

      ![](./assets/bs128.png)

1. Next, you will see the following screen, that shows a yellow box which states that **Your request to deploy here is pending**.

    ![](./assets/bs129.png)

1. This message is showing because our changes in the beginning of the lab made sure that the **Power Automate cloud flow** is now triggered. We are working on a fresh environment, so it can take a while before the approval solution is deployed. Best is to take a break now, since it can take `5-10` minutes before your next step.

1. Open a new browser tab and go to [Outlook web](https://outlook.office.com) and wait for the approval email. After `5-10 minutes` (only the first time!) it should arrive.

1. In the approval mail you will see a couple of familiar parts:  

    - You will see the title of the **Approval (1)**  

    - You will see the **Deployment notes (2)**

    - You will see **Approve / Reject buttons (3)**, select **Approve (4)**

    - You will be able to add **Comments**, select **Approved! (5)** as comments

    - You will be able to **Submit** the approval / rejection. Select **Submit (6)**

      ![](./assets/bs130.png)      

1. Close the **Outlook** browser tab, and you will see (sometimes you have to refresh) that the deployment to production is in progress.

    ![](./assets/run-deploy-to-prod-approval-in-progress.png)

1. After the deployment is finished, you will see that the deployment is finished.

    ![](./assets/bs131.png)

And that's how the deployment with approvals works!

### Solution Checker Warning

In the meantime, you should've gotten another email.

1. Go to [Outlook web](https://outlook.office.com).

1. Look for an email with the subject **Solution checked for issues during import**.

    It should look something like this:

    ![](./assets/warn-solution-checker-prod.png)

     >**Note**: This may take a few moments to appear. In the meantime, please feel free to proceed with the next lab.
    
     This email shows there are no solution checker issues found in our solution we just deployed to production: well done!

## End of labs

This is the end of lab 4. Select page 5 below to move to the next lab.
