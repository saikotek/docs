---
title: "So migrieren Sie eine Website von einem Webhosting auf einen VPS"
excerpt: "Erfahren Sie, wie Sie Ihre Website von einem Shared Hosting auf einen OVHcloud VPS migrieren"
updated: 2024-11-06
---

## Ziel

Ihre Website entwickelt sich weiter, und der Ressourcenverbrauch wird immer stärker, sodass Ihr Webhosting nicht mehr Ihren Bedürfnissen in Bezug auf die Leistung oder die Fähigkeit zur Bewältigung komplexerer Aufgaben entspricht. Die Migration auf einen VPS verbessert die Geschwindigkeit und Reaktionsgeschwindigkeit Ihrer Website, erhöht die verfügbaren Computing-Ressourcen (CPU, RAM etc.) und hat mehr Kontrolle über die Server-Umgebung. Diese Anleitung konzentriert sich auf die wesentlichen Schritte für eine effektive Migration auf einen VPS bei gleichzeitiger Gewährleistung der Dienstkontinuität.

**Erfahren Sie, wie Sie Ihre Website von einem Shared Hosting auf einen VPS migrieren.**

## Voraussetzungen

- Sie verfügen über ein aktives [Webhosting](/links/web/hosting) Angebot.
- Sie haben einen [VPS](/links/bare-metal/vps) in Ihrem OVHcloud Account abonniert.
- Sie sind in Ihrem [OVHcloud Kundencenter](/links/manager) eingeloggt.

## In der praktischen Anwendung

> [!warning]
>
> OVHcloud stellt Ihnen Dienste zur Verfügung, für deren Konfiguration, Verwaltung und Verwaltung Sie die alleinige Verantwortung tragen. Es liegt somit in Ihrer Verantwortung, sicherzustellen, dass diese ordnungsgemäß funktionieren.
>
> Wir stellen Ihnen diese Anleitung zur Verfügung, um Sie bei gängigen Aufgaben bestmöglich zu begleiten. Wir empfehlen Ihnen jedoch, falls Sie Hilfe brauchen, einen [spezialisierten Dienstleister](/links/partner) zu kontaktieren. Für externe Dienstleistungen bieten wir leider keine Unterstützung. Weitere Informationen finden Sie im Abschnitt [„Weiterführende Informationen“](#go-further) dieser Anleitung.
>

### Schritt 1 - Sicherung der Dateien und der Datenbank Ihrer Website <a name="step1"></a>

Der erste Schritt besteht darin, alle Dateien Ihrer Website zu sichern, in der Regel über das **F**ile **T**ransfer **P**rotocol (**FTP**) sowie die dazugehörige Datenbank.

Wenn Sie WordPress verwenden, folgen Sie unserer Anleitung „[Backup Ihrer WordPress Installation](/pages/web_cloud/web_hosting/how_to_backup_your_wordpress)“, um zu erfahren, wie Sie die Dateien und Datenbanken Ihrer WordPress-Website sichern, und fahren Sie dann mit [Schritt 2](#step2) fort.

#### Schritt 1.1 - Verbindung mit dem FTP-Speicherplatz Ihres Webhostings

Folgen Sie den Schritten unserer Anleitung „[Mit dem FTP-Speicherplatz eines Webhostings verbinden](/pages/web_cloud/web_hosting/ftp_connection)“, um sich mit dem FTP-Speicherplatz Ihres Webhostings zu verbinden.

#### Schritt 1.2 - Dateien per FTP sichern <a name="step1.2"></a>

Wenn Sie kein CMS (WordPress, Joomla!, Drupal, PrestaShop etc.) verwenden, laden Sie eine vollständige Sicherung aller Dateien in Ihrem FTP-Bereich auf Ihr lokales Gerät herunter. Dazu gehören alle HTML-, CSS-, JavaScript-, Bild- und Konfigurationsdateien (`config.php`, `.env` usw.), aus denen Ihre Website besteht. Stellen Sie sicher, dass Sie alle Ordner und Dateien im Stammverzeichnis (oft als `public_html` oder `www` bezeichnet) abrufen, damit der gesamte Inhalt, der für den Betrieb Ihrer Website erforderlich ist, für die Migration gesichert wird.

Wenn Sie ein CMS verwenden und seine Dateien sichern, wählen Sie die für dieses CMS geeignete Backup-Methode aus, indem Sie auf den entsprechenden Tab klicken.

> [!tabs]
> PrestaShop
>>
>> Sichern Sie für PrestaShop kritische Verzeichnisse wie:
>>
>> - `/admin`: für Backoffice-Dateien.
>> - `/modules`: für installierte Module.
>> - `/img`: für alle Bilder und Symbole.
>> - `/themes`: für die Dateien des Themes Ihrer Website.
>>
>> Weitere Informationen zur Struktur der PrestaShop-Dateien finden Sie in der [offiziellen technischen Dokumentation](https://docs.prestashop-project.org/welcome).
>>
> Joomla!
>>
>> Für Joomla! umfassen die wichtigen Dateien, die gesichert werden müssen, die folgenden Verzeichnisse:
>>
>> - `/administrator`: für das Verwaltungsinterface.
>> - `/components`, `/plugins`: für installierte Erweiterungen.
>> - `/images`: für die Mediendateien Ihrer Website.
>>
>> Weitere Informationen zur Struktur der Joomla!-Dateien finden Sie in der [offiziellen Joomla!-Dokumentation](https://docs.joomla.org/).
>>
> Drupal
>>
>> Für Drupal sind folgende wichtige Ordner zu sichern:
>>
>> - `/sites`: enthält die für Ihre Site spezifischen Dateien.
>> - `/modules`: und `/themes`: für benutzerdefinierte Module und Designs.
>>
>> Weitere Informationen finden Sie in der [offiziellen Drupal-Dokumentation](https://www.drupal.org/docs).

> [!primary]
>
> Nachdem Sie alle Dateien Ihrer Website heruntergeladen haben, stellen Sie sicher, dass Sie sie in einem leicht identifizierbaren lokalen Ordner ablegen, damit sie leichter auf den VPS übertragen werden können.

#### Schritt 1.3 - Datenbank sichern

> [!PRIMARY]
>
> Wenn Sie bereits eine Web Cloud Database für Ihre Website verwenden, können Sie diese auch ohne Migration weiter verwenden. Ihr VPS stellt eine Verbindung zur Web Cloud Database her, um die Daten zu verwalten.

Wenn Sie vorhaben, die Datenbank auf den VPS zu migrieren, folgen Sie den Schritten in unserer Anleitung „[Backup einer Webhosting-Datenbank exportieren](/pages/web_cloud/web_hosting/sql_database_export)“, um Ihre Datenbank zu sichern.

### Schritt 2 - Ihren VPS konfigurieren <a name="step2"></a>

> [!PRIMARY]
>
> Wenn Sie noch keine VPS haben, besuchen Sie die [VPS-Produktseite von OVHcloud](/links/bare-metal/vps), um einen VPS zu kaufen. Achten Sie darauf, einen VPS zu wählen, der den Anforderungen Ihrer Website in Bezug auf Ressourcen (RAM, CPU, Storage...) und die technischen Spezifikationen Ihres CMS entspricht. Wenn Sie noch nicht mit VPS vertraut sind, lesen Sie unsere Anleitung „[Erste Schritte mit einem VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)“.

#### Schritt 2.1 - Verbindung mit Ihrem VPS

In der Anleitung „[Erste Schritte mit einem VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)“ erfahren Sie, wie Sie sich mit Ihrem VPS verbinden.

#### Schritt 2.2 - Installation und Konfiguration eines Webservers auf Ihrem VPS <a name="step2.2"></a>

Sobald Sie mit Ihrem VPS verbunden sind, installieren und konfigurieren Sie eine Web-Entwicklungsumgebung auf Ihrem VPS. Dieser Schritt ist unbedingt notwendig, um sicherzustellen, dass Ihr Server für die Aufnahme Ihrer Website bereit ist, nachdem die Dateien und die Datenbank übertragen wurden.

Um diese Web-Umgebung zu installieren, lesen Sie unsere Anleitung „[Web-Entwicklungsumgebung auf einem VPS oder Dedicated Server installieren](/pages/bare_metal_cloud/virtual_private_servers/install_env_web_dev_on_vps)“.

### Schritt 3 - Dateien Ihrer Website per SFTP übertragen

Die Verwendung des **S**ecure **F**ile **T**ransfer **P**rotocol (**SFTP**) ist die empfohlene Methode, um Dateien von Ihrer Website auf Ihren VPS zu übertragen. Es bietet ein höheres Sicherheitsniveau als FTP, da die Verschlüsselung durch den SSH-Dienst verwendet wird, der bereits standardmäßig auf Ihrem VPS von OVHcloud aktiviert ist.

#### Schritt 3.1 - Verbindung zu Ihrem VPS per SFTP

Folgen Sie dem Schritt „SFTP-Verbindung herstellen“ in unserer Anleitung „[FileZilla mit Ihrem OVHcloud Hosting nutzen](/pages/web_cloud/web_hosting/ftp_filezilla_user_guide)“ und verwenden Sie die folgende Konfiguration:

- **Host**: Verwenden Sie die IP-Adresse Ihres VPS.
- **Kennung** und **Passwort**: die Kennungen Ihres SSH-Benutzerkontos auf dem VPS.
- **Port**: Verwenden Sie Port 22 (Standard für SFTP).

#### Schritt 3.2 - Dateien von Ihrer Website auf den VPS übertragen

Wenn Sie auf Ihrem VPS eingeloggt sind, wird die Ordnerstruktur der lokalen Dateien links im FileZilla Interface und die Ordnerstruktur Ihres VPS rechts angezeigt.

Wählen Sie die Dateien für Ihre Website und die Datenbank aus, die Sie in [Schritt 1.2](#step1.2) heruntergeladen haben. Ziehen Sie sie in das Webverzeichnis Ihres VPS auf der rechten Seite des Interface. Das Webverzeichnis ist der Ort, an dem die Dateien Ihrer Website gespeichert werden, um im Internet verfügbar zu sein. Standardmäßig kann dies ein Ordner mit dem Namen `/var/www/html` oder ein anderes Verzeichnis sein, das während der Installation des Webservers in [Schritt 2.2](#step2.2) konfiguriert wurde. Stellen Sie sicher, dass Sie die Dateien in dem Ordner ablegen, der als Webstamm konfiguriert ist, damit die Website ordnungsgemäß funktioniert.

### Schritt 4 - Datenbank auf Ihren VPS importieren (optional)

> [!warning]
>
> Wenn Ihre Datenbank bereits auf einem Web Cloud Databases Dienst gehostet ist, muss sie nicht auf den VPS migriert werden. Sie können die Datenbank im Web Cloud Databases Dienst belassen und Ihren VPS so konfigurieren, dass er sich mit dieser Datenbank verbindet ([Schritt 5](#step5)).

Wenn Sie die Datenbank auf Ihren VPS importieren möchten, folgen Sie den nachstehenden Schritten.

Loggen Sie sich via SSH in Ihrem VPS ein, indem Sie den Abschnitt „Mit Ihrem VPS verbinden“ unserer Anleitung „[Erste Schritte mit einem VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)“ lesen.

Wenn Sie via SSH mit Ihrem VPS verbunden sind, verwenden Sie die folgende Befehlszeile, um den Import der Datenbank durchzuführen.

Im folgenden Beispiel verwenden wir MySQL als **D**ata**B**ase **M**anagement **S**ystem (**DBMS**). Verwenden Sie die offizielle DBMS-Dokumentation, die Sie in [Schritt 2.2](#step2.2) installiert haben, um die Datenbank über die entsprechende Befehlszeile in Ihren VPS zu importieren.

```php
<?php
system("mysql -u user_name -p db_name < root/to/file.sql
");
?>
```

Ersetzen Sie `user_name` durch Ihren MySQL-Benutzernamen, `db_name` durch den Namen der zu importierenden Datenbank und `root/to/file.sql` durch den Pfad der gesicherten SQL-Datei.

### Schritt 5 - Konfigurationsdateien Ihrer Website einrichten <a name="step5"></a>

Nachdem Sie die Dateien Ihrer Website hochgeladen und gegebenenfalls die Datenbank auf Ihren VPS importiert haben, ist es wichtig, die Konfigurationsdateien Ihrer Website zu aktualisieren, um deren einwandfreie Funktion sicherzustellen. Die wichtigsten Variablen, die angepasst werden müssen, sind häufig die Datenbankverbindungsinformationen und die Ordnerpfade. Hier sind die spezifischen Konfigurationen, die für die wichtigsten CMS aktualisiert werden müssen.

> [!tabs]
> WordPress
>>
>> Bearbeiten Sie die folgenden Variablen in der Datei `wp-config.php`:
>>
>> - **DB_NAME**: Name der Datenbank.
>> - **DB_USER**: Der Datenbankbenutzer.
>> - **DB_PASSWORD**: Das Passwort des Benutzers.
>> - **DB_HOST**: Der Host der Datenbank (normalerweise localhost auf einem VPS).
>>
>> Weitere Informationen finden Sie in der [offiziellen WordPress-Dokumentation](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/).
>>
>> Weitere Informationen zur Sicherheit finden Sie in der offiziellen Dokumentation zu den [Datei-Berechtigungen für WordPress](https://wordpress.org/support/article/changing-file-permissions/)
>>
> PrestaShop
>>
>> Bearbeiten Sie die folgenden Variablen in der Datei `parameters.php`:
>>
>> - **database_host**: Der Host der Datenbank.
>> - **database_name**: Der Name der Datenbank.
>> - **database_user**: Der Datenbankbenutzer.
>> - **database_password**: Das Datenbankkennwort.
>>
>> Weitere Informationen finden Sie in der [offiziellen PrestaShop-Dokumentation](https://devdocs.prestashop-project.org/8/development/configuration/configuring-prestashop/).
>>
>> Weitere Informationen zur Sicherheit finden Sie in der [offiziellen Dokumentation](https://devdocs.prestashop-project.org/) zu Dateiberechtigungen für PrestaShop.
>>
> Joomla!
>>
>> Bearbeiten Sie die folgenden Variablen in der Datei `configuration.php`:
>>
>> - **public $host**: Der Host der Datenbank (oft localhost).
>> - **public $db**: Der Name der Datenbank.
>> - **public $user**: Der Datenbankbenutzer.
>> - **public $password**: Das Datenbankkennwort.
>>
>> Weitere Informationen finden Sie in der [offiziellen Dokumentation von Joomla!](https://docs.joomla.org/).
>>
>> Weitere Informationen zur Sicherheit finden Sie in der offiziellen Dokumentation zu den [Dateiberechtigungen für Joomla!](https://docs.joomla.org/What_are_the_recommended_file_and_directory_permissions%3F)
>>
> Drupal
>>
>> Bearbeiten Sie die folgenden Variablen in der Datei `settings.php`:
>>
>> - **Host**: Der Host der Datenbank (oft localhost).
>> - **database**: Name der Datenbank.
>> - **username**: Der Datenbankbenutzer.
>> - **password**: Das Passwort der Datenbank.
>>
>> Weitere Informationen finden Sie in der [offiziellen Drupal-Dokumentation](https://www.drupal.org/documentation).
>>
>> Weitere Informationen zur Sicherheit finden Sie in der offiziellen Dokumentation zu den [Dateiberechtigungen für Drupal](https://www.drupal.org/docs/administering-a-drupal-site/security-in-drupal/securing-file-permissions-and-ownership)
>>
> Ohne CMS
>>
>> **1. Datenbankverbindungsinformationen aktualisieren**
>>
>> Identifizieren Sie die Konfigurationsdateien (wie `config.php` oder `.env`). Einige können sich in Unterordnern befinden. Suchen Sie in diesen Dateien nach den Datenbankverbindungseinstellungen, und ändern Sie diese entsprechend den neuen Verbindungswerten des VPS:
>>
>> - **DB_HOST**: Adresse des Datenbankservers.
>> - **DB_NAME**: Name der Datenbank.
>> - **DB_USER**: Datenbankbenutzer.
>> - **DB_PASSWORD**: Passwort.
>>
>> **2. Dateipfade konfigurieren**
>>
>> Einige Websites verwenden absolute Pfade (Beispiel: `/home/user/public_html/`) für bestimmte Dateien oder Ressourcen wie Bilder, CSS-Dateien usw. Stellen Sie sicher, dass diese Pfade der Struktur des Servers auf dem VPS entsprechen, z. B. `/var/www/html/`.
>>
>> Um Fehler beim Laden von Dateien oder fehlerhafte Verknüpfungen zu vermeiden, stellen Sie sicher, dass diese Pfade in allen Konfigurationsdateien, `.htaccess` oder anderen Skripten, die Verknüpfungen zu diesen Ressourcen enthalten, angepasst werden. Dadurch wird sichergestellt, dass die Website auch nach der Migration alle Elemente findet, die für ihr ordnungsgemäßes Funktionieren erforderlich sind.
>>
>> **3. .htaccess-Datei bearbeiten** (optional)
>>
>> Stellen Sie sicher, dass die Datei `.htaccess` für die neue Umgebung konfiguriert ist. Wenn Sie die URLs mithilfe von Rewrite-Regeln (`RewriteRule`) anpassen, überprüfen Sie, ob die Pfade für die Struktur Ihres VPS geeignet sind (Beispiel: `/var/www/html/` anstelle von `/public_html/`). So wird sichergestellt, dass Weiterleitungen und Zugänge reibungslos funktionieren.
>>
>> Wenn die Datei `.htaccess` Zugriffsbeschränkungen oder Sicherheitseinstellungen enthält, z. B. das Deaktivieren der Verzeichnisliste oder die Konfiguration der Zwischenspeicherung, ändern Sie diese Einstellungen entsprechend den Sicherheitseinstellungen und -bedingungen Ihres neuen Servers.
>>
>> **4. Datei- und Ordnerberechtigungen konfigurieren**
>>
>> Stellen Sie sicher, dass die Berechtigungen (z. B. `chmod`) für Dateien und Ordner korrekt konfiguriert sind, um Zugriffsfehler zu vermeiden. Auf einem VPS sind die empfohlenen Berechtigungen oft `755` für Ordner und `644` für Dateien, aber dies kann je nach Ihren Sicherheitsanforderungen variieren.

Wenn Sie eine Web Cloud Databases Datenbank verwenden, überprüfen Sie, ob Ihr VPS sich mit dieser verbinden darf. Fügen Sie hierzu die IP-Adresse des VPS zur Liste der autorisierten IP-Adressen hinzu. Diese Konfiguration erlaubt es, den Zugriff auf die Datenbank abzusichern und Verbindungsprobleme zu vermeiden. Lesen Sie den Abschnitt „Autorisieren einer IP-Adresse“ unserer Anleitung „[Erste Schritte mit Web Cloud Databases](/pages/web_cloud/web_cloud_databases/starting_with_clouddb)“.

### Schritt 6 - Ihren Domainnamen mit der IP-Adresse des VPS verbinden

> [!PRIMARY]
>
> Bevor Sie die Einträge in Ihrer DNS Zone ändern, um auf die IP-Adresse des VPS zu verweisen, wird empfohlen, den **T**ime **T**o **L**ive (**TTL**) zu reduzieren. Dadurch wird die Propagation von Änderungen beschleunigt, da die DNS-Server die Informationen schneller aktualisieren. Folgen Sie dem Schritt „Die Propagationszeit“ unserer Anleitung „[Bearbeiten der OVHcloud DNS-Zone](/pages/web_cloud/domains/dns_zone_edit)“, um die TTL anzupassen und die Einträge so zu konfigurieren, dass die Domain auf den VPS zeigt.

Um den Domainnamen Ihrer Website auf Ihren VPS verweisen zu lassen, konfigurieren Sie die DNS-Einträge der Domain so, dass der Traffic auf die öffentliche IP-Adresse Ihres VPS geleitet wird. Um Sie bei diesem Vorgang zu unterstützen, folgen Sie unserer Anleitung „[Bearbeiten der OVHcloud DNS-Zone](/pages/web_cloud/domains/dns_zone_edit)“.

### Schritt 7 - Funktionstüchtigkeit Ihrer Website überprüfen

Testen Sie nach Abschluss der Migration Ihre Website, um sicherzustellen, dass sie wie erwartet funktioniert. Überprüfen Sie alle wichtigen Funktionen (Formulare, Benutzerverbindungen, Onlinezahlung usw.), und stellen Sie sicher, dass alle Seiten korrekt angezeigt werden.

### Schritt 8 - Ihren VPS absichern

Nachdem Sie Ihre Website auf Ihren VPS migriert haben, ist es entscheidend, Ihren Server zu sichern, um Ihre Daten zu schützen und das reibungslose Funktionieren Ihrer Dienste zu gewährleisten. Hier sind einige Maßnahmen, die Sie ergreifen müssen, um die Sicherheit Ihres VPS zu erhöhen:

- Das von OVHcloud bereitgestellte SSH-Passwort und den Standard-SSH-Zugriffsport ändern.
- Konfigurieren einer Firewall
- Konfigurieren der Zwei-Faktor-Authentifizierung (2FA).
- Die Logs überwachen.
- usw.

Eine vollständige Liste der bewährten Sicherheitspraktiken finden Sie in unserer Anleitung „[Einen VPS absichern](/pages/bare_metal_cloud/virtual_private_servers/secure_your_vps)“.

## Weiterführende Informationen <a name="go-further"></a>
 
Kontaktieren Sie für spezialisierte Dienstleistungen (SEO, Web-Entwicklung etc.) die [OVHcloud Partner](/links/partner).
 
Treten Sie unserer [User Community](/links/community) bei.