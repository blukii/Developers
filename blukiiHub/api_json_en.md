blukii Hub JSON API
================================

In this documentation the JSON API structure and its variants is described.

Push interface overview
--------------

The blukii Hub receives data of all blukii Smart Beacons and sends it to your configured server. You must ensure that your server correctly interprets and processes the data from the blukii Hub. The data is sent from the blukii Hub via a HTTP POST or HTTP PUT interface in JSON format. The following is a structure of a JSON record. The structure of a data record depends on the hardware variant and the configuration of the blukii Sensor Beacon or blukii Smart Beacon. 


There are two formats that can be chosen by [Data Transfer Configuration](configuration_en.md#data-transfer):

* [Version 1.0](api_json_en_1.md): Default format with parsed values

* [Version 2.0](api_json_en_2.md): Optimized format for saving data with byte coded records (since version 3.0.5.3)


