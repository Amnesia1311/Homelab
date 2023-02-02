## Ziele
Nach Abschluss dieser Lektion sollten Sie in der Lage sein: 
• Die grundlegenden Funktionen eines Session Border Controllers (SBC) zu beschreiben 
• Den Bootvorgang und die OS-Services des Session Border Controllers zu besprechen 
• Oracle Acme Packet Produktcodes zu interpretieren

### Kapitel 1, Session Border Controllers
- Was ist ein Session Border Controller
- Oracle SBC Funktionen

Session Border Controller sind session-aware Geräte, die die Kontrolle von End-to-End, interaktiven Kommunikationen über IP-Netzwerkgrenzen ermöglichen. 
•Session: Jede Echtzeit-, interaktive Sprach-, Video- oder Multimediakommunikation mit IP-Signalisierungsprotokollen 
	– SIP 
	– H.323 
	– MGCP/NCS 
	– Megaco/H.248 
• Grenze: IP-IP-Netzwerkgrenze 
	– Service Provider <-> Unternehmenskunde 
	-  Service Provider <-> Endkundenpopulation 
	-  Service Provider <-> Service Provider 
- • Kontrolle: Funktionen, die sich auf Sicherheit, Service-Erreichbarkeit, SLA-Sicherstellung, Umsatz- und Gewinnschutz sowie regulatorische Compliance erstrecken.

Ein Session Border Controller (SBC) ist eine Produktkategorie, die Premium-Interaktionsdienste - Sprach-, Video- oder Multimediakommunikation über IP-Netzwerkgrenzen - ermöglicht. SBCs befinden sich an der Netzwerkgrenze des Service-Providers und ergänzen bestehende Edge-Router. Sie integrieren die Signalisierungs- und Mediacontrol eng und dienen sowohl als Quelle als auch als Ziel für alle Signalisierungsnachrichten und Medienströme, die den Provider-Netzwerk betreten oder verlassen. Das session-aware Networking ist das architektonische Modell von Oracle, um hochwertige, end-to-end interaktive Kommunikationen über mehrere IP-Netzwerke zu ermöglichen. Eine Session wird definiert als jede Echtzeit-, interaktive Sprach-, Video- oder Multimediakommunikation mit IP-Signalisierungsprotokollen wie SIP, H.323, MGCP/NCS oder Megaco/H.248. Die Grenze ist jede IP-IP-Netzwerkgrenze, z.B. zwischen Service-Provider und Kunden oder zwischen zwei Service-Providern. Der "Controller" in SBC bezieht sich auf Steuerungsfunktionen, die Anforderungen in den Bereichen Sicherheit, Service-Level-Sicherstellung, Compliance, Interoperabilität usw. erfüllen.

### Integrated Signaling and Media Control
Oracle Communications Session Border Controller integrieren Überwachung der Leistung von QoS, Routenrichtlinien und Echtzeitbeschränkungen.
![](Oracle/SBC/_assets/SBCSignaling.png)

SBCs befinden sich an der Kante des Unternehmens- oder Provider-Netzwerks und ergänzen bestehende Edge-Geräte. Sie führen die erforderlichen Steuerungsfunktionen durch, indem sie die Signalisierung von Sessions und die Mediensteuerung eng integrieren. SBCs arbeiten als SIP Back-to-Back User Agents (B2BUA), MGCP Back-to-Back Call Agent/Gateways (B2BCA/GW) und/oder H.323 Back-to-Back Gatekeeper/Gateways (B2BGK/GW). Was das bedeutet, ist, dass SBCs die Quelle und das Ziel für alle Signalisierungsnachrichten und Medienströme sind, die in das Netzwerk des Providers eintreten und das Netzwerk verlassen. Das session-aware Networking ist unser architektonisches Modell, um hochwertige, end-to-end interaktive Kommunikationen über IP-Netzwerke zu ermöglichen. Es überwindet die Mängel der Signalisierung von Sessions und der Mediensteuerung von heutigen IP-Netzwerken, indem es vier funktionale Elemente integriert (die in der Illustration beschrieben werden), die interagieren und Informationen dynamisch teilen.

### SBC Functions

Signaling proxy/control  
• Back-to-back session agent (B2BSA)

-   –  SIP B2BUA
    
-   –  H.323 B2BGK/GW
    
-   –  MGCP/NCS B2BCA/GW
    
    Media proxy/control
    
• RTP NAT/relay
![](_assets/SBCFunction.png)
Der SBC stellt Signalisierungs-Proxy-Funktionen für SIP, H.323 und MGCP/NCS bereit. Dazu gehören Zugriffssteuerung, Signalisierungsbeschränkungen und Topologie-Verstecken/NAPT. Der SBC interfaciert mit mehreren Netzwerken. Gegenüber jedem dieser Netzwerke stellt er sich als Proxy für die Signalisierung und als Quelle/Ziel für Medien dar. Obwohl der SBC für die externen Geräte wie ein Proxy aussieht, ist die SIPD-Anwendung, die ein Back-to-Back User Agent (B2BUA) ist, die bedeutende Komponente. Sie ist der Terminierung für eine eingehende Session, für die sie eine ausgehende Session zum endgültigen Zielort initiiert. Sie verbindet dann die beiden Sessions, blockiert Informationen, die blockiert werden müssen, übersetzt Informationen, die übersetzt werden müssen und lässt andere Informationen unverändert passieren. Das Blockieren oder Übersetzen von IP-Adressen und Ports auf diese Weise wird auch als "Topologie-Verstecken" bezeichnet. Die funktionsbezogenen Medienblöcke stellen ähnliche Mechanismen - Beendigung und Neuinitiation - für Medien tragende IP-Pakete bereit. Aufgrund von anspruchsvolleren Echtzeitanforderungen wird dies durch spezielle Hardware erreicht.
### Where Are SBCs Located?
![](_assets/SBCWhere.png)
Das Beispiel in der Folie demonstriert, wo die SBCs in VoIP-Netzwerken liegen können. Ein SBC befindet sich im Rechenzentrum des Unternehmens-Hauptquartiers und zwei weitere SBCs befinden sich in den Netzwerken von Service-Providern. Der SBC im Rechenzentrum ist mit mehreren Service-Providern für SIP-Trunking-Dienste verbunden. Mehrere SIP-Trunk-Service-Provider ermöglichen Redundanz und Kostenminimierung beim Routing. Der SBC leitet Anrufe über SIP-Trunks für PSTN-Verbindungen weiter. Der gleiche SBC ist auch über ein privates Netzwerk per IP-Backbone wie Multiprotocol Label Switching (MPLS) vom Rechenzentrum zu einigen Filialen verbunden. Der SBC verwendet Kostenminimierung und Lastenausgleich bei ausgehenden Anrufen von Filialen zu den Netzwerken der Service-Provider. Die Internetverbindung des SBC ermöglicht es Heimarbeitern und mobilen Mitarbeitern, das Internet zu nutzen, um sich mit ihrer IP-Telefonieumgebung zu verbinden, auch wenn sie NAT-Geräte durchlaufen müssen.
### Zusammenfassung
• Ein Session Border Controller (SBC) bietet im Allgemeinen Premium-Funktionen, um Echtzeit-Interaktionssessions über eine Netzwerkgrenze zu steuern (Sicherheit, Medienverarbeitung, SLA usw.). 
• Der Oracle Communications SBC: 
	– Wirkt als SBC 
	– Bereitstellung von Signalisierungs-Proxy-Funktionen für SIP, H.323 und MGCP/NCS-Protokolle 
	– Verarbeitung von Medien-Proxy-Funktionen wie Zugriffssteuerung, Medienbeschränkungen, Topologie-Verstecken und Transcoding.
## Topic 2: Software and Services
-   Operating System Boot Process
    
-   Release Naming Conventions
    
-   Operating System Services
### 3800/4500 Boot Process
![](_assets/SBCBoot.png)
1.  Der BIOS Boot-Loader, wie bei einem normalen PC, lädt von einem absoluten Speicherort auf der Festplatte das nächste Boot-Programm namens bootrom.sys. Das BIOS lässt dann den CPU zum bootrom.sys Code-Einstieg springen.
2.  Das bootrom.sys-Programm, das das Dateisystem kennt, lädt die Stage2-Datei und lässt den CPU in dessen Code-Einstieg springen. Stage2, (auch bekannt als "acmeboot")
3. Wenn acmeboot gestartet wird und die Leertaste gedrückt wird, wird ein interaktives Menü angezeigt und der Operator kann die Boot-Parameter (die sich im NVRAM Bootparam Bereich befinden) einsehen oder ändern. 
4. Wenn das interaktive Menü angezeigt wurde, muss der Befehl "reboot" (im Menü) verwendet werden, um fortzufahren, unabhängig davon, ob Boot-Parameter geändert wurden oder nicht. Dies startet den Boot-Prozess erneut von Schritt 1.
5.  Acmeboot liest die Bootparam-Daten und erfährt, wenn das normale Boot-Image geladen werden soll, sowie welche IP-Adresse und Netzmaske es der Management-Schnittstelle (wancom0) zuweisen muss. 
6. Acmeboot liest Teile der Image-Datei.
7. Acmeboot dekomprimiert die Teile und schreibt sie in vorbestimmte absolute RAM-Speicherplätze. 
6. Der CPU springt zum Einstiegspunkt des Linux-Kernels. Der Linux-Kernel (unter Verwendung des Prozesses "init") führt die gesamte Umgebungsinitialisierung durch. Der NNOS ist eine Sammlung von Oracle-Anwendungsprozessen, von denen einige im privilegierten "Kernel-Modus" und andere im "Benutzer-Modus" ausgeführt werden. Der Befehlszeileninterpreter (ACLI) ist einer von ihnen. Das System ist jetzt betriebsbereit.
### 4600/3900/6100/6300 Boot Process
![](_assets/SBCBoot6100.png)
1.  Der BIOS Boot-Loader, wie bei einem normalen PC, lädt von einem absoluten Speicherort auf der Festplatte das nächste Boot-Programm namens "GRUB", das in der Linux-Welt weit verbreitet ist. Das BIOS lässt dann den CPU zum GRUB-Code-Einstieg springen.
2.  Wenn GRUB gestartet wird und die ESC-Taste gedrückt wird, kann der Operator GRUB anweisen, ein Wiederherstellungsbild zu laden (falls das Haupt-Boot-Image beschädigt ist). Wenn keine ESC eingegeben wurde, wird der Haupt-Boot-Prozess fortgesetzt und das Stage 3 Boot-Programm, traditionell "acmeboot" genannt, geladen und gestartet.
3. Wenn acmeboot gestartet wird und die Leertaste gedrückt wird, wird ein interaktives Menü angezeigt und der Operator kann die Boot-Parameter (die sich im NVRAM Bootparam Bereich befinden) einsehen oder ändern. 
4. 3a. Wenn das interaktive Menü angezeigt wurde, muss der Befehl "Neustart" (im Menü) verwendet werden, um fortzufahren, unabhängig davon, ob Boot-Parameter geändert wurden oder nicht. Dies startet den Boot-Prozess erneut von Schritt 1.
5. 4.  Acmeboot liest die Bootparam-Daten und erfährt, welches normale Boot-Image geladen werden soll, sowie welche IP-Adresse und Netzmaske es der Management-Schnittstelle (wancom0) zuweisen muss. 
6. 5a. Acmeboot liest Teile der Bilddatei. 
7. 5b. Acmeboot dekomprimiert die Teile und schreibt sie in vorbestimmte absolute RAM-Speicherplätze.
8. 6.  Der CPU springt zum Einstiegspunkt des Linux-Kernels. Der Linux-Kernel (unter Verwendung des Prozesses "init") führt die gesamte Umgebungsinitialisierung durch. Der NNOS ist eine Sammlung von Oracle-Anwendungsprozessen, von denen einige im privilegierten "Kernel-Modus" und andere im "Benutzer-Modus" ausgeführt werden. Der Befehlszeileninterpreter (ACLI) ist einer von ihnen. Das System ist jetzt betriebsbereit.