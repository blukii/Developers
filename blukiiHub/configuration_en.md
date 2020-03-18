# blukii Hub Configuration

This documentation describes the configuration options of the blukii hub.

## Call the configuration interface

Currently is no configuration interface available. This will be delivered soon. If you want to configure something, please call 077729/888-4220.

## Configuration

### Server Url
```properties
blukii.data.service.serverUrl=https://192.168.10.21:8087/push
```
Remote server to which the data of the blukiiHub should be sent. By default this value is empty.

### HTTP Method
```properties
blukii.data.service.httpMethod=POST
```
The Http methods which are used to push the data to the remote server. 

Valid values are:
- _POST_
- _PUT_

Default Value is:
- _POST_

### PushOption
```properties
blukii.data.service.pushOption=amount
```
Sets the push trigger.

Valid values are:
- _amount_: Push the data to remote server when the amount of frames is received. When there are many sending beacons around the blukiiHub the preferred option should be _interval_.  
- _interval_: Push the data to remote server when the interval is expired.

Default value is:
- _amount_

```properties
blukii.data.service.amount=1
```
The amount of frames, that will be collected before sending it to the server. In this example, the push server is called after one Frame.
This Value is only valid, if the _pushOption_ is set to _amount_.  

Default value is:
- 1

```properties
blukii.data.service.interval=
```
The interval in milliseconds. This value is only valid, if the _pushOption_ is set to _interval_.

Default value is:
- nil

### Authentification for remote Server
```properties
blukii.data.service.authentication.type=
```
Valid values are:
- [Empty]: For no authentification
- _basic_: HTTP Basic Authentication. Requieres: _username_, _password_ 
- _oauthCC_: OAuth Client Credetials Gant Requieres: _clientId_, _secret_
- _oauthPW_: OAuth User Password Grant: _username_, _password_, _clientId_, _secret_

Default value is:
- [Empty]

```properties
blukii.data.service.authServerUrl=
```


```properties
blukii.data.service.username=
blukii.data.service.password=
```
Username and password to authentificate with _basic_ or _oauthPW_.

```properties
blukii.data.service.clientId=
blukii.data.service.secret=
```
clientId and secret to authentificate with _oauthCC_ or _oauthPW_.

# Filter Frames
Specify which type of data (Frames) will be pushed to the remote server.

```properties
blukii.data.service.filterType.All=true
```
If _All_ is set to true, all Beacon frames will be pushed to the remote server. Values _SensorBeacon_, _eddystone_, _IBeacon_ will be ignored. 

```properties
blukii.data.service.filterType.SensorBeacon=
```
If _SensorBeacon_ is set to true, all Sensor frames will be pushed to the remote server.

```properties
blukii.data.service.filterType.Eddystone=
```
If _Eddystone_ is set to true, all Eddystone frames will be pushed to the remote server.

```properties
blukii.data.service.filterType.IBeacon=
```
If _IBeacon_ is set to true, all iBeacon frames will be pushed to the remote server.