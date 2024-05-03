blukii Hub JSON API 1.0
================================

In this documentation the JSON API structure 1.0 is described.

Software version: 3.0.5.3.

Push interface overview
--------------

In the example below, the following configuration was used:

* blukii Hub

  * Serial number: hubAEB6DC04

  * IP address in local network: 192.168.178.41

* blukii Smart Beacon

  * blukii\_address: 04EE03DBD02B

  * Frames iBeacon, Eddystone UID, Eddystone TLM, Device Tracing and Special Frame enabled

* blukii Sensor Beacon

  * blukii\_address: CC78AB5E7627

  * all sensor readings are sent

**Output example of the push interface**

```java
{
    "id": "hubAEB6DC04",
    "localIp": "192.168.178.41",
    "items": [
        {
            "macAddress": "04EE03DBD02B",
            "blukiiId": "blukii BXXXXX 04EE03DBD02B",
            "batteryPct": 100,
            "batteryMV": 3363,
            "activeTime": 236,
            "timestamp": 1657898818334,
            "rssi": [
                {
                    "rssi": -57,
                    "timestamp": 1657898818023
                },
                {
                    "rssi": -58,
                    "timestamp": 1657898818650
                },
                {
                    "rssi": -57,
                    "timestamp": 1657898818334
                },
                {
                    "rssi": -57,
                    "timestamp": 1657898818863
                },
                {
                    "rssi": -58,
                    "timestamp": 1657898818955
                }
            ],
            "iBeaconData": [
                {
                    "uuid": "626C756B-6969-2E63-6F6D-626561636F6E",
                    "major": 3,
                    "minor": 1,
                    "measuredPower": -57,
                    "timestamp": 1657898818023
                }
            ],
            "eddystoneTLM": [
                {
                    "batteryMV": 3363,
                    "temperature": 0,
                    "packets": 241,
                    "activeTime": 2360,
                    "timestamp": 1657898818650
                }
            ],
            "eddystoneUID": [
                {
                    "uidNamespace": "626C756B626561636F6E",
                    "uidInstance": "000000030001",
                    "timestamp": 1657898818334
                }
            ],
            "deviceTracing": {
                "id": 13,
                "devices": [
                    {
                        "id": 11,
                        "rssi": -45,
                        "timestamp": 1657898818863
                    },
                    {
                        "id": 10,
                        "rssi": -45,
                        "timestamp": 1657898818863
                    },
                    {
                        "id": 3,
                        "rssi": -59,
                        "timestamp": 1657898818863
                    }
                ]
            },
            "SpecialFrame": [
                {
                "type": 2,
                "timestamp": 1657898818955,
                "data": "0100000000000000010080"
                }
            ]
        },
        {
            "macAddress": "CC78AB5E7627",
            "blukiiId": "blukii BXXXXX CC78AB5E7627",
            "type": "SENSOR_BEACON",
            "batteryPct": 100,
            "advInterval": 400,
            "firmware": "003.011",
            "timestamp": 1657898818128,
            "rssi": [
                {
                    "rssi": -18,
                    "timestamp": 1657898818545
                },
                {
                    "rssi": -18,
                    "timestamp": 1657898817396
                },
                {
                    "rssi": -18,
                    "timestamp": 1657898817813
                },
                {
                    "rssi": -18,
                    "timestamp": 1657898818128
                }
            ],
            "beaconSensorData": {
                "environment": [
                    {
                        "airPressure": 1008.9,
                        "light": 245,
                        "humidity": 49,
                        "temperature": 26.5625,
                        "timestamp": 1657898818545
                    }
                ],
                "magnetism": [
                    {
                        "x": -36,
                        "y": 16,
                        "z": 1212,
                        "timestamp": 1657898817396
                    }
                ],
                "acceleration": [
                    {
                        "x": 1294,
                        "y": 982,
                        "z": -4651,
                        "timestamp": 1657898817813
                    }
                ]
            },
            "iBeaconData": [
                {
                    "uuid": "626C756B-6969-2E63-6F6D-626561636F6E",
                    "major": 3,
                    "minor": 1,
                    "measuredPower": -57,
                    "timestamp": 1657898818128
                }
            ]
        }
    ]
}
```

Basically, a new block is added per blukii from which the Hub receives data. Such a block always consists of:

* _macAddress_: MAC Address of the blukii.

* _rssi_: Returns a list of records with information about the Bluetooth connection.

Depending on the configuration and hardware variant of the blukii, the following parts may be added:

* _beaconSensorData_: Returns a list of data with magnetism, acceleration and/or environment data.

* _iBeaconData_: Returns a list of datasets with the iBeacon Data such as UUID, Major, Minor and measured Power.

* _eddystoneUID_: Returns a list of datasets with uidNamespace and uidInstance.

* _eddystoneTLM_: Returns a list of datasets with the Eddystone TLM data.

* _deviceTracing_: Returns a list of datasets with the Device Tracing data.

* _SpecialFrame_: Returns a list of datasets with the Special Frame data.

Description of nodes and values
--------------

### General

```java
"macAddress": "CC78AB5E7627",
"blukiiId": "blukii BXXXXX CC78AB5E7627",
"type": "SENSOR_BEACON",
"batteryPct": 100,
"batteryMV": 3363,
"activeTime": 236,
"advInterval": 400,
"firmware": "003.011",
"timestamp": 1657898818128,
```

* _macAddress_: Bluetooth MAC address of the current blukii. This field is always available.

* _blukiiId: blukii Id of the current blukii. This field is always available._

* _type_: The type of the blukii Beacon. Valid values: “SENSOR\_BEACON” and “SMART\_BEACON”. If this field is not defined, the type is “SMART\_BEACON”.

* _batteryPct: Battery state of the last received Frame. Value is in \[%\]. This field is only included, when it was received._

* _batteryMV: Battery state of the last received Frame. Value is in milli volts (mV). This field is only included, when it was received._

* _activeTime: Active life time since last startup. Value is in seconds. This field is only included, when it was received._

* _advInterval_: Advertising interval of the Beacon. This field is only included, when it was received.

* _firmware_: Firmware version of the beacon. This field is only included, when it was received.

* _timestamp_: UTC timestamp in milliseconds of the last received frame. This field is always available.

### Rssi

Rssi contains a list of records, in JSON format, with the following content:

```java
"rssi": [
    {
        "rssi": -57,
        "timestamp": 1657898818023
    },
    {
        "rssi": -58,
        "timestamp": 1657898818650
    },
    {
        "rssi": -57,
        "timestamp": 1657898818334
    }
],
```

* _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

* _rssi_: RSSI measured value in \[dBm\].

The records are sorted in ascending order according to timestamp.

### Beacon Sensor Data

```java
"beaconSensorData": [
                      "magnetism": [ ... ],
                      "acceleration": [ ... ],
                      "environment": [ ... ]
]
```

Entries that are available depending on the configuration of the blukiis:

* _magnetism_: Returns a list of data sets with measured values of the magnetic sensor.

* _acceleration_: Returns a list of data records with measured values of the acceleration sensor.

* _environment_: Returns a list of datasets with environmental metrics such as barometric pressure, light, humidity, and temperature.

*Magnetism*

Magnetism contains a list of records, in JSON format, with the following content:

```java
"magnetism": [
            {
              "timestamp": 1657898817396,
              "x": 4035,
              "y": -2220,
              "z": 5621
            },
            {
              "timestamp": 1657898817813,
              "x": 4013,
              "y": -2168,
              "z": 5690
            }
          ]
```

* _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

* _x_: Magnetic flux density through the X-axis of the sensor in \[mGauss\].

* _y_: Magnetic flux density through the Y-axis of the sensor in \[mGauss\].

* _z_: Magnetic flux density through the Z-axis of the sensor in \[mGauss\].

The records are sorted in ascending order according to timestamp.

*Acceleration*

```java
"acceleration": [
                  {
                    "timestamp": 1657898817396,
                    "x": -24,
                    "y": -30,
                    "z": 1167
                  },
                  {
                    "timestamp": 1657898817813,
                    "x": -27,
                    "y": -29,
                    "z": 1172
                  }
                ]
```

* _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

* _x_: acceleration in the X direction in \[mg\].

* _y_: acceleration in the Y direction in \[mg\].

* _z_: acceleration in the Z direction in \[mg\].

The records are sorted in ascending order according to timestamp.

*Environment*

```java
"environment": [
                  {
                    "timestamp": 1657898817396,
                    "airPressure": 938,
                    "light": 40,
                    "humidity": 14,
                    "temperature": 23.1875
                  },
                  {
                    "timestamp": 1657898817813,
                    "airPressure": 938,
                    "light": 40,
                    "humidity": 14,
                    "temperature": 23.1875
                  }
                ]
```

* _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

* _airPressure_: air pressure in \[hPa\].

* _light_: Illuminance in \[lux\].

* _humidity_: Humidity in \[%\].

* _temperature_: temperature in \[°C\].

The records are sorted in ascending order according to timestamp.

### iBeacon Data

```java
"iBeaconData": [
                  {
                    "uuid": "626C756B-6969-2E63-6F6D-626561636F6E",
                    "major": 3,
                    "minor": 5002,
                    "measuredPower": -57,
                    "timestamp": 1657898818023
                  },
                  {
                    "uuid": "626C756B-6969-2E63-6F6D-626561636F6E",
                    "major": 3,
                    "minor": 5002,
                    "measuredPower": -57,
                    "timestamp": 1657898818650
                  }
                ]
```

* _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

* _uuid_: The uuid of the iBeacon frame.

* _major_: Major value of the iBeacon frame.

* _minor_: Minor value of the iBeacon frame.

* _measuredPower_: Measured power value of the iBeacon frame.

The records are sorted in ascending order according to timestamp.

### Eddystone UID

```java
"eddystoneUID": [
                  {
                    "uidNamespace": "F7826DA6BC5B71E0893E",
                    "uidInstance": "7A6C4E51414E",
                    "timestamp": 1657898818334
                  },
                  {
                    "uidNamespace": "F7826DA6BC5B71E0893E",
                    "uidInstance": "7A6C4E51414E",
                    "timestamp": 1657898818650
                  }
                ]
```

* _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

* _uidNamespace_: The 10-byte Namespace ID of the beacon.

* _uidInstance_: The 6-byte Instance ID of the beacon.

The records are sorted in ascending order according to timestamp.

### Eddystone TLM

```java
"eddystoneTLM": [
                  {
                    "batteryMV": 3000,
                    "temperature": 22.5,
                    "packets": 38589588,
                    "activeTime": 40501320,
                    "timestamp": 1584449212283
                  },
                  {
                    "batteryMV": 3000,
                    "temperature": 22.5,
                    "packets": 38589589,
                    "activeTime": 40501320,
                    "timestamp": 1584449212392
                  }
                ]
```

* _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

* _batteryMV_: The current battery voltage in \[mV\].

* _temperature_: The beacon temperature in \[°C\].

* _packets_: Count of advertised frames.

* _activeTime_: Time since powered on or reboot in seconds.

The records are sorted in ascending order according to timestamp.

### Device Tracing

```java
"deviceTracing": {
    "id": 13,
    "devices": [
        {
            "id": 11,
            "rssi": -45,
            "timestamp": 1657898818863
        },
        {
            "id": 10,
            "rssi": -45,
            "timestamp": 1657898818863
        },
        {
            "id": 3,
            "rssi": -59,
            "timestamp": 1657898818863
        }
    ]
}
```

* _id_: Device tracing id of the current blukii (inherited from iBeacon minor value).

* _devices_: List of other devices, that was received by blukii scan.

* _devices.id: Device tracing id of the received blukii (inherited from iBeacon minor value)._

* _devices.rssi:_ RSSI measured value in \[dBm\] of the received blukii (inherited from iBeacon minor value).

* _devices.timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

The records are sorted in ascending order according to timestamp.


### Special Frame

```java
"SpecialFrame": [
    {
        "type": 2,
        "timestamp": 1714730342847,
        "data": "0100000000000000010080"
    },
    {
        "type": 2,
        "timestamp": 1714730343460,
        "data": "0100000000000000010080"
    },
    {
        "type": 2,
        "timestamp": 1714730344066,
        "data": "0100000000000000010080"
    }
]
```

* _type_: Special Frame type index.

* _data_: Byte record of frame content.

* _timestamp_: Time of data acquisition in the form of a Unix timestamp in milliseconds.

The records are sorted in ascending order according to timestamp.
