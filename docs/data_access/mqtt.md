# MQTT

First, connect to the cloud.iO MQTT broker at **`CLOUDIO_HOST:8883`**. The cloud.iO CA cert and user/password are required.

!> If the endpoints you want to read values from are using CBOR message format, the payload will not be readable with a simple MQTT client.

## Subscribe to an attribute update

#### Example

Topic:
```mqtt
SUBSCRIBE @update/17e5338e-2443-43a1-b382-2c101c12cc03/electricity_meter/L1/current
```

Payload:
```json
{
	"constraint": "Measure",
	"type": "Number",
	"timestamp": 1.657092653914E12,
	"value": 5.68
}
```

## Publish to an attribute set

#### Example

Topic:
```mqtt
PUBLISH @set/17e5338e-2443-43a1-b382-2c101c12cc03/thermostat/room_1/temperature_setpoint
```

Payload:
```json
{
	"constraint": "Setpoint",
	"type": "Number",
	"timestamp": 1.657092653914E12,
	"value": 20.0
}
```