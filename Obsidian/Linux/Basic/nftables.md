## Was ist nftables
nftables ist eine moderne Paketfilter framework für (**Linux**)[[linux]]. 
**nftables** in a nutshell:
- Verfügbar ab Linux kernels >= 3.13.
-   Kommt mit einer neuen cli nft. Syntax ist anders zu **(iptables)[[IPTables]]**.
-   Kommt mit einem kompatibiltätslayer, sodass iptables Kommandos über das nftables framework laufen
-   It provides a generic set infrastructure that allows you to construct maps and concatenations. You can use these new structures to arrange your ruleset in a multidimensional tree which **drastically** reduces the number of rules that need to be inspected until reaching the final action on a packet.
### Unterschiede zu iptables
- neue Syntax
- Tables und chains sind voll konfigurierbar.
- Eine nftable Regel kann mehrere aktionen durchführen
## # nft command line
Es gibt ein Konfigurationsfile unter `/etc/nftable.conf`
**family** zeigt auf die folgenden table types: _ip_, _arp_, _ip6_, _bridge_, _inet_, _netdev_.
```bash
nft list tables <family>
```
Gibt das gesamte nft ruleset aus
```bash
nft list ruleset
```
dport=destination port, ip gibt an das es sich um ipv4 handelt. saddr=source Address
```bash
tcp dport 9523 ip saddr 192.168.178.0/24 accept;
```
