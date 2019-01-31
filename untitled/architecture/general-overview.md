# General Overview

The whole Betbook FE application is split into three main layers:

* Data Access Layer
* Query Layer
* UI Layer

These layers have their own purpose and are _glued_ together with **Behavior** module \(like a big nice cake\). 

The diagram below outlines the basic idea, that lays behind these composition:

![](../../.gitbook/assets/betbook-fe-architecture.png)

As you can see, each layer only contains limited amount of modules, used in our application. And arrows between them represent the data flow.

**Behavior** module can perform reads from **Data Access Layer** \(**DAL**\) by accessing Redux store object or by calling services API. Data can be passed to these services too.

**Query Layer** can only read data from **DAL**, transform it \(if required\) and its output then can be consumed by **UI Layer** or by **Behavior** module.

**UI Layer** just consumes data provided by **Query Layer** and invoke actions defined in **Behavior** module.

