---
layout: post
title: Tradeof Analytics Tutorial
permalink: /tradeoff-analytics/
---


##Tradeoff Analytics Tutorial

> In this tutorial you will learn how to create a simple web application that will provide Tradeoff Analytics as its service in analyzing the given data.
<br>
>Access Git Repository [here](https://github.com/giodeealbayda/tradeoffanalytics.git).

####Copy the Github Repository
1. Open a web browser tab and login to [Github](https://github.com/). In this tutorial, we will refer to this browser tab as `GITHUB TAB`.
2. Using the same web browser tab (`GITHUB TAB`), go to the Github repository[`https://github.com/giodeealbayda/tradeoffanalytics'](https://github.com/giodeealbayda/tradeoffanalytics).
3. For the repository by clicking the `Fork` button.
4. Verify that you have successfully forked the repository by checking its name:

	**Name of Repository:**
	
	```text
	<username>/tradeoffanalytics
	```
	
	The repository contains the following.
	
	```text
	tradeoffanalytics/
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
	|			    |----home.jsp
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
	
	`src` has two subdirectories: `main/java` and `main/webapp`. 

	`src/main/java` contains the Java class `src/main/Connector/Connector.java` which connects the application to the Tradeoff Analytics service. In addition, it contains the `src/main/Servlet/TradeOffServlet.java` which processes the data from the web application. 

	`src/main/webapp` contains the JSP page `src/webapp/home.java` which is the interface of the web application. This is where the value of each data can be manipulated by the user before the data processing
 
	`build` has two subdirectories: `classes` and `libs`. 

	`build/classes` is used to hold the the `.class` files that will be created later when you compile the web application.

	`build/libs` is used to store the `.war` file which will be created after compiling the web application.

	<br>
	
####Create a Bluemix DevOps Project based on the Github Repository
1. Open another web browser tab and login to [Bluemix DevOps](https://hub.jazz.net).
2. Click `CREATE PROJECT`.
3. Name your project `tradeoffanalytics-delivery-pipeline`.
4. Clink `Link to an existing GitHub repository`.
	>If this is the first time you will link a Bluemix DevOps project to a GitHub repository, you will be asked to authorize your Bluemix DevOps account to access your GitHub account.  Proceed with confirming access.

	<br>
5. Select the repository `<username>/tradeoffanalytics`.
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

	The editor shows the working directory (and not the GitHub repository you forked earlier).  The working directory is very similar to a local directory in your hard drive.  In fact, when you chose to link the existing `<username>/tradeoffanalytics` remote repository in an earlier step, you basically instructed Bluemix DevOps to clone the said remote repository to the working directory.  This is very similar to cloning the remote repository to a local repository (i.e., the one in a hard drive).

	However, notice that there are additional files/subdirectories (e.g., `.cfignore` and `launchConfigurations`) that were added in the working directory.  These were added automatically when the Bluemix DevOps project was created.  To sync the working directory with the GitHub repository `<username>/tradeoffanalytics`, these files/directories need to be pushed to the GitHub remote repository.

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
	| **Git URL** | https://github.com/<username>/tradeoffanalytics.git |
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
	| **Deploy Script** | `#!/bin/bash`<br>`cf push tradeoffanalytics-<your_name> -m 256M -p build/libs/tradeoffanalytics.war`  |	
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

	Recall that in the creating a Web Application using Gradle, the following commands are used:

	Command | Purpose
	---|---
	`gradle assemble` | build `tradeoffanalytics.war`
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
6. On the `TRADEOFFANALYTICS-APP TAB`: Go to `http://tradeoffanalytics-<your_name>.mybluemix.net/home.jsp`.

	**Output:**
	||||||||
	|---|---|---|---|
	|**Choices:**|**Price**|**RAM**|**Screen**|
	| Galaxy S4 | 50 | 45 | 5 |
	| iPhone 5 | 99 | 40 | 4 |
	| MyPhone | 5 | 30000 | 5000 |
	| LG Optimus G | 10 | 300 | 5 |
	| | | | **Analyze** |
	
####Analyze how the Tradeoff Analytics Service Works

This tutorial only covers the basic functions of the Tradeoff Analytics Service. All of the functions needed by the service to work is found in the `TradeOffServlet.java`. The servlet is found in the `src/main/java/Servlet` directory.

####Run the Sample Application
The web application is composed of only one webpage wherein the user is allowed to modify the default specifications of each phone. For this activity, the values will not be modified to show the obvious winner given the specifications.

1. Click the `Analyze` button in order to process the data.
2. The processed JSON will be presented on the screen. The top choice will have a value of `FRONT` while the others that does not match the category will have `EXCLUDED`.

```text
{ "problem": { "columns": [ { "key": "price", "type": "numeric", "goal": "min", "is_objective": true, "range": { "low": 0.0, "high": 100.0 } }, { "key": "screen", "type": "numeric", "goal": "max", "is_objective": true }, { "key": "ram", "type": "numeric", "goal": "max", "is_objective": false } ], "options": [ { "description_html": "", "key": "1", "name": "Galaxy S4", "values": { "price": 50.0, "screen": 5.0, "ram": 45.0 } }, { "description_html": "", "key": "2", "name": "iPhone 5", "values": { "price": 99.0, "screen": 4.0, "ram": 40.0 } }, { "description_html": "", "key": "3", "name": "MyPhone", "values": { "price": 5.0, "screen": 5000.0, "ram": 30000.0 } }, { "description_html": "", "key": "4", "name": "LG Optimus G", "values": { "price": 10.0, "screen": 5.0, "ram": 300.0 } } ], "subject": "phone" }, "resolution": { "solutions": [ { "solution_ref": "1", "status": "EXCLUDED" }, { "solution_ref": "2", "status": "EXCLUDED" }, { "solution_ref": "3", "status": "FRONT" }, { "solution_ref": "4", "status": "EXCLUDED" } ] } }
```
It can be seen that the objects are passed together with their corresponding values. Since the RAM and Screen value of `MyPhone` is the best it will be compared to the other phones, it is the top choice returned by the service.

####Analyze `TradeOffServlet.java`
The output of the service is generated because of the functions of the Tradeoff Analytics service that are being called in the `TradeOffServlet.java`. This servlet is found in the `src/main/java/Servlet/` directory.

1. A new `Problem` with `phone` as its subject was initialized as seen in the code. A `Problem` is a JSON object in the body of the request to the service's `dilemmas` API.
```text
Problem problem = new Problem("phone");
```
<br>
2.  After initializing the `Problem`, we need to define the objectives my creating an ArrayList of `Column`.  Initialization of `Column` and its objectives are shown below:
```text
List <Column> columns = new ArrayList<Column>();

columns.add(new NumericColumn().withRange(0,100).withKey(price).withGoal(Goal.MIN)
			.withObjective(true));
			columns.add(new NumericColumn().withKey(screen).withGoal(Goal.MAX).withObjective(true));
			columns.add(new NumericColumn().withKey(ram).withGoal(Goal.MAX));
```

>**Important:**
>`withRange(low,high)` means that the value needs to match the range in order to qualify.
>`withGoal(Goal.MIN **OR** Goal.MAX)` means that the direction for the column. `MIN` indicates that the goal is to minimize the objective while `MAX` indicates that the goal is to maximize the objective.
>**Goal** is meaningful only for columns for which have `.withObjective(true)`.  By default, the value of `Goal` is `MAX`.

<br>
3. We need to define the options to choose by placing the values of each phone in a HashMap. `Option` object defines the fields of the possible options. The specification of options are shown below:
```text
List<Option> options = new ArrayList<Option>();
            problem.setOptions(options);

            HashMap<String, Object> galaxySpecs = new HashMap<String, Object>();
            galaxySpecs.put(price, Double.parseDouble(request.getParameter("price1")));
            galaxySpecs.put(ram, Double.parseDouble(request.getParameter("ram1")));
            galaxySpecs.put(screen, Double.parseDouble(request.getParameter("screen1")));
            options.add(new Option("1", "Galaxy S4").withValues(galaxySpecs));

            HashMap<String, Object> iphoneSpecs = new HashMap<String, Object>();
            iphoneSpecs.put(price, Double.parseDouble(request.getParameter("price2")));
            iphoneSpecs.put(ram, Double.parseDouble(request.getParameter("ram2")));
            iphoneSpecs.put(screen, Double.parseDouble(request.getParameter("screen2")));
            options.add(new Option("2", "iPhone 5").withValues(iphoneSpecs));

            HashMap<String, Object> testSpecs = new HashMap<String, Object>();
            testSpecs.put(price, Double.parseDouble(request.getParameter("price3")));
            testSpecs.put(ram, Double.parseDouble(request.getParameter("ram3")));
            testSpecs.put(screen, Double.parseDouble(request.getParameter("screen3")));
            options.add(new Option("3", "MyPhone").withValues(testSpecs));

            HashMap<String, Object> optimusSpecs = new HashMap<String, Object>();
            optimusSpecs.put(price, Double.parseDouble(request.getParameter("price4")));
            optimusSpecs.put(ram, Double.parseDouble(request.getParameter("ram4")));
            optimusSpecs.put(screen, Double.parseDouble(request.getParameter("screen4")));
            options.add(new Option("4", "LG Optimus G").withValues(optimusSpecs));
```
<br>
4. After initializing the options, we must call the `Dilemma` service in order to get the solution to the problem. We need to pass the `problem` JSON object as a parameter to the `dilemma` object.
```text
Dilemma dilemma = service.dilemmas(problem);
```
<br>
5. The resolution of the problem can be accessed in the `dilemma` object. As said before, the solution will have `FRONT` as its status and those that did not qualify will have `EXCLUDED` as its status.

>**Important:**
>If there is a tie among the options, they will all have `FRONT` as their status.<br>
####Delete the Bluemix Applications

1. Delete the application in your Bluemix account.

	This will free up some resources which is essential to accommodate new applications and services you want to deploy in the future.
2. You may retain the Bluemix DevOps project `DEVOPS-DELIVERY-PIPELINE` and your <username>/tradeoffanalytics GitHub repository.

	The DevOps project and the GitHub repository are needed in the Bluemix DevOps Services Track and Plan Tutorial.

3. You may close all the browser tabs you have opened.
	
	<br>
	
####End of Tutorial

Go back to the [List of Tutorials](/tutorial-list).
