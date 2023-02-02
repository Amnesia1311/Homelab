## Session Initiation Protocol
- Stellt die Signalisierungsebene eines session-based multimedia-system
- Ermöglicht den Aufbau, Kontrolle, und abbau von sessions, sowie einige andere Dienste
- Ist verantwortlich welche Medientyp genutzt wird
- Wird verwendet mit anderen Protokollen, um eine Kommunikation zu erstellen, z.b.: SDP, RTP, DNS, HTTP, ENUM, RADIUS, DIAMETER
- SIP verwendet ein Request-Respone Modell
- SIP-Messages sind text
- Kann über UDP, TCP, TLS transportiert werden, das darunterliegende Netzwerk ist IPv4/6
- Wird oft als Protokoll der ISO-Schicht 5 bezeichnet. Es kombiniert jedoch funktionen der Schichten 5, 6 und 7
- Session Description Protocol, SDP, das als "Body" in den SIP-Signalisierungs Nachrichten, um die Medienattribute auszuhandeln
- Real-Time Protocol (RTP) und Real-Time Control Protocol (RTCP) Pakete (über UDP) werden verwendet, um tatsächliche Payload- bzw. QoS-bezogene Informationen zu übertragen.
### Basic SIP: User Agent
- User Agent(UA) 
	- Ein SIP-Endgerät(zb ein Telefon)
	- kann als UAC oder UAS fungieren
- User Agent Client(UAC): Ist ein Software Prozess der:
	- Inititiert das senden von requests
	- Empfängt responses
- User Agent Server(UAS): Ein Software Prozess der:
	- Requests empfängt
	- Antwortet mit responses


Aus RFC 3261: User-Agent-Client (UAC): Ein User-Agent-Client ist eine logische Einheit, die eine neue Anfrage erstellt eine neue Anfrage erstellt und dann die Client-Transaktionsstatus-Maschinerie verwendet, um sie zu senden. Die Rolle des UAC besteht nur für die Dauer dieser Transaktion. Mit anderen Worten: Wenn ein Stück Software eine Anfrage initiiert, agiert sie für die Dauer dieser Transaktion als UAC. Erhält sie später eine Anfrage erhält, übernimmt sie die Rolle eines User-Agent-Servers für die Bearbeitung dieser Transaktion.

UAC-Core: Der Satz von Verarbeitungsfunktionen, die von einer UAC benötigt werden und über der 
Transaktions- und Transportschicht liegen.

User Agent Server (UAS): Ein User-Agent-Server ist eine logische Einheit, die eine Antwort 
auf eine SIP-Anfrage erzeugt. Die SIP-Response nimmt die Anfrage an, lehnt sie ab oder leitet sie weiter. Diese Rolle besteht nur für die Dauer der jeweiligen Transaktion. Mit anderen Worten: Wenn eine Software antwortet(response) auf eine anfrage(request), fungiert sie für die Dauer dieser Transaktion als UAS. Erzeugt sie später eine Anfrage, übernimmt sie übernimmt sie die Rolle eines User-Agent-Clients(UAC) für die Bearbeitung dieser Transaktion.

UAS-Core: Der Satz von Verarbeitungsfunktionen, der für eine UAS erforderlich ist und über der 
Transaktions- und Transportschich sitzt. 

User Agent (UA): Eine logische Einheit, die sowohl als User Agent Agent-Client und User-Agent-Server fungieren kann.

### Basic SIP: Server
- Proxy-Server
	- Bietet proxy und message weiterleitung an
- Registrar
	- Registriert Endpunkte, sodass Sie in einer Domain bekannt sind
	- Erstellt Lokations Datenbank einträge(bindings) in folgender form: end-point identity + current IP-address:port
- Redirect Server
	- Bietet weiterleitungs services
	- Kann Proxys entlassten oder ganz eleminieren
- Back-to-Back User Agent
	- Ein Gerät das als Endpunkt für calls dient. Es kann die calls weiterverarbeiten und die calls neu erstellt
	- Somit hat der B2BUA ein isolations effekt und kann für security und andere services genutzt werden

Der Proxy-Server arbeitet, wie der Begriff schon sagt, im Auftrag eines SIP-Geräts, indem er Informationen verwendet (z. B. Routing-Informationen), die dem Gerät nicht zur Verfügung stehen, und leitet die SIP-Nachrichten des Geräts weiter. Ein Softswitch ist ein Beispiel für eine Implementierung, die die Proxy Funktionen und die entsprechende Software umfasst.

In einem gut organisierten System muss das System wissen, welche Benutzer derzeit existieren (oder aktiv sind) und wo sie sich befinden (geografisch oder in Form von IP-Adressen). Um dieses Wissen zu erhalten Wissen aufrechtzuerhalten, registrieren sich Telefone (und möglicherweise andere Geräte) im System, indem sie mit dem einem Registrar interagieren.

In kleinen Systemen (z. B. in einem Büro oder auf einem kleinen Campus) wird ein anrufendes Telefon versuchen seine erste SIP-Nachricht an einen Server zusenden, den es für einen Proxy hält. Das ist ein sogenannter Redirect-Server, dieser antwortet dem Telefon mit Informationen, die es dem anrufenden Telefon ermöglicht, dass angerufenen Telefon direkt zu konaktieren.

Vereinfacht ausgedrückt, nimmt ein Back-To-Back User Agent (B2BUA) einen Anruf so entgegen, als wäre er das Ziel. Er leitet dann einen Anruf an das eigentliche Ziel weiter und "überbrückt" diese beiden Anrufe. Da er während der gesamten Sitzung in der Mitte steht, kann der B2BUA alles ändern: Signalisierungsinformationen, Adressen, Verschlüsselung und mehr. Dies nutzt viele gewünschte Premium-Funktionen, von denen die wichtigste die SIP-Netzwerksicherheit ist. 

### SIP-Messages
Es gibt zwei arten: Request und Responses. Die Struktur ist wie folgt:
- Start line = "Request line" oder "Status line" für Responses
- Header = Mehrere lines auch "Header fields"
- Body (optional, ähnlich wie ein Anhang in einer Mail)
	- Session Description Protocol (SDP)  - sehr üblich
	- XML Informationen
	- Instant messaging text
	- Other data

Alle SIP-Messages sind entweder eine request von einem UAC oder eine Response von einem UAS. Die Nachrichten sind nach RFC 822, "Standard for the format of ARPA internet text messages", formatiert. Diese textbasierten Nachrichten ähneln in Aussehen und Handhabung dem Hypertext TransferProtocol (HTTP), einem Anwendungsprotokoll, das die Regeln für die Übertragung von Informationen im Web definiert. SIP-Messages sind ASCII-basiert, ähnlich wie HTTP; der Nachteil ist, dass ASCII-basierte Messages mehr Bandbreite verbrauchen als binär formatierte Messages. Jede SIP-Message enthält eine Start-line, gefolgt von Header-Fields und einem optionalen Message-Body. Die Start-line enthält unterschiedliche Informationen, je nachdem, ob es sich bei der Nachricht um eine Request oder eine Response handelt.









