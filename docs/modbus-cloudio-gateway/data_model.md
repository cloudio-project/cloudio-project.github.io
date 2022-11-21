# Data model

This file describes the cloudio structure for a device. One file corresponds to one cloud.iO node.


### Example 

```xml
<node>
    <object name="information">
        <attribute name="string-ID" type="Integer" constraint="Status" description="The string number"/>
        <attribute name="string-data-timestamp" type="Integer" constraint="Status" description="The UTC timestamp of the measurements"/>
    </object>
    <object name="output">
        <attribute name="OutDCA" type="Integer" constraint="Measure" description="String output current in mA"/>
        <attribute name="OutDCV" type="Integer" constraint="Measure" description="String output voltage in mV"/>
        <attribute name="DCWh" type="Integer" constraint="Measure" description="Daily integrated string output energy in Wh"/>
    </object>
    <object name="input">
        <attribute name="In1DCV" type="Integer" constraint="Measure" description="String input 1 voltage in mV"/>
        <attribute name="In2DCV" type="Integer" constraint="Measure" description="String input 2 voltage in mV"/>
        <attribute name="In1DCA" type="Integer" constraint="Measure" description="String input 1 current in mA"/>
        <attribute name="In2DCA" type="Integer" constraint="Measure" description="String input 2 current in mA"/>
    </object>
</node>
```

The file is composed of one node, with some objects. In the objects are attributes. And the attributes have name, type, constraint and description (not mandatory).

### Type 
type possible values : ["Boolean", "Integer", "Number", "String"]


### Constraint
constraint possible values : ["Static", "Parameter", "Status", "Setpoint", "Measure", "Invalid"]