# Websocket

The STOMP/Websocket protocol can be used to subscribe to update, set, didset and log messages.

#### Examples

A python STOMP/Websocket client code:
```python
import websocket
import time
from threading import Thread
from wstompy.connection import WebSocketStompClient

websocket.enableTrace(True)

host = '192.168.37.130'
url = f'ws://{host}:8080/api/v1/events'
client = WebSocketStompClient(
    header_host=host,
    socket_url=url,
    custom_headers={'Authorization': 'Basic YWRtaW46RU1DMWVJalloQ3RvYW9zdw=='},
    subprotocols=['v12.stomp']
)
Thread(target=client.run_forever).start()
while not client.stomp_is_connected:
    time.sleep(0.1)
client.subscribe(id='1234', destination='/update/afa305a7-a4b0-4830-81f5-82572d4a2377/myNode/myObject/myMeasure')
client.subscribe(id='1234', destination='/set/afa305a7-a4b0-4830-81f5-82572d4a2377/myNode/myObject/mySetPoint')
client.subscribe(id='1234', destination='/didSet/afa305a7-a4b0-4830-81f5-82572d4a2377/myNode/myObject/mySetPoint')
client.subscribe(id='12345', destination='/log/afa305a7-a4b0-4830-81f5-82572d4a2377')

while True:
    time.sleep(1)
```

A javascript STOMP/Websocket client code:

``` js
var url = "ws://192.168.37.130:8080/api/v1/events";
var stompClient = Stomp.client(url);
stompClient.connect({Authorization: 'Basic YWRtaW46RU1DMWVJalloQ3RvYW9zdw=='}, function (frame) {
	console.log('Connected: ' + frame);
	stompClient.subscribe('/update/8aecad7e-2e69-4d0b-a656-a88395dbc2cf/myNode/myObject/myMeasure', function (message) {
		console.log(JSON.parse(message.body).value)
	});
});
```