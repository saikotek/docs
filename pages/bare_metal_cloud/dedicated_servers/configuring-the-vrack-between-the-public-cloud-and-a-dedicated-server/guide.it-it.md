---
title: 'Configurare la vRack tra un’istanza Public Cloud e un server dedicato'
excerpt: 'Scopri come configurare una rete privata tra un’istanza Public Cloud e un server dedicato'
updated: 2024-11-08
---

## Obiettivo

La [vRack](/links/network/vrack) OVHcloud è una rete privata che permette di configurare l'indirizzamento tra due o più [Server dedicati](/links/bare-metal/bare-metal) OVHcloud. ma permette anche di aggiungere [istanze Public Cloud](/links/public-cloud/compute) alla rete privata per creare un’infrastruttura di risorse fisiche e virtuali.

**Questa guida ti mostra come configurare una rete privata tra un’ [istanza Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps) e un [Server dedicato](/links/bare-metal/bare-metal).**
## Prerequisiti

* Aver creato un' [istanza Public Cloud OVHcloud](/pages/public_cloud/compute/public-cloud-first-steps)
* Aver attivato un servizio [vRack](/links/network/vrack)
* Disporre di un [server dedicato](/links/bare-metal/bare-metal) compatibile con la vRack
* Avere accesso allo [Spazio Cliente OVHcloud](/links/manager)
* Una gamma di indirizzi IP privati di tua scelta

> [!warning]
> Questa funzionalità potrebbe non essere disponibile o essere limitata sui [server dedicati **Eco**](/links/bare-metal/eco-about).
>
> Consulta la nostra [pagina comparativa](/links/bare-metal/eco-compare) per maggiori informazioni.

## Procedura

### Aggiungere un progetto Public Cloud alla vRack

> [!primary]
> Questo non si applica ai progetti appena creati che vengono consegnati automaticamente con una vRack. Per visualizzare la vRack dopo aver creato il progetto, clicca sul menu `Bare Metal Cloud`{.action} e poi su `Network`{.action} nella scheda a sinistra. Clicca su `Rete Privata vRack`{.action} per visualizzare le vRack.
>
> Puoi anche ritirare il progetto dalla vRack che gli è stata assegnata e associarlo a un'altra vRack se lo desideri, in particolare se disponi già di una vRack esistente con il tuo o i tuoi server dedicati.

Per i progetti meno recenti, una volta ordinata la [vRack](/links/network/vrack), accedi al menu `Bare Metal Cloud`{.action}, clicca su `Network`{.action} nella scheda a sinistra e poi su `Rete Privata vRack`{.action}. Seleziona la tua vRack nella lista.

Nella lista dei servizi compatibili, seleziona il progetto che vuoi aggiungere alla vRack, poi clicca sul pulsante `Aggiungi`{.action}.

![aggiungere un progetto alla vrack](images/addprojectvrack.png){.thumbnail}

### Integrare un'istanza nella vRack

Le potrebbero presentarsi due situazioni:

- L'istanza non esiste ancora.
- l’istanza esiste già e sarà necessario aggiungerla alla vRack.

#### Caso di una nuova istanza

Per maggiori informazioni, consulta la guida [Creare un'istanza Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps). Durante la creazione di un’istanza, allo Step 5 è possibile specificare una rete privata in cui integrare l’istanza.

#### Caso di un'istanza esistente

È possibile associare un'istanza esistente a una rete privata.

Con il tuo progetto legato alla vRack, sei pronto a creare reti private.

Nella scheda Public Cloud, clicca su `Private Network`{.action} nel menu di sinistra sotto **Network**.

Clicca sul pulsante `Aggiungi una rete privata`{.action}.

![create private network](images/vrack2022-03.png){.thumbnail}

Nella pagina successiva è possibile personalizzare diverse impostazioni.

Nel passo 1, seleziona la Region in cui vuoi inserire la rete privata.

![select region](images/vrack2024-01.png){.thumbnail}

Per poter comunicare tra loro, i due servizi devono essere "taggati" con lo stesso **VLAN ID**.

Questo può essere configurato allo Step 2.

![configure network](images/configure_private_network.png){.thumbnail}

Questo step offre diverse opzioni di configurazione. Ai fini di questa guida, ci concentreremo sugli elementi necessari. Fare clic sulle schede seguenti per visualizzare i dettagli:

> [!tabs]
> **Nome della rete privata**
>>
>> Immettere un nome per la rete privata.<br>
>>
> **Opzioni di rete del layer 2**
>>
>> Di default, il VLAN ID dei server dedicati è **0**. Per utilizzare questo VLAN ID per un’istanza, è necessario contrassegnare la rete privata con la VLAN **0**.
>> Selezionare la casella **Set a VLAN ID** e selezionare VLAN ID **0**.
>>
>> Se non si seleziona la casella, il sistema assegnerà un numero di identificazione VLAN casuale alla rete privata.
>>
> **Utilizzo di un VLAN ID diverso**
>>
>> Se non si intende utilizzare l'ID VLAN **0**, è possibile selezionare un ID diverso compreso tra 1 e 4000. Si applicano le seguenti regole:
>>
>> - La rete privata associata all’istanza Public Cloud deve essere "taggata" con questo identificativo della VLAN.
>> - Durante la configurazione della vRack sul server dedicato, questa VLAN ID deve essere inclusa nel file di configurazione di rete.
>>
>> > [!primary]
>> > Per il Public Cloud, definisci un VLAN ID unico per ogni rete privata. Non è possibile definire lo stesso VLAN ID su due reti private diverse.
>>
>> > [!primary]
>> > A differenza dei server dedicati (quando si utilizza un VLAN ID diverso da 0), non è necessario includere direttamente il VLAN ID nel file di configurazione di rete dell'istanza Public Cloud una volta che è stato impostato nello Spazio Cliente OVHcloud.
>>
>> Esempio: se la tua rete privata di istanza è "taggata" con la VLAN 2, questo VLAN ID deve essere incluso solo nella configurazione di rete del server dedicato. Per maggiori informazioni, consulta questa guida: [Creare diverse VLAN nella vRack](/pages/bare_metal_cloud/dedicated_servers/creating-multiple-vlan-in-a-vrack).<br>
>>
> **Opzioni DHCP di distribuzione degli indirizzi**
>>
>> È possibile mantenere la classe IP privata di default o utilizzarne un'altra.
>>

Una volta terminata la configurazione, clicca su `Crea`{.action}. Questa operazione potrebbe richiedere alcuni minuti.

Nella dashboard dell’istanza corrispondente, clicca sul pulsante `...`{.action} nella casella "Reti", accanto a "Reti private" e seleziona `Associa una rete`{.action}.

![attach network](images/vrack2021-01.png){.thumbnail}

Nella nuova finestra, seleziona le reti private da associare all’istanza e clicca su `Associa`{.action}.

![attach network](images/attach_network.png){.thumbnail}

### Configura le interfacce di rete

Per configurare le interfacce di rete sulla nuova istanza Public Cloud e sul server dedicato, utilizza questa guida: [Configura più server dedicati nella vRack](/pages/bare_metal_cloud/dedicated_servers/vrack_configuring_on_dedicated_server).

## Per saperne di più

Contatta la nostra [Community di utenti](/links/community).