
# Quickstart with the blukii Hub

This short guide will show you how to get your blukii Hub up and how to get the data from a Sensor Beacon.

## 1. Connect blukii Hub to power sulpply
- Connect the blukii Hub with the supplied power supply unit and ensure the power supply.

Attention: Before the startup (exception: not when power supply cable is attached for the first time) or shutdown of the blukii Hub it is important to press the little button on the side of the hub.
- On startup after pressing the button please wait until the led is constantly on. Then the hub is up and running.
- On shutdown ater pressing the button the led will blink 3 times and is constantly on again. As soon as shutdown ist reached led will be switched off.


## 2. Determine the IP address / host name of the blukii Hub
The blukii Hub is assigned an IP address that is needed to retrieve data.
The IP address can be determined as follows:
- For small networks over the router.
- For large networks you need to contact your network administrator   

## 3. Place blukii Sensor Beacon near the blukii Hub
- Place a blukii Sensor Beacon near the blukii Hub.
The blukii Sensor Beacon now sends readings to the blukii Hub.

## 4. Show blukii Sensor Beacon
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

## 5. Choose blukii Sensor Beacon
```
http://<hostname>/api/blukii/<blukii_address>
```
Instead of `<hostname>` enter the IP address / hostname of your blukii Hub and instead of `<blukii_address>` the address of the blukii Sensor Beacon determined in step 4.

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
Depending on the hardware variant and configuration of your blukii Sensor Beacon you will receive readings of your blukii Sensor Beacon Output.


You have successfully completed the initial commissioning. A more detailed explanation and description of all functions can be found here: [API Documentation](doku_api_en.md)

The configuration file of the blukii Hub with a detailed explanation for the different parameters can be found here: [blukii Hub Configuration File](configuration_en.md) 
