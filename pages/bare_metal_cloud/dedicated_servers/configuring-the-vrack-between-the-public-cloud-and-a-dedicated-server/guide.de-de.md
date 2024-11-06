---
title: 'vRack zwischen Public Cloud und Dedicated Server einrichten'
excerpt: 'Erfahren Sie hier, wie Sie ein privates Netzwerk zwischen Public Cloud Instanzen und Dedicated Servern einrichten'
updated: 2024-11-05
---

> [!primary]
> Diese Übersetzung wurde durch unseren Partner SYSTRAN automatisch erstellt. In manchen Fällen können ungenaue Formulierungen verwendet worden sein, z.B. bei der Beschriftung von Schaltflächen oder technischen Details. Bitte ziehen Sie im Zweifelsfall die englische oder französische Fassung der Anleitung zu Rate. Möchten Sie mithelfen, diese Übersetzung zu verbessern? Dann nutzen Sie dazu bitte den Button "Beitragen" auf dieser Seite.
>

## Ziel

OVHcloud [vRack](/links/network/vrack/) ist ein privates Netzwerk, mit dem Sie das Routing zwischen zwei oder mehr OVHcloud [Dedicated Servern](/links/bare-metal/bare-metal) einrichten können. Darüber hinaus können Sie auch [Public Cloud Instanzen](https://www.ovh.de/public-cloud/instances/) zu Ihrem privaten Netzwerk hinzufügen, um eine Infrastruktur aus physischen und virtuellen Ressourcen zu erstellen.

**Diese Anleitung erklärt, wie Sie eine [Public Cloud Instanz](/pages/public_cloud/compute/public-cloud-first-steps) und einen [dedizierten Server](/links/bare-metal/bare-metal) über vRack verbinden.**

## Voraussetzungen

- Sie haben eine [Public Cloud Instanz](/pages/public_cloud/compute/public-cloud-first-steps) in Ihrem Kunden-Account.
- Sie haben ein [vRack](/links/network/vrack) in Ihrem Kunden-Account eingerichtet.
- Sie haben einen [Dedicated Server](/links/bare-metal/bare-metal) (kompatibel mit vRack) in Ihrem Kunden-Account.
- Sie haben Zugriff auf Ihr [OVHcloud Kundencenter](/links/manager).
- Sie haben einen privaten IP-Adressbereich für das vRack festgelegt.

> [!warning]
> Diese Funktion kann nur eingeschränkt oder nicht verfügbar sein, falls ein Dedicated Server der [**Eco** Produktlinie](https://eco.ovhcloud.com/de/about/) eingesetzt wird.
>
> Weitere Informationen finden Sie auf der [Vergleichsseite](https://eco.ovhcloud.com/de/compare/).

## In der praktischen Anwendung

### Public Cloud Projekt zum vRack hinzufügen

> [!primary]
> Dies gilt nicht für neu erstellte Projekte, da die automatisch mit einem vRack ausgeliefert werden. Um das vRack anzuzeigen, nachdem das Projekt erstellt wurde, gehen Sie in das Menü `Bare Metal Cloud`{.action} und klicken Sie auf `Network`{.action}. Klicken Sie auf `Privates Netzwerk vRack`{.action}, um alle vRacks anzuzeigen.
>
> Sie können das Projekt auch aus dem zugewiesenen vRack entfernen und an ein anderes vRack anhängen, etwa wenn bereits ein vRack für dedizierte Server besteht.

Bei älteren Projekten gehen Sie nach der Bestellung Ihres [vRack](/links/network/vrack) in das Menü `Bare Metal Cloud`{.action}, klicken Sie links auf `Network`{.action} und dann auf `Privates Netzwerk vRack`{.action}. Wählen Sie Ihr vRack aus der Liste aus.

Wählen Sie in der Liste der verfügbaren Dienstleistungen das Projekt aus, das Sie zum vRack hinzufügen möchten, und klicken Sie dann auf den Button `Hinzufügen`{.action}.

![Projekt zum vRack hinzufügen](images/addprojectvrack.png){.thumbnail}

### Instanz in das vRack integrieren

Es können zwei Situationen auftreten:

- Die Instanz existiert noch nicht.
- Die Instanz existiert bereits und Sie müssen sie zum vRack hinzufügen.

#### Im Fall einer neuen Instanz

Wenn Sie Hilfe benötigen, folgen Sie zunächst [dieser Anleitung](/pages/public_cloud/compute/public-cloud-first-steps). Bei der Erstellung einer Instanz können Sie in Schritt 5 ein privates Netzwerk angeben, in das Ihre Instanz integriert werden soll. Wählen Sie dann im dargestellten Drop-down-Menü Ihr zuvor erstelltes vRack aus.

#### Im Fall einer bereits bestehenden Instanz

Sie können eine vorhandene Instanz einem privaten Netzwerk zuordnen.

Mit Ihrem Projekt im Zusammenhang mit dem vRack können Sie private Netzwerke erstellen.

Klicken Sie im Tab Public Cloud im linken Menü unter **Network** auf `Private Network`{.action}.

Klicken Sie auf `Privates Netzwerk hinzufügen`{.action}.

![create private network](images/vrack2022-03.png){.thumbnail}

Auf der nächsten Seite können Sie mehrere Einstellungen anpassen.

Wählen Sie in Schritt 1 die Region aus, in der Sie das private Netzwerk platzieren möchten.

![select region](images/vRack2024-01.png){.thumbnail}

Damit die beiden Dienste miteinander kommunizieren können, müssen sie mit derselben **VLAN-ID** getaggt sein.

Diese kann in Schritt 2 konfiguriert werden.

![configure network](images/configure_private_network.png){.thumbnail}

Dieser Schritt bietet mehrere Konfigurationsoptionen. Für die Zwecke dieser Anleitung werden wir uns auf die notwendigen Elemente konzentrieren. Klicken Sie auf die Tabs, um Details anzuzeigen:

> [!tabs]
> **Name des privaten Netzwerks**
>>
>> Geben Sie einen Namen für Ihr privates Netzwerk ein.
>>
> **Netzwerk-Optionen von Layer 2**
>>
>> Die VLAN-ID für Dedicated Server ist standardmäßig **0**. Um diese VLAN-ID für eine Instanz zu verwenden, muss das private Netzwerk ebenfalls mit dem VLAN **0** gekennzeichnet werden.  
>> Aktivieren Sie die Option **Set a VLAN ID** und wählen Sie VLAN ID **0** aus.
>>
>> Wenn Sie die Option nicht aktivieren, weist das System Ihrem privaten Netzwerk eine zufällige VLAN-ID zu.
>>
> **Verwendung einer anderen VLAN-ID**
>>
>> Wenn Sie die VLAN-ID **0** nicht verwenden möchten, können Sie eine andere ID zwischen 1 und 4000 auswählen. Es gelten folgende Regeln:
>>
>> - Das private Netzwerk, das mit der Public Cloud Instanz verbunden ist, muss mit dieser VLAN-ID „tagged“ werden.
>> - Bei der Konfiguration des vRacks auf dem Dedicated Server muss diese VLAN-ID in der Netzwerkkonfigurationsdatei enthalten sein.
>>
>> [!primary]
>> Für die Public Cloud definieren Sie eine eindeutige VLAN-ID pro privatem Netzwerk. Es ist nicht möglich, dieselbe VLAN-ID in zwei verschiedenen privaten Netzwerken einzurichten.
>>
>> [!primary]
>> Im Gegensatz zu Dedicated Servern (bei Verwendung einer VLAN-ID ungleich 0) ist es nicht erforderlich, die VLAN-ID direkt in die Netzwerkkonfigurationsdatei der Public Cloud-Instanz einzufügen, sobald sie im OVHcloud Kundencenter eingerichtet wurde.
>>
>> Beispiel: Wenn Ihr privates Netzwerk der Instanz mit VLAN 2 getaggt ist, muss diese VLAN-ID nur in der Netzwerkkonfiguration des Dedicated Servers enthalten sein. Weitere Informationen finden Sie in folgender Anleitung: [Mehrere VLANs im vRack erstellen](/pages/bare_metal_cloud/dedicated_servers/creating-multiple-vlan-in-a-vrack).
>>
> **Verteilungsoptionen für DHCP-Adressen**
>>
>> Sie können den standardmäßigen privaten IP-Bereich beibehalten oder einen anderen IP-Bereich verwenden.
>>

Klicken Sie nach Abschluss der Konfiguration auf `Erstellen`{.action}. Dieser Vorgang kann einige Minuten dauern.

Klicken Sie im Dashboard der entsprechenden Instanz auf den Button `...`{.action} im Feld "Netzwerke" neben "Privates Netzwerk(e)" und wählen Sie `Netzwerk verbinden`{.action}.

![attach network](images/vRack2021-01.png){.thumbnail}

Wählen Sie im angezeigten Fenster das oder die privaten Netzwerke aus, die Sie mit Ihrer Instanz verbinden möchten, und klicken Sie auf `Anfügen`{.action}.

![attach network](images/attach_network.png){.thumbnail}


### Netzwerkinterfaces konfigurieren

Konfigurieren Sie anschließend die Netzwerkinterfaces auf Ihrer neuen Public Cloud Instanz und Ihrem Dedicated Server mithilfe dieser Anleitung: "[Mehrere dedizierte Server im vRack konfigurieren](/pages/bare_metal_cloud/dedicated_servers/vrack_configuring_on_dedicated_server)".

## Weiterführende Informationen

Für den Austausch mit unserer User Community gehen Sie auf <https://community.ovh.com/en/>.
