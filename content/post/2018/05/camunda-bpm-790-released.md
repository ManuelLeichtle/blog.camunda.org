+++
author = "Nikola Koevski & Roman Smirnov"
categories = ["Execution"]
date = "2018-05-31T12:00:00+02:00"
tags = ["Release Note"]
title = "Camunda 7.9.0 Released"

+++

Camunda BPM platform 7.9.0 is released and the highlights are:

<!-- FEATURES LIST BEGINS -->
* First feature
* Second feature
* Third feature
* [XX Fixes]()
<!-- FEATURES LIST ENDS -->

In addition, Wildfly 11, JBoss EAP 7.1, Tomcat 9, and the database Maria DB 10.2 are now officially supported.

You can [Download Camunda for free](https://camunda.com/download/) (click on Preview Release) or [Run it with Docker](https://hub.docker.com/r/camunda/camunda-bpm-platform/).

We have also released the Camunda Spring Boot Starter 3.0.0 (TODO: link to BLOG POST), which relies on Spring Boot 2.0.0 by default.

To see a full list of the changes, please check out our [Release Notes](https://app.camunda.com/jira/secure/ReleaseNote.jspa?projectId=10230&version=15301)
and the list of [Known Issues](https://app.camunda.com/jira/issues/?jql=affectedVersion%20%3D%207.9.0).

If you want to dig in deeper, you can find the source code on [GitHub](https://github.com/camunda/camunda-bpm-platform/releases/tag/7.9.0).

<!-- FEATURES EXPLANATIONS BEGIN -->

## Clients for External Tasks

* Non-Java-developers can implement their service task in NodeJS
* in addition their exists a java client that can be embedded
* link to quickstarts that shows how to install and use clients

## Significant History Cleanup Performance Improvements

So far, the history cleanup was implemented in a way, that it could only be run in one thread. This guaranteed, that the history cleanup process 
does not overload too much the application server and the database and does not have significant impact on the process engine performance. 
However, it can happen, that history cleanup is configured to be run only at nights and at night the application is not used, thus nobody cares about the process engine performance.
In such cases, you can now parallelize the history cleanup process, by defining **degree of parallelism**, which st the end means the possible number of threads, 
simultaneously performing the cleanup.

Below you can see the comparison of history cleanup performance in case you run it in one or in three threads.

The test was performed on the engine running on normal PC and Oracle 12 as a database.

{{< figure class="main teaser no-border" src="history-cleanup-number.png">}}

{{< figure class="main teaser no-border" src="history-cleanup-number-per-sec.png">}} 

In order to enable the feature, you should define the `historyCleanupDegreeOfParallelism` configuration parameter. For more information check 
[the docs](https://docs.camunda.org/manual/7.9/reference/deployment-descriptors/tags/process-engine/#history-cleanup-configuration-parameters)

## Transient Variables
 
Various data, accompanying the process flow, is usually stored as process variables. But it is often the case, that there is some raw input data 
(huge XML or JSON file or similar), which must be preprocessed before being used in the process. Before version 7.9 you had to choose: either preprocess it "outside" 
the process and then pass the extracted granular process variables to the engine, or to implement "data processing" step inside the process, which forced you
to pass the whole raw data as a process variable. This means that it would be stored in the database and even if you later remove the variable, it would still 
remain in history tables.

This problem can now be solved with the help of transient variables. You can pass the transient variable to the process and be sure that it 
will never be saved in the database. Though, it will be accessible as a normal variable till the next database transaction commit.

Imaging such process:

{{< figure class="main teaser no-border" src="transient_variables.png" >}}
  
You can start it with this REST call:
```test
POST /message

{
  "messageName" : "supportRequest",
  "processVariables" : {
    "requestData" : { 
      "value" : "[huge JSON content here]", 
      "type": "String"
      "valueInfo": {
        "transient": true
      }
    }
  }
}

```
or via Java API:

```java
runtimeService.createMessageCorrelation("supportRequest")
      //true in the second parameter indicates transient variable
      .setVariable("requestData", Variables.stringValue("huge JSON content here", true))      
      .correlate();
```

Message correlation will start the new process instance, then the service task "Extract client data" will be executed, where passed variable can be used to extract
 client id and another data. After that the database transaction will be committed (as the process has reached the waiting state), saving client id and other data in dedicated variables, 
 but `requestData` will cease to exist.

More information on usage of transient variables can be found in [the docs](https://docs.camunda.org/manual/latest/user-guide/process-engine/variables/#transient-variables).

## Docker Container for Camunda BPM Platform Enterprise

* link to docs

## New Features in Camunda Cockpit

### Sortable Columns

* a gif showing how to use it

### User Operation Log

* shows who executed which kind of operation


<!-- FEATURES EXPLANATIONS END -->

## Much more

There are many more smaller features and bugfixes in the release which aren't presented here in the blogpost. The [full release notes](TODO) provide the details.

## Register for the Webinar

If you have not already, make sure to place a last-minute registration for the free release webinars - [German](TODO) and [English](TODO).

## Your Feedback Matters!

With every release we constantly strive to improve Camunda BPM. To make this possible, we are reliant on your feedback. Feel free to share your ideas and suggestions with us.

You can contact us by writing a post in the [forum](https://forum.camunda.org/).

Furthermore, if you have any feedback related to User Experience, things that keep bugging you, things that you think should work differently etc., please share your thoughts with us at [https://camundabpm.userecho.com](https://camundabpm.userecho.com)
