# 🚀 Lab 3: Deploy

## Lab 3 - Tasks

In this lab, you will go though the following tasks:

- Create your first pipeline
- Run the deployment to the QA environment

### Task 1: Create your first pipeline

In this task, you will create your first pipeline. The `Deployment Pipeline Configuration` app that you installed in lab 1 will be used for that.

1. Go to the [maker portal](https://make.powerapps.com), and make sure you are in the `Prod` environment.

    ![](./assets/prod-env-pipelines-installed(1).png)

2. Navigate to **Apps (1)** then select the **elipses(...) (2)** next to **Deployment Pipeline Configuration** app and click on **Play (3)**.

    ![](../assets/bs71.png)

3. The app will open in a new tab:

    ![](./assets/create-pipeline-app(1).png)

    Explore the app to get familiar with the available menu items.

    - To begin with, you'll land on the `Overview` section when you open the app. This serves as the `Pipelines Dashboard`, displaying the latest updates on active runs and pipelines. Don’t worry if it appears empty at first — that’s expected.

    - Next, the `Pipeline Setup` section allows you to view your configured environments and pipelines.

    - The `Deployments` section provides access to the run history and the corresponding solution artifacts.

    - Finally, there's a `Settings` section, where you can manage security teams, configure advanced settings, and customize various aspects of the app.

#### Task 1.1 : Create a New Pipeline

1. To create a new pipeline, click on **⋮ (1)** in the `Pipelines Dashboard` and select **+ New (2)**.

    ![](./assets/create-pipeline-new-pipeline(1).png)

2. A side panel titled **Quick Create: Deployment Pipeline** will appear.

    - Set the Name to **My first pipeline** **(1)**.

    - Keep the remaining settings as they are and click **Save and Close (2)** to save the pipeline.

        ![](./assets/create-pipeline-new-pipeline(2)(1).png)

3. You’ll be redirected to the `Pipelines Dashboard`, where **My first pipeline** will now be listed.

4. Select **My first pipeline**.

    ![](./assets/create-pipeline-new-pipeline(3)(1).png)

5. You’ll be taken to a form where, under the General tab you can enter the details for your pipeline.

    ![](./assets/create-pipeline-new-pipeline-details(1).png)

6. As you scroll down, you’ll notice the following content beneath:

    ![](./assets/create-pipeline-new-pipeline-saved(1).png)

    As you can see there are two sections: **Linked Development Environments** & **Deployment Stages**.

    - **Linked Development Environments**: A pipeline can be connected to multiple development environments. This is especially useful when you work with several development setups while sharing the same test and production environments.

      In this lab, we’ll link only one development environment. However, keep in mind that in a real-world company setting, you can associate more than one environment here..

    - **Deployment Stages**: The Deployment Stages section allows you to add stages that follow your development environment. For example, in today’s lab, we’ll be adding a stage called `Deploy to QA`, followed by another called `Deploy to Prod`. What’s great is that you can define the order by setting preceding stages—this ensures that `Deploy to QA` runs before `Deploy to Prod`.

#### Task 1.2 Create a development environment

1. Let’s move forward with the lab by adding a new development environment. To do this, click the **New Development Environment (1)** button located in the Linked Development Environments section.

    ![](./assets/create-pipeline-new-development-env-create(1).png)

1. A sidebar will appear, allowing you to enter the details of the `Dev` environment created in Lab 01.

    - Set Name as **Dev** **(1)**.

    - Click on the drop-down button and choose the Environment Type as **Development Environment** **(2)** .

        ![](./assets/create-pipeline-new-development-env-details(1).png)

1. For the next step, make sure to grab the `Environment Id` from the Power Platform Admin Center

    - Open a new tab and go to the [Power Platform Admin Center](https://aka.ms/ppac)

        ![](./assets/create-pipeline-new-development-env-ppac-dev(1).png)

    - Select **Manage (1)** from the menu on the left, then click on **Environments (2)** and select the Environment named **Dev** **(3)**.

        ![](./assets/create-pipeline-new-development-env-ppac-dev(2)(1).png)

    - Copy the **Environment ID**. 

        ![](../assets/bs72.png)

4. Paste the **Environment ID** copied in the above step, in the **EnvironmentId (1)** section of **Quick Create: Deployment Environment** window, then click **Save and Close (2)**.

    ![](./assets/bs73.png)

5. If all went well, you'll see the following screen. 

    ![](./assets/create-pipeline-new-development-env-saved(1).png)

    >**Note:** *Refresh* the page if you don't see it

#### Task 1.3 : Add the first deployment stage

1. Now select the **+ New Deployment Stage** button  to add the first deployment stage.

    ![](./assets/create-pipeline-new-deployment-stage(1).png)

2. This will open a new form, where you can enter details about your first deployment stage.

    - Add Name as **Deploy to QA**.

        ![](./assets/create-pipeline-new-deployment-stage(2)(1).png)

        >**Note:** We're leaving the Description and Previous Deployment stage empty, because we don't have a previous deployment stage, since this is our first stage.

1. Click on the input box next to **Target Deployment Environment ID** to bring up a small popup that lets you add a new deployment environment. Select **+ New**.
    
    ![](./assets/create-pipeline-new-deployment-stage(3)(1).png)

1. A new sidebar will appear, allowing you to provide information about your QA environment.

    ![](./assets/create-pipeline-new-deployment-stage(4)(1).png)

1. In the sidebar, add the following details:

    - Set the Name as **QA (1)**.

    - From the drop-down, select EnvironmentType as **Target Environment (2)**.

        ![](./assets/create-pipeline-new-development-env-ppac-qa(1).png)

1. To add the **Environment ID** of the test environment

    - Open a new tab and go to the [Power Platform Admin Center](https://aka.ms/ppac)

        ![](./assets/create-pipeline-new-development-env-ppac-dev(1).png)

    - Select **Manage (1)** from the menu on the left, then click on **Environments (2)** and select the Environment named **QA** **(3)**.

        ![](./assets/create-pipeline-new-development-env-ppac-qa(2)(1).png)

     - Copy the **Environment ID**. 

        ![](./assets/create-pipeline-new-development-env-ppac-qa(3)(1).png)

1. Paste the Environment ID copied in the above step, in the **EnvironmentId (1)** section of **Quick Create: Deployment Environment** window, then click **Save and Close (2)**.

    ![](./assets/bs74.png)

1. Select **Save and Close** from the bar on top.
   
    ![](./assets/create-pipeline-new-development-env-details(4)(1).png)

### Task 1.4 : Add the `Deploy to prod` deployment stage

1. Select the **+ New Deployment Stage** button again to add a second deployment stage: 

    ![](./assets/create-pipeline-deploy-to-prod(1).png) 

1. Add the following details: 

    - Set Name as **Deploy to prod (1)**.

    - Leave the **Description** empty.

    - In **Previous Deployment Stage**, search and select for the **Deploy to QA (2)** stage.

      ![](./assets/bs75.png)

1. Click on the input box next to **Target Deployment Environment ID** to bring up a small popup that lets you add a new deployment environment. Select **+ New**.

    ![](./assets/create-pipeline-new-deployment-stage(5)(1).png)

    > **Note:**  There is a setting field called `Pre Deployment Step Required`. We're not using that in this case, but think about what could that be used for. During the workshop, the trainers will show an example of it.

1. A new sidebar will appear, allowing you to provide information about your **QA environment**.

    ![](./assets/create-pipeline-new-deployment-stage(4)(1).png)

1. Add the following details:

    - Set Name as **Prod (1)**.

    - Set the Environment Type to **Target Environment (2)**.

        ![](./assets/create-pipeline-new-development-env-ppac-prod(1).png)

1. For the next step, make sure to grab the `Environment Id` from the Power Platform Admin Center

    - Open a new tab and go to the [Power Platform Admin Center](https://aka.ms/ppac)

        ![](./assets/create-pipeline-new-development-env-ppac-dev(1).png)

    - Select **Manage (1)** from the menu on the left, then click on **Environments (2)** and select the Environment named **Prod** **(3)**.

        ![](./assets/bs78.png)

     - Copy the **Environment ID**. 

        ![](./assets/bs76.png)

1. Paste the **Environment ID** copied in the above step, in the **EnvironmentId (1)** section of **Quick Create: Deployment Environment** window, then click **Save and Close (2)**.

    ![](./assets/bs77.png)

1. Select **Save and Close** from the bar on top.
   
    ![](./assets/create-pipeline-new-development-env-details(6)(1).png)

### Task 2: Run the deployment to the QA environment

In this task, you’ll deploy the solution built in Lab 2 to both the QA and Production environments. We’ll begin by deploying it to QA. So far in this lab, you’ve set up a pipeline along with its associated stages. But how exactly does a maker move a solution from the `Dev` environment to the `QA` and `Prod` environments?

1. Go to the [Power Apps Maker Portal](https://make.powerapps.com).

1. Click on Environment **(1)** and make sure to select the **Dev (2)** environment.
    ![](../Media/L3T04.png)

1. Go to **Solutions** (1) from the left navigation menu and select the **MPPC 23** (2) solution by clicking on its display name.

    ![](../Media/L3T05.png)

1. Click on the **🚀 Rocket icon** for pipelines from the left-hand navigation panel.

    ![](./assets/bs79.png)

1. This will open a new screen displaying an overview of all the stages you configured in the previous step.

    ![](./assets/bs84.png)

1. Click on the **Deploy here** button. This will open a sidebar where you can choose to either start the deployment immediately or schedule it for later.

    ![](./assets/bs80.png)

1. Notice the message displayed below the deployment schedule. It indicates that this pipeline uses AI to generate a solution overview. Click **Next**.

    ![](./assets/bs82.png)

1. This takes you to the `Summary` section, where you’ll find key details about the solution you're deploying to the QA environment, including an AI-generated solution overview. Now the AI suggested solution overview is added in the `Deployment notes` box **(1)** and then click on **Deploy (2)**.

    ![](./assets/bs83.png)

     >**Note**: You may get an error like **Validation failed due to Missing dependencies**, in that case please navigate to **Real Estate Showings** app, click on **Save** and select **Publish** again. Repeat this for 2-3 times.

     - Then navigate back to the **Summary** page and click on **Deploy** again.

1. It will take a couple of minutes to deploy the solution to the QA environment. After it's done, the overview page for the pipelines should look like this:

    ![](./assets/bs85.png)

As you can see, the last deployed solution version and last deployed date time are visible here.

### Test if the solution was correctly deployed to QA

1. Of course, you want to see for yourself if the deployment was successful, so select the **Go to this environment** button in the `Deploy to QA` stage.

    ![](./assets/bs86.png)

1. Select **Solutions (1)** in the left navigation. Navigate to **All (2)** tab. Check if the `MPPC 23` solution with `version 1.0.0.1` is installed in the `QA` environment **(3)**.

    ![](./assets/bs87.png)

1. Open the `MPPC 23`solution by selecting the **display name**.

    ![](./assets/bs88.png)

1. Click on the **elipses (...) (1)** next to **App**  canvas app, (`App` app is the `Real Estate Property` canvas app that you have created in `Lab 2 Task 1.1`) and select the **Play (2)** button.

    ![](./assets/bs89.png)

1. This will open the app in a new tab.

    ![](./assets/bs90.png)

    It will look like your app is broken, since it will have the message `Getting your data`, but it's working fine! The problem is that there is no data in this environment, because we just deployed the solution here. Let's fix that!

1. Select the **+ New** button on the left side of the screen.

    ![](./assets/bs91.png)

1. Fill in the following fields with the information below:

    - Address: `432 Elm Street, Riverside, CA 92501` **(1)**

    - Price: `350000` **(2)**  

    - Size: `1800` **(3)**   

    - OwnerEmail: `emily.johnson@example.com` **(4)**   

    - ID: `101` **(5)**

    - Owner: `Emily Johnson` **(6)**   

    - Image: `https://raw.githubusercontent.com/microsoft/PowerPlatformAdvocates/main/MSLearn/AIModule/Images/property1.jpg` **(7)**

    - Select the **check** to save the new row **(8)**

      ![](./assets/bs92.png)

1. Now you will see at least one row in the app and the app should look more familiar with the photo and the Power Apps Ideas formatting we did in lab 2.

    ![](./assets/bs93.png)

1. Navigate back to **MPPC 23 Solution > All** page.    

1. Select **elipses (...) (1)** next to **Real Estate Showings** canvas app and select the **Play (2)** button.

    ![](./assets/bs94.png)

1. This will open the app in a new tab.

    ![](./assets/bs95.png)

    Again, it will look like your app is broken, since it will have the message `Getting your data`, but it's working fine!

1. Select the **+ New** button on the left side of the screen.

    ![](./assets/bs96.png)

1. Fill in the following fields with the information below:

    - Property Address: `432 Elm Street, Riverside, CA 92501` **(1)**

    - Agent: `James Bond` **(2)**

    - Appointment Status: `Pending` **(3)**   

    - Showing Date: `<Pick the date of today - don't change the time>` **(4)**     

    - Showing Time: `<Pick the date of today - change the time to 10:00>` **(5)** 

    - Client Name: `Austin Powers` **(6)**     

    - Client Email: `austin@example.com` **(7)**

    - Select the **check** to save the new row **(8)**

      ![](./assets/bs98.png)

1. Now you will see at least one row in the app and the app should look more familiar like the `Real Estate Showings` app we created in lab 2.

    ![](./assets/bs99.png)

Now you know the app works in **QA**, let's deploy it to production.

## Review

In this lab you have completed the following tasks:

- Create your first pipeline
- Run the deployment to the QA environment

    
### Congratulations! you have successfully completed this lab, please click on **Next** to continue with the next lab
