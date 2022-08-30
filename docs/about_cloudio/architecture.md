# The architecture

Here is an overview of the **cloud.iO architecture** and **components**:

<p align="center">
  <img src="about_cloudio/_media/architecture.svg" style="width:50%" />
  <div class="caption" style="text-align: center">Cloud.iO architecture</div>
</p>

The **cloud.iO cluster** is composed of the **cloud.iO microservices** and well known open source components.  

## Cloud.iO microservices

The **cloud.iO microservices** are written in [Kotlin](https://kotlinlang.org/), using the [Spring Framework](https://spring.io).

---

<p align="center">
  <img src="https://kotlinlang.org/docs/images/kotlin-logo.png" style="width:10%" />
  <br><br>
Write concise and expressive code while maintaining full compatibility and interoperability with Java.
</p>

*Source: https://kotlinlang.org*

---

---

<p align="center">
  <img src="https://spring.io/images/spring-logo-9146a4d3298760c2e7e49595184e1975.svg" style="width:12%" />
  <br><br>
	With its versatile set of features, Spring is the world's most popular Java framework. When it's paired with Kotlin, and its concise syntax, 
	the two make the ultimate combo for application development.
</p>


*Source: https://kotlinlang.org/lp/server-side/*

---



## Message Broker

**Cloud.iO** uses [RabbitMQ](https://www.rabbitmq.com/) as **message broker**:

---

<p align="center">
  <img src="https://www.rabbitmq.com/img/logo-rabbitmq.svg" style="width:15%" />
<br><br><center>
With tens of thousands of users, RabbitMQ is one of the most popular open source message brokers. From T-Mobile to Runtastic, RabbitMQ is used worldwide at small startups and large enterprises.<br><br>
RabbitMQ is lightweight and easy to deploy on premises and in the cloud. It supports multiple messaging protocols. RabbitMQ can be deployed in distributed and federated configurations to meet high-scale, high-availability requirements.<br><br>
RabbitMQ runs on many operating systems and cloud environments, and provides a wide range of developer tools for most popular languages. 
</center>
</p>


*Source: https://www.rabbitmq.com/*

---
## Time Series Database *(TSDB)*

**Cloud.iO** uses [InfluxDB](https://www.influxdata.com/products/influxdb-overview/) as **time series database**:

---

<p align="center">
  <img src="https://raw.githubusercontent.com/ioBroker/ioBroker.influxdb/HEAD/admin/influxdb.png" style="width:7%" />
  <br><br>
InfluxDB is the open source time series database that is community supported. As a single-node, it is easy to deploy on the edge, locally on a laptop, or on a server for development.
</p>

*Source: https://www.influxdata.com/*

---

## Object-Relational Database *(ORDB)*

**Cloud.iO** uses [PostgreSQL](https://www.postgresql.org/) as **object-relational database**:

---

<p align="center">
  <img src="https://www.postgresql.org/media/img/about/press/elephant.png" style="width:6%" />
  <br><br>
PostgreSQL is a powerful, open source object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.
</p>

*Source: https://www.postgresql.org/*

---
