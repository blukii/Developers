Hardware Inputs and Outputs
===========================

Antenna Port
------------

The delivery contains a antenna that has to be mounted on the Antenna port.

It can be replaced with other antennas for special use cases (e.g. directional antenna). Please note, that the antenna model has to be certified for blukii Hub.

USB-C Port
----------

USB-C is primarily used for power supply.

Additionally you can read the system logs via serial port.

Push Button
-----------

The Push button provides two features:

* Short Press (less than 5 seconds): The [Configuration Website](configuration_en.md) can be accessed for a defined amount of seconds (see Configuration Access setting)

* Long Press (more than 5 seconds): The [WLAN Credential settings](networksetup_en.md) are removed and the blukii Hub is restarted. Then the blukii Hub Access Point will be activated.

LED
---

### Red LED

The red LED signals the connection status:

* On: Access Point is active

* Blink fast: Connecting to WLAN

* Blink slow: Connection to WLAN established

* Off: Connected to WLAN

### Green LED

The green LED signals the operation status:

* On: The Hub is started and busy.

* Off: A data push request is currently running.

### Red and Green LED simultaneously

Both LEDs are slowly blinking: The hub is doing software update.
