# QuickStart guide blukii Hub

This short guide will show you how to get your blukii Hub up and how to get the data from a blukii Sensor Beacon or a blukii Smart Beacon.

## 1. Connect blukii Hub to power supply
- Connect the blukii Hub with an Ethernet cable to a Router or a Switch with an DHCP Server in the network. 
- Connect the blukii Hub with the supplied power supply unit and ensure the power supply. As soon as the status LED is constantly green, the hub is up and running. 

## 2. Place blukii Beacon near the blukii Hub
Place a blukii Beacon near the blukii Hub.
The blukii Beacon now sends readings to the blukii Hub.

## 3. Configure Remote Server

Download [Link](https://apps.blukii.com/hub/blukiiAdminPanel_Setup_1.0.0.exe) and install the Admin Panel 

Login with your User and ClientID. The Client ID is only one time valid. 

How to get a User and ClientID?
- Login with User and Password given with the Product
 - or - 
- Reqest User and Login at the support account (add the hub ID(s) to the message)
 - or - 
- If user already exists request for hub assignment

open Hub and add a Configuration. Detailed Configuration Parameter are explained here: [blukii Hub Configuration](configuration_en.md) 

## 4. Get Data
The blukii Hub will send periodically data to the configured server. A detailed explanation and description of all functions can be found here: [API Push Interface](doku_api_en.md)