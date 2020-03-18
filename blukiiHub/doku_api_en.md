# Customer documenetation blukii Hub
In this documentation the api  functions of the blukii hub are described.

## Push interface

The blukii hub received data of all blukiis and sends it to your configured server.
You must ensure that your server correctly interprets and processes the data from the blukii Hub.
The data is sent from the blukii hub via a HTTP POST or HTTP PUT interface in JSON format.
The following is a structure of a JSON record. The structure of a data record depends on the hardware variant and the configuration of the blukii sensorBeacon or smartBeacon. In the example below, the following configuration was used:
- blukii Hub
  - Serial number: SMAA9ET9WL
- blukii smartBeacon
  - blukii_address: CC78AB6FFEBF
  - Frames iBeacon, EddystoneUID, EddystoneURL and EddystoneTLM enabled 
- blukii sensorBeacon
  - blukii_address: CC78AB6FD698
  - all sensor readings are sent

**Output example of the push interface**
```
{
    "id": "SMAA9ET9WL",
    "data": [
        {
            "blukiiId": "CC78AB6FFEBF",
            "macAddress": "CC78AB6FFEBF",
            "rssi": [
                {
                    "rssi": -55,
                    "timestamp": 1584449211921
                },
                {
                    "rssi": -54,
                    "timestamp": 1584449212522
                },
                {
                    "rssi": -55,
                    "timestamp": 1584449212829
                },
                {
                    "rssi": -56,
                    "timestamp": 1584449212929
                }
            ],
            "iBeaconData": [
                {
                    "uuid": "626C756B-6969-2E63-6F6D-626561636F6E",
                    "major": 3,
                    "minor": 3124,
                    "measuredPower": -57,
                    "timestamp": 1584449211921
                }
            ],
            "eddystoneUID": [
                {
                    "uidNamespace": "626C756B626561636F6E",
                    "uidInstance": "00000003000A",
                    "timestamp": 1584449212522
                }
            ],
            "eddystoneTLM": [
                {
                    "battery": 3000,
                    "temperature": 0,
                    "packets": 38591923,
                    "activeTime": 40524260,
                    "timestamp": 1584449212829
                }
            ],
            "eddystoneURL": [
                {
                    "url": "https://myin.fo/Iuaf8",
                    "timestamp": 1584449212929
                }
            ]
        },
        {
            "blukiiId": "CC78AB6FD698",
            "macAddress": "CC78AB6FD698",
            "type": "SENSOR_BEACON",
            "battery": 94,
            "advInterval": 100,
            "firmware": "003.007",
            "rssi": [
                {
                    "rssi": -59,
                    "timestamp": 1584449212158
                },
                {
                    "rssi": -62,
                    "timestamp": 1584449212470
                },
                {
                    "rssi": -58,
                    "timestamp": 1584449212088
                }
            ],
            "beaconSensorData": {
                "acceleration": [
                    {
                        "x": 551,
                        "y": 988,
                        "z": 457,
                        "timestamp": 1584449212158
                    }
                ],
                "magnetism": [
                    {
                        "x": 1388,
                        "y": -3539,
                        "z": 321,
                        "timestamp": 1584449212470
                    }
                ],
                "environment": [
                    {
                        "airPressure": 954.7,
                        "light": 0,
                        "humidity": 32,
                        "temperature": 21.234375,
                        "timestamp": 1584449212088
                    }
                ]
            }
        }
    ]
}
```
Basically, a new block is added per Beacon from which the Hub receives data.
Such a block always consists of:
- _macAddress_: MAC Address of the blukii.
- _rssi_: Returns a list of records with information about the Bluetooth connection.

Depending on the configuration and hardware variant of the Beacon, the following parts may be added:
- _beaconSensorData_: Returns a list of data with magnetism, acceleration and/or environment data. 
- _iBeaconData_: Returns a list of datasets with th iBeacon Data such as UUID, Major, Minor and measuredPower.
- _eddystoneUID_: Returns a list of datasets with uidNamespace and uidInstance.
- _eddystoneURL_: Returns a list of urls.
- _eddystoneTLM_: Returns a list of datasets with the Eddysteon TLM data.

### Detailed description of the values

#### General
```
"blukiiId": "CC78AB6FD698"
"macAddress": "CC78AB6FD698",
"type": "SENSOR_BEACON",
"battery": 94,
"advInterval": 100,
"firmware": "003.007",
```

- _blukiiId_: blukii Id of the current blukii. This field is always available.
- _macAddress_: Bluetooth MAC address of the current blukii. This field is always available.
- _type_: The type of the blukii Beacon. Valid values: "SENSOR_BEACON", "SMART_BEACON", "UNKNOWN", "SMART_KEY". This Field is only included, when it was received.
- _battery_: Battery state of the last received Frame. Value is in [%]. This Field is only included, when it was received.
- _advInterval_: Advertising interval of the Beacon. This Field is only included, when it was received.
- _firmware_: Firmware version of the beacon. This Field is only included, when it was received.

#### Rssi
Rssi contains a list of records, in JSON format, with the following content:
```
"rssi": [
          {
            "rssi": -55,
            "timestamp": 1584449211921
          },
          {
            "rssi": -57,
            "timestamp": 1584449212829
          }
        ]
```
- _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.
- _rssi_: RSSI measured value in [dBm].

The records are sorted in ascending order according to timestamp.

#### Beacon Sensor Data
```
"beaconSensorData": [
                      "magnetism": [ ... ],
                      "acceleration": [ ... ],
                      "environment": [ ... ]
]
```

Entries that are available  depending on the configuration of the blukiis: 
- _magnetism_: Returns a list of data sets with measured values of the magnetic sensor.
- _acceleration_: Returns a list of data records with measured values of the acceleration sensor.
- _environment_: Returns a list of datasets with environmental metrics such as barometric pressure, light, humidity, and temperature.

##### Magnetism
Magnetism contains a list of records, in JSON format, with the following content:
```
"magnetism": [
            {
              "timestamp": 1519734268623,
              "x": 4035,
              "y": -2220,
              "z": 5621
            },
            {
              "timestamp": 1519734266497,
              "x": 4013,
              "y": -2168,
              "z": 5690
            }
          ]
```
- _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.
- _x_: Magnetic flux density through the X-axis of the sensor in [mGauss].
- _y_: Magnetic flux density through the Y-axis of the sensor in [mGauss].
- _z_: Magnetic flux density through the Z-axis of the sensor in [mGauss].

The records are sorted in ascending order according to timestamp.

##### Acceleration
```
"acceleration": [
                  {
                    "timestamp": 1519734269152,
                    "x": -24,
                    "y": -30,
                    "z": 1167
                  },
                  {
                    "timestamp": 1519734268602,
                    "x": -27,
                    "y": -29,
                    "z": 1172
                  }
                ]
```
- _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.
- _x_: acceleration in the X direction in [mg].
- _y_: acceleration in the Y direction in [mg].
- _z_: acceleration in the Z direction in [mg].

The records are sorted in ascending order according to timestamp.

##### Environment
```
"environment": [
                  {
                    "timestamp": 1519734268362,
                    "pressure": 938,
                    "light": 40,
                    "humidity": 14,
                    "temperature": 23.1875
                  },
                  {
                    "timestamp": 1519734267939,
                    "pressure": 938,
                    "light": 40,
                    "humidity": 14,
                    "temperature": 23.1875
                  }
                ]
```

- _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.
- _pressure_: air pressure in [hPa].
- _light_: Illuminance in [lux].
- _humidity_: Humidity in [%].
- _temperature_: temperature in [°C].

The records are sorted in ascending order according to timestamp.

#### iBeacon Data
```
"iBeaconData": [
                  {
                    "uuid": "626C756B-6969-2E63-6F6D-626561636F6E",
                    "major": 3,
                    "minor": 5002,
                    "measuredPower": -57,
                    "timestamp": 1584449212186
                  },
                  {
                    "uuid": "626C756B-6969-2E63-6F6D-626561636F6E",
                    "major": 3,
                    "minor": 5002,
                    "measuredPower": -57,
                    "timestamp": 1584449213186
                  }
                ]
```

- _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.
- _uuid_: The uuid of the iBeacon frame.
- _major_: Major value of the iBeacon frame.
- _minor_: Minor value of the iBeacon frame. 
- _measuredPower_: Measured power value of the iBeacon frame.

The records are sorted in ascending order according to timestamp.

#### Eddystone UID
```
"eddystoneUID": [
                  {
                    "uidNamespace": "F7826DA6BC5B71E0893E",
                    "uidInstance": "7A6C4E51414E",
                    "timestamp": 1584449212635
                  },
                  {
                    "uidNamespace": "F7826DA6BC5B71E0893E",
                    "uidInstance": "7A6C4E51414E",
                    "timestamp": 1584449213635
                  }
                ]
```

- _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.
- _uidNamespace_: The 10-byte Namespace ID of the beacon.
- _uidInstance_: The 6-byte Instance ID of the beacon.

The records are sorted in ascending order according to timestamp.

#### Eddystone URL
```
"eddystoneURL": [
                  {
                    "url": "https://myin.fo/hgKfM",
                    "timestamp": 1584449212896
                  },
                  {
                    "url": "https://myin.fo/hgKfM",
                    "timestamp": 1584449213896
                  }
                ]
```

- _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.
- _url_: The eddystone URL of the beacon.

The records are sorted in ascending order according to timestamp.

#### Eddystone TLM
```
"eddystoneTLM": [
                  {
                    "battery": 3000,
                    "temperature": 22.5,
                    "packets": 38589588,
                    "activeTime": 40501320,
                    "timestamp": 1584449212283
                  },
                  {
                    "battery": 3000,
                    "temperature": 22.5,
                    "packets": 38589589,
                    "activeTime": 40501320,
                    "timestamp": 1584449212392
                  }
                ]
```
- _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.
- _battery_: The current battery voltage in [mV].
- _temperature_: The beacon temperature in [°C].
- _packets_: Count of advertised frames.
- _activeTime_: Time since powered on or reboot in seconds.

The records are sorted in ascending order according to timestamp.

