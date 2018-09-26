+++
author = "Yana Vasileva"
categories = ["Execution"]
tags = ["Release Note"]
date = "2018-09-28T12:00:00+01:00"
title = "Camunda 7.10.0-alpha4 Released"
+++

**Camunda BPM 7.10.0-alpha4** is here and the highlights are:

* Extending the BPMN Viewer in Cockpit
* Support for Java 9 / 10 & 11
* [X Bug Fixes](https://app.camunda.com/jira/issues/?jql=issuetype%20%3D%20%22Bug%20Report%22%20AND%20fixVersion%20%3D%207.10.0-alpha4)


You can <a href="https://camunda.com/download/">Download Camunda for free</a> (click on Preview Release) or <a href="https://hub.docker.com/r/camunda/camunda-bpm-platform/">Run it with Docker</a>.


If you are interested, you can see the complete [release notes](https://app.camunda.com/jira/secure/ReleaseNote.jspa?projectId=10230&version=15332)
and the list of [known issues](https://app.camunda.com/jira/issues/?jql=affectedVersion%20%3D%207.10.0-alpha4).

If you want to dig in deeper, you can find the source code on [GitHub](https://github.com/camunda/camunda-bpm-platform/releases/tag/7.10.0-alpha4).

<!--more-->

## Extending the BPMN Viewer in Cockpit
BPMN diagrams in Cockpit are rendered and displayed by the [bpmn.js toolkit](https://bpmn.io/toolkit/bpmn-js/). Bpmn.js 
can be extended with additional modules as well as so called moddle extensions. 

An additional module refers to the extension of the feature set, wheareas a moddle extension makes it possible to add custom 
attributes and elements to the BPMN 2.0 model.

Starting with this release, it is possible to use the extension mechanism of bpmn.js through Camunda Cockpit to customize 
the default behavior of the BPMN viewer.

To extend the BPMN Viewer, the file `app/cockpit/scripts/config.js` needs to be adjusted as follows:
```javascript
var camCockpitConf = {
  ...
  bpmnJs: {
    additionalModules: {
      // a JavaScript file, which represents a module
      myCustomModule: 'my-custom-module/module'
    },
    moddleExtensions: {
      // a JSON file, which represents a moddle extension
      myCustomModdleExtension: 'my-custom-moddle/moddle'
    }
  }
  ...
};
```

For further information, please see the documentation of [Cockpit](https://docs.camunda.org/manual/develop/webapps/cockpit/extend/configuration/#bpmn-diagram-viewer-bpmn-js)
and [bpmn.js](https://bpmn.io/toolkit/bpmn-js/walkthrough/#extend-the-modeler).

## Support for Java 9 / 10 & 11
Camunda BPM is now on the cutting-edge of Java since this release brings support for Java 9 & 10 as well as for Java 11 
– which has been released just a few days ago.

## Next Steps…
As usual the fourth alpha release is scheduled for the end of the next month and we are already working on it.

Among other things, we are working on the following topics, which are planned to be released in one of the next alpha releases:

* Support of latest Wildfly version
* bpmn-js plugins are available in Cockpit

To get a complete overview of already implemented and planned features, please take a look at the [roadmap](https://camunda.com/learn/community/#roadmap) for the bigger list of planned features.

The minor release of **Camunda BPM 7.10** is coming this fall (November 30, 2018).

## Your Feedback Is Highly Appreciated!

With every release we constantly strive to improve **Camunda BPM**. To make this possible, we rely on your feedback.
Feel free to share your ideas and suggestions with us.

You can contact us by writing a post in the [forum](https://forum.camunda.org/).
