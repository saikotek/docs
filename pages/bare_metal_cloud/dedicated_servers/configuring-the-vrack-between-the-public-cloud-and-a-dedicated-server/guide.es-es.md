---
title: 'Configurar el vRack entre Public Cloud y un servidor dedicado'
excerpt: 'Cómo configurar una red privada entre una instancia de Public Cloud y un servidor dedicado'
updated: 2024-11-05
---

> [!primary]
> Esta traducción ha sido generada de forma automática por nuestro partner SYSTRAN. En algunos casos puede contener términos imprecisos, como en las etiquetas de los botones o los detalles técnicos. En caso de duda, le recomendamos que consulte la versión inglesa o francesa de la guía. Si quiere ayudarnos a mejorar esta traducción, por favor, utilice el botón «Contribuir» de esta página.
>

## Objetivo

El [vRack](/links/network/vrack/) de OVHcloud es una red privada que permite configurar el direccionamiento entre dos o más [servidores dedicados](/links/bare-metal/bare-metal) de OVHcloud. También permite añadir [instancias de Public Cloud](https://www.ovhcloud.com/es-es/public-cloud/) para crear una infraestructura de recursos físicos y virtuales.

**Esta guía explica cómo configurar la red privada entre una [instancia de Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps) y un [servidor dedicado](/links/bare-metal/bare-metal).**

## Requisitos

* Haber creado una [instancia de Public Cloud de OVHcloud.](/pages/public_cloud/compute/public-cloud-first-steps)
* Haber activado un servicio [vRack.](/links/network/vrack/)
* Tener un [servidor dedicado](/links/bare-metal/bare-metal) compatible con el vRack.
* Estar conectado al [área de cliente de OVHcloud.](/links/manager)
* Un rango de direcciones IP privadas que elija.

> [!warning]
> Esta funcionalidad puede no estar disponible o estar limitada en los [servidores dedicados **Eco**](https://eco.ovhcloud.com/es-es/about/).
>
> Para más información, consulte nuestra [comparativa](https://eco.ovhcloud.com/es-es/compare/).

## Procedimiento

### Añadir un proyecto de Public Cloud al vRack

> [!primary]
> No se aplicará a los proyectos recién creados que se entreguen automáticamente con un vRack. Para ver el vRack una vez creado el proyecto, vaya al menú `Bare Metal Cloud`{.action} y haga clic en `Network`{.action} en la pestaña de la izquierda. Haga clic en `Red privada vRack`{.action} para ver el vRack(s).
>
> También puede retirar el proyecto del vRack que le haya sido atribuido y asociarlo a otro vRack si lo desea, especialmente si ya tenía un vRack existente con su servidor o servidores dedicados.

Para los proyectos más antiguos, una vez contratado el [vRack](/links/network/vrack), acceda al menú `Bare Metal Cloud`{.action}, haga clic en `Network`{.action} en la pestaña de la izquierda y seleccione `Red privada vRack`{.action}. Seleccione el vRack de la lista.

Seleccione el proyecto que quiera añadir al vRack y haga clic en el botón `Añadir`{.action}.

![Añadir un proyecto al vRack](images/addprojectvrack.png){.thumbnail}

### Integrar una instancia en el vRack

Puede darse dos situaciones:

- La instancia aún no existe.
- La instancia ya existe y debe añadirla al vRack.

#### Caso de una nueva instancia

Si necesita ayuda, consulte la guía [Crear una instancia de Public Cloud](/pages/public_cloud/compute/public-cloud-first-steps#create-instance). Al crear una instancia, podrá especificar, en el paso 4, una red privada en la que integrar su instancia. Seleccione el vRack anteriormente creado en el menú desplegable que aparece.

#### Caso de una instancia ya existente

Es posible asociar una instancia existente a una red privada.

Con su proyecto relacionado con el vRack, estará listo para crear redes privadas.

En la pestaña Public Cloud, haga clic en `Private Network`{.action} en el menú de la izquierda, en **Network**.

Haga clic en el botón `Añadir una red privada`{.action}.

![create private network](images/vrack2022-03.png){.thumbnail}


En la siguiente página, puede personalizar varias opciones de configuración.

En el paso 1, seleccione la región en la que desea colocar la red privada.

![select region](images/vrack2024-01.png){.thumbnail}

Para que los dos servicios puedan comunicarse entre sí, deben estar etiquetados con el mismo **VLAN ID**.

Puede configurarlo en el paso 2.

![configure network](images/configure_private_network.png){.thumbnail}

Este paso ofrece varias opciones de configuración. A efectos de esta guía, nos centraremos en los elementos necesarios. Haga clic en las fichas siguientes para ver los detalles:

> [!tabs]
> **Nombre de la red privada**
>>
>> Introduzca un nombre para la red privada.<br>
>>
> **Opciones de red de la capa 2 (L2)**
>>
>> Por defecto, el VLAN ID de los servidores dedicados es **0**. Para utilizar este VLAN ID para una instancia, será necesario marcar la red privada con la VLAN **0**.
>> Marque la casilla **Set a VLAN ID** y seleccione VLAN ID **0**.
>>
>> Si no marca la casilla, el sistema asignará un número de identificador de VLAN aleatorio a su red privada.
>>
> **Uso de una VLAN ID diferente**
>>
>> Si no va a utilizar el VLAN ID **0**, puede seleccionar un ID diferente entre 1 y 4000. Se aplican las siguientes reglas:
>>
>> - La red privada asociada a la instancia Public Cloud debe estar «etiquetada» con este identificador de VLAN.
>> - Al configurar el vRack en el servidor dedicado, esta VLAN ID debe incluirse en el archivo de configuración de red.
>>
>> [!primary]
>> Para Public Cloud, defina un VLAN ID único por red privada. No es posible definir el mismo VLAN ID en dos redes privadas diferentes.
>>
>> [!primary]
>> A diferencia de los servidores dedicados (cuando se utiliza un VLAN ID distinto de 0), no es necesario incluir directamente el VLAN ID en el archivo de configuración de red de la instancia Public Cloud una vez configurado en el área de cliente de OVHcloud.
>>
>> Ejemplo: si su red privada de instancia está «etiquetada» con la VLAN 2, esta VLAN ID debe incluirse en la configuración de red del servidor dedicado únicamente. Para más información, consulte la siguiente guía: [Crear varias VLAN en el vRack](/pages/bare_metal_cloud/dedicated_servers/creating-multiple-vlan-in-a-vrack).<br>
>>
> **Opciones de distribución de direcciones DHCP**
>>
>> Puede conservar el rango IP privado por defecto o utilizar otro diferente.
>>

Una vez completada la configuración, haga clic en `Crear`{.action}. Esta operación puede tardar unos minutos.

En el panel de control de la instancia correspondiente, haga clic en el botón `...`{.action} en la casilla «Redes», junto a «Red(s) privada(s)», y seleccione `Asociar una red`{.action}.

![attach network](images/vrack2021-01.png){.thumbnail}

En la nueva ventana, seleccione las redes privadas que quiera asociar a su instancia y haga clic en «Asociar» {.action}.

![attach network](images/attach_network.png){.thumbnail}


### Configurar las interfaces de red

A continuación, configure las interfaces de red en la nueva instancia de Public Cloud y en el servidor dedicado con esta guía: [Configurar varios servidores dedicados en el vRack](/pages/bare_metal_cloud/dedicated_servers/vrack_configuring_on_dedicated_server){.external}.

## Más información

Interactúe con nuestra comunidad de usuarios en <https://community.ovh.com/en/>.