blukii Hub JSON API 2.0
================================

In this documentation the JSON API structure 2.0 is described.

Last modified for version: 3.0.5.3.

Push interface overview
--------------

**Output example of the push interface**

```java
{
  "id": "hub86C274E0",
  "localIp": "192.168.178.41",
  "data": [
    "F05ECD2555ACBB9155263E8F0100006401626C756B69692E636F6D626561636F6E00010001C7",
    "665544332211ADC455263E8F0100006420020100000000000000010080",
    "F05ECD2555ACB8CA56263E8F0100006402CE626C756B626561636F6E000000010001",
    "665544332211ABF856263E8F0100006420020100000000000000010080",
    "F05ECD2555ACB9F257263E8F0100006402CE626C756B626561636F6E000000010001",
    "665544332211AB2558263E8F0100006420020100000000000000010080",
    "F05ECD2555ACB95959263E8F01000064040CEC000000003F510000C06C"
  ]
}
```

This format contains the raw byte data of each received data frame.

* _id_: hub ID

* _localIp: IP address in local network

* _data_: array of received data frames (raw bytes), see coding below



Data frame coding
--------------

### Common Frame Part

| MAC | RSSI | Timestamp | Battery | Type | Content |
| --- | --- | --- | --- | --- | --- |
| 6 bytes | 1 byte  | 8 bytes | 1 byte | 1 byte | N bytes |

* _MAC_: 6 bytes array: MAC address of blukii Beacon 

* _RSSI_: 1 signed byte: RSSI measured value in \[dBm\].

* _Timestamp_: 8 bytes (unsigned int64 little endian): Time of data acquisition in the form of a Unix timestamp in milliseconds.

* _Battery_: 1 byte (unsigned int8): Battery percentage.

* _Type_: 1 byte (unsigned int8): Frame Data Type
    * _0x01_: iBeacon
    * _0x02_: Eddystone UID
    * _0x04_: Eddystone TLM
    * _0x10_: Device Tracing
    * _0x20_: Special

* _Content_: Array of N bytes: lenght and data depends on the Frame Data Type, see sections below

The records are sorted in ascending order according to timestamp.

### iBeacon Content

_Frame Data Type_: 0x01

_Content Length_: 21 Bytes


| UUID | Major | Minor | Measured Power |
| --- | --- | --- | --- |
| 16 bytes | 2 bytes | 2 bytes | 1 byte |

* _UUID_: 16 bytes array: iBeacon UUID

* _Major_: 2 bytes (unsigned int16 big endian): iBeacon Major

* _Minor_: 2 bytes (unsigned int16 big endian): iBeacon Minor

* _Measured Power_: 1 signed byte: iBeacon Measured Power in \[dBm\].


### Eddystone UID Content

_Frame Data Type_: 0x02

_Content Length_: 17 Bytes


| TxPower | Namespace | Instance |
| --- | --- | --- |
| 1 byte | 10 bytes | 6 bytes |

* _TxPower_: 1 signed byte: Eddystone TxPower value in \[dBm\].

* _Namespace_: 10 bytes array: Eddystone UID Namespace

* _Instance_: 6 bytes array: Eddystone UID Instance


### Eddystone TLM Content

_Frame Data Type_: 0x04

_Content Length_: 12 Bytes


| Battery | Temperature | Packets | Active Time |
| --- | --- | --- | --- |
| 2 bytes | 2 bytes | 4 bytes | 4 bytes |

* _Battery_: 2 bytes (unsigned int16 big endian): Battery capacity in millivolts

* _Temperature_: 2 bytes float as 8.8 fix-point number (-127..128):
    * Byte 0: Integer part
    * Byte 1: Decimal part: (x/256)
    * Value 0x8000: no temperature sensor available

* _Packets_: 4 bytes (unsigned int16 big endian): Number of Data Frames the Beacon has sent since startup

* _Active Time_: 4 bytes (unsigned int16 big endian): Time since startup in 0.1 seconds resolution


### Device Tracing Content

_Frame Data Type_: 0x10

_Content Length_: 22 Bytes


| Device Id | Tracing Set | Frame Index | Found Devices
| --- | --- | --- | --- |
| 2 bytes | 1 byte | 1 byte | 16 bytes


* _Device Id_: 2 bytes (unsigned int16 big endian): Device tracing id of the current blukii (inherited from iBeacon minor value).

* _Tracing Set_: 1 byte (unsigned int8): Device Tracing Set index that is increased after each scan period.

* _Frame Index_: 1 byte (unsigned int8): Frame index as part of one Tracing Set.

* _Found Devices_: List of up to 6 other devices that were scanned in last scan period, see coding below.

#### Device Tracing Found Devices Content

| Id 0 | RSSI 0 | Id 1 | RSSI 1 | ... | Id 5 | RSSI 5 |
| --- | --- | --- | --- | --- | --- | --- |
| 2 bytes | 1 byte | 2 bytes | 1 byte | ... | 2 bytes | 1 byte |

* _Id n_: 2 bytes (unsigned int16 big endian): Device tracing id of the found blukii (inherited from iBeacon minor value).
    * 0xFFFF: less than n+1 device tracing blukiis found

* _RSSI n_: 1 signed byte: RSSI measured value in \[dBm\]. of the found blukii (inherited from iBeacon minor value).
    * 0x80: less than n+1 device tracing blukiis found

The Found Devices are sorted according to RSSI value with highest value first.


### Special Frame Content

_Frame Data Type_: 0x20

_Content Length_: special content defined


| Special Type | Special Content
| --- | --- |
| 1 byte | N bytes

* _Special Type_: 1 byte (unsigned int8): Special Frame Data Type

* _Content_: Array of N bytes: lenght and data depends on the Special Frame Data Type
