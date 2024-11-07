---
title: 'Exchange - Kontaktgruppen erstellen'
excerpt: 'Erfahren Sie hier, wie Sie Mailinglisten in Exchange verwalten'
updated: 2024-11-04
---

<style>
.w-600 {
  max-width:600px !important;
}
.h-600 {
  max-height:600px !important;
}
</style>

## Ziel

Mit Exchange Gruppen können mehrere Benutzer durch Senden von E-Mails an eine Gruppenadresse untereinander kommunizieren. Mit dieser kollaborativen Funktion können Sie Mailinglisten erstellen und verwalten, die sowohl Exchange Benutzer als auch externe Kontakte enthalten können.

**In dieser Anleitung wird erläutert, wie Sie Exchange Gruppen über das OVHcloud Kundencenter und die Outlook Web App (OWA) verwenden.**

## Voraussetzungen

- Sie haben Zugriff auf das [OVHcloud-Kundencenter](/links/manager).
- Sie haben eine [OVHcloud Exchange Lösung](/links/web/emails-hosted-exchange), die bereits eingerichtet ist.

## In der praktischen Anwendung

### Eine neue Gruppe erstellen

Loggen Sie sich in Ihrem [OVHcloud Kundencenter](/links/manager) ein und wählen Sie unter `Microsoft`{.action} und `Exchange`{.action} Ihren Exchange Dienst aus. Gehen Sie dann auf den Tab `Gruppen`{.action}.

![contactgroups](images/exchange-groups-create01.png){.thumbnail .w-600 .h-600}

Wenn Sie auf `Kontaktgruppe erstellen`{.action} klicken, öffnet sich ein neues Fenster, in dem Sie die Gruppeneinstellungen definieren können:

![contactgroups](images/exchange-groups-create02.png){.thumbnail .w-600 .h-600}

- **E-Mail-Adresse**: Geben Sie eine neue Adresse ein, um Nachrichten an die Mailingliste zu senden. Achten Sie darauf, keine bereits funktionierende Adresse zu verwenden.
- **Gruppenname**: Verwenden Sie den Namen, der in Ihrem [OVHcloud Kundencenter](/links/manager) und [OVHcloud Web Messaging](/links/web/email) (OWA) angezeigt wird.
- **Maximale Größe für Ein- und Ausgabe**: Sie können die maximale Größe für ein- und ausgehende E-Mails angeben.
- **In Outlook ausblenden**: Wenn dieses Kontrollkästchen aktiviert ist, wird die Gruppenadresse nicht in der Adressliste des Exchange Dienstes angezeigt.
- **Authentifizierung erforderlich**: Wenn dieses Kontrollkästchen aktiviert ist, können nur Benutzer derselben Plattform Nachrichten mit der Gruppenadresse senden.

Klicken Sie auf `Weiter`{.action}, um fortzufahren.

Wählen Sie auf der zweiten Seite die **Kontakte** der Gruppe aus, und geben Sie die **Administratoren** an. Diese Auswahl erfolgt ausschließlich unter den bereits im Dienst aufgeführten E-Mail-Adressen und externen Kontakten.

- **Administratoren**: E-Mail-Accounts, die E-Mails an alle Gruppenkontakte senden dürfen.
- **Kontakte**: E-Mail-Accounts, die von Administratoren an die Gruppe gesendete E-Mails empfangen.

> [!primary]
>
> Bitte beachten Sie, dass Administratoren als **Kontakte** konfiguriert sein müssen, um Gruppen-E-Mails zu erhalten.

![ContactGroups](images/exchange-groups-create03.png){.thumbnail .w-600 .h-600}

Klicken Sie auf `Weiter`{.action}, um fortzufahren, und klicken Sie auf `Bestätigen`{.action}, um Ihre Auswahl abzuschließen.

### Gruppen verwalten

Nachdem Sie Ihre Gruppe erstellt haben, können Sie die von Ihnen festgelegten Einstellungen ändern. Klicken Sie dazu auf `...`{.action} rechts neben der Gruppe in der Tabelle.

![contactGroups](images/exchange-groups-options01.png){.thumbnail .w-600 .h-600}

#### Benutzer in einer Gruppe verwalten

Um `Kontakte` zu Ihrer Gruppe hinzuzufügen oder `Administratoren` zu definieren, klicken Sie auf den Button `...`{.action} und dann auf `Benutzer konfigurieren`{.action}. Markieren Sie die Attribute, die Sie an die E-Mail-Adressen in der Spalte `E-Mail-Account` anhängen möchten.

> [!primary]
>
> Eine Gruppe kann bis zu 10.000 Kontakte enthalten.

![ContactGroups](images/exchange-group-options-users01.png){.thumbnail .w-600 .h-600}

#### Delegierungen einer Gruppe verwalten

Die Menüoption `Delegierungen konfigurieren`{.action} wird angezeigt. Diese Option erlaubt es Ihnen, den Zugriff auf dieselbe Weise zu delegieren, wie Sie es für einen Exchange Account tun. Weitere Informationen finden Sie in [dieser Anleitung](/pages/web_cloud/email_and_collaborative_solutions/microsoft_exchange/feature_delegation).

![contactGroups](images/exchange-groups-options-delegation01.png){.thumbnail .w-600 .h-600}

> [!primary]
>
> Bitte beachten Sie, dass es einige Minuten dauern kann, bis alle Änderungen an diesem Dienst wirksam werden. Sie können den Status der meisten Operationen überprüfen, indem Sie im horizontalen Menü die Optionen `Mehr`{.action} und `Aktuelle Tasks`{.action} auswählen.

### Nachricht an eine Gruppe mit OWA senden

Sie können jetzt Ihre Mailingliste über [OVHcloud Webmail](/links/web/email) (OWA) testen: Senden Sie einfach eine E-Mail an die Gruppenadresse.

![contactgroups](images/exchange-groups-step6.png){.thumbnail}

## Weiterführende Informationen

[Berechtigungen eines Exchange Accounts übertragen](/pages/web_cloud/email_and_collaborative_solutions/microsoft_exchange/feature_delegation)

[OWA mit einem Exchange Account verwenden](/pages/web_cloud/email_and_collaborative_solutions/using_the_outlook_web_app_webmail/email_owa)

[Kalender in OWA freigeben](/pages/web_cloud/email_and_collaborative_solutions/using_the_outlook_web_app_webmail/owa_calendar_sharing)

Kontaktieren Sie für spezialisierte Dienstleistungen (SEO, Web-Entwicklung etc.) die [OVHcloud Partner](/links/partner).

Wenn Sie Hilfe bei der Nutzung und Konfiguration Ihrer OVHcloud Lösungen benötigen, beachten Sie unsere [Support-Angebote](/links/support).

Treten Sie unserer [User Community](/links/community) bei.
