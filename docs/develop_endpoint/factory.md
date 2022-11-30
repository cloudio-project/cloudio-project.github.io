# Factory

Nodes can be generated and added automatically from a JSON description file. This file contains the cloud.iO node structure and a type. The type can be `CloudioNode` for a standard cloud.iO node, or any other class that inherits from `CloudioDynamicNode`.

Additional properties can be added to the nodes or objects:

```json
{  
   "nodes": {  
      "myNodeFromFactory": {  
         "type": "CloudioNode",  
         "objects": {  
            "myObject": {  
               "properties": {  
                  "test": 1.0,  
                  "second-property": "foobar"  
               },  
               "attributes": {  
                  "myInt": {  
                     "constraint": "Measure",  
                     "type": "Integer"  
                  },  
                  "mySetPoint": {  
                     "constraint": "SetPoint",  
                     "type": "Number"  
                  }  
               }  
            }  
         }  
      },  
      "myCustomNodeFromFactory": {  
         "type": "localTest.MyNode",  
         "properties": {  
            "test": 1.0,  
            "my-awesome-property": "foo"  
         },  
         "objects": {  
            "myObject": {  
               "properties": {  
                  "test": 0.0,  
                  "test1": "bar"  
               },  
               "attributes": {  
                  "myInt": {  
                     "constraint": "Measure",  
                     "type": "Integer"  
                  }  
               }  
            }  
         }  
      }  
   }  
}
```

To get the additional properties, the node class must implement `CloudioFactoryConfigurable`:
```java
public class MyNode extends CloudioDynamicNode implements CloudioFactoryConfigurable {  
  
    public MyObject myObject;  
  
    @Override  
    public void setConfigurationProperties(Map<String, Object> properties) {  
    }  
}
```