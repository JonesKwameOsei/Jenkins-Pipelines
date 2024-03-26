# Jenkins-Pipelines
Defining automated and reusable workflows for continuous integration and continuous delivery (CI/CD) processes within Jenkins.
## Overview
In this project, we aim to leverage Jenkins high level automation and robust capabilities to make **integration simple, repeatable process** of the software development workflow to drastically reduce costs and respond to **early defects**. 

## Install Plugins
Jenkins require plugins to run the pipelines, hence, we will need to install these first. The underlisted plugins will be installed in Jenkins:
  - SonarQube Scanner
  - Nexus Artifact Uploader
  - Pipeline Utility Steps
  - Pipeline Maven Integration
  - Blue Ocean
1. On the the **Jenkins Dashboard**, click on **Manage Jenkins**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/27ab847c-1852-4ce6-82c0-55e603f2e5ce)<p>
2. On the **Manage Jenkins** page, click on **Plugins**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/4f21a5ce-58a1-4eef-9bc7-1bd1c715ce80)<p>
3. On the **Plugins** page, click on **Available plugins**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/752c4dd4-ff16-486b-9cfd-549666e20989)<p>
4. In the **search bar**, type in **SonarQube Scanner** and **check mark** it.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/8f67c327-bc93-40be-a6a2-2a9e176acf46)<p>
5. Repeat **step 4** for the remaining plugins listed above.<p>
6. Next, click on **install**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/7fd7631f-5b38-433a-95a9-caf12287bf03)<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/085f0edf-5f26-40d2-b31a-c134d294a11b)<p>
7. Navigate to the **Jenkins Dashboard**.

## Create Pipeline Job 
Creating pipeline jobs in **Jenkins** is essential for automating and orchestrating the software delivery process. Pipelines allow **DevOps teams** to define the entire **build, test, and deployment process as code**, which brings several benefits such as **consistency**, ***visibility**, **reproducibility**, **traceability** and **efficiency**. To create the pipeline job:
1. Click on **New Item** on the Jenkins dashboard.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/c7e2290c-d5ef-4180-9cb5-bbe1623b819c)<p>
2. Enter a name in the **Enter an item name** field. For example, **webapp-pipeline-job**.
3. Select **Pipeline** and click **OK**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/ec449fec-137a-4375-8a2f-d9771dd7f473)<p>
4. On the **configuration** page, add a **descrioption** to the pipeline. This is optional but gives a brief details of the pipeline. <p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/507793d6-4a5d-4fbb-9c19-c68b62b42ba0)<p>
5. Next, click on **Pipeline** under **Configure**.
6. At the **Pipeline** section, under **Definition**, click on the drop down and select **Pipeline script** from the options. **NB**: This option is chosen becuase we donot have a **Jenkins file** in our version control.
7. Next, it is time to write the **pipeline scripts**. Jenkins provides a sample script to try hands on.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/7c5ae642-8acf-4cd2-a853-f731b47dcf38)<p>
i. Write a script for **Git clone**, click **Apply** and **Save**.
```
pipeline {
    agent any
    tools {
        maven 'maven3.9.6'
    }

    stages {
        stage('Git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/JonesKwameOsei/web-app.git'
            }
        }
    }
}
```
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/6a79ce0e-a561-43c0-84c7-e48c7fd9332b)
















