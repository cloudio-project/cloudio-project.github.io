---
title: "How It Works"
link: how-it-works
weight: 2
style: center
bg: gray
color: white
fa-icon: angle-double-down
---

![cloud.iO Architecture]({{ site.url }}images/architecture.png)

In the center of cloud.iO is a slightly modified version of the MIT Licensed [RabbitMQ message broker](https://www.rabbitmq.com). 
The modifications allows cloud.iO to authenticate devices, applications and users and check for the permission of actually posting
messages or subscribe to a given topic.

Embedded devices and monitoring devices will connect via MQTT. Applications and the core cloud.iO services use the AMQP protocol. The default
implementations of the cloud.iO services uses MongoDB and InfluxDB as storage. Those can be replaced with other storage backends with ease.

More informations to follow...