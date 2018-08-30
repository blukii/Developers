# blukii Hub Configuration

In dieser Dokumentation werden die Konfigurationsmöglichkeiten des blukii Hubs beschrieben.

##Aufruf der Konfigurationsoberfläche
Die Konfigurationsoberfläche wird über folgende URL aufgerufen:
```
http://<hostname>/conf
```
**Beispiel:**
```
http://192.168.178.20/conf
```
Auf der Loginseite kann sich mit dem Benutzer "admin" und dem Passwort "admin" angemeldet werden.

##Konfiguration
Die Konfiguration ist in drei sections aufgeteilt:
- blukiiHub Configuration: Hier sind alle Konfigurationsparameter für den blukiiHub zu setzten
- Log-Files: Hier können die Logfiles für Supportzwecke heruntergeladen werden
- Change Password: Hier kann das Passwort des Benutzers admin geändert werden.

### blukiiHub Configuration
Im Formularfeld werden die Parameter im INI Format dargestellt. Hier kann wie folgt konfiguriert werden:

#### Section blukiiHub
In dieser Section sind die Parameter für den blukiiHub Collector.
```
push_server = http://localhost/api/
```
Server, an den die Daten des blukiiHub Collectors gesendet werden sollen. Default ist der interne blukiiHub Server.

```
put_interval = 60
```
Interval in Sekunden, indem die Daten an push_server gesendet werden.

```
transaction_interval = 1
```
Interval in Sekunden in dem die Daten vom Scan Services in die interne Datenbank geschrieben werden.

```
log_level = 0
```
Loglevel für den blukiiHub Collector.
Loglevels:
- 0 = Critical
- 1 = Warning
- 2 = Info
- 3 = Debug

#### Section blukiiServer
In dieser Section sind die Parameter für den blukiiHub Server.
```
buffer_time = 1440
```
Zeit in Minuten, in der auf dem Server die Daten vorgehalten werden. Alles was älter als x Minuten ist, wird aus der DB gelöscht.

```
log_level = 0
```
Loglevel für den blukiiHub Server.
Loglevels:
- 0 = Critical
- 1 = Warning
- 2 = Info
- 3 = Debug

#### Section blukiiSystem
In dieser Section sind die System Parameter für den blukiiHub.

```
hostname = blukiiHub
```
Der Name des blukiiHubs. Mit diesem Namen ist der blukiiHub im Netzwerk sichtbar.

```
dhcp = True
```
Aktivieren/Deaktivieren des DHCP-Clients. Wert muss vorhanden sein.

```
ip = 192.168.178.10
```
IP Adresse des blukiiHub.

```
gateway = 192.168.178.1
```
Das Default Gateway für den blukiiHub.

```
dns_server = 192.168.178.1
```
DNS Server des blukiiHubs. Mehrere Können via komma getrennt eingetragen werden. 

```
ssh = False
```
Aktivieren/Deaktivieren von SSH. Nur für den Support!

```
ntp =
```
Angabe eine eigenen NTP Servers für die Zeitsynchronistation.
