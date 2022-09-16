# UUID - friendlyName

## Get friendlyName from UUID

Endpoints **friendlyName** and metadata can be found using the REST API.

```http
GET http://**your cloudio hostname**/api/v1/endpoints/**the UUID**
```
```json
{
	"uuid": "a70011f3-1ba6-4ccd-8596-0f555196560c",
	"friendlyName": "myAwesomeEndpoint",
	"banned": false,
	"online": false,
	"metaData": {
		"location": "Sion"
	},
	"version": "v0.2",
	"messageFormatVersion": 2,
	"supportedFormats": [
		"JSON",
		"CBOR"
	],
	"groupMemberships": [
		"group_a"
	]
}
```

## Get UUID from friendlyName

UUID can be found from a **friendlyName**, using the REST API.

```http
GET http://**your cloudio hostname**/api/v1/endpoints?friendlyName=**the friendly name**
```
```json
[
	{
		"uuid": "a70011f3-1ba6-4ccd-8596-0f555196560c",
		"friendlyName": "myAwesomeEndpoint",
		"banned": false,
		"online": true,
		"permission": "OWN"
	}
]
```
!> As the friendlyNames are not unique, you could have multiple endpoints as result.