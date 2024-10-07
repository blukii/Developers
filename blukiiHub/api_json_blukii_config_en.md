blukii Device configuration via Hub JSON
================================

This documentation describes the blukii configuration commands and result feedback in blukii Hub JSON body.

This lets the HTTP server configure blukii Devices via blukii Hub.  

Last modified for version: 3.0.7.8.


## Configuration data via Response body


```java
{
  "blukiis": [
    {
        "mac": "F05ECD25578B",
        "update": "2",
        "key": "11223344AABBCCDD11223344AABBCCDD",
        "timeout": "10",
        "commands": [
            "B0020109C40101140064002C01",
            "B0010104C201BC02"
        ]
    },
    {
        "mac": "F05ECD2567AB",
        "update": "42",
        "key": "55667788AABBCCDD5566778844AABBCCDD",
        "timeout": "60",
        "commands": [
            "B0020109C401020A00C8002003",
            "B0010104C2012C01"
        ]
    }
  ]
}
```

Notes: 
* The described format is valid for JSON API version 1.0 and 2.0.
* The blukii configuration data is only interpreted by the blukii Hub, if the HTTP response code is 200 (HTTP_OK) or 201 (HTTP_ACCEPTED).

This format contains a blukii array with configuration data. 

Fields of a blukii array item

* _mac_: mac address of blukii device

* _update_: Update index for the configuration data. If new configuration data wants to be updated to the blukii device the update index must be changed. Otherwise it will be ignored. Range: 0..255

* _key_: (optional) Secure key of blukii device. This is needed for blukii authentication, if secure connect is enabled on blukii device. Secure Keys are provided by blukii Manager or blukii Support for blukii device owner.

* _timeout_: (optional) Configuration Timeout in seconds. If blukii Hub does not find the blukii device within this timeout period, the configuration will be stopped.<br>Default value: 600s (10 min). Range 1..65535s

* _commands_: array of BLE GATT commands, see coding below.


### Command coding

Note: The commands are derived from the blukii GATT command definition. Detailed information is provided by blukii Support.

**Coding of a command array item**

| Characteristic | Value |
| --- | --- |
| 2 bytes | N bytes |

* _Characteristic_: 2 bytes characteristic UUID. Valid values:
    * B001 .. B01F (blukii Service Characteristic)
    * 2081 .. 208F (Eddystone URL Service Characteristic)

* Value: N bytes value. Value range is defined by the characteristic definition. See blukii GATT commands documentation.


## blukii config result in Hub data JSON
For each blukii configuration item that is sent via blukii Hub to a blukii device, a config result information will be sent back to the server. This is included in the JSON body of a following hub data request.


The coding will be shown for JSON 1.0 and 2.0.

### JSON 1.0

The config result data will be added as node *blukiiState* to the data JSON (see [Version 1.0](api_json_en_1.md)). In this manual only the config result data is explained. 

```java
{
    "id": "hub86C274E0",
    "localIp": "192.168.178.41",
    "items": [
        {
            "macAddress": "F05ECD25578B",
            "blukiiId": "blukii BXXXXX F05ECD25578B",
            "timestamp": 1718028955108,
            "blukiiState": {
                "config": [
                    {
                        "update": 2,
                        "result": 0,
                        "reason": 2,
                        "timestamp": 1718028955108
                    }
                ],
            }
        },
        {
            "macAddress": "F05ECD2567AB",
            "blukiiId": "blukii BXXXXX F05ECD2567AB",
            "timestamp": 1718028957784,
            "blukiiState": {
                "config": [
                    {
                        "update": 42,
                        "result": 3,
                        "reason": 1,
                        "timestamp": 1718028957784
                    }
                ],
            }
        }
    ]
}
```

**Contents of block *blukiiState***:

* _update_: Update index of blukii configuration data item

* _result_: Configuration Result. 
    * 0 (_Succeeded_): All commands successfully executed.
    * 1 (_Unauthorized_): In case of secure connect is enabled, no or no valid secure key has been defined in configuration data.
    * 2 (_Invalid_): One or more configuration data fields are missing or invalid.
    * 3 (_Failed_): The configuration of the blukii device failed. The field *reason* contains more information.
    * 4 (_Timeout_): The timeout, set in configuration data, has been exceeded because the blukii device has been out of reach.
    * 5 (_Internal Error_): Internal Application error

* _reason_: Status info based on _result_ value:
    * _result_=0 (_Succeeded_): Number of successful executed commands
    * _result_=3 (_Failed_):
        * 255: Connection error
        * 0..N: Index of command, that causes an error. 
        * Note: If command index is greater than 0, the first commands has be executed successfully!
    * _else_: Always 0
    
* _timestamp_: UTC timestamp in milliseconds of the blukii device configuration or error.

### JSON 2.0

The config result data will be added to the data JSON (see [Version 2.0](api_json_en_2.md)) as item of the frame data array. In this manual only the config result data is explained. 

```java
{
  "id": "hub86C274E0",
  "localIp": "192.168.178.41",
  "data": [
    "F05ECD25578B64E46D810290010000008001020002",
    "F05ECD2567AB6458788102900100000080012A0301"
  ]
}
```

**Data frame coding**

| MAC | RSSI | Timestamp | Battery | Type | Subtype | Update | Result | Reason
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 6 bytes | 1 byte  | 8 bytes | 1 byte | 1 byte | 1 byte | 1 byte | 1 byte | 1 byte |

* _MAC_: 6 bytes array: MAC address of blukii Beacon 

* _RSSI_: 1 byte: Always 0x64 for config result

* _Timestamp_: 8 bytes (unsigned int64 little endian): Time of device configuration in the form of a Unix timestamp in milliseconds.

* _Battery_: 1 byte: Always 0x00 for config result

* _Type_: 1 byte: Frame Data Type: _0x80_ for blukii result data

* _Subtype_: 1 byte: Frame Data Subtype: _0x01_ for config result data

* _Result_: 1 byte: Configuration Result. 
    * _0x00_ (_Succeeded_): All commands successfully executed.
    * _0x01_ (_Unauthorized_): In case of secure connect is enabled, no or no valid secure key has been defined in configuration data.
    * _0x02_ (_Invalid_): One or more configuration data fields are missing or invalid.
    * _0x03_ (_Failed_): The configuration of the blukii device failed. The field *reason* contains more information.
    * _0x04_ (_Timeout_): The timeout, set in configuration data, has been exceeded because the blukii device has been out of reach.
    * _0x05_ (_Internal Error_): Internal Application error

* _Reason_: 1 byte: Status info based on _result_ value:
    * _result=0x00_ (_Succeeded_): Number of successful executed commands
    * _result=0x03_ (_Failed_):
        * _0xFF_: Connection error
        * else: Index of command, that causes an error. 
        * Note: If command index is greater than 0, the first commands has be executed successfully!
    * _else_: Always 0

The records are sorted in ascending order according to timestamp.
