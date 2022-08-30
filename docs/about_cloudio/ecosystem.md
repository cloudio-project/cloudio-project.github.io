# The cloud.iO ecosystem
The **cloud.iO** ecosystem is composed of three layers: **application**, **core services** and **endpoint**:

<p align="center">
  <img src="about_cloudio/_media/elements.svg" style="width:40%" />
  <div class="caption" style="text-align: center">The cloud.iO elements</div>
</p>

## Application
An **application** is a computer programs that can:

* get the endpoint's data structure.
* subscribe to input signals, which are typically results of sensors measurement.
* receive updates of subscribed input values without polling.
* set values of output signals, which are typically set points for actuators.
* access past values for any input or output signals.
* get actual and historical data for endpoint's attributes.
* process 


## Core services
The main objectives of the **cloud.iO core services** *(cloud.iO cluster)* are:

* to decouple **applications** from **endpoints** by providing a syntactic abstraction layer.
* to keep up-to-date the topology of cloud.iO **endpoints** and their current status.
* to log history values of all input signals and to make the allow **applications** querying them.
* to enable **applications** access to the current topology as well as the history logs.
* to enforce privacy rules based on access rights.


## Endpoint

Endpoints are distributed field devices featuring:

* a TCP/IP interface to access cloud.iO **core services**.
* a set of sensors and/or actuators either directly integrated in the endpoint device or connected by some (local) networking technology like Zigbee for example.

It needs a SSL certificate to communicate with cloud.iO (MQTTs protocol). The definitions (interfaces, pre-processing steps, ...) are stored in **cloud.iO**, 
but the implementation is done on back-end solutions, depending on the type of **endpoint**.

An **endpoint** does:

* publish his complete data model (including current values) when connecting to the cloud.
* publish a message when disconnected from the cloud.
* sends a message every time data of his data model has changed.
* allow **applications** or users to change the data from the outside (control, parameters).

An **endpoint** can:
* have a gateway only function.
* do a local data processing.

## User
A **user** is the owner of **endpoints** and **applications**. A **user**:
* owns one or more **endpoints**.
* can give other **users** access to his **endpoints**.
* can give **applications** access to his **endpoints**.
* can write his own **applications**.