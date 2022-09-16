# The data structure

A **cloud.iO endpoint** is composed of **nodes**, **objects** and **attributes**:

<p align="center">
  <img src="about_cloudio/_media/data_structure.svg" style="width:70%" />
  <div class="caption" style="text-align: center">Endpoint data structure</div>
</p>

Every element of the data model can be identified by an **identifier** *(ID)*.

## Endpoint
An **endpoint** is identified by a **UUID**, which is a unique identifier pseudo-randomly generated.
As the **UUID** is not *"human user friendly"*, every endpoint is also identified with a **friendlyName** that can be freely choosen.
> As the **friendlyNames** are free, it's possible that 2 **endpoints** share the same **friendlyName**. This won't cause troubles to **cloud.iO** as it works internally with **UUIDs** only.  

An **endpoint** is composed by one or more **nodes**.

## Node
A **node** is identified by a its parent endpoint **UUID** and a **nodeName**. The endpoint is free to choose the **nodeName**.
A **node** will typically correspond to a device, actuator or sensor to which the **endpoint** can access/control.   
A **node** can implement one or more **interfaces**. This functionality can per example be used when an **endpoint** as access to multiple devices with the same type.  
A **node** is composed by one or more **objects**.

## Object
An **object** is identified by its parent element *(**node** or **object**)* identifier, plus an **objectName**. The endpoint is free to choose the **objectName**.  
An **object** is used to organize the data and **attributes** inside a **node**.
> The **objects** in **objects** feature allows **cloud.iO** to support flexible and extensible structures. 
To identify an object contained in another one, simply append the child object name to the parent identifier:<br>
*UUID/nodeName/objectName1/objectName2*

An **object** is composed by none, one or more **objects** and one or more **attributes**.

## Attribute
An **attribute** is identified by its parent **object** identifier, plus an **attributeName**. The endpoint is free to choose the **attributeName**.   
Every **attribute** must have a **constraint** and a **type**.

### Constraints
Four **constraints** are defined:
<p align="center">
  <img src="about_cloudio/_media/constraints.svg" style="width:30%" />
</p>

* **Measure**: typically a sensor acquired value.
* **Status**: computed value.
* **Parameter**: configuration element. Its value should be shutdown resistive *(it's up to the endpoint developer to store the **parameter** value)*.
* **Setpoint**: typically an actuator's **setpoint**.

### Types
Four **types** exists:
* Integer
* Double
* Boolean
* String

As well as arrays of the above **types**.