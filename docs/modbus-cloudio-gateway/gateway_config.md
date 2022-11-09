# Gateway configuration

This file links all the different config files together. It has a list of devices with a [device-model](/modbus-cloudio-gateway/device_model) - [data-model](/modbus-cloudio-gateway/data_model) - [mapping combo](/modbus-cloudio-gateway/mapping), and a link to the [cloud.iO properties](/modbus-cloudio-gateway/cloudio_properties) file.

**Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|[**gateway**](#gateway)<br/>(Gateway base settings)|`object`|This section describe the identification of the gateway.<br/>|yes|
|[**cloudio**](#cloudio)<br/>(Cloud\.iO base settings)|`object`|This section describe the cloud.iO settings.<br/>|yes|
|[**comm\-protocol**](#comm-protocol)<br/>(Communication Protocol list)|`array`|This section describe all the communication protocols, that has to be created.<br/>|yes|
|[**devices**](#devices)<br/>(Devices list)|`object[]`|This section describe all devices connected to the gateway.<br/>|yes|

**Additional Properties:** not allowed<br/>


**Example**

```yaml
gateway:
  name: gridlab-enapter-EL2-1
  description: "1x Enapter EL 2.1"

cloudio:
  endpoint: 24394175-dc71-4657-b12a-edd2cd6042f7
  config-file-name: cloudio-properties-dcbus-enapter-el02

comm-protocol:
  - type: core
    module-name: core_controller

  - type: modbusTCP
    module-name: modbus_enapter
    ip: 127.0.0.1
    port: 502
    framer: ModbusSocketFramer
    timeout: 5.0
  
devices:
  - name: gateway
    device-model: core/core
    comm-protocol: core_controller  # refer to one comm-protocol above
    mapping: core/core_map1
    cloudio-model: core/core

  - name: Electrolyser-EL2-1
    device-model: Enapter/Electrolyser_EL2_1_FW1_8_3
    comm-protocol: modbus_enapter  # refer to one comm-protocol above
    mapping: Enapter/Electrolyser_EL2_1_FW1_8_3_map1
    cloudio-model: Enapter/Electrolyser_EL2_1_FW1_8_3
    comm-parameters:
      unit-identifier: 1
```

<a name="gateway"></a>
## Gateway base settings

This section describe the identification of the gateway.


**Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**name**<br/>(Gateway Name)|`string`|Gateway type identification.<br/>|yes|
|**description**<br/>(Gateway Description)|`string`|Gateway type description.<br/>|yes|

**Additional Properties:** not allowed<br/>
<a name="cloudio"></a>
## Cloud\.iO base settings

This section describe the cloud.iO settings.


**Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**endpoint**<br/>(Endpoint UUID)|`string`|UUID the cloud.iO endpoint.<br/>|yes|
|**config\-file\-name**<br/>(Cloud\.iO config file name)|`string`|Name of the cloud.iO config located in the cloudio folder (no extension).<br/>|yes|

**Additional Properties:** not allowed<br/>
<a name="comm-protocol"></a>
## Communication Protocol list

This section describe all the communication protocols, that has to be created.


**Items**

<br>**Option 1 (optional):** 
Description of the Core component.


**Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**type**<br/>(Communication Protocol Type)|`string`|Type of the communication protocol to create.<br/>|yes|
|**module\-name**<br/>(Communication Protocol Name)|`string`|Name of the communication protocol to create, reference for devices.<br/>|yes|

**Additional Properties:** not allowed<br/>

<br>**Option 2 (optional):** 
Description of the Modbus component.


**Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**type**<br/>(Communication Protocol Type)|`string`|Type of the communication protocol to create.<br/>Pattern: ^modbusTCP$<br/>|yes|
|**module\-name**<br/>(Communication Protocol Name)|`string`|Name of the communication protocol to create, reference for devices.<br/>|yes|
|**ip**<br/>(Communication Protocol IP)|`string`|IP of the communication protocol to create, can be overrided by ENV vars.<br/>Format: `"ipv4"`<br/>|yes|
|**port**<br/>(Communication Protocol Port)|`integer`|Port of the communication protocol to create<br/>Minimum: `0`<br/>Maximum: `65535`<br/>|yes|
|**framer**<br/>(Modbus TCP Framer)|`string`|Modbus TCP Framer to create.<br/>Enum: `"ModbusSocketFramer"`, `"ModbusTlsFramer"`, `"ModbusRtuFramer"`, `"ModbusAsciiFramer"`, `"ModbusBinaryFramer"`<br/>|yes|

**Additional Properties:** not allowed<br/>

**Minimum Items:** 1<br/>
**Unique Items:** yes<br/>
<a name="devices"></a>
## Devices list

This section describe all devices connected to the gateway.



**Items: Device description**


Device description of every device one by one.

**Item Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**name**<br/>(Device Name)|`string`|Device Name, correspond to the cloudio Node Name.<br/>|yes|
|**device\-model**<br/>(Device model file name)|`string`|Device model file name from the device-model folder (no extension).<br/>|yes|
|**comm\-protocol**<br/>(Communication protocol)|`string`|Link to the protocol module-name to use, link to the comm-protocol section<br/>|yes|
|**mapping**<br/>(Mapping file name)|`string`|Mapping file name from the mapping folder (no extension).<br/>|yes|
|**cloudio\-model**<br/>(Cloud\.iO Model file name)|`string`|Cloud.iO Model file name from the cloudio/device folder (no extension).<br/>|yes|
|[**comm\-parameters**](#devicescomm-parameters)<br/>(Communication Protocol Parameters)|`object`|Communication Protocol Parameters specific to this device.<br/>|no|

**Item Additional Properties:** not allowed<br/>
**Minimum Items:** 1<br/>
**Unique Items:** yes<br/>
**Example**

```yaml
devices:
  - name: gateway
    device-model: core/core
    comm-protocol: core_controller  # refer to one comm-protocol above
    mapping: core/core_map1
    cloudio-model: core/core

  - name: Electrolyser-EL2-1
    device-model: Enapter/Electrolyser_EL2_1_FW1_8_3
    comm-protocol: modbus_enapter  # refer to one comm-protocol above
    mapping: Enapter/Electrolyser_EL2_1_FW1_8_3_map1
    cloudio-model: Enapter/Electrolyser_EL2_1_FW1_8_3
    comm-parameters:
      unit-identifier: 1
```

<a name="devicescomm-parameters"></a>
### Communication Protocol Parameters

Communication Protocol Parameters specific to this device.


**Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**unit\-identifier**<br/>(Modbus Unit Identifier)|`integer`|ModbusTCP Unit Identifier, for addressing specific unit id<br/>Minimum: `0`<br/>Maximum: `255`<br/>|no|
|**offset**<br/>(Modbus Offset)|`integer`|Offset on all modbus TCP register addresses<br/>|no|

**Additional Properties:** not allowed<br/>

