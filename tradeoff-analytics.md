---
layout: post
title: Junit Basics
permalink: /junit-basics/
---


##Tradeoff Analytics Tutorial

> In this tutorial you will learn how to create a simple web application that will provide Tradeoff Analytics as its service in analyzing the given data.

<br>
> Access Git Repository <a href="http://github.com/giodeealbayda/tradeoffanalytics1.git">here</a>.

####Copy Sample Application

1. Open a terminal window and create the directory `tradeoff-analytics` in the root directory.  Go to the created directory.

	```	
	> mkdir tradeoffanalytics
	> cd tradeoffanalytics
	```

	<br>
	
2. Download the <a href="https://github.com/giodeealbayda/tradeoffanalytics1/blob/master/tradeoffanalytics1.war?raw=true">`tradeoffanalytics1.war`</a> file and place it inside the `tradeoffanalytics` directory.

	The `tradeoffanalytics1` directory has two subdirectories: `src` and `build`.

	```
	tradeoffanalytics1/
	|
	|----src/
	|    |
	|    |----main/Connector/
	|    |           	|----Connector.java
	|    |                  
	|    |----main/Servlet/
	|    |		      |----TradeOffServlet.java
	|    |
	|    |----webapp/
	|    |		|----newjsp1.jsp
	|                       
	|                       
	|
	|----build/
	     |
	     |----classes/
	     |    |
	     |    |----main/
	     |    |	   |----Connector/
	     |    |	   |----Servlet/
	     |    |
	     |----libs/
	``` 
 
	`src` has two subdirectories: `main` and `webapp`. 

	`src/main` contains the Java class `src/main/Connector/Connector.java` which connects the application to the Tradeoff Analytics service. In addition, it contains the `src/main/Servlet/TradeOffServlet.java` which processes the data from the web application. 

	`src/webapp` contains the JSP page `src/webapp/newjsp1.java` which is the interface of the web application. This is where the value of each data can be manipulated by the user before the data processing
 
	`build` has two subdirectories: `classes` and `libs`. 

	`build/classes` is used to hold the the `.class` files that will be created later when you compile the web application.

	`build/libs` is used to store the `.war` file which will be created after compiling the web application.

	<br>

####Deploy Sample Application in Bluemix using the `cf` tool.


1. Open a terminal window and go to the `tradeoffanalytics` directory.
2. Login to your Bluemix account using the `cf` tool.
	```
	> cf login -a https://api.ng.bluemix.net -s dev
	```
3. Upload the sample application to your Bluemix account.
	```
	> cf push tradeoffanalytics-< your_name > -m 256M -p tradeoffanalytics1.war
	```
	**Example:**
	```
	> cf push tradeoffanalytics-giodee -m 256M -p tradeoffanalytics1.war
	```
4. Go back to the browser tab containing your Bluemix account. In the menu, click `DASHBOARD`.
   The `Applications` section of your dashboard shows a widget representing the application `tradeoffanalytics-<your_name>` you deployed earlier.
5. Click the widget of your application to see its overview.

####Add a Tradeoff Analytics Service and Bind it to the Sample Application
1. On the left pane, click the `Overview` link.
2. Click the `ADD A SERVICE OR API` link. You will be redirected to the `Catalog` page.
3. Look for the `Tradeoff Analytics` service and click it.
4. Click the `CREATE` button.
5. When asked to restage your application, click the `RESTAGE` button. Wait for your application to restage.
6. Open another broswer tab (do not close the browser tabl containing your Bluemix account). Go to `tradeoffanalytics-<your_name>.mybluemix.net/newjsp1.jsp` to test if the sample application can already connect to the created Tradeoff Analytics Service.

####Analyze How the Sample Application and Tradeoff Analytics Service Works
1. In order for the functions of the Tradeoff Analytics service to work, `Gradle` is required to download the libraries needed to solve the dependency
2. 

####Copy a Github Repository
1. Open a web browser tab and login to [Github](https://github.com/). In this tutorial, we will refer to this browser tab as `GITHUB TAB`.
2. Using the same web browser tab (`GITHUB TAB`), go to the Github repository[`https://github.com/giodeealbayda/tradeoffanalytics1'](https://github.com/giodeealbayda/tradeoffanalytics1).
3. For the repository by clicking the `Fork` button.
4. Verify that you have successfully forked the repository by checking its name:

	**Name of Repository:**
	
	```text
	<username/tradeoffanalytics1
	```
	
	The repository contains the following.
	
	```text
	tradeoffanalytics1/
	|
	|----build.gradle
	|
	|----src/
	|	|----main/
	|		 |----java/
	|		 |	  |----Connector/
	|		 |	  |		|----Connector.java
	|		 |	  |
	|		 |	  |----Servlet/
	|		 |		      |----TradeOffServlet.java
	|		 |
	|		 |----webapp/
	|			    |----newjsp1.jsp
	|----build/
	|	  |----classes/
	|	  |	      |----main/
	|	  |		       |----Connector/
	|	  |		       |----Servlet/
	|	  |
	|	  |----libs/
	|	  |
	|	  |----tmp/
	|	  	  |----war/
	```
	<br>

####Create a Bluemix DevOps Project based on the Github Repository
1. Open another web browser tab and login to [Bluemix DevOps](https://hub.jazz.net).
2. Click `CREATE PROJECT`.
3. Name your project `tradeoffanalytics-delivery-pipeline`.
4. Clink `Link to an existing GitHub repository`.
	>If this is the first time you will link a Bluemix DevOps project to a GitHub repository, you will be asked to authorize your Bluemix DevOps account to access your GitHub account.  Proceed with confirming access.

	<br>
5. Select the repository `<username>/tradeoffanalytics1`.
6. Ensure the following options are chosen:

	||||
	|---|---|---|
	| **Private Project** | checked |
	| **Add features for Scrum development** | checked |
	| **Make this a Bluemix Project** | checked |
	| **Region** | IBM Bluemix US South |
	| **Organization** | you may leave the default selection |		
	| **Space** | dev |

	<br>
7. Click the `CREATE` button. Wait for your project to be created.
8. Click the `EDIT CODE` button. You will be redirected to the Bluemix DevOps' editor. In this tutorial, we will refer to this browser tab as `DEVOPS-EDITOR TAB`.

	The editor shows the working directory (and not the GitHub repository you forked earlier).  The working directory is very similar to a local directory in your hard drive.  In fact, when you chose to link the existing `<username>/tradeoffanalytics1` remote repository in an earlier step, you basically instructed Bluemix DevOps to clone the said remote repository to the working directory.  This is very similar to cloning the remote repository to a local repository (i.e., the one in a hard drive).

	However, notice that there are additional files/subdirectories (e.g., `.cfignore` and `launchConfigurations`) that were added in the working directory.  These were added automatically when the Bluemix DevOps project was created.  To sync the working directory with the GitHub repository `<username>/tradeoffanalytics1`, these files/directories need to be pushed to the GitHub remote repository.

	<br>
9. On the `DEVOPS-EDITOR TAB`: Click (open in another browser tab) the `Git Repository` icon found on the left side of the screen.  We will refer to this browser tab as `DEVOPS-GIT TAB`.

	<br>

10. On the `DEVOPS-GIT TAB`: on the `Working Directory` section (right side of the page) Set the following values:

	||||
	|---|---|---|
	| **Select All** | checked |
	| **Commit message** | files created when Bluemix DevOps project was created |

	<br>

11. On the `DEVOPS-GIT TAB`: Click the `Commit` button.
12.  On the `DEVOPS-GIT TAB`: Click the `Push` button.

	Your working directory and GitHub repository are now synced.

	<br>
	
13.  On the `GITHUB TAB`: Refresh the page and verify that `.cfignore` and `launchConfigurations` are added.

	You are now ready to create the delivery pipeline (i.e., build stage, test stage, deploy stage).

	<br>
	
14.  On the `DEVOPS-GIT TAB`: Click (open in another browser tab) the `BUILD & DEPLOY` button.  We will refer to this browser tab as `DEVOPS-DELIVERY-PIPELINE TAB`.


	<br>

####Create a Build Stage
1.  On the `DEVOPS-DELIVERY-PIPELINE TAB`: Click the `ADD STAGE` button.  Change the stage name `MyStage` to `Build Stage`.

2. On the `DEVOPS-DELIVERY-PIPELINE TAB`: On the `INPUT` tab, set the following values:

	||||
	|---|---|---|
	| **Input Type** | SCM Repository |
	| **Git URL** | https://github.com/<username>/tradeoffanalytics1.git |
	| **Branch** | master |
	| **Stage Trigger** | Run jobs whenever a change is pushed to Git |

	<br>

2. On the `DEVOPS-DELIVERY-PIPELINE TAB`: On the `JOBS` tab, click the `ADD JOB` link and select `Build`.   Change the job name `Build` to `Gradle Assemble`.  Set the following values:

	||||
	|---|---|---|
	| **Builder Type** | Gradle |		
	| **Build Shell Command** | `#!/bin/bash`<br>`gradle assemble`  |	
	| **Stop running this stage if this job fails** | checked |

	<br>

3. On the `DEVOPS-DELIVERY-PIPELINE TAB`:  Click the `SAVE` button.

	<br>
	
####Create a Test Stage

1. On the `DEVOPS-DELIVERY-PIPELINE TAB`: Click the `ADD STAGE` button.  Change the stage name `MyStage` to `Test Stage`.

2. On the `DEVOPS-DELIVERY-PIPELINE TAB`: On the `INPUT` tab, set the following values:

	||||
	|---|---|---|
	| **Input Type** | Build Artifacts |
	| **Stage** | Build Stage |
	| **Job** | Gradle Assemble |
	| **Stage Trigger** | Run jobs when the previous stage is completed |

	<br>

3. On the `DEVOPS-DELIVERY-PIPELINE TAB`: On the `JOBS` tab, click the `ADD JOB` link and select `Test`.   Change the job name `Test` to `JUnit Test through Gradle`.  Set the following values:

	||||
	|---|---|---|
	| **Tester Type** | Simple |		
	| **Test Command** | `#!/bin/bash`<br>`gradle test`  |	
	| **Stop running this stage if this job fails** | checked |

	<br>

4. On the `DEVOPS-DELIVERY-PIPELINE TAB`:  Click the `SAVE` button.

	<br>

####Create a Deploy Stage

1. On the `DEVOPS-DELIVERY-PIPELINE TAB`: Click the `ADD STAGE` button.  Change the stage name `MyStage` to `Dev Deploy Stage`.

	>Unlike the build and test stages which are named `Build Stage` and `Test Stage`, respectively, the name of the deploy stage you are about to create is `Dev Deploy Stage` to denote that that the application will be deployed in the `dev` space of your Bluemix account.  Another deploy stage will be created later.

	<br>

2. On the `DEVOPS-DELIVERY-PIPELINE TAB`: On the `INPUT` tab, set the following values:

	||||
	|---|---|---|
	| **Input Type** | Build Artifacts |
	| **Stage** | Build Stage |
	| **Job** | Gradle Assemble |
	| **Stage Trigger** | Run jobs when the previous stage is completed |

	<br>

3. On the `DEVOPS-DELIVERY-PIPELINE TAB`: On the `JOBS` tab, click the `ADD JOB` link and select `Deploy`.   Change the job name `Deploy` to `Cloud Foundry Push to Dev Space`.  Set the following values:

	||||
	|---|---|---|
	| **Deployer Type** | Cloud Foundry |		
	| **Target** | IBM Bluemix US South - https://api.ng.bluemix.net |		
	| **Organization** | you may leave the default selection |		
	| **Space** | dev |	
	| **Application Name** | blank |		
	| **Deploy Script** | `#!/bin/bash`<br>`cf push calculator-<your_name> -m 256M -p build/libs/tradeoffanalytics1.war`  |	
	| **Stop running this stage if this job fails** | checked |

	>**IMPORTANT:** In the `cf push` command, make sure to change `<your_name>` to your name.
	
	<br>

4. On the `DEVOPS-DELIVERY-PIPELINE TAB`:  Click the `SAVE` button.

	You have created a delivery pipeline. 

	<br>

#### Deploy the Application through the Delivery Pipeline

1.  On the `DEVOPS-DELIVERY-PIPELINE TAB`:  Click (open in another browser tab) the `View logs and history ` link of the `Build Stage`.  We will refer to this browser tab as `DEVOPS-BUILD-STAGE-LOGS TAB`.

2.  On the `DEVOPS-DELIVERY-PIPELINE TAB`:  Click (open in another browser tab) the `View logs and history ` link of the `Test Stage`.  We will refer to this browser tab as `DEVOPS-TEST-STAGE-LOGS TAB`.

3.  On the `DEVOPS-DELIVERY-PIPELINE TAB`:  Click (open in another browser tab) the `View logs and history ` link of the `Dev Deploy Stage`.  We will refer to this browser tab as `DEVOPS-DEV-DEPLOY-STAGE-LOGS TAB`.

	The `DEVOPS-BUILD-STAGE-LOGS TAB`, `DEVOPS-TEST-STAGE-LOGS TAB`, `DEVOPS-DEV-DEPLOY-STAGE-LOGS TAB` will allow you to monitor the status of the delivery pipeline in each stage.

	Recall that in the [Creating a Web Application using Gradle Tutorial](/gradle-web-application) the following commands are used:

	Command | Purpose
	---|---
	`gradle assemble` | build `calcuapp.war`
	`gradle test` | run the JUnit test
	`cf push` | deploy the web application in Bluemix

	These three commands are exactly the same commands that the three stages will do.

	<br>
	
4.  On the `DEVOPS-DELIVERY-PIPELINE TAB`:  Click the `Run Stage` icon of the `Build Stage`.

	Notice that the status of the `Build Stage` changes to `STAGE RUNNING`.

	Once the status of `Build Stage` changes to `STAGE PASSED`, the `Test Stage` will automatically start.

	Similarly, when the status of `Test Stage` changes to `STAGE PASSED`, the `Dev Deploy Stage` will automatically start.

	Wait for the status of the `Dev Deploy Stage` to change to `STAGE PASSED`.

	You may view the `DEVOPS-BUILD-STAGE-LOGS TAB`, `DEVOPS-TEST-STAGE-LOGS TAB`, `DEVOPS-DEV-DEPLOY-STAGE-LOGS TAB` to see the logs related to the execution of the three stages.

	<br>
	
5. Open another web browser tab. We will refer to this browser as the `TRADEOFFANALYTICS-APP TAB`.
6. On the `TRADEOFFANALYTICS-APP TAB`: Go to `http://tradeoffanalytics-<your_name>.mybluemix.net/newjsp1.jsp`.

	**Output:**
	```
	<INSERT OUTPUT HERE>
	```

#### Automatically start the Delivery Pipeline
In the previous step, you manually started the delivery pipeline by clicking the 
####Create Bluemix Devops Services Deliver Pipeline based on the Github Repository
1. Open another web browser tab and login to <a href="http://hub.jazz.net">`Bluemix Devops`</a>.
2. Click `CREATE PROJECT`.
3. Name your project `tradeoff-delivery-pipeline`.
4. Click `Link to an existing Github repository`.


####Delete the Sample Application and the Tradeoff Analytics Service
1. Go back to the browser tab containing your Bluemix account. In the menu, click `DASHBOARD`.
2. Click the `gear` icon in the widget of the sample application.
3. Click the `Delete App` entry. In the `Services` tab, make sure that the `Tradeoff Analytics` service is selected. In the `Routes` tab, make sure that the route (i.e., URL) is selected.
4. Click the `DELETE` button.
	
####End of Tutorial

Go back to the [List of Tutorials](/tutorial-list).
