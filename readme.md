dhcp

tidigare har vi arbetat med fasta ipadresser i den här uppgiften ska vi arbeta med dynamiska ipadresser, för detta behöver vi installera dhcp, Dynamic Host Configuration Protocol, det är redan gjort i vagrantfilen, på gateway/routern är en dhcp server installerad, [dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) och på klienterna är nätverksinterfacen konfigurerade för att använda dhcp.

Vagrantfilen består av en gateway/router och två klientmaskiner.

Ladda ner filen, cd och vagrant up

```bash
git clone https://github.com/bojohan/dhcp.git
cd dhcp
vagrant up
```

Nu ska vi titta på vad som händer när klienterna får sina ipadresser.


Skriv upp och notera följande under labben?

Vad är mac adress?

När och vad inträffar under?

- DHCPDISCOVER
- DHCPREQUEST
- DHCPOFFER
- DHCPACK


Vi börjar med att kolla logiflerna på routern. Vi är intresserade av att läsa rader som innehåller DHCP

```bash
vagrant ssh gateway
sudo less /var/log/syslog|grep DHCP

```

Gå upp tills ni hittar DHCPDISCOVER, där står något sådant häref

```
Sep 11 10:34:16 vagrant-ubuntu-trusty-64 dnsmasq-dhcp[2664]: DHCPDISCOVER(eth1) 08:00:27:fb:db:0b
Sep 11 10:34:16 vagrant-ubuntu-trusty-64 dnsmasq-dhcp[2664]: DHCPOFFER(eth1) 192.168.0.96 08:00:27:fb:db:0b
Sep 11 10:34:16 vagrant-ubuntu-trusty-64 dnsmasq-dhcp[2664]: DHCPREQUEST(eth1) 192.168.0.96 08:00:27:fb:db:0b
Sep 11 10:34:16 vagrant-ubuntu-trusty-64 dnsmasq-dhcp[2664]: DHCPACK(eth1) 192.168.0.96 08:00:27:fb:db:0b client
```

När nätverkskonfigurationen startar på vår klient så söker den efter en dhcp server som kan tillhandahålla en ledig ipadress, som adress skickar den med sin macadress.

dhcp servern uppmärksammans och erbjuder en ipadress.

klienten accepterar ipadressen.

servern bekräftar.


Test själva att det fungerar..

happy hacking
