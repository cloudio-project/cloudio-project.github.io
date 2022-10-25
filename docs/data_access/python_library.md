# Python Library

The [cloudio-connector-python](https://pypi.org/project/cloudio-connector-python/) library helps for cloud.iO application development.

It can read cloud.iO endpoints data model and values, write setpoints and parameters, access to the historical values and subscribe to attributes *on changed* events.

## Read/Write attributes
### Example
```python
cc = CloudioConnector("https://example.com", "user", "password")

sp = AttributeId(uuid='ba3d3ec2-23b6-45a8-827a-3b3133a69076', node='myNode', 
                    objects=['myObject'], attribute='mySetPoint')
mea = AttributeId(uuid=cc.get_uuid('demo'), node='myNode', 
                    objects=['myObject'], attribute='myMeasure')

# get the last value of an attribute
last_val = cc.get_last_value(mea)
print(str(mea) + ' ' + str(last_val))

# get the mean value of the last 15 minutes
mean = cc.get_mean_value(mea, 15*60)

# write the value of an attribute
cc.write_value(sp, 1.0)      
```
## Get attributes time series
### Example
```python
cc = CloudioConnector("https://example.com", "user", "password")

sp = AttributeId(uuid='ba3d3ec2-23b6-45a8-827a-3b3133a69076', node='myNode', 
                    objects=['myObject'], attribute='mySetPoint')
mea = AttributeId(uuid=cc.get_uuid('demo'), node='myNode', 
                    objects=['myObject'], attribute='myMeasure')

tm_mea = TimeSeries(mea, start=datetime.now() - datetime.timedelta(hours=24), 
                    stop=datetime.now(), resample='15m')
tm_sp = TimeSeries(sp, start=datetime.now() - datetime.timedelta(hours=24), 
                    stop=datetime.now(), resample='15m')

# get attribute time series
data = cc.get_time_series(tm_mea)

# convert cloudio time series to panda data frame
cc.data_frame(data, serie_name="My Measure")

# get multiple time series with multithreading
data = cc.get_multiple_time_series([tm_mea, tm_sp])
    
```
## Attributes on changed events
### Example
```python
class Example(AttributeListener):
    def __init__(self):
        cc = CloudioConnector("https://example.com", "user", "password")
        cc.add_attribute_listener(self)

        attr = AttributeId(uuid=cc.get_uuid('demo'), node='myNode', 
                            objects=['myObject'], attribute='myMeasure'),
        
        # subscribe to attribute on change event
        cc.subscribe_to_attribute(attr)
        
    # this method is called when a subscribed attribute has changed
    def attribute_has_changed(self, attribute: AttributeId, value):
        print(str(attribute) + ' ' + str(value))
```
