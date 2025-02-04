---
title: Network Bridge einrichten
excerpt: Erfahren Sie hier, wie Sie den Internet-Zugang für Ihre virtuellen Maschinen konfigurieren
updated: 2024-12-13
---

> [!primary]
>
> Seit dem 6. Oktober 2022 heißt unser Dienst "Failover-IP" nun [Additional IP](/links/network/additional-ip). Die Namensänderung hat keine Auswirkungen auf dessen technische Funktionen.
>

## Ziel

Bridged Networking kann verwendet werden, um Ihre virtuellen Maschinen zu konfigurieren. Es einige Anpassungen erforderlich, damit die Netzwerkkonfiguration in unserem Netzwerk funktioniert.

## Voraussetzungen

- Sie verfügen über einen [Dedicated Server](/links/bare-metal/bare-metal) mit installiertem Hypervisor (Citrix Xen Server, Proxmox, etc.).
- Sie verfügen über mindestens eine mit dem Server verbundene [Additional IP](/links/network/additional-ip).
- Sie haben Zugriff auf Ihr [OVHcloud Kundencenter](/links/manager) oder die [OVHcloud API](/pages/manage_and_operate/api/first-steps).

> [!warning]
> Diese Funktion kann nur eingeschränkt oder nicht verfügbar sein, falls ein Dedicated Server der [**Eco** Produktlinie](/links/bare-metal/eco-about) eingesetzt wird.
>
> Weitere Informationen finden Sie auf der [Vergleichsseite](/links/bare-metal/eco-compare).
>
> Diese Anleitung gilt nicht für Server der Reihen [Scale](https://www.ovhcloud.com/de/bare-metal/scale/) und [High Grade](https://www.ovhcloud.com/de/bare-metal/high-grade/).
>
> Weitere Informationen finden Sie in den folgenden Anleitungen: [Netzwerk auf Proxmox VE auf den High Grade & SCALE-Reihen konfigurieren](/pages/bare_metal_cloud/dedicated_servers/proxmox-network-HG-Scale) und [Netzwerk auf Windows Server mit Hyper-V auf den High Grade & SCALE-Reihen konfigurieren](/pages/bare_metal_cloud/dedicated_servers/hyperv-network-HG-Scale).

## In der praktischen Anwendung

Die Grundschritte sind unabhängig von dem darunterliegenden System immer gleich:

- Erstellung einer virtuellen MAC-Adresse für eine [Additional IP](/links/network/additional-ip)
- Ändern der MAC-Adresse der virtuellen Maschine (VM) auf diese neue Adresse
- Konfuguration von **IP-Adresse**, **Netzmaske**, **Gateway** und **Route zum Gateway** innerhalb der VM

Die Codebeispiele in den folgenden Anweisungen sind durch Ihre eigenen Werte zu ersetzen:

- "SERVER_IP": die Haupt-IP-Adresse Ihres Servers
- "ADDITIONAL_IP": Ihre Additional IP-Adresse
- "GATEWAY_IP": die Adresse des Default-Gateways

### Eine virtuelle MAC-Adresse zuweisen

> [!warning]
> Bei einem IP-Block werden die virtuellen MAC-Adressen für jede einzelne IP im Block erstellt.

Loggen Sie sich in Ihr [OVHcloud Kundencenter](/links/manager), gehen Sie zum Bereich `Bare Metal Cloud`{.action} und öffnen Sie `Network`{.action}. Klicken Sie dann auf `IP`{.action}.

Klicken Sie auf den Tab `Additional IP`{.action}.

![manage IPs](images/manageIPs2022.png){.thumbnail}

Klicken Sie auf `...`{.action} in der betreffenden Zeile um das Kontextmenü zu öffnen und klicken Sie dann auf `Virtuelle MAC-Adresse hinzufügen`{.action}.

![Virtuelle MAC-Adresse hinzufügen (1)](images/addvmac.png){.thumbnail}

Wählen Sie `ovh`{.action} in der Drop-down-Liste "Typ" aus, wenn Sie nicht VMware ESXi verwenden - andernfalls wählen Sie `vmware`{.action}. Geben Sie einen Namen in das Feld "Name der virtuellen Maschine" ein und klicken Sie anschließend auf `Bestätigen`{.action}.

![Virtuelle MAC-Adresse hinzufügen (2)](images/addvmac2.png){.thumbnail}

Nach einigen Sekunden erscheint eine virtuelle MAC-Adresse in der Spalte "Virtuelle MAC-Adresse" in der Zeile Ihrer Additional IP-Adresse. Diese virtuelle MAC-Adresse wird benötigt, wenn Sie Ihre VM auf dem Host einrichten.

### Die Adresse des Gateways bestimmen <a name="determinegateway"></a>

Um Ihre virtuellen Maschinen für den Internetzugriff zu konfigurieren, müssen Sie das Gateway Ihres Host-Servers, also des Dedicated Servers, kennen.

Sie können das Gateway auch über [Ihr Kundencenter](#viacontrolpanel) oder die [OVHcloud API](#viaapi) abrufen.

#### Über Ihr Kundencenter <a name="viacontrolpanel"></a>

Loggen Sie sich in Ihr [OVHcloud Kundencenter](/links/manager) ein, gehen Sie in den Bereich `Bare Metal Cloud`{.action} und wählen Sie Ihren Server in `Dedicated Server`{.action} aus.

Das Ihrem Server zugewiesene IPv4-Gateway wird im Tab `Allgemeine Informationen`{.action} im Bereich `Netzwerk` angezeigt. Nachdem Sie die Adresse kopiert haben, setzen Sie die Konfiguration fort.

![gateway](images/ipv4_information.png){.thumbnail}

#### Über die OVHcloud API <a name="viaapi"></a>

Klicken Sie auf der [OVHcloud API Seite](https://eu.api.ovh.com/console/) oben rechts auf `Login`{.action} ein. Geben Sie auf der nächsten Seite Ihre OVHcloud Kundenkennung ein.

Führen Sie den folgenden API-Aufruf unter Angabe des internen Servernamens (Beispiel: `ns3956771.ip-169-254-10.eu`) aus:

> [!api]
>
> @api {v1} /dedicated/server GET /dedicated/server/{serviceName}/specifications/network
>

### Host vorbereiten

> [!primary]
>
Für alle Betriebssysteme und Distributionen **muss**** Ihre virtuelle Maschine mit der virtuellen MAC-Adresse konfiguriert werden, die in Ihrem [OVHcloud Kundencenter](/links/manager) hinterlegt wurde.
>

#### Proxmox

> [!warning]
>
> Die folgenden Anweisungen gelten für einen virtuellen Rechner, der zuvor mit einem bereits installierten Betriebssystem erstellt wurde. Wenn Sie noch keine VM erstellt haben, gehen Sie zu den Optionen auf der Seite [Qemu/KVM Virtual Machine](https://pve.proxmox.com/wiki/Qemu/KVM_Virtual_Machines){.external} (EN) von Proxmox.
>

Nach Erstellung der VM und während diese noch ausgeschaltet ist:

 1\. Wählen Sie die VM aus.<br>
 2\. Öffnen Sie den Bereich `Hardware`.<br>
 3\. Wählen Sie `Network Device` aus.<br>
 4\. Klicken Sie auf den Button `Edit`.<br>

![zum Netzwerk-Device navigieren](images/proxmox_01.png){.thumbnail}

Fügen Sie anschließend die zuvor erzeugte vMAC-Adresse hinzu.

![Netzwerk-Peripherie öffnen](images/proxmox_02.png){.thumbnail}

Sie können nun Ihre VM starten und zu den nächsten Schritten, abhängig vom installierten Betriebssystem, übergehen.

#### VMware ESXi

> [!warning]
>
> Der ESXi Hypervisor wird von OVHcloud nicht mehr unterstützt. Weitere Informationen finden Sie auf [dieser Seite](/pages/bare_metal_cloud/dedicated_servers/esxi-end-of-support).
>

> [!warning]
>
> Die folgenden Anweisungen gelten für einen virtuellen Rechner, der zuvor mit einem bereits installierten Betriebssystem erstellt wurde. Wenn Sie keine VM erstellt haben, lesen Sie die Anleitung [Eine virtuelle Maschine im VMware Host-Client erstellen](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-77AB6625-F968-4983-A230-A020C0A70326.html){.external} (EN) auf der VMware-Seite.
>

Nach Erstellung der VM und während diese noch ausgeschaltet ist klicken Sie mit der rechten Maustaste darauf und klicken dann auf `Edit settings`.

![VM Kontextmenü](images/vmware_01.png){.thumbnail}

Erweitern Sie `Network Adapter 1`, ändern Sie den Wert im Drop-down-Menü `MAC Address` zu `Manual` und geben Sie die die zuvor erzeugte vMAC-Adresse ein.

![Die Einstellungen ändern](images/vmware_02.png){.thumbnail}

Sie können nun Ihre VM starten und zu den nächsten Schritten, abhängig vom installierten Betriebssystem, übergehen.

### Die virtuellen Maschinen konfigurieren <a name="configurationsteps"></a>

> [!warning]
>
> Beachten Sie, dass in den folgenden Beispielen davon ausgegangen wird, dass Sie als Benutzer mit erhöhten Berechtigungen angemeldet sind. Daher wird *sudo* vor jedem Befehl verwendet. Wenn Sie als *root* angemeldet sind, müssen Sie dies nicht tun.
>

#### Debian

Standardmäßig befindet sich die Netzwerkkonfigurationsdatei der virtuellen Maschine in `/etc/network/interfaces`.

Wenn Sie in der Shell Ihrer virtuellen Maschine eingeloggt sind, führen Sie folgenden Befehl aus, um den Namen Ihres Interface zu identifizieren:

```bash
ls /sys/class/net
```

Erstellen Sie anschließend eine Kopie der Konfigurationsdatei, damit Sie jederzeit zur vorherigen Version zurückkehren können:

```bash
sudo cp /etc/network/interfaces /etc/network/interfaces.bak
```

Im Falle eines Fehlers können Sie dann die folgenden Befehle nutzen:

```bash
sudo rm -f /etc/network/interfaces
sudo cp /etc/network/interfaces.bak /etc/network/interfaces
```

Ändern Sie die Datei, sodass sie die folgende Konfiguration widerspiegelt. Ersetzen Sie `INTERFACE_NAME`, `ADDITIONAL_IP` und `GATEWAY_IP` durch eigene Werte.

```bash
sudo nano /etc/network/interfaces
```

```console
auto lo
iface lo inet loopback

# The primary network interface
auto INTERFACE_NAME
iface INTERFACE_NAME inet static
address ADDITIONAL_IP
netmask 255.255.255.255
gateway GATEWAY_IP
```

**Beispiel**

```console
auto lo
iface lo inet loopback

# The primary network interface
auto ens192
iface ens192 inet static
address 192.0.2.1
netmask 255.255.255.255
gateway 203.0.113.254
```

Speichern und schließen Sie die Datei.<br>
Als Nächstes bearbeiten oder erstellen Sie die Datei `/etc/resolv.conf`:

```bash
sudo nano /etc/resolv.conf
```

Fügen Sie folgende Zeile hinzu:

```console
nameserver 213.186.33.99
```

Speichern und schließen Sie die Datei.<br>
Nun müssen Sie Ihr Netzwerkinterface online stellen. Geben Sie hierzu den folgenden Befehl ein (ersetzen Sie `ens192` durch eigene Werte):

```bash
sudo ip link set ens192 up
```

Starten Sie anschließend den Netzwerkdienst mit folgendem Befehl neu:

```bash
sudo systemctl restart networking
```

Um zu überprüfen, ob die virtuelle Maschine mit dem Internet verbunden ist, verwenden Sie folgenden Befehl:

```bash
ping -c 4 example.com
PING example.com (93.184.215.14) 56(84) bytes of data.
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=1 ttl=55 time=29.3 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=2 ttl=55 time=24.9 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=3 ttl=55 time=30.8 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=4 ttl=55 time=27.0 ms

--- example.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 24.925/28.028/30.840/2.254 ms
```

Wenn Sie eine Antwort erhalten, wurde die Additional IP korrekt konfiguriert. Ist das nicht der Fall, starten Sie die virtuelle Maschine neu, und wiederholen Sie den Ping-Befehl.


#### Red Hat Betriebssysteme und darauf basierende (CentOS, Rocky Linux 8/9, Alma Linux 8/9, etc.)

Standardmäßig befindet sich die Netzwerkkonfigurationsdatei der virtuellen Maschine in `/etc/sysconfig/network-scripts/`.

Wenn Sie in der Shell Ihrer virtuellen Maschine eingeloggt sind, führen Sie folgenden Befehl aus, um den Namen Ihres Interface zu identifizieren:

```bash
ip a
```

Erstellen Sie anschließend eine Kopie der Konfigurationsdatei, damit Sie jederzeit zur vorherigen Version zurückkehren können:

```bash
sudo cp /etc/sysconfig/network-scripts/ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0.bak
```

Im Falle eines Fehlers können Sie dann die folgenden Befehle nutzen:

```bash
sudo rm -f etc/sysconfig/network-scripts/ifcfg-eth0
sudo cp /etc/sysconfig/network-scripts/ifcfg-eth0.bak etc/sysconfig/network-scripts/ifcfg-eth0
```

Sie können diese Datei dann mittels `nmcli` bearbeiten. Ersetzen Sie `ADDITIONAL_IP` und `GATEWAY_IP` durch eigene Werte.

IP-Adresse hinzufügen:

```bash
sudo nmcli connection modify interface_name IPv4.address ADDITIONAL_IP/32
```

Gateway hinzufügen:

```bash
sudo nmcli connection modify interface_name IPv4.gateway GATEWAY_IP
```

DNS-Server hinzufügen:

```bash
sudo nmcli connection modify interface_name IPv4.dns 213.186.33.99
```

Ändern der Konfiguration zu "Manual":

```bash
sudo nmcli connection modify interface_name IPv4.method manual
```

Persistente Konfiguration:

```bash
sudo nmcli con mod interface_name connection.autoconnect true
```

Starten Sie das Netzwerk mit folgendem Befehl neu:

```bash
sudo nmcli device down interface_name;nmcli device up interface_name
```

Um zu überprüfen, ob die virtuelle Maschine mit dem Internet verbunden ist, verwenden Sie folgenden Befehl:

```bash
ping -c 4 example.com
PING example.com (93.184.215.14) 56(84) bytes of data.
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=1 ttl=55 time=29.3 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=2 ttl=55 time=24.9 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=3 ttl=55 time=30.8 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=4 ttl=55 time=27.0 ms

--- example.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 24.925/28.028/30.840/2.254 ms
```

Wenn Sie eine Antwort erhalten, wurde die Additional IP korrekt konfiguriert. Ist das nicht der Fall, starten Sie die virtuelle Maschine neu, und wiederholen Sie den Ping-Befehl.

Weitere Informationen zu `nmcli` finden Sie auf [dieser Seite](https://docs.redhat.com/de/documentation/red_hat_enterprise_linux/7/html/networking_guide/sec-using_the_networkmanager_command_line_tool_nmcli).

#### FreeBSD

Standardmäßig befindet sich die Netzwerkkonfigurationsdatei der virtuellen Maschine in `/etc/rc.conf`.

Wenn Sie mit der Shell Ihrer virtuellen Maschine verbunden sind, führen Sie folgenden Befehl aus, um den Namen Ihres Interface zu identifizieren:

```bash
ifconfig
```

Erstellen Sie anschließend eine Kopie der Konfigurationsdatei, damit Sie jederzeit zur vorherigen Version zurückkehren können.

```bash
sudo cp /etc/rc.conf /etc/rc.conf.bak
```

Im Falle eines Fehlers können Sie mit den folgenden Befehlen zurückgehen:

```bash
sudo rm -f /etc/rc.conf
sudo cp /etc/rc.conf.bak /etc/rc.conf
```

Ändern Sie die Datei, sodass sie die folgende Konfiguration widerspiegelt, ersetzen Sie `ADDITIONAL_IP` und `GATEWAY_IP` durch eigene Werte. In diesem Beispiel lautet der Schnittstellenname `em0`. Ersetzen Sie diesen Wert, wenn er nicht zutrifft.

```console
ifconfig_em0="inet ADDITIONAL_IP netmask 255.255.255.255 broadcast ADDITIONAL_IP"
static_routes="net1 net2"
route_net1="-net GATEWAY_IP/32 -interface em0"
route_net2="default GATEWAY_IP"
```

Speichern und schließen Sie die Datei.  
Öffnen/erstellen Sie anschließend die Datei `/etc/resolv.conf` und fügen Sie die folgende Zeile ein:

```console
nameserver 213.186.33.99
```

Speichern und schließen Sie die Datei und starten Sie die VM neu.

Um zu überprüfen, ob die virtuelle Maschine vollständig mit dem Internet verbunden ist, verwenden Sie folgenden Befehl:

```bash
ping -c 4 example.com
PING example.com (93.184.215.14) 56(84) bytes of data.
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=1 ttl=55 time=29.3 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=2 ttl=55 time=24.9 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=3 ttl=55 time=30.8 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=4 ttl=55 time=27.0 ms

--- example.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 24.925/28.028/30.840/2.254 ms
```

Wenn Sie eine Antwort erhalten, wurde die Additional IP korrekt konfiguriert. Ist das nicht der Fall, starten Sie die virtuelle Maschine neu, und wiederholen Sie den Ping-Befehl.

#### Ubuntu

Deaktivieren Sie zuerst cloud-init:

```bash
touch /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg
```

> [!warning]
>
> Wenn Sie Ihre VM mit cloud-init konfigurieren möchten, besuchen Sie [diese Seite](https://cloud-init.io/).
>

Fügen Sie diese Zeile zur Datei `99-disable-network-config.cfg` hinzu:

```bash
network: {config: disabled}
```

Erstellen Sie anschließend die Netzwerkkonfigurationsdatei in `/etc/netplan/` mit folgendem Befehl:

```bash
touch /etc/netplan/00-installer-config.yaml
```

Wenden Sie dann diese Berechtigungen auf `/etc/netplan` an:

```bash
cd /etc/netplan
sudo chmod 600 *.yaml
```

Führen Sie den folgenden Befehl aus, um den Namen Ihres Interface zu identifizieren:

```bash
ip addr
```

Erstellen Sie anschließend eine Kopie der Konfigurationsdatei, damit Sie schnell zur vorherigen Version zurückkehren können:

```bash
sudo cp /etc/netplan/00-installer-config.yaml /etc/netplan/00-installer-config.yaml.bak
```

Im Falle eines Fehlers können Sie dann die folgenden Befehle nutzen:

```bash
sudo rm -f /etc/netplan/00-installer-config.yaml
sudo cp /etc/netplan/00-installer-config.yaml.bak /etc/netplan/00-installer-config.yaml
```

Öffnen Sie anschließend die Netzwerkkonfigurationsdatei:

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

Wenn Sie die Datei zur Bearbeitung geöffnet haben, editieren Sie sie mit den folgenden Änderungen. Ersetzen Sie `INTERFACE-NAME`, `ADDITIONAL_IP` und `GATEWAY_IP` durch eigene Werte.

```yaml
network:
  ethernets:
    INTERFACE-NAME:
      dhcp4: true
      addresses:
          - ADDITIONAL_IP/32
      nameservers:
          addresses:
              - 213.186.33.99   
      routes:
           - to: 0.0.0.0/0
             via: GATEWAY_IP
             on-link: true
  version: 2
```

**Beispiel**

```yaml
network:
  ethernets:
    ens18:
      dhcp4: true
      addresses:
          - 192.0.2.1/32
      nameservers:
          addresses:
              - 213.186.33.99
      routes:
           - to: 0.0.0.0/0
             via: 203.0.113.254
             on-link: true
  version: 2
```

Speichern und schließen Sie die Datei. Sie können die Konfiguration mit folgendem Befehl testen:

```bash
sudo netplan try
```

Wenn sie korrekt ist, verwenden Sie folgenden Befehl:

```bash
sudo netplan apply
```

Um zu überprüfen, ob die virtuelle Maschine mit dem Internet verbunden ist, verwenden Sie folgenden Befehl:

```bash
ping -c 4 example.com
PING example.com (93.184.215.14) 56(84) bytes of data.
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=1 ttl=55 time=29.3 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=2 ttl=55 time=24.9 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=3 ttl=55 time=30.8 ms
64 bytes from 93.184.215.14 (93.184.215.14): icmp_seq=4 ttl=55 time=27.0 ms

--- example.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 24.925/28.028/30.840/2.254 ms
```

Wenn Sie eine Antwort erhalten, wurde die Additional IP korrekt konfiguriert. Ist das nicht der Fall, starten Sie die virtuelle Maschine neu, und wiederholen Sie den Ping-Befehl.

#### Windows Server/Hyper-V

Bevor Sie Ihre virtuelle Maschine konfigurieren, erstellen Sie einen virtuellen Switch.

Führen Sie `ipconfig /all`{.action} über die Kommandozeile Ihres Dedicated Servers aus und notieren Sie den Namen der Netzwerkkarte mit der Haupt-IP-Adresse des Servers.

Erstellen Sie im Hyper-V Manager einen neuen virtuellen Switch und legen Sie die Art der Verbindung als `Extern`{.action} fest.

Wählen Sie den Adapter mit der IP-Adresse des Servers aus und haken Sie die Option `Dem Betriebssystem erlauben, diese Netzwerkkarte freizugeben`{.action} an.

![networkbridging](images/network-bridging-windows-2012-1.jpg){.thumbnail}

> [!primary]
> 
> Dieser Schritt ist nur einmal für einen Hyper-V Server erforderlich. Für alle VMs ist ein **virtueller Switch** erforderlich, um die **virtuellen Netzwerkkarten** der VM mit dem **physischen Adapter** des Servers zu verbinden.
> 

Wählen Sie nun die VM aus, zu der Sie die Additional IP hinzufügen möchten. Verwenden Sie den Hyper-V Manager, um die Einstellungen der virtuellen Maschine zu ändern, und fahren Sie sie herunter.

Erweitern Sie den Netzwerkadapter im linken Menü und klicken Sie auf `Erweiterte Einstellungen`{.action}. Ändern Sie die MAC-Adresse auf `Statisch`{.action} und geben Sie die virtuelle MAC-Adresse für die Additional IP ein. Klicken Sie anschließend auf `OK`{.action}, um die Änderungen anzuwenden.

![networkbridging](images/network-bridging-windows-2012-2.jpg){.thumbnail}

Starten Sie anschließend die VM und loggen Sie sich als Administrator ein. Greifen Sie auf das `Netzwerk- und Freigabecenter`{.action} der Systemsteuerung zu und klicken Sie auf `Ethernet`{.action}. Klicken Sie auf den Button `Eigenschaften`{.action}.

Wählen Sie `Internet Protocol Version 4 (TCP/IPv4)`{.action} aus und klicken Sie dann auf `Eigenschaften`{.action}.

![networkbridging](images/network-bridging-windows-2012-3.jpg){.thumbnail}

Wählen Sie im Fenster mit den IPv4-Eigenschaften `Die folgende IP-Adresse verwenden`{.action}. Tragen Sie die Additional IP im IP-Adressfeld ein und geben Sie als Subnetzmaske "255.255.255.255" ein.

Geben Sie anschließend die IP-Adresse des Gateways Ihres Servers im zugehörigen Feld ein und tragen Sie im Feld `Bevorzugter DNS Server`{.action} "213.186.33.99" ein.

Klicken Sie auf `OK`{.action} und ignorieren Sie die nachfolgende Warnmeldung.

![networkbridging](images/network-bridging-windows-2012-4.jpg){.thumbnail}

Nach Neustart des Servers sollte die VM über die Additional IP mit dem Internet verbunden sein.

#### Troubleshooting

Wenn Sie nicht in der Lage sind, eine Verbindung zwischen Ihrer VM und dem öffentlichen Netzwerk herzustellen, und Sie Netzwerkprobleme vermuten, starten Sie den Server im Rescue-Modus neu und konfigurieren Sie das Bridging-Netzwerk direkt auf dem Host.

Hierzu geben Sie die folgenden Befehle ein, wobei Sie die Parameter "MAC_ADDRESS" mit der im Kundencenter erzeugten vMAC ersetzen und "ADDITIONAL_IP" mit Ihrer Additional IP:

```bash
ip link add name test-bridge link eth0 type macvlan
ip link set dev test-bridge address MAC_ADDRESS
ip link set test-bridge up
ip addr add ADDITIONAL_IP/32 dev test-bridge
```

Pingen Sie nun Ihre Additional IP von einem externen Gerät aus an. 

- Wenn der Host antwortet, bedeutet das wahrscheinlich, dass es auf der virtuellen Maschine oder dem Host einen Konfigurationsfehler gibt, der die Additional IP daran hindert, im normalen Betrieb zu funktionieren.

- Wenn die IP immer noch nicht funktioniert, öffnen Sie bitte ein Support-Ticket über das [Help Center](https://help.ovhcloud.com/csm?id=csm_cases_requests).

## Weiterführende Informationen

Treten Sie unserer [User Community](/links/community) bei.