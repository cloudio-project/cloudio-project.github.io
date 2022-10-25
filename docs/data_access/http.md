# HTTP

## Read last value / data model

The data model and last values of each [endpoint data model](/about_cloudio/data_structure) element can be requested.

In order to do this, send a request to the REST API:
```http
GET http://**your cloudio hostname**/api/v1/data/**ID of the element**
```

You can find below some request examples with the response data:

#### Endpoint
```http
GET http://example.com/api/v1/data/17e5338e-2443-43a1-b382-2c101c12cc03
```
```json
{
    "version": "v0.2",
    "messageFormatVersion": 2,
    "supportedFormats": [
        "JSON",
        "CBOR"
    ],
    "nodes": {
        "electricity_meter": {
            "online": true,
            "implements": [],
            "objects": {
                "L1": {
                    "conforms": null,
                    "objects": {},
                    "attributes": {
                        "voltage": {
                            "constraint": "Measure",
                            "type": "Number",
                            "timestamp": 1.655818756118E12,
                            "value": 232.8
                        },
                        "current": {
                            "constraint": "Measure",
                            "type": "Number",
                            "timestamp": 1.657092653914E12,
                            "value": 5.68
                        }
                    }
                }
            }
        }
    }
}
```
#### Node
```http
GET http://example.com/api/v1/data/17e5338e-2443-43a1-b382-2c101c12cc03/electricity_meter
```
```json
{
	"online": true,
	"implements": [],
	"objects": {
		"L1": {
			"conforms": null,
			"objects": {},
			"attributes": {
				"voltage": {
					"constraint": "Measure",
					"type": "Number",
					"timestamp": 1.655818756118E12,
					"value": 232.8
				},
				"current": {
					"constraint": "Measure",
					"type": "Number",
					"timestamp": 1.657092653914E12,
					"value": 5.68
				}
			}
		}
	}
}    
```
#### Object
```http
GET http://example.com/api/v1/data/17e5338e-2443-43a1-b382-2c101c12cc03/electricity_meter/L1
```
```json
{
	"conforms": null,
	"objects": {},
	"attributes": {
		"voltage": {
			"constraint": "Measure",
			"type": "Number",
			"timestamp": 1.655818756118E12,
			"value": 232.8
		},
		"current": {
			"constraint": "Measure",
			"type": "Number",
			"timestamp": 1.657092653914E12,
			"value": 5.68
		}
	}
}    
```

#### Attribute
```http
GET http://example.com/api/v1/data/17e5338e-2443-43a1-b382-2c101c12cc03/electricity_meter/L1/current
```
```json
{
	"constraint": "Measure",
	"type": "Number",
	"timestamp": 1.657092653914E12,
	"value": 5.68
}
```

## Read history data
History data of the endpoints can be accessed in a **JSON** or **CSV** format using the REST API.

In order to do this, send a request to the REST API:
```http
GET http://**your cloudio hostname**/api/v1/history/**ID of the attribute**
```

!> The history data of only **one** attribute can be requested at a time.

#### JSON
Here is an example of a request followed by the JSON response:
```http
GET http://example.com/api/v1/history/17e5338e-2443-43a1-b382-2c101c12cc03/electricity_meter/L1/current
Headers: {
	Accept: application/json
}
```
```json
[
	{
		"time": "2018-08-20T07:11:51.971Z",
		"value": 5.68
	},
	{
		"time": "2018-08-20T07:11:58.572Z",
		"value": 4.26
	}
]
```
#### CSV
Here is an example of a request followed by the JSON response:
```http
GET http://example.com/api/v1/history/17e5338e-2443-43a1-b382-2c101c12cc03/electricity_meter/L1/current
Headers: {
	Accept: text/csv
}
```
```csv
2018-08-20T07:11:51.971Z;5.68
2018-08-20T07:11:58.572Z;4.26
```
#### Filters
Filters can be added to the requests. They must be passed as **URL parameter**.

|Name|Description|Available values|Default values|
|---|---|---|---|
|from|Optional start date (UTC) in the format 'yyyy-MM-ddTHH:mm:ss'.|-|No start date.|
|to|Optional end date (UTC) in the format 'yyyy-MM-ddTHH:mm:ss'.|-|No end date.|
|resampleInterval|Optional interval to resample data to. The format is a number followed by n, u, ms, s, m, h, d or w.|-|No resampling.|
|resampleFunction|Function used to resample data. Only considered when a resample interval was given too.|COUNT, DISTINCT, INTEGRAL, MEAN, MEDIAN, MODE, SPREAD, STDDEV, SUM, FIRST, LAST, MAX, MIN|MEAN|
|fillValue|Value to use fill resampled intervals with no data. Only considered when a resample interval was given too.|NONE, NULL, ZERO, PREVIOUS, LINEAR|NONE|
|max|Maximal number of entries to return.|-|1000|
|separator|CSV Separator.|-|;|

!> Requesting too many datapoints will lead to a http timeout.

## Write setpoints and parameters

Setpoints and parameters attributes can be written using the REST API. The value is sent in **URL parameter**, always using the key *value*.
```http
PUT http://**your cloudio hostname**/api/v1/history/**ID of the attribute**?value=**the value you want to send**
```

Example:
```http
PUT http://example.com/api/v1/history/17e5338e-2443-43a1-b382-2c101c12cc03/thermostat/room_1/temperature_setpoint?value=22.0
```
