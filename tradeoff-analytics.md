---
layout: post
title: Tradeof Analytics Tutorial
permalink: /tradeoff-analytics/
---

Download PPT Presentation [here](somewhere).
<br>
Access Git Repository [here](https://github.com/giodeealbayda/tradeoff-analytics.git).

>In this tutorial you will learn how to create a simple web application that will provide Tradeoff Analytics as its service in analyzing the given data.

###Copy Sample Application
You will download a copy of sample application that you will deploy in your Bluemix Account.

1. Create the directory `tradeoff-analytics` in your root directory.
2. Download [tradeoff-analytics.war](https://github.com/giodeealbayda/giodeealbayda.github.io/blob/master/tradeoff-analytics.war?raw=true) and save it in the `tradeoff-analytics` directory.

####Deploy Sample Application in Bluemix using the cf tool
1. Open a terminal window and go to the `tradeoff-analytics` directory.

2. Login to your Bluemix account using the cf tool.
``` 
cf login -a https://api.ng.bluemix.net -s dev
```
<br>
3. Upload the sample application to your Bluemix account.
``` 
cf push tradeoff-analytics-< your_name > -m 256M -p tradeoff-analytics.war
```
<br>
4. Go back to the browser tab containing your Bluemix account. In the menu, click `DASHBOARD`.
<br>5. Click the widget of your application to see its overview.

###Add Tradeoff Analytics Service and Bind it to the Sample Application
1. Login to your [Bluemix Account](http://www.ibm.biz/bluemixph).
2. Go to your `DASHBOARD`.
3. Click the `ADD A SERVICE OR API` link. You will be redirected to the Catalog page.
4. Look for `Tradeoff Analytics` service and click it.
5. In the `Service name` text box, type `tradeoff-analytics-service` or any name that you want for the service.
6. Click the `CREATE` button.
7. When asked to restage your application, click the `RESTAGE` button. Wait for your application to restage.
8. Open another browser tab, and type in the url `tradeoff-analytics-< your_name >.mybluemix.net` to see if your application works.

###Analyze how the Tradeoff Analytics Service Works

This tutorial only covers the basic functions of the Tradeoff Analytics Service. All of the functions needed by the service to work is found in the `TradeOffServlet.java`. The servlet is found in the `src/main/java/Servlet` directory.

####Run the Sample Application
The web application is composed of only one webpage wherein the user is allowed to modify the default specifications of each phone. For this activity, the values will not be modified to show the obvious winner given the specifications.

1. Click the `Analyze` button in order to process the data.
2. The processed JSON will be presented on the screen. The top choice will have a value of `FRONT` while the others that does not match the category will have `EXCLUDED`.

```
{
  "problem": {
    "columns": [
    {
     "key": "price",
     "type": "numeric",
     "goal": "min",
     "is_objective": true,
     "range": {
       "low": 0.0,
       "high": 100.0
     }
    },
    {
     "key": "screen",
     "type": "numeric",
     "goal": "max",
     "is_objective": true
    },
    {
     "key": "ram",
     "type": "numeric",
     "goal": "max",
     "is_objective": false
     }
    ],
    "options": [
     {
      "description_html": "",
      "key": "1",
      "name": "Galaxy S4",
      "values": {
        "price": 50.0,
        "screen": 5.0,
        "ram": 45.0
       }
     },
    {
     "description_html": "",
     "key": "2",
     "name": "iPhone 5",
     "values": {
       "price": 99.0,
       "screen": 4.0,
       "ram": 40.0
      }
     },
     {
      "description_html": "",
      "key": "3",
      "name": "MyPhone",
      "values": {
        "price": 5.0,
        "screen": 5000.0,
        "ram": 30000.0
        }
      },
      { 
       "description_html": "",
       "key": "4",
       "name": "LG Optimus G",
       "values": {
         "price": 10.0,
         "screen": 5.0,
         "ram": 300.0
          }
       }
      ],
      "subject": "phone"
     },
     "resolution": {
       "solutions": [
        {
          "solution_ref": "1",
          "status": "EXCLUDED"
        }, 
        { 
          "solution_ref": "2",
          "status": "EXCLUDED"
        },
        { 
          "solution_ref": "3",
          "status": "FRONT"
        },
        { 
          "solution_ref": "4",
          "status": "EXCLUDED"
        }
     ]
   }
}
```
It can be seen that the objects are passed together with their corresponding values. Since the RAM and Screen value of `MyPhone` is the best it will be compared to the other phones, it is the top choice returned by the service.

**< your_name >/tradeoff-analytics repository:**
	
	```
	<username>/tradeoff-analytics
	
	
	The repository contains the following.
	
	
	tradeoff-analytics/
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
###Delete the sample application for housekeeping

1. Go to Bluemix.
2. Click `DASHBOARD`.
3. From the Applications List, click the `GEAR ICON` of the `tradeoff-analytics-< your_name >` application. In the `SERVICES` tab, make sure that Tradeoff Analytics service is selected. In the `ROUTES` tab, make sure that the route (i.e., URL) is selected.
4. Choose `DELETE APP`.

####End of Tutorial

Go back to the [List of Tutorials](/tutorial-list).
