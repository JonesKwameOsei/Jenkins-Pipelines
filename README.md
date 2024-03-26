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
        maven 'Maven3.9.6'
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

### Build Artifact with Jenkins and Maven
1. Click on **Build Now** on the **webapp-pipeline-job** page. This instructs **Jenkns** builds the first job, **cloning the git repo**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/1c6e60cf-f20e-4b32-bc3e-89a16dad2d0c)<p>
The build has been successful. Jenkins has clone the **Github repo** containing the source code.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/b7411e31-73de-4dac-bdfb-a75414aea47c)<p>

![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/3ca668f8-a7f9-4704-9694-c5d49ae8396c)<p>
At this point, we can understand the job properly courtesy **Blue Ocean**, one of the plugins we installed earlier. <p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/fff9a4a4-2cda-42d0-904d-f0e1d06c083e)<p>

2. Click **Configure** on the Job page, click **Pipeline** under **Configure**.
3. Add another **stages** for the the job. These stages will **build, test and package the artifact with maven**.
```
/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any
    tools {
        maven 'Maven3.9.6'
    }

    stages {
        stage('Git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/JonesKwameOsei/web-app.git'
            }
        }

        stage('Build with Maven') {
            steps{
                sh "mvn clean"
            }
        }

        stage('Testing with Maven') {
            steps{
                sh "mvn  test"
            }
        }

        stage('Package with Maven') {
            steps {
                sh "mvn package"
            }
        }
    }
}
```
4. Click **Apply** and **Save**.
5. On the **webapp-pipeline-job** page, click **Build** for Jenkins to build the artifact with **Maven**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/afe8adb1-5973-4293-b2ec-ea20122718ea)<p>
We can observe that Jenkins executed the build processes according to the order of the stages specified.<p> Let is look into how **Jenkins** utilised **Maven** to build the artifact in **Bleu Ocean**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/b18222a2-de94-4198-a729-2ec3b28a5a7f)<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/6bc8eec0-3150-4a21-a862-5fedf63711f1)<p>


### Testing Artifact with Jenkins and SonarCube
At this stage, we will test the built artifact with sonarqube utilising **Jenkins'** automation processes. 
1. Navigate  to the main Jenkins dashboard, click on **Manage Jenkins**, then click on **tools**. <p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/0579c40c-9672-4f4d-8ad9-1a4cd6441a4a)<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/0e79c630-8d34-4bb4-a4b7-90d9244a23a7)<p>
2. On the **Tools** page, scroll down to **SonarQube Scanner installations**, click on **add SonarQube Scanner**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/1e20c96c-3a07-457e-a3ce-11c38cf490df)<p>
3. Under **SonarQube Scanner**, configure the following:
- Name: Sonar5.0
- Version: SonarQube Scanner 5.0.1.3006. NB: Select the latest version.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/02ea5bb8-be06-4324-b837-bddc71bd1411)<p>
4. Click **Apply** and **Save**.
5. Next, click **System** under **System Configuration** to configure **SonarQube server**.
6. On the **System** page, scroll down to **SonarQube servers** and click on **Add SonarQube**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/1c48121a-8a01-4e8d-8a30-9f27a8c9f615)<p>
7. Generate token from **SonarQube server**
- Click the user profile next to the **Search for projects** bar, then click **My Account**.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/c750467e-e728-48e9-9133-d21bc99bbe11)<p>
- Select the **security tab**<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/b0697fa0-dce4-4513-a22b-a68080338555)<p>
- Enter the **Name** for the token, select **Global Analysis Token** under the **Type**, Select one of the options for the **Expires in** and **Generate** the token. **NB**: Pay attention to the warning after generating the token and copy it. 
8. **Check mark** the **Environment variables** and configure the following under the **SonarQube installations**:
- Name: SonarQube (it can be any name)
- Server URL: http://localhost:9000 (if it's an Amazon EC2 instance, then: http://instanceIPAddress:9000)
- Server authentication token: Click **+ Add**, select **Jenkins** to add SonarQube credentials as below.<p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/d495ecd4-abda-4934-bb34-01abc8da5933)<P>
- Click the drop down under the **Server authentication token** and select the credential we created. <p>
![image](https://github.com/JonesKwameOsei/Jenkins-Pipelines/assets/81886509/13a52f3f-164f-44d9-b491-cf8cfb94646e)



























