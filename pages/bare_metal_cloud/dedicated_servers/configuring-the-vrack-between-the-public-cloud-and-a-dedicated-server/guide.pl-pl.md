---
title: 'Konfiguracja sieci vRack między Public Cloud a serwerem dedykowanym'
excerpt: 'Dowiedz się, jak skonfigurować prywatną sieć między instancją Public Cloud a serwerem dedykowanym'
updated: 2024-11-07
---

> [!primary]
> Tłumaczenie zostało wygenerowane automatycznie przez system naszego partnera SYSTRAN. W niektórych przypadkach mogą wystąpić nieprecyzyjne sformułowania, na przykład w tłumaczeniu nazw przycisków lub szczegółów technicznych. W przypadku jakichkolwiek wątpliwości zalecamy zapoznanie się z angielską/francuską wersją przewodnika. Jeśli chcesz przyczynić się do ulepszenia tłumaczenia, kliknij przycisk "Zgłóś propozycję modyfikacji" na tej stronie.
>

## Wprowadzenie

[vRack](/links/network/vrack) OVHcloud to prywatna sieć, która umożliwia konfigurację adresowania między dwoma lub kilkoma [Serwerami dedykowanymi](/links/bare-metal/bare-metal) OVHcloud. Umożliwia ponadto dodawanie [instancji Public Cloud](https://www.ovhcloud.com/pl/public-cloud/) do Twojej prywatnej sieci w celu utworzenia infrastruktury z zasobów fizycznych i wirtualnych.

**Niniejszy przewodnik wyjaśnia, jak skonfigurować sieć prywatną między [instancją Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps) a [serwerem dedykowanym](/links/bare-metal/bare-metal).**

## Wymagania początkowe

* Utworzenie [instancji Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps)
* Aktywowanie usługi [vRack](/links/network/vrack)
* Posiadanie [serwera dedykowanego](/links/bare-metal/bare-metal) kompatybilnego z usługą vRack
* Dostęp do [Panelu klienta OVHcloud](/links/manager)
* Wybrany zakres prywatnych adresów IP

> [!warning]
> Funkcja ta może być niedostępna lub ograniczona na [serwerach dedykowanych **Eco**](https://eco.ovhcloud.com/pl/about/).
>
> Aby uzyskać więcej informacji, zapoznaj się z naszym [porównaniem](https://eco.ovhcloud.com/pl/compare/).


## W praktyce

### Dodaj projekt Public Cloud do sieci vRack

> [!primary]
> Nie dotyczy to nowo utworzonych projektów, które są automatycznie dostarczane z siecią vRack. Aby wyświetlić sieć vRack po utworzeniu projektu, przejdź do menu `Bare Metal Cloud`{.action} i kliknij `Network`{.action} w zakładce po lewej stronie. Kliknij opcję `Prywatna sieć vRack`{.action}, aby wyświetlić sieć(e) vRack(s).
>
> Możesz również usunąć przypisany projekt z sieci vRack i przypisać go do innej sieci vRack, jeśli chcesz, zwłaszcza jeśli posiadasz już istniejący vRack na swoim (swoich) serwerze(ach) dedykowanym(ych).

W przypadku starszych projektów, po zamówieniu usługi [vRack](/links/network/vrack) przejdź do menu `Bare Metal Cloud`{.action}, kliknij `Network`{.action} w zakładce po lewej stronie, a następnie kliknij `Private Network`vRack`{.action}. Wybierz vRack z listy.

Na liście dostępnych usług zaznacz projekt, który chcesz dodać do szafy vRack, następnie kliknij przycisk `Dodaj`{.action}.

![Dodaj projekt do sieci vRack](images/addprojectvrack.png){.thumbnail}

### Zintegruj instancję z usługą vRack

Mogą wystąpić dwie sytuacje:

- Instancja jeszcze nie istnieje.
- Instancja już istnieje i należy ją dodać do sieci vRack.

#### Przypadki nowej instancji

Jeśli potrzebujesz pomocy, zapoznaj się z przewodnikiem [Tworzenie instancji Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps). Podczas tworzenia instancji możesz w etapie 5 określić sieć prywatną, do której chcesz zintegrować Twoją instancję.

#### Przypadki istniejącej instancji

Istniejącą instancję można powiązać z siecią prywatną.

Dzięki projektowi vRack możesz tworzyć prywatne sieci.

W karcie Public Cloud kliknij `Private Network`{.action} w menu po lewej stronie, pod **Network**.

Kliknij przycisk `Utwórz prywatną sieć`{.action}.

![create private network](images/vrack2022-03.png){.thumbnail}

Na następnej stronie możesz spersonalizować wiele ustawień.

W etapie 1 wybierz regiony, w którym chcesz umieścić sieć prywatną.

![select region](images/vrack2024-01.png){.thumbnail}

Aby obie usługi mogły się ze sobą komunikować, muszą mieć "tagi" tego samego **VLAN ID**.

Można go skonfigurować w etapie 2.

![configure network](images/configure_private_network.png){.thumbnail}

Ten etap oferuje kilka opcji konfiguracji. Na potrzeby tego przewodnika skupimy się na niezbędnych elementach. Kliknij poniższe zakładki, aby wyświetlić szczegółowe informacje:

> [!tabs]
> **Nazwa sieci prywatnej**
>>
>> Wprowadź nazwę sieci prywatnej.<br>
>>
> **Opcje sieciowe warstwy 2**
>>
>> Domyślnie VLAN ID dla serwerów dedykowanych to **0**. Aby użyć tego identyfikatora VLAN dla instancji, konieczne będzie oznaczenie prywatnej sieci VLAN **0** również.
>> Zaznacz pole wyboru **Set a VLAN ID** i wybierz VLAN ID **0**.
>>
>> Jeśli nie zaznaczysz tego pola, system przypisze losowy numer identyfikacyjny VLAN do Twojej prywatnej sieci.
>>
> **Korzystanie z innego identyfikatora VLAN**
>>
>> Jeśli nie zamierzasz korzystać z VLAN ID **0**, możesz wybrać inny identyfikator z zakresu od 1 do 4000. Stosuje się następujące zasady:
>>
>> - Sieć prywatna powiązana z instancją Public Cloud musi być "oznaczona" tym identyfikatorem VLAN.
>> - Podczas konfigurowania sieci vRack na serwerze dedykowanym, ten identyfikator sieci VLAN musi być zawarty w pliku konfiguracji sieci.
>>
>> [!primary]
>> W przypadku usługi Public Cloud definiujesz pojedynczy VLAN ID dla każdej sieci prywatnej. Nie można ustawić tego samego VLAN ID w dwóch różnych sieciach prywatnych.
>>
>> [!primary]
>> W przeciwieństwie do serwerów dedykowanych (gdy używany jest VLAN ID inny niż 0), nie jest konieczne bezpośrednie uwzględnianie VLAN ID w pliku konfiguracji sieci instancji Public Cloud po jego skonfigurowaniu w Panelu klienta OVHcloud.
>>
>> Przykład: jeśli prywatna sieć instancji jest "oznaczona" VLAN 2, ten VLAN ID musi być zawarty w konfiguracji sieci tylko serwera dedykowanego. Więcej informacji znajdziesz w przewodniku: [Tworzenie wielu sieci VLAN w sieci vRack](/pages/bare_metal_cloud/dedicated_servers/creating-multiple-vlan-in-a-vrack).<br>
>>
> **Opcje dystrybucji adresów DHCP**
>>
>> Możesz zachować domyślny zakres prywatnych adresów IP lub użyć innego zakresu.
>>

Po zakończeniu konfiguracji kliknij przycisk `Utwórz`{.action}. Może to potrwać kilka minut.

W dashboardzie odpowiedniej instancji kliknij przycisk `...`{.action} w polu "Siec" obok "Prywatna(e) sieć(-i)" i wybierz `Przypisz sieć`{.action}.

![attach network](images/vrack2021-01.png){.thumbnail}

W oknie, które się pojawi, wybierz prywatną sieć lub sieci, które chcesz przypisać do swojej instancji i kliknij przycisk `Przypisz`{.action}.

![attach network](images/attach_network.png){.thumbnail}

### Konfiguracja interfejsów sieciowych

Następnie, przy użyciu tego przewodnika, skonfiguruj interfejsy sieciowe na nowej instancji Public Cloud i serwerze dedykowanym: [Konfiguracja kilku serwerów dedykowanych w sieci vRack](/pages/bare_metal_cloud/dedicated_servers/vrack_configuing_on_dedicated_server).

## Sprawdź również

Przyłącz się do społeczności naszych użytkowników na stronie <https://community.ovh.com/en/>.