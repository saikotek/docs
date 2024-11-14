---
title: "Jak migrować stronę WWW z hostingu na serwer VPS"
excerpt: "Dowiedz się, jak przenieść Twoją stronę WWW z hostingu na serwer VPS OVHcloud"
updated: 2024-11-06
---

## Wprowadzenie

Twoja strona WWW zmienia się, a zużycie zasobów zmienia się w taki sposób, że hosting nie odpowiada już Twoim potrzebom w zakresie wydajności lub możliwości przetwarzania bardziej złożonych zadań. Przejście na VPS pozwala na zwiększenie szybkości i responsywności strony www, na zwiększenie dostępnych zasobów obliczeniowych (CPU, RAM, itp.) i na uzyskanie większej kontroli nad środowiskiem serwerowym. Niniejszy przewodnik opisuje kluczowe etapy migracji i zachowania ciągłości działania serwera VPS.

**Dowiedz się, jak przenieść Twoją stronę WWW z hostingu na serwer VPS.**

## Wymagania początkowe

- Posiadanie aktywnego [hostingu](/links/web/hosting).
- Wykupienie usługi [VPS](/links/bare-metal/vps) na Twoim koncie OVHcloud.
- Dostęp do [panelu klienta OVHcloud](/links/manager).

## W praktyce

> [!warning]
>
> OVHcloud udostępnia różnorodne usługi, jednak to Ty odpowiadasz za ich konfigurację i zarządzanie nimi. Ponosisz więc odpowiedzialność za ich prawidłowe funkcjonowanie.
>
> Oddajemy w Twoje ręce niniejszy przewodnik, którego celem jest pomoc w jak najbardziej optymalnym wykonywaniu bieżących zadań. Jednak w przypadku trudności zalecamy skontaktowanie się z [wyspecjalizowanym dostawcą](/links/partner). Niestety firma OVH nie jest w stanie udzielić Ci wsparcia w tym zakresie. Więcej informacji znajduje się w sekcji ["Sprawdź również"](#go-further) niniejszego przewodnika.
>

### Etap 1 - Wykonaj kopię zapasową plików i bazy danych Twojej strony WWW <a name="step1"></a>

Pierwszy etap polega na wykonaniu kopii zapasowej wszystkich plików Twojej strony WWW, zazwyczaj w dniu **F**ile **T**ransfer **P**rotocol (**FTP**), wraz z bazą danych.

Jeśli korzystasz z modułu WordPress, zapoznaj się z naszym przewodnikiem "[Zapisz stronę WWW z modułem WordPress](/pages/web_cloud/web_hosting/how_to_backup_your_wordpress)", aby dowiedzieć się, jak utworzyć kopię zapasową plików i bazy danych Twojej strony WWW WordPress, a następnie przejdź do [etapu 2](#step2).

#### Etap 1.1 - Logowanie do przestrzeni dyskowej FTP Twojego hostingu

Postępuj zgodnie z kolejnymi instrukcjami zawartymi w przewodniku "[Logowanie do przestrzeni dyskowej FTP hostingu](/pages/web_cloud/web_hosting/ftp_connection)", aby zalogować się do przestrzeni dyskowej FTP Twojego hostingu.

#### Etap 1.2 - Wykonaj kopię zapasową plików przez FTP <a name="step1.2"></a>

Jeśli nie korzystasz z CMS-a (WordPress, Joomla!, Drupal, PrestaShop, etc.), pobierz lokalnie pełną kopię zapasową wszystkich plików z przestrzeni FTP na swoje urządzenie. Obejmuje to wszystkie pliki HTML, CSS, JavaScript, obrazy i pliki konfiguracyjne (`config.php`,`.env`, etc.), które tworzą Twoją stronę WWW. Upewnij się, że odzyskasz wszystkie katalogi i pliki z katalogu głównego (często o nazwie `public_html` lub `www`), aby wszystkie treści niezbędne do działania Twojej strony zostały zapisane na potrzeby migracji.

Jeśli używasz CMS-a do zapisywania plików, wybierz odpowiednią dla niego metodę tworzenia kopii zapasowych i kliknij wybraną zakładkę.

> [!tabs]
> PrestaShop
>>
>> W przypadku PrestaShop wykonaj kopie zapasowe krytycznych katalogów, takich jak:
>>
>> -`/admin`: dla plików związanych z back-office.
>> -`/modules`: dla zainstalowanych modułów.
>> -`/img`: dla wszystkich obrazów i ikon.
>> -`/themes` : dla plików motywu twojej strony.
>>
>> Aby uzyskać więcej informacji na temat struktury plików PrestaShop, sprawdź ich [oficjalną dokumentację techniczną](https://docs.prestashop-project.org/welcome).
>>
> Joomla!
>>
>> Dla modułu Joomla! ważne pliki, których kopię zapasową chcesz wykonać, obejmują katalogi:
>>
>> -`/administrator`: dla interfejsu administracyjnego.
>> -`/components`,`/plugins` : dla zainstalowanych rozszerzeń.
>> -`/images`: dla plików multimedialnych twojej strony.
>>
>> Więcej informacji na temat struktury plików Joomla! znajdziesz w [oficjalnej dokumentacji Joomla!](https://docs.joomla.org/).
>>
> Drupal
>>
>> Dla Drupala, ważne katalogi do skopiowania to:
>>
>> -`/sites`: która zawiera pliki specyficzne dla twojej strony.
>> -`/modules`: et`/themes`: pour les modules et themes Personalised.
>>
>> Więcej informacji znajdziesz w [oficjalnej dokumentacji Drupal](https://www.drupal.org/docs).

> [!primary]
>
> Po pobraniu wszystkich plików z Twojej strony WWW, zapisz je w łatwo rozpoznawalnym folderze lokalnym, co ułatwi ich późniejszy transfer na serwer VPS.

#### Etap 1.3 - Wykonaj kopię zapasową bazy danych

> [!primary]
>
> Jeśli używasz już bazy danych Web Cloud Database dla Twojej strony WWW, możesz nadal z niej korzystać bez jej przenoszenia. Twój VPS połączy się z bazą danych Web Cloud Database, aby zarządzać danymi.

Jeśli planujesz przeniesienie bazy danych na serwer VPS, wykonaj kolejne kroki opisane w przewodniku "[Tworzenie i pobieranie kopii zapasowej bazy danych na hostingu WWW](/pages/web_cloud/web_hosting/sql_database_export)", aby wykonać kopię zapasową bazy danych.

### Etap 2 - Konfiguracja serwera VPS <a name="step2"></a>

> [!primary]
>
> Jeśli nie posiadasz jeszcze serwera VPS, zapoznaj się z [stroną produktu VPS OVHcloud](/links/bare-metal/vps), aby zamówić VPS. Upewnij się, czy wybierasz VPS odpowiadający potrzebom Twojej strony WWW w zakresie zasobów (RAM, CPU, przestrzeń dyskowa, itp.) oraz specyfikacji technicznej CMS. Jeśli nie jesteś zaznajomiony z serwerami VPS, zapoznaj się z naszym przewodnikiem "[Pierwsze kroki z serwerem VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)".

#### Etap 2.1 - Logowanie do serwera VPS

Przejdź do sekcji "Logowanie do serwera VPS" w naszym przewodniku "[Pierwsze kroki z serwerem VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)", aby zalogować się do serwera VPS.

#### Etap 2.2 - Instalacja i konfiguracja serwera www na serwerze VPS <a name="step2.2"></a>

Po połączeniu z VPS, zainstaluj i skonfiguruj na serwerze VPS środowisko programistyczne. Jest to niezbędne do zapewnienia, aby serwer był gotowy na zainstalowanie Twojej strony WWW po zakończeniu transferu plików i bazy danych.

Aby zainstalować to środowisko internetowe, zapoznaj się z naszym przewodnikiem "[Instalowanie środowiska programistycznego na serwerze VPS lub serwerze dedykowanym](/pages/bare_metal_cloud/virtual_private_servers/install_env_web_dev_on_vps)".

### Etap 3 - Przesyłanie plików z Twojej strony WWW przez SFTP

Użyj **S**ecure **F**ile **T**ransfer **P**rotocol (**SFTP**) jest zalecaną metodą przesyłania plików z Twojej strony www na Twój serwer VPS. Zapewnia on wyższy poziom bezpieczeństwa niż FTP, dzięki szyfrowaniu dostarczanemu przez usługę SSH, która została już domyślnie włączona na Twoim serwerze VPS OVHcloud.

#### Etap 3.1 - Logowanie do serwera VPS za pomocą SFTP

Postępuj zgodnie z etapem "Uruchom połączenie SFTP" w naszym przewodniku "[Korzystanie z FileZilla na Twoim hostingu OVHcloud](/pages/web_cloud/web_hosting/ftp_filezilla_user_guide)" przy użyciu następującej konfiguracji:

- **Host** : użyj adresu IP serwera VPS.
- **Identyfikator** i **hasło** : hasło do konta użytkownika SSH na serwerze VPS.
- **Port** : użyj portu 22 (domyślny port SFTP).

#### Etap 3.2 - Przeniesienie plików z Twojej strony WWW na serwer VPS

Po zalogowaniu się do VPS, po lewej stronie ekranu FileZilla zostanie wyświetlone drzewo plików lokalnych, a po prawej stronie drzewo plików Twojego serwera VPS.

Wybierz pliki strony WWW i bazę danych, które pobrałeś w trakcie [etap 1.2](#step1.2). Przeciągnij je do katalogu www serwera VPS po prawej stronie interfejsu. Katalog WWW to miejsce, w którym przechowywane będą pliki Twojej strony WWW, umożliwiające do niej dostęp przez Internet. Domyślnie może to być folder o nazwie`/var/www/html` lub inny katalog skonfigurowany podczas instalacji serwera www podczas [etap 2.2](#step2.2). Upewnij się, że umieszczasz pliki w folderze skonfigurowanym jako katalog główny sieci Web, aby Twoja witryna działała poprawnie.

### Etap 4 - Import bazy danych na serwer VPS (opcjonalnie)

> [!warning]
>
> Jeśli baza danych jest już hostowana w ramach usługi Web Cloud Databases, nie musisz migrować jej na VPS. Możesz zachować bazę danych w usłudze Web Cloud Databases i skonfigurować serwer VPS, aby łączył się z tą bazą danych ([etap 5](#step5)).

Jeśli chcesz importować bazę danych na Twój serwer VPS, wykonaj poniższe kroki.

Zaloguj się do serwera VPS przez SSH i zapoznaj się z sekcją "Logowanie do serwera VPS" w naszym przewodniku "[Pierwsze kroki z serwerem VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps)".

Po połączeniu się z Twoim serwerem VPS za pomocą SSH skorzystaj z poniższego wiersza poleceń, aby wykonać import bazy danych.

W poniższym przykładzie używamy MySQL jako **D**ata**B**ase **M**anagement **S**ystem (**DBMS**). Skorzystaj z oficjalnej dokumentacji systemu zarządzania bazą danych, który zainstalowałeś podczas [etap 2.2](#step2.2), aby zaimportować bazę danych na serwer VPS za pomocą wiersza poleceń.

```php
<?php
system("mysql -u user_name -p db_name < root/to/file.sql
");
?>
```

Zmień `user_name` na nazwę użytkownika MySQL, `db_name` na nazwę bazy danych do zaimportowania, oraz `root/to/file.sql` na ścieżkę do zapisanego pliku SQL.

### Etap 5 - Ustaw pliki konfiguracyjne Twojej strony WWW <a name="step5"></a>

Po przesłaniu plików Twojej strony WWW i, w stosownych przypadkach, zaimportowaniu bazy danych do Twojego serwera VPS, ważne jest, abyś zaktualizował pliki konfiguracyjne Twojej strony WWW, aby zapewnić jej prawidłowe funkcjonowanie. Głównymi zmiennymi, które należy dostosować, są często informacje o połączeniach z bazą danych, a także ścieżki dostępu do folderów. Poniżej przedstawiamy konkretne konfiguracje, które należy zaktualizować dla najpopularniejszych systemów CMS.

> [!tabs]
> WordPress
>>
>> Zmień następujące zmienne w pliku `wp-config.php`:
>>
>> - **DB_NAME**: nazwa bazy danych.
>> - **DB_USER**: użytkownik bazy danych.
>> - **DB_PASSWORD**: hasło użytkownika.
>> - **DB_HOST**: host bazy danych (zazwyczaj localhost na serwerze VPS).
>>
>> Aby uzyskać więcej informacji, zapoznaj się z [oficjalną dokumentacją WordPress](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/).
>>
>> Aby uniknąć problemów z zabezpieczeniami, zapoznaj się z oficjalną dokumentacją dotyczącą [uprawnień plików dla WordPressa](https://wordpress.org/support/article/changing-file-permissions/)
>>
> PrestaShop
>>
>> Zmień następujące zmienne w pliku `parameters.php`:
>>
>> - **database_host**: host bazy danych.
>> - **database_name**: nazwa bazy danych.
>> - **database_user**: użytkownik bazy danych.
>> - **database_password**: hasło do bazy danych.
>>
>> Więcej informacji znajdziesz w [oficjalnej dokumentacji PrestaShop](https://devdocs.prestashop-project.org/8/development/configuration/configuring-prestashop/).
>>
>> Aby uniknąć problemów z zabezpieczeniami, zapoznaj się z [oficjalną dokumentacją](https://devdocs.prestashop-project.org/) dotyczącą uprawnień plików dla PrestaShop.
>>
> Joomla!
>>
>> Zmień następujące zmienne w pliku `configuration.php`:
>>
>> - **public $host**: host bazy danych (często localhost).
>> - **public $db**: nazwa bazy danych.
>> - **public $user**: użytkownik bazy danych.
>> - **public $password**: hasło do bazy danych.
>>
>> Więcej informacji można znaleźć w [oficjalnej dokumentacji Joomla!](https://docs.joomla.org/).
>>
>> Aby uniknąć problemów z zabezpieczeniami, zapoznaj się z oficjalną dokumentacją dotyczącą [uprawnień plików dla Joomla!](https://docs.joomla.org/What_are_the_recommended_file_and_directory_permissions%3F)
>>
> Drupal
>>
>> Zmień następujące zmienne w pliku `settings.php`:
>>
>> - **host**: Host bazy danych (często LocalHost).
>> - **database**: nazwa bazy danych.
>> - **username**: użytkownik bazy danych.
>> - **password**: hasło do bazy danych.
>>
>> Więcej informacji można znaleźć w [oficjalnej dokumentacji Drupal](https://www.drupal.org/documentation).
>>
>> Aby uniknąć problemów z zabezpieczeniami, zapoznaj się z oficjalną dokumentacją dotyczącą [uprawnień plików dla Drupal](https://www.drupal.org/docs/administering-a-drupal-site/security-in-drupal/securing-file-permissions-and-ownership)
>>
> Bez CMS
>>
>> **1. Aktualizuj informacje o połączeniu z bazą danych**
>>
>> Znajdź pliki konfiguracyjne (jak `config.php` lub`.env`). Niektóre z nich mogą znajdować się w podfolderach. Znajdź w tych plikach ustawienia połączenia z bazą danych i zmień je zgodnie z nowymi wartościami połączenia na serwerze VPS:
>>
>> - **DB_HOST**: adres serwera bazy danych.
>> - **DB_NAME**: nazwa bazy danych.
>> - **DB_USER**: użytkownik bazy danych.
>> - **DB_PASSWORD**: hasło.
>>
>> **2. Konfiguruj ścieżki plików**
>>
>> Niektóre strony WWW używają ścieżek bezwzględnych (np.:`/home/user/public_html/`) dla określonych plików lub zasobów, takich jak obrazy, pliki CSS, etc. Sprawdź, czy ścieżki te są odpowiednio dostosowane do struktury serwera na serwerze VPS, np.`/var/www/html/`.
>>
>> Aby uniknąć błędów podczas wczytywania plików lub zerwanych łączy, upewnij się, że ścieżki zostały dostosowane we wszystkich plikach konfiguracyjnych,`.htaccess` i innych skryptach zawierających łącza do tych zasobów. Dzięki temu strona WWW może poprawnie odnaleźć wszystkie elementy niezbędne do prawidłowego działania nawet po migracji.
>>
>> **3. Edytuj plik .htaccess** (opcjonalnie)
>>
>> Upewnij się, że plik` htaccess` jest poprawnie skonfigurowany dla nowego środowiska. Jeśli używasz reguł przepisywania (`RewriteRule`) do personalizacji adresów URL, sprawdź, czy ścieżki są dostosowane do struktury serwera VPS (przykład:`/var/www/html/` zamiast`/public_html/`). Dzięki temu przekierowania i dostępy działają prawidłowo.
>>
>> Jeśli plik`.htaccess` zawiera ograniczenia dostępu lub ustawienia zabezpieczeń, takie jak wyłączenie listy katalogów lub ustawienie pamięci podręcznej, zmień te ustawienia tak, aby były zgodne z konfiguracjami i zabezpieczeniami Twojego nowego serwera.
>>
>> **4. Konfigurowanie uprawnień plików i folderów**
>>
>> Upewnij się, że uprawnienia (na przykład: `chmod`) plików i folderów są skonfigurowane poprawnie, aby uniknąć błędów dostępu. Na serwerze VPS zalecane uprawnienia to często `755` dla katalogów i `644` dla plików, ale może się różnić w zależności od potrzeb w zakresie bezpieczeństwa.

Jeśli korzystasz z bazy danych Web Cloud Databases, sprawdź, czy Twój VPS ma uprawnienia do łączenia się z nią. W tym celu dodaj adres IP serwera VPS do listy dozwolonych adresów IP. Zabezpiecza to dostęp do bazy danych i pozwala uniknąć problemów z połączeniem. Zapoznaj się z sekcją "Autoryzacja adresu IP" naszego przewodnika "[Pierwsze kroki z usługą Web Cloud Databases](/pages/web_cloud/web_cloud_databases/starting_with_clouddb)".

### Etap 6 - Przypisz domenę do adresu IP serwera VPS

> [!primary]
>
> Przed zmianą rekordów strefy DNS tak, aby wskazywały na adres IP serwera VPS, zaleca się zmniejszenie wartości **T**ime **T**o **L**ive (**TTL**). Przyspieszy to propagację zmian, ponieważ serwery DNS będą szybciej aktualizować informacje. Aby dostosować TTL i skonfigurować rekordy tak, aby wskazywały na serwer VPS, postępuj zgodnie z etapem "Czas propagacji" opisanym w przewodniku "[Modyfikacja strefy DNS](/pages/web_cloud/domains/dns_zone_edit)".

Aby przekierować domenę Twojej strony WWW na Twój serwer VPS, skonfiguruj wpisy DNS domeny tak, aby kierowały ruch na publiczny adres IP Twojego serwera VPS. Zapoznaj się z przewodnikiem "[Modyfikacja strefy DNS](/pages/web_cloud/domains/dns_zone_edit)".

### Etap 7 - Sprawdzenie prawidłowego działania Twojej strony WWW

Po zakończeniu migracji przetestuj Twoją stronę WWW, aby upewnić się, że działa zgodnie z oczekiwaniami. Sprawdź wszystkie najważniejsze funkcje (formularze, połączenia użytkowników, płatności online, itp.) i upewnij się, że wszystkie strony wyświetlają się poprawnie.

### Etap 8 - Zabezpieczenie serwera VPS

Po przeniesieniu strony WWW na Twój VPS, zabezpieczenie serwera jest kluczowe, aby chronić dane i zagwarantować prawidłowe działanie usług. Poniżej przedstawiamy kilka kroków, które należy podjąć, aby zwiększyć bezpieczeństwo Twojego serwera VPS:

- Zmiana domyślnego hasła SSH i portu dostępu SSH dostarczanych przez OVHcloud.
- Konfiguracja zapory sieciowej.
- Konfiguracja weryfikacji dwuetapowej (2FA).
- Monitorowanie logów.
- Itp.

Pełna lista dobrych praktyk bezpieczeństwa znajduje się w przewodniku "[Zabezpieczenie serwera VPS](/pages/bare_metal_cloud/virtual_private_servers/secure_your_vps)".

## Sprawdź również <a name="go-further"></a>
 
W przypadku wyspecjalizowanych usług (pozycjonowanie, rozwój, etc.) skontaktuj się z [partnerami OVHcloud](/links/partner).
 
Dołącz do [grona naszych użytkowników](/links/community).