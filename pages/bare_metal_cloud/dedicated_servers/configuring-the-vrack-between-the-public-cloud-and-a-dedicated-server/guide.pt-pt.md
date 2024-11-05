---
title: 'Configurar o vRack entre o Public Cloud e um servidor dedicado'
excerpt: 'Saiba como configurar uma rede privada entre uma instância Public Cloud e um servidor dedicado'
updated: 2024-11-05
---

> [!primary]
> Esta tradução foi automaticamente gerada pelo nosso parceiro SYSTRAN. Em certos casos, poderão ocorrer formulações imprecisas, como por exemplo nomes de botões ou detalhes técnicos. Recomendamos que consulte a versão inglesa ou francesa do manual, caso tenha alguma dúvida. Se nos quiser ajudar a melhorar esta tradução, clique em "Contribuir" nesta página.
>

## Sumário

O [vRack](/links/network/vrack/) da OVHcloud é uma rede privada que lhe permite configurar o direcionamento entre dois ou mais [servidores dedicados](/links/bare-metal/bare-metal) da OVHcloud. Além disso, permite-lhe também adicionar [instâncias Public Cloud](https://www.ovhcloud.com/pt/public-cloud/) à sua rede privada para criar uma infraestrutura de recursos físicos e virtuais.

**Este manual explica-lhe como configurar uma rede privada entre uma instância Public Cloud e um servidor dedicado.**

## Requisitos

* Ter criado uma [instância Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps)
* Ter ativado um serviço [vRack](/links/network/vrack/)
* Dispor de um [servidor dedicado](/links/bare-metal/bare-metal) compatível com o vRack
* Ter acesso à [Área de Cliente OVHcloud](/links/manager)
* Um intervalo de endereços IP privados à sua escolha

> [!warning]
> Esta funcionalidade pode estar indisponível ou limitada nos [servidores dedicados **Eco**](https://eco.ovhcloud.com/pt/about/).
>
> Para mais informações, consulte o nosso [comparativo](https://eco.ovhcloud.com/pt/compare/).

## Instruções

### Adicionar um projeto Public Cloud ao vRack

> [!primary]
> Esta opção não se aplica a projetos recém-criados que sejam automaticamente entregues com vRack. Para visualizar o vRack após a criação do projeto, aceda ao menu "Bare Metal Cloud" {.action} e clique em "Network" {.action}" no separador à esquerda. Clique em `Rede privada vRack`{.action} para visualizar o(s) vRack(s).
>
> Pode igualmente retirar o projeto do vRack que lhe foi atribuído e associá-lo a outro vRack se o desejar, em especial se já tinha um vRack existente com o(s) seu(s) servidor(es) dedicado(s).

No caso de projetos mais antigos, depois de adquirir o [vRack](/links/network/vrack), aceda ao menu `Bare Metal Cloud`{.action}, clique em `Network`{.action} no separador à esquerda e, a seguir, em `Rede privada vRack`{.action}. Selecione o seu vRack na lista.

Na lista dos serviços elegíveis, selecione o projeto que deseja adicionar ao vRack e, a seguir, clique no botão `Adicionar`{.action}.

![Adicionar um projeto ao vRack](images/addprojectvrack.png){.thumbnail}


### Integrar uma instância no vRack

Existem duas situações:

- A instância ainda não existe.
- A instância já existe e deve adicioná-la ao vRack.

#### Caso de uma nova instância

Se precisar de ajuda, consulte o guia: [Criar uma instância Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps). Ao criar uma instância, poderá especificar, na etapa 5, uma rede privada na qual poderá integrar a sua instância.

#### Caso de uma instância já existente

Pode associar uma instância existente a uma rede privada.

Com o seu projeto associado ao vRack, está pronto a criar redes privadas.

No separador Public Cloud, clique em `Private Network`{.action} no menu à esquerda em **Network**.

Clique no botão "Adicionar uma rede privada" {.action}.

![create private network](images/vrack2022-03.png){.thumbnail}

A página seguinte permite personalizar várias definições.

No passo 1, selecione a região na qual pretende colocar a rede privada.

![select região](images/vrack2024-01.png){.thumbnail}

Para que os dois serviços possam comunicar entre si, devem ser « marcados » com o mesmo **VLAN ID**.

Pode configurá-lo na etapa 2.

![configure network](images/configure_private_network.png){.thumbnail}

Esta etapa oferece várias opções de configuração. Para as necessidades deste guia, vamos concentrar-nos nos elementos necessários. Clique nos separadores abaixo para visualizar os detalhes:

> [!tabs]
> **Nome da rede privada**
>>
>> Introduza um nome para a sua rede privada.<br>
>>
> **Opções de rede do layer 2**
>>
>> Por predefinição, o VLAN ID dos servidores dedicados é **0**. Para utilizar este VLAN ID para uma instância, será necessário marcar a rede privada com a VLAN **0** também.
>> Selecione a caixa **Set a VLAN ID** e selecione VLAN ID **0**.
>>
>> Se não selecionar esta opção, o sistema atribuirá um número de ID de VLAN aleatório à sua rede privada.
>>
> **Utilização de um VLAN ID diferente**
>>
>> Se não pretende utilizar o VLAN ID **0**, pode selecionar um ID diferente entre 1 e 4000. São aplicáveis as seguintes regras:
>>
>> - A rede privada ligada à instância Public Cloud deve ser « » com este identificador de VLAN.
>> - Aquando da configuração do vRack no servidor dedicado, este VLAN ID deve ser incluído no ficheiro de configuração de rede.
>>
>> [!primary]
>> Para o Public Cloud, deve definir um VLAN ID único por rede privada. Não é possível definir o mesmo VLAN ID em duas redes privadas diferentes.
>>
>> [!primary]
>> Ao contrário dos servidores dedicados (quando se utiliza um VLAN ID diferente de 0), não é necessário incluir diretamente o VLAN ID no ficheiro de configuração de rede da instância Public Cloud depois de ter sido configurado na Área de Cliente OVHcloud.
>>
>> Exemplo: se a sua rede privada de instância « está » com a VLAN 2, este VLAN ID deve ser incluído na configuração de rede do servidor dedicado apenas. Para mais informações, consulte o seguinte guia: [Criar várias VLAN no vRack](/pages/bare_metal_cloud/dedicated_servers/creating-multiple-vlan-in-a-vrack).<br>
>>
> **Opções de distribuição dos endereços DHCP**
>>
>> Pode conservar o intervalo de IP privado por predefinição ou utilizar outro.
>>

### Configurar as interfaces de rede

De seguida, configure as interfaces de rede na nova instância Public Cloud e no seu servidor dedicado através deste guia: [Configurar vários servidores dedicados no vRack](/pages/bare_metal_cloud/dedicated_servers/vrack_configuring_on_dedicated_server).

## Quer saber mais?
 
Fale com a nossa comunidade de utilizadores: <https://community.ovh.com/en/>.