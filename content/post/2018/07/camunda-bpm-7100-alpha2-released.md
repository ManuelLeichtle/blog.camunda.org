+++
author = "Nikola Koevski"
categories = ["Execution"]
tags = ["Release Note"]
date = "2018-08-03T16:00:00+02:00"
title = "Camunda 7.10.0-alpha2 Released"

+++

The second alpha release of **Camunda BPM 7.10** is here and the highlights are:

* Cascading History Cleanup based on process hierarchy
* Notable Security fixes
* Feature 3
* Feature 4
* More support enviorments - PostgreSQL 10.4 and MariaDB 10.3
* [## Bug Fixes](https://app.camunda.com/jira/issues/?jql=issuetype%20%3D%20%22Bug%20Report%22%20AND%20fixVersion%20%3D%207.10.0-alpha1)

You can <a href="https://camunda.com/download/">Download Camunda for free</a> (click on Preview Release) or <a href="https://hub.docker.com/r/camunda/camunda-bpm-platform/">Run it with Docker</a>.

<!-- update links -->
If you are interested, you can see the complete [release notes](https://app.camunda.com/jira/secure/ReleaseNote.jspa?projectId=10230&version=15318)

and the list of [known issues](https://app.camunda.com/jira/issues/?jql=affectedVersion%20%3D%207.10.0-alpha1).

If you want to dig in deeper, you can find the source code on [GitHub](https://github.com/camunda/camunda-bpm-platform/releases/tag/7.10.0-alpha1).

<!-- notable features & fixes - start -->

## Cascading History Cleanup based on process hierarchy

## Notable Security fixes

### CSRF Prevention Filter

With the CSRF Prevention Filter the Webapps are even more secure. The CSRF filter is enabled by default, validating each modifying request performed through the webapps. The filter implements a (per-session) _Synchronization Token_ method for CSRF validation with an optional _Same Origin with Standard Headers_ verification.

If you would like to enable the additional _Same Origin with Standard Headers_ verification, the `targetOrigin` init-parameter should be set to the application expected deployment domain in the `web.xml` file of your application.

### Whitelist patterns for User, Group and Tenant IDs

Another security fix is resource whitelisting. From now on User, Group and Tenant IDs can be matched against a Whitelist Pattern to determine if the provided ID is acceptable or not. The default (global) Regular Expression pattern to match against is **"[a-zA-Z0-9]+|camunda-admin" (7.10+)* i.e. any combination of alphanumeric values or _'camunda-admin'_.

If your organisation allows the usage of additional characters (ex.: special characters), the ProcessEngineConfiguartion propery `generalResourceWhitelistPattern` should be set with the appropriate pattern in the engine's configuration file. Standard [Java Regular Expression](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html) syntax can be used. For example, to accept any character, the following property value can be used:

```xml
<property name="generalResourceWhitelistPattern" value=".+"/>
```

The definition of different patterns for User, Group and Tenant IDs is possible by using the appropriate configuration propery:

```xml
<property name="userResourceWhitelistPattern" value="[a-zA-Z0-9-]+" />
<property name="groupResourceWhitelistPattern" value="[a-zA-Z]+" />
<property name="tenantResourceWhitelistPattern" value=".+" />
```

Note that if a certain pattern isn't defined (ex. the tenant whitelist pattern), the general pattern will be used, either the default one (`"[a-zA-Z0-9]+|camunda-admin"`) or one defined in the configuration file.

## Feature 3

## Feature 4

<!-- notable features & fixes - end -->

## Take a Sneak Peek at What Is Next
We are already eagerly busy preparing for the next alpha release, which is scheduled for end of July.

Among other things, we are working on the following topics, which are planned to be released in one of the next alpha releases:

* Future feature 1
* Future feature 2

And there is more to come! Take a look at the [roadmap](https://camunda.com/learn/community/#roadmap) for the bigger list of planned features.


## Your Feedback Is Highly Appreciated!

With every release we constantly strive to improve **Camunda BPM**. To make this possible, we rely on your feedback.
Feel free to share your ideas and suggestions with us.

You can contact us by writing a post in the [forum](https://forum.camunda.org/).
