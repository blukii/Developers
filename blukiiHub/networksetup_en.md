# Initial blukii Hub Network Setup

Two steps are initially needed to configure the blukii Hub.

## Connect to blukii Hub access point

blukii Hub sends a WLAN Access Point, if there are no WLAN Credentials configured.

- WLAN Access Point Network Name: blukii Hub Serial Number (e.g. “hubabcd0123”)
- WLAN password: “blukiihub”

If the WLAN Access Point is active the red LED is continuously on.

## Configure WLAN Credentials

If connected to the WLAN Access Point you can access the blukii Hub Configuration Website via <http://192.168.4.1/>.

![Alt text](images/config_wlan.png)

Insert your WLAN credentials and save it.

The blukii Hub restarts after 3 seconds and tries to connect to your WLAN.

During connecting the red LED is blinking fast. If the connection has been established, the LED is blinking slowly for 10 seconds. Finally the red LED keeps off as long the WLAN connection is stable.

Now you can access the [Configuration Website](configuration_en.md) after connecting to the same WLAN as the blukii Hub.

## Connection problems

If the red LED is blinking for more than a few seconds, the blukii Hub cannot establish the connection to the target network. The WLAN credentials might be wrong.

You can reset the WLAN credentials by holding the button pressed until the red LED is continuously on.

Now the WLAN Aaccess Point is activated and you can repeat the WLAN configuration again.
