## Verwalten der Konfiguration und boot parameters
### Backup and Restore
Prüfen der vorhandenen Backups
```
display backups
sh dir /code/bkups
backup-config "filname" running
```
Wiederherstellen eines Backups
```
restore-backup "filename"
```
Danach mit `show conf` prüfen das die configuration im editing RAM geladen ist. Wenn das erfolgreich war kann mit `save-config` die Konfiguration in das file `DataDoc.gz` geschrieben werden. Abschließend die Konfiguration mit `activate-config` aktivieren.

### Kontrollieren der Bootparameter
- In den Konfigurationsmodung wechseln. `conf t`
- `bootparam` eintippen
- Mit `Enter` kann jeder einzelene Bootparameter durchgegangen werden und ggf. angepasst werden. 
- `Target Name` ändert den Prompt

### Reboot SBC
Der SBC kann mit den folgenden befehlen rebootet werden.
```
reboot
reboot force
reboot activate
```

## Start von scratch
- Prüfen ob konfiguration vorhanden ist
```
display-current-config
display-running-config
show run conf
```
- In den Konfigurationsmodus wechseln und in die `system` branch und das Element `system-config` auswählen
- Mit `show` prüfen das kein Objekt ausgewählt ist
- Danach die folgenden Parameter wie gewünscht anpassen
```
hostname Training
description "Any SBC"
location "Germany, Cologne"
mib-system-contact "Jan"
mib-system-name "Training SBC"
mib-system-location "Germany, Cologne"
default-gateway "YOUR-IP-Gateway"
telnet-timeout 3600
console-timeout 3600
```
Sobald alle gewünschten Parameter konfiguriert sind, muss mit `done` das Objekt quitiert werden.
- Danach mit `quit` in den Konfigurationsmodus verlassen und `save-config` & `activate-config `die Konfiguration speichern und aktivieren.
## Bereitstellen der Interfaces
### Physikalische Interfaces
- Wechseln in das Konfigurationsmenü `conf t
- Danach in das Element `system >> phy-interfaces` wechseln
- Folgende erstes Objekt(interface) konfiguieren
```
name MOO
slot 0
port 0
operation-type Media
```
- Danach mit `done` commiten und somit das Objekt deselecten. 
- Zweites Objekt(interface) konfigurieren
```
name M10
slot 1
port 0
operation-type Media
```
- Wieder mit `done` das Objekt commiten
- Zum Verifizieren kann nun mit `select` geprüft werden, ob beide Objekte angelegt wurden
### Bereitstellen der Network interfaces
Netzwerk interface werden on-top der physikalischen Interface konfiguriert. Hier werden sozusagen L2 & L3 Schicht konfiguiert.
- Konfiguration wird unter `system >> network-interfaces` vorgenommen.
```
name M00 -> Selber Name wie phy-Interfaces, Achtung diese werden somit verknüpft
sub-port-id 0 -> VLAN
ip-address 10.0.6.11
netmask 255.255.255.0
gateway 10.0.6.1
```
- Abschließend mit `done` das Objekt erstellen und deselecten
- Zweites Network-Interface erstellen
```
name M10 -> Selber Name wie phy-Interfaces, Achtung diese werden somit verknüpft
sub-port-id 0 -> VLAN
ip-address 10.0.5.11
netmask 255.255.255.0
gateway 10.0.5.1
```
## SBC Concepts
### Konfiguration der Core und Peer Realm
- Im Konfigurationsmodus in `media-manager >> realm-config` wechseln
- Peer Realm erstellen
```
identifier peer1
network-interface M00:0
addr-prefix 0.0.0.0 -> erlaubte IP-Adressen
```
- Mit `done` abschließen
Core Realm erstellen
```
identifier core1
network-interface M10:0
addr-prefix 0.0.0.0 -> erlaubte IP-Adressen
```
- Mit `done` abschließen
- Abschließend mit `select` prüfen das die beiden Objekte erstellt wurden
## SIP Interfaces
### Globales SIP-Element Konfigurieren
- Im Konfigurationsmenü zu `session-router >> sip-config` wechseln.
- Danach das SIP-Protokoll für den SBC aktivieren.
```
state enabled
dialog-transparency disabled -> Generiert eine neue Call-ID
```
### Konfigurieren der SIP-Interfaces für Peer & Core
- Im Konfigurationsmenü zu `session-router >> sip-interface` wechseln
- SIP-Interface peer erstellen
```
realm-id peer1
```
Danach in das Sub-Element `sip-ports` wechseln
```
address 10.0.5.11
```
- Abschließend mit `done - exit - done -exit` das neue SIP-Interface speichern
- Die Steps müssen für das Core-Interface wiederholt werden und die IP-Adresse entsprechend angepasst  werden
##  Konfigurieren Media Services
### Konfigurieren MediaManager
- Im Konfigurationsmenü zu `media-manager >> media-manager` wechseln
- Folgende Parameter müssen konfiguriert werden
```
state enabled
latching enabled  -> Erwartet immer in der Quell-Adresse des ersten Pakets
```
### Konfigurieren der steering pools für peer & core
- In das Konfigurationsmenü `media-manger >> steering-pool` wechseln
- Folgende Parameter müssen konfiguriert werden
```
ip address 10.0.5.11
realm-id peer1
start-port 200000
end-port 290000
```
Das selbe entsprechend für die Core seite wiederholen
## Peering
### Konfigurieren der Policy-Based Realm Bridging (PBRB)
Erstellen der one2one policy-based peering Konfiguration. Dies ermöglicht das Komunizieren zwischen den beiden Realms
- In das Konfigurationsmenü wecheseln `session-router >> local-policy` 
```
to-address *
from-address *
source-realm core1
policy-attributes
	realm peer1
	nexthop 10.0.5.101
```
- Mit `done - exit - done - exit` die local-policy erstellen.
- Damit ist es allen Teilnehmern aus dem core1 Realm * Anzurufen
```
to-address *
from-address *
source-realm peer1
policy-attributes
	realm core1
	nexthop 10.0.6.100
```
- Mit `done - exit - done - exit` die local-policy erstellen.
- Damit ist es allen externen Teilnehmern gestattet, jeglich Rufnummer im Core1 Realm anzurufen. 
### Erstellen von Header Manipulation Rules (HMR)
- Erstellen einer neuen sip-manipulation Regel `session-router >> sip-manipulation` 
- HMR hat drei Verschachtelungsebenen
- Das erste Element `sip-manipulation`
```
name NAT_IP1
description "Hide topology information leak"
```
- Die zweite ebene `header-field`
- Es wird hier der TO Header angepasst
```
header-name to
action manipulate
msg-type request
```
- `show` um die Konfiguration zu verifizieren
- Danach in das dritte Subelement `element-rules` wechseln
```
name my_To_er
type uri-host
action replace
match-val-type ip
new-value $REMOTE_IP
```
- `done - exit` um zurück in das Header-Rule level zukommen
- `done - exit` um  zurück in das SIP-Manipulation zukommen
- Jetzt wird das FROM Header angepasst
```
name my_From_Hr
header-name From
action manipulate
msg-type request
```
- Jetzt wieder tiefer in das `element-rules` Menü wechseln
```
name my_From_Er
type uri-host
action replace
match-val-type ip
new-value $LOCAL_IP
```
`done - exit` um zurück in das Header-Rule level zukommen
`done - exit` um  zurück in das SIP-Manipulation zukommen
`done - exit` um die HMR zu erstellen
### HMR Realm zuweiseen
- Im Konfigurationsmenü `media-manager >> realm-config` 
- `select <your-peer>`
- Dem Parameter `out-manipulationid NAT_IP1` hinzufügen
- Mit `done - exit` speichern
### Konfigurieren SIP Access Controll in Peering
Der SIP-Traffic auf der Peering Seite soll für eine bestimmte IP-Adress Range begrenzt werden, sowie der SIP-Traffic ist nur für einen bestimmten session-agent erlaubt.
- `media-manager >> realm-config`
```
addr-prefix 10.0.7.0/24
```
`session-router >> sip-interface >> sip-port`
```
allow-anonymous realm-prefix
```
### Konfigurieren eines Session-Agent
Der Session Agent liegt über der Realm Konfig und kann z.b. SIP-Trunks beinhalten. Mit einem Session-Agent sind auch erweiterte Auswertungen des SIP-Traffic möglich
- Konfigrieren unter `session-router >> session-agent`
```
hostname StudentCore1
ip-address 10.0.5.101
realmid  peer1
```

## Access-Backbone Umgebung
### Erstellen des access und Backbone Realm
- In das folgende Menü wechseln `media-manager >> realm-config` und beide Realms erstellen
```
identifier access1
network-interfaces M00:0
addr-prefix 0.0.0.0
```
`done - exit`
```
identifier backbone1
network-interfaces M10:0
addr-prefix 0.0.0.0
```
`done - exit`
### Erstellen der access & backbone SIP-Interfaces
- In das Menü `session-router >> sip-interfaces` wechseln
- Access Realm erstellen
```
realm-id access1
nat-traversal always  -> Wenn Client hinter NAT
registration-caching enabled
sip-ports
	address 10.0.5.11
	allow-anonymous registred
```
`done - exit - done`
- Backbone Realm erstellen
```
realm-id backbone1
sip-ports
	address 10.0.6.11
```
`done - exit - done`
### Erstellen der Local-Policy
- In das Menü `session-router >> local-policy` wechseln und die notwendigen Policy erstellen
```
from-address *
to-address *
source-realm access1
description "access1-to-backbone1" 
policy-attributes
	next-hop 10.0.6.100
	realm backbone
```
`done - exit - done`
```
from-address *
to-address *
source-realm backbone1
description "backbone1-to-access1"
policy-attributes
	next-hop 10.0.5.101
	realm access1
```
`done - exit - done`
### Erstellen der steering-pools
- In das folgende Menü wechseln `media-manager >> steering-pool
- Für beide Realms müssen die Pools konfiguriert werden
```
realm-id access1
ip-address 10.0.5.11
start-port 20000
end-port 29999
```
`done`
```
realm-id backbone1
ip-address 10.0.6.11
start-port 30000
end-port 39999
```
`done`
### Prüfen der Konfiguration
- Zeigt die registrierten Anwender
`sh sipd endpoint-ip <Extension>`
- Je nach Umgebung ebenfalls wichtig
```
Registrar-domain 
Registrar-host 
Registrar-port
```
## Konfigurieren High Availabillity
### Vorbereitung für HA
1. Sicherstellen das beide SBC richtig verkabelt sind
2. `show media physical` um die beiden base MAC-Adressen zu ermitteln
3. Ermitteln welche virtuellen MAC-Adressen die media-interfaces nutzen werden
### Konfigurieren des primären SBC
- Die virtuelle MAC-Adresse muss dem Physikalischen Interface hinzugefügt werden
- Erstellen der wancom1 & wancom2 phy-interface
```
name wancom1
slot 0
port 1
wancom-health-score 8
```
`done`
```
name wancom2
slot 0
port 2
wancom-health-score 9
```
`done`
- Erstllen der Network-Interfaces über wancom1 & wancom2
```
name wancom1
pri-utility-addr 10.0.4.1
sec-utility-addr 10.0.4.2
netmask 255.255.255.252
```
`done`
````
name wancom2
pri-utility-addr 10.0.4.3
sec-utility-addr 10.0.4.4
netmask 255.255.255.255
```
