# Mapping

This file describes the mapping between a [device model](modbus-cloudio-gateway/device_model) and a [data model](modbus-cloudio-gateway/data_model).


**Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**type**<br/>(File type)|`string`|Type of the file, always mapping<br/>Pattern: mapping<br/>|yes|
|**version**<br/>(Mapping file version)|`string`|Version of the file<br/>|yes|
|**name**<br/>(Name of the file)|`string`|Name of the file<br/>|yes|
|**fullname**<br/>(Full name of the file)|`string`|Full name of the file<br/>|yes|
|**force\-update**<br/>(Forced update rate)|`string`|Update rate of all the values in cloud.iO. Refer to a refresh-rate value<br/>|yes|
|[**refresh\-rate**](#refresh-rate)<br/>(Refresh rate declaration)|`object`|Refresh list declaration, with name and value in seconds<br/>|yes|
|[**map**](#map)<br/>(Mapping list)|`object[]`|This section describe all the mapping links between HW and cloud.iO (device-model and cloudio-model).<br/>|yes|

**Additional Properties:** not allowed<br/>


**Example**

```yaml
type: mapping

version: 0.1.0

name: Electrolyser_EL2_1_FW1_8_3_map_template
fullname: Electrolyser EL2.1 Firmware 1.8.3 mapping template

force-update: slow

refresh-rate:   # in millisecond
    daily: 86400   # every day
    slow: 15       # every 10s
    fast: 2        # every 2s

map:
# base-settings
- {cloudio-name: base-settings.unix-time, comm-name: unix-time, type: int, permission: RW,refresh-rate: fast}

...
```

<a name="refresh-rate"></a>
## Refresh rate declaration

Refresh list declaration, with name and value in seconds

**Example**

```yaml
refresh-rate:   # in millisecond
    daily: 86400   # every day
    slow: 15       # every 10s
    fast: 2        # every 2s
```

This list is extensible.

<a name="map"></a>
## Mapping list

This section describes all the mapping links between [device model](modbus-cloudio-gateway/device_model) and [data model](modbus-cloudio-gateway/data_model).


**Items: Mapping value description**


Description of the mapping link for one value.

**Item Properties**

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**cloudio\-name**<br/>(Cloud\.io Reference Name)|`string`|Reference to the topic name for cloud.iO (link to cloudio-model file).<br/>|yes|
|[**comm\-name**](#commname)||Modbus register name to read/write|yes|
|**type**<br/>(Value Type)|`string`|Type of the value (bool, int, float, str or string)<br/>Enum: `"bool"`, `"int"`, `"float"`, `"str"`, `"string"`<br/>|yes|
|**permission**<br/>(Value permission access)|`string`|Value permission access (R or W).<br/>Enum: `"R"`, `"W"`<br/>|yes|
|**refresh\-rate**<br/>(Value Refresh rate)|`string`|Refresh rate of this value, refer to refresh-rate definition.<br/>|yes|
|**out**<br/>(Read modification expression)|`string`|Modification expression before sending the value to cloud.iO.<br/>Emum: `"to_signed(val, nb_bits)"`, `"to_float32(val)"`|no|
|**in**<br/>(Write modification expression)|`string`|Modification expression before writing the value to the device.<br/>`"to_unsigned(val, nb_bits)"`, `"from_float32(val)"`|no|

**Item Additional Properties:** not allowed<br/>
**Unique Items:** yes<br/>


**Example**

```yaml
- {cloudio-name: level-switches.very-low-electrolyte-temperature-switch, comm-name: very-low-electrolyte-temperature-switch, type: bool, permission: R,refresh-rate: fast}
- {cloudio-name: level-switches.chassis-water-presence-switch, comm-name: chassis-water-presence-switch, type: bool, permission: R,refresh-rate: fast}
- {cloudio-name: level-switches.electrolyte-level, comm-name: [high-electrolyte-level-switch, very-high-electrolyte-level-switch, low-electrolyte-level-switch, medium-electrolyte-level-switch], type: int, permission: R,refresh-rate: fast, out: "len([x for x in val if x == 1])"}  # count the number of 1 => states of the tank

```

<a name="commname"></a>
## Comm\-name

This part is the Modbus register name to read/write. It can be a string or a list of string(only read-only). In the case of a string, the value can be accessed in the `out` parameter with the `val` identifier. In the case of a list of string, the `val` identifier is a list of value.

**Example**

```yaml
- {cloudio-name: actual-values.inlet-air-temperature, comm-name: inlet-air-temperature, type: int, permission: R,refresh-rate: fast, out: "to_signed(val, 16)"}
- {cloudio-name: actual-values.apparent-power, comm-name: [apparent-power-L1, apparent-power-L2, apparent-power-L3], type: int, permission: R,refresh-rate: fast, out: "val[0] + val[1] + val[2]"}


```
