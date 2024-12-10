---
title: "Enterprise File Storage - Conservar un snapshot automático"
excerpt: "Cómo conservar los snapshots automáticos de su solución Enterprise File Storage utilizando la API de OVHcloud"
updated: 2024-11-28
---

Los snapshots **automáticos** son creados por una [Política de Snapshots](/pages/storage_and_backup/file_storage/enterprise_file_storage/netapp_snapshot_policy) siguiendo las reglas asociadas a la misma.

Conservar un snapshot **automático** impide su rotación mediante la política de snapshots y, por tanto, su eliminación. El snapshot pasa a ser de tipo `manual`.

**Aprenda a conservar un snapshot automático de su solución Enterprise File Storage utilizando la API de OVHcloud.**

## Requisitos

- Tener contratado un servicio de OVHcloud [Enterprise File Storage](/links/storage/enterprise-file-storage)
- Estar conectado a la [API de OVHcloud](/links/api)
- Disponer de un volumen Enterprise File Storage con un snapshot `automático`

> [!success]
> Si no está familiarizado con el uso de la API de OVHcloud, consulte nuestra guía "[Primeros pasos con las API de OVHcloud](/pages/manage_and_operate/api/first-steps)".

## Procedimiento

1\. Identifique el `id` del snapshot utilizando la siguiente llamada a la API:

> [!api]
>
> @api {v1} /storage GET /storage/netapp/{serviceName}/share/{shareId}/snapshot
>

- `{serviceName}` es el identificador único del servicio
- `{shareId}` es el identificador del volumen al que pertenece el snapshot

![HoldSnapshot](images/hold_snapshot_step_1.png){.thumbnail}

2\. Conserve el snapshot utilizando la siguiente llamada a la API:

> [!api]
>
> @api {v1} /storage POST /storage/netapp/{serviceName}/share/{shareId}/snapshot/{snapshotId}/hold

- `{serviceName}` es el identificador único del servicio
- `{shareId}` es el identificador del volumen al que pertenece el snapshot
- `{snapshotID}` es el identificador del snapshot recuperado en el paso anterior

> [!warning]
>
> Una vez realizada la operación de conservación (`hold`), se modificarán el `id` y el `type` del snapshot. No obstante, se conservarán sus propiedades `name`, `createdAt` y `path`.
> Tome nota del nuevo `id` si desea continuar realizando operaciones en el snapshot.

![RevertSnapshot](images/hold_snapshot_step_2.png){.thumbnail}

**El snapshot *automático* se conserva y se convierte en un snapshot *manuel*.**

## Más información

Si necesita formación o asistencia técnica para implantar nuestras soluciones, póngase en contacto con su representante de ventas o haga clic en [este enlace](/links/professional-services) para obtener un presupuesto y solicitar un análisis personalizado de su proyecto a nuestros expertos del equipo de Servicios Profesionales.

Interactúe con nuestra [comunidad de usuarios](/links/community).