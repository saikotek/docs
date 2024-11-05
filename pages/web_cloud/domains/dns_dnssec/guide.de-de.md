---
title: "Domainnamen mit DNSSEC absichern"
excerpt: "Erfahren Sie hier, wie Sie Ihre Domainnamen durch die Aktivierung von DNSSEC vor Cache Poisoning schützen können"
updated: 2024-10-29
---

## Ziel 

DNS-Server hosten DNS-Zonen, die die DNS-Konfiguration von Domainnamen enthalten. Über diese Konfigurationen wird Ihr Domainname mit den zugehörigen Diensten verknüpft (Hosting-Server Ihrer Website, E-Mail-Server für Ihren Domainnamen, etc.).

In einigen Fällen können Daten, die über DNS-Server laufen, von Hackern abgefangen werden. Das Ziel ist, eingehenden Traffic für den betroffenen Domainnamen an ihre Websites und E-Mail-Adressen umzuleiten. Dazu wird der Cache des DNS-Servers manipuliert, um eine abweichende DNS-Konfiguration auf Ihren Domainnamen anzuwenden. Dies wird als "Cache Poisoning" bezeichnet. 

Die **D**omain **N**ame **S**ystem **SEC**urity Extensions (**DNSSEC**) ermöglichen es, die DNS-Konfiguration Ihres Domainnamens durch Überprüfung und Authentifizierung der DNS-Antworten vor "Cache Poisoning" zu schützen.

> [!primary]
>
> Die DNSSEC-Option steht derzeit für bei OVHcloud registrierte Domainnamen mit der Endung **.it** nicht zur Verfügung.
>

**Diese Anleitung erklärt, wie Sie DNSSEC für Ihren Domainnamen aktivieren, um ihn vor "Cache Poisoning" zu schützen.**

Weitere Informationen zur Funktionsweise von **DNSSEC** finden Sie auf unserer Seite "[DNSSEC verstehen](/links/web/domains-dnssec){.external}".

Lesen Sie dazu auch unsere Anleitungen zu [OVHcloud DNS-Servern](/pages/web_cloud/domains/dns_server_general_information) und zur [Bearbeitung von OVHcloud DNS-Zonen](/pages/web_cloud/domains/dns_zone_edit).

## Voraussetzungen

- Sie verfügen über einen Domainnamen.
- Der Domainname hat eine mit DNSSEC kompatible Endung.
- Sie haben Zugriff auf Ihr [OVHcloud Kundencenter](/links/manager).

## In der praktischen Anwendung

Um zu überprüfen, ob Ihre Domain die OVHcloud DNS-Konfiguration verwendet, loggen Sie sich in Ihrem [OVHcloud Kundencenter](/links/manager){.external} ein und gehen Sie in den Bereich `Web Cloud`{.action}. Klicken Sie in der linken Spalte auf `Domainnamen`{.action} und wählen Sie die betreffende Domain aus der Liste aus. Wählen Sie den Tab `DNS-Server`{.action} aus, nachdem Sie sich in der betreffenden Domain befinden.

Enden die Namen der DNS-Server auf *ovh.net* (mit Ausnahme des Servers *snds2.ovh.net*), *ovh.ca* oder *anycast.me*, verwendet Ihre Domain die OVHcloud DNS-Server.

> [!primary]
>
> Die Aktivierung / Deaktivierung von **DNSSEC** dauert **24** Stunden.
>
> Wenn Sie die Ihrem Domainnamen zugeordneten DNS-Server zu einem späteren Zeitpunkt ändern möchten, wird die Änderung der DNS-Server seitens OVHcloud erst nach Deaktivierung von **DNSSEC** wirksam. Danach wird eine zusätzliche Verzögerung von **24** bis **48** Stunden für die DNS-Propagierung der Änderung erforderlich sein.
>
> Insgesamt wird die Änderung der DNS-Server einer Domain mit aktivem **DNSSEC** nach **48** bis **72** Stunden voll wirksam.
>

Die Aktivierung von **DNSSEC** ist in drei unten aufgeführten Fällen möglich.

### Fall 1 - Ihre Domain ist bei OVHcloud registriert und verwendet die DNS-Server von OVHcloud

So aktivieren (oder deaktivieren) Sie die **DNSSEC** Lösung für Ihre Domain:

1. Verbinden Sie sich mit Ihrem [OVHcloud Kundencenter](/links/manager).
2. Klicken Sie oben im Kundencenter auf den Tab `Web Cloud`{.action}.
3. Klicken Sie in der linken Spalte auf das Dropdown-Menü `Domainnamen`{.action}.
4. Wählen Sie die betreffende Domain aus.

Die angezeigte Seite enthält allgemeine Informationen zu Ihrer Domain. Dort können Sie den Aktivierungsstatus von **DNSSEC** für diesen Dienst überprüfen.

Überprüfen Sie im Feld `Sicherheit` den Status neben `Sichere Delegation (DNSSEC)`.

![dnssec](/pages/assets/screens/control_panel/product-selection/web-cloud/domain-dns/general-information/activate-dnssec.png){.thumbnail}

Über den Aktivierungsbutton oberhalb von `Sichere Delegation (DNSSEC)`{.action} können Sie **DNSSEC** für Ihre Domain aktivieren oder deaktivieren. Wenn Sie diese Aktion ausführen, erscheint ein neues Fenster, in dem Sie die Änderung bestätigen können.

![dnssec](/pages/assets/screens/control_panel/product-selection/web-cloud/domain-dns/general-information/activate-dnssec-confirmation.png){.thumbnail}

### Fall 2 - Ihre Domain ist bei OVHcloud registriert und verwendet nicht die DNS-Server von OVHcloud

Wenden Sie sich in dieser Situation an den Anbieter, der die DNS-Konfiguration Ihrer Domain verwaltet, und fragen Sie ihn nach den DNSSEC Aktivierungsparametern ("Key Tag" / "Flag" / "Algorithm" / "Public key (encoded in base64)").

Führen Sie nach dem Abrufen dieser 4 Einstellungen die folgenden Aktionen aus:

1. Verbinden Sie sich mit Ihrem [OVHcloud Kundencenter](/links/manager).
2. Klicken Sie oben im Kundencenter auf den Tab `Web Cloud`{.action}.
3. Klicken Sie in der linken Spalte auf das Dropdown-Menü `Domainnamen`{.action}.
4. Wählen Sie die betreffende Domain aus.
5. Klicken Sie auf der angezeigten Seite auf die Registerkarte `DS-Einträge`{.action}. **Dieser Tab erscheint nur, wenn Ihre Domain externe DNS-Server verwendet**.
6. Klicken Sie auf der neu angezeigten Seite rechts auf die Schaltfläche `Bearbeiten`{.action} und dann auf die Schaltfläche `+`{.action}.
7. Tragen Sie in die 4 Formulare `Key Tag`, `Flag`, `Algorithmus` und `Öffentlicher Schlüssel (Base64-kodiert)` die von Ihrem aktuellen Anbieter übermittelten Daten ein.
8. Wenn Sie alle vier Formulare ausgefüllt haben, klicken Sie rechts in der Tabelle auf die blaue Schaltfläche `Bestätigen`{.action}.

![dnssec](/pages/assets/screens/control_panel/product-selection/web-cloud/domain-dns/ds-records/edit-plus-dashboard.png){.thumbnail}

### Fall 3 - Ihre Domain ist nicht bei OVHcloud registriert und verwendet die DNS-Server von OVHcloud

> [!warning]
>
> Vergewissern Sie sich bei Ihrem aktuellen Registrar, dass noch keine DNSSEC Option für Ihre Domain aktiviert ist.

Im Gegensatz zum **Fall 2** müssen Sie hier bei OVHcloud die Einstellungen zur Aktivierung des DNSSEC abrufen ("Key Tag" / "Flag" / "Algorithm" / "Public key (encoded in base64)").

Hierzu müssen Sie die [OVHcloud API](/pages/manage_and_operate/api/first-steps) verwenden und folgende Aktionen ausführen:

- Besuchen Sie unsere Website [OVHcloud API](/links/api) (überprüfen Sie, ob Sie sich auf `https://eu.api.ovh.com` befinden, wenn Ihre Dienste in Europa gehostet werden, und auf `https://ca.api.ovh.com`, wenn sie außerhalb Europas gehostet werden).
- Klicken Sie auf der angezeigten Seite in der Mitte auf `Explore the OVHcloud API`{.action}.
- Verwenden Sie auf der neu angezeigten Seite und links auf der Seite das Dropdown-Menü rechts neben dem Formular `v1`{.action} und wählen Sie die Option `/domain` aus.
- Suchen Sie in der unten in der linken Spalte angezeigten Liste nach der folgenden API, und klicken Sie auf diese: **POST /domain/zone/{zoneName}/dnssec**. Sie können auch direkt auf diesen Link klicken:

> [!api]
>
> @api {v1} /domain POST /domain/zone/{zoneName}/dnssec
>

- Auf der rechten Seite wird dann der Node mit den verschiedenen auszufüllenden Formularen angezeigt.
- Klicken Sie oben rechts auf `Authenticate`{.action} und dann auf `Login with OVHcloud SSO`{.action}.
- Das Login-Interface für Ihr [OVHcloud Kundencenter](/links/manager) wird geöffnet.
- Melden Sie sich bei Ihrem Account an und klicken Sie auf `Authorize`{.action}, um die OVHcloud API mit den Diensten in Ihrem Kundencenter zu verwenden.
- Anschließend werden Sie automatisch zur vorherigen Seite der API weitergeleitet **POST /domain/zone/{zoneName}/dnssec** und sind nun authentifiziert.
- Auf der rechten Seite wird das auszufüllende Formular angezeigt.
- Füllen Sie das Formular im Teil `PATH PARAMETERS` wie folgt aus:
- `zoneName`: Tragen Sie hier die betreffende Domain ein (Beispiel: `domain.tld`).

![API](/pages/assets/screens/api/post-domain-zone-zonename-dnssec.png){.thumbnail}

Wenn Sie das Formular ausgefüllt haben, klicken Sie unten rechts im zuvor ausgefüllten Abschnitt auf die blaue Schaltfläche `Try`{.action}.

Nach einigen Minuten erhalten Sie eine E-Mail von OVHcloud an die Kontakt-E-Mail-Adresse Ihrer OVHcloud DNS-Zone.  
Diese E-Mail enthält die 4 notwendigen Parameter ("Key Tag" / "Flag" / "Algorithm" / "Public key (encoded in base64)"), um DNSSEC beim Registrar Ihrer Domain zu aktivieren.

> [!success]
>
> Überprüfen Sie Ihren Spam-Ordner, wenn Sie die E-Mail nach einer Stunde nicht erhalten haben.

Um den Vorgang abzuschließen, wenden Sie sich mit den 4 Einstellungen an den aktuellen Registrar Ihrer Domain, um die DNSSEC Option auf ihrer Seite zu aktivieren.

## Weiterführende Informationen

[Allgemeine Informationen zu den OVHcloud DNS-Servern](/pages/web_cloud/domains/dns_server_general_information)

[OVHcloud DNS-Zone bearbeiten](/pages/web_cloud/domains/dns_zone_edit)

[Erste Schritte mit der OVHcloud API](/pages/manage_and_operate/api/first-steps)

Kontaktieren Sie für spezialisierte Dienstleistungen (SEO, Web-Entwicklung etc.) die [OVHcloud Partner](/links/partner).

Wenn Sie Hilfe bei der Nutzung und Konfiguration Ihrer OVHcloud Lösungen benötigen, beachten Sie unsere [Support-Angebote](/links/support).

Treten Sie unserer [User Community](/links/community) bei.
