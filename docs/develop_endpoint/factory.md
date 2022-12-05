# Factory

Nodes can be generated and added automatically from a JSON description file. This file contains the cloud.iO node structure and type. The type can be `CloudioNode` for a standard cloud.iO node, or any other class that inherits from `CloudioDynamicNode`.

Additional properties can be added to the endpoint, nodes or objects:

```json
{  
	"properties": {  
		"myEndpointProperty": 1.0
    }, 
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

To get the additional properties, the endpoint, node or object class must implement `CloudioFactoryConfigurable`:
```java
public class MyNode extends CloudioDynamicNode implements CloudioFactoryConfigurable {  
  
    public MyObject myObject;  
  
    @Override  
    public void setConfigurationProperties(Map<String, Object> properties) {  
    }  
}
```

### Example

An example endpoint factory is available [here](https://github.com/cloudio-project/cloudio-endpoint-factory-example). A counter node is added based on a JSON description file. Three optional properties can be set in the description file:

- The counter step.
- The delay between each step.
- The counter max value.
