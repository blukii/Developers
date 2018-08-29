![ ](Bilder/Quick.PNG)

# Quickstart with the blukii Hub

This short guide will show you how to get your blukii Hub up and how to get the data from a sensorBeacon.

## 1. Connect blukii Hub to power sulpply
- Connect the blukii Hub with the supplied power supply unit and ensure the power supply.

## 2. Determine the IP address / host name of the blukii Hub
The blukii Hub is assigned an IP address that is needed to retrieve data.
The IP address can be determined as follows:
- For small networks over the router.
- For large networks you need to contact your network administrator   

## 3. Place blukii sensorBeacon near the blukii Hub
- Place a blukii sensorBeacon near the blukii Hub.
The blukii sensorBeacon now sends readings to the blukii Hub.

## 4. Show blukii sensorBeacon
You can execute the following commands with a standard browser of your choice.
  ```
  http://<hostname>/api/blukii
  ```
 Instead of `<hostname>` enter the IP address / hostname of your blukii Hub. As output you will get a list of all blukiis that send data to the blukii Hub.

  **Output example:**
  ```
  [
    {
        "address": "12ACA0B72EFF",
        "battery": 100
    }
  ]
  ```
  - _address_: blukii_address, uniquely identifies each blukii.

## 5. Choose blukii sensorBeacon
```
http://<hostname>/api/blukii/<blukii_address>
```
Instead of `<hostname>` enter the IP address / hostname of your blukii Hub and instead of `<blukii_address>` the address of the blukii sensorBeacon determined in step 4.

**Output example**
```
last_entries	       1000
blukii	               "2471894DAECA"
firstValue	       1519378905.967
lastValue	       1519893372.801
rssi_default	       […]
unknown_default	       […]
magnet_default	       […]
acceleration_default   […]
environment_default    […]
```
Depending on the hardware variant and configuration of your blukii sensorBeacon you will receive readings of your blukii sensorBeacon Output.


You have successfully completed the initial commissioning. A more detailed explanation and description of all functions can be found here: [API Documentation](doku_api_en.md)
