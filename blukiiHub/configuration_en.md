# blukii Hub Configuration

This documentation describes the configuration options of the blukii hub.

## Call the configuration interface
The configuration interface is called via the following URL:
```
http://<hostname>/conf
```
**Example:**
```
http://192.168.178.20/conf
```
On the login page you can log in with the user "admin" and the password "schneider".

## Configuration
The configuration is divided into three sections:
- blukiiHub Configuration: Here are all configuration parameters for the blukiiHub set
- Log-Files: Here you can download the logfiles for support purposes
- Change Password: Here the password of the user admin can be changed.

### blukiiHub Configuration
The form field displays the parameters in INI format. Here can be configured as follows:

#### Section blukiiHub
In this section are the parameters for the blukiiHub Collector.
```
push_server = http://localhost/api/
```
Server to which the data of the blukiiHub Collector should be sent. Default is the internal blukiiHub server.

```
put_interval = 60
```
Interval in seconds by sending the data to push_server.

```
transaction_interval = 1
```
Interval in seconds in which the data is written by the Scan Services into the internal database.

```
log_level = 0
```
Loglevel for the blukiiHub Collector.
Loglevels:
- 0 = Critical
- 1 = Warning
- 2 = Info
- 3 = Debug

Attention: Please use Loglevel higher than 0 only for a short period of time. Ohterwise there is the risk of the memory card filling up what leads to the system not working any more.

#### Section blukiiServer
In this section are the parameters for the blukiiHub server.
```
buffer_time = 1440
```
Time in minutes in which data is kept on the server. Anything older than x minutes will be deleted from the DB.

```
log_level = 0
```
Loglevel for the blukiiHub Server.
Loglevels:
- 0 = Critical
- 1 = Warning
- 2 = Info
- 3 = Debug

Attention: Please use Loglevel higher than 0 only for a short period of time. Ohterwise there is the risk of the memory card filling up what leads to the system not working any more.

#### Section blukiiSystem
In this section are the system parameters for the blukiiHub.

```
hostname = blukiiHub
```
The name of the blukiiHub. With this name, the blukiiHub is visible in the network.

```
dhcp = True
```
Enable / disable the DHCP client. Value must be present.

```
ip = 192.168.178.10
```
IP address of the blukiiHub.

```
gateway = 192.168.178.1
```
The default gateway for the blukiiHub.

```
dns_server = 192.168.178.1
```
DNS server of the blukiiHubs. Several servers can be entered separately via comma.


```
ntp =
```
Specify your own NTP server for the time synchronization station.
