# Device model


This file describes the device modbus registers structure.


**Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**type**<br/>(File type)|`string`|Type of the file, always device_description<br/>Pattern: device\_description<br/>|yes|
|**version**<br/>(Device model version)|`string`|Version of the file<br/>|yes|
|**name**<br/>(Name of the file)|`string`|Name of the file|yes|
|**fullname**<br/>(Full name of the file)|`string`|Full name of the file<br/>|yes|
|**communication**<br/>(Type of communication)|`string`|The type of communication for this device, `modbusTCP` or `modbusRTU`<br/>|yes|
|[**data**](#data)<br/>(Modbus register list)|`object[]`|This section describe all the modbus registers for this device.<br/>|yes|

**Additional Properties:** not allowed<br/>



**Example**

```yaml
type: device_description

version: 0.1.0

name: Electrolyser_EL2_1_FW1_8_3
fullname: Electrolyser EL2.1 Firmware 1.8.3

communication: modbusTCP

data:
# base-settings
- {name: unix-time, addr: 0, length: 4, type: hr}

...
```


## Modbus register list

This section describe all the modbusTCP register for this device.


**Items: Register description**


Description of the modbusTCP register.

**Item Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**name**<br/>(Register Name)|`string`|Register arbitrary name for mapping file.<br/>|yes|
|**addr**<br/>(Register modbus address)|`integer`|Register modbus address.<br/>|yes|
|**length**<br/>(Length of the register)|`integer`|Number of consecutive 16bits register that represent the value (length=1 => 16bits)<br/>|yes|
|**type**<br/>(Register Type)|`string`|Type of the modbus register (co=Coil, di=Discrete input, ir=Input register, hr=Holding register)<br/>Enum: `"co"`, `"di"`, `"ir"`, `"hr"`<br/>|yes|

**Item Additional Properties:** not allowed<br/>
**Minimum Items:** 1<br/>
**Unique Items:** yes<br/>
**Example**

```yaml
- {name: unix-time, addr: 0, length: 4, type: hr}
- {name: reboot, addr: 4, length: 1, type: hr}
- {name: locate-electrolyser, addr: 5, length: 1, type: hr}
```

