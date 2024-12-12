---
title: Enterprise File Storage - Conservare uno Snapshot automatico
excerpt: "Scopri come conservare gli Snapshot automatici della tua soluzione Enterprise File Storage utilizzando l’API OVHcloud"
updated: 2024-11-28
---

## Obiettivo

Gli Snapshot **automatici** sono creati da una [Politica di Snapshot](/pages/storage_and_backup/file_storage/enterprise_file_storage/netapp_snapshot_policy) seguendo le regole associate.

Conservare uno Snapshot **automatico** ne impedisce la rotazione tramite la politica di Snapshot e quindi la sua eliminazione. Lo Snapshot diventa di tipo `manual`.

**Questa guida ti mostra come conservare uno Snapshot automatico della soluzione Enterprise File Storage tramite l’API OVHcloud.**

## Prerequisiti

- Disporre di una soluzione OVHcloud [Enterprise File Storage](/links/storage/enterprise-file-storage)
- Avere accesso all’[API OVHcloud](/links/api)
- Disporre di un volume Enterprise File Storage con uno Snapshot `automatico`

> [!success]
> Se non hai familiarità con l'API OVHcloud, consulta la nostra guida "[Iniziare a utilizzare le API OVHcloud](/pages/manage_and_operate/api/first-steps)".

## Procedura

1\. Identifica l`id` dello Snapshot utilizzando questa chiamata API:

> [!api]
>
> @api {v1} /storage GET /storage/netapp/{serviceName}/share/{shareId}/snapshot
>

- `{serviceName}` è l’identificativo unico del servizio
- `{shareId}` è l’identificativo del volume a cui appartiene lo Snapshot

![HoldSnapshot](images/hold_snapshot_step_1.png){.thumbnail}

2\. Conserva lo Snapshot utilizzando questa chiamata API:

> [!api]
>
> @api {v1} /storage POST /storage/netapp/{serviceName}/share/{shareId}/snapshot/{snapshotId}/hold

- `{serviceName}` è l’identificativo unico del servizio
- `{shareId}` è l’identificativo del volume a cui appartiene lo Snapshot
- `{snapshotID}` è l’identificativo dello Snapshot recuperato precedentemente

> [!warning]
>
> Una volta effettuata l’operazione di conservazione (`hold`), l’`id` e il `type` dello Snapshot saranno modificati. Tuttavia, le proprietà `name`, `createdAt` e `path` verranno mantenute.
> Prendi nota del nuovo `id` se vuoi continuare a eseguire operazioni sullo Snapshot.

![RevertSnapshot](images/hold_snapshot_step_2.png){.thumbnail}

**Lo Snapshot *automatico* viene ora conservato e diventa uno Snapshot *manuale*.**

## Per saperne di più

Se avete bisogno di formazione o di assistenza tecnica per implementare le nostre soluzioni, contattate il vostro rappresentante o cliccate su [questo link](/links/professional-services) per ottenere un preventivo e richiedere un'analisi personalizzata del vostro progetto da parte dei nostri esperti del team Professional Services.

Contatta la nostra [Community di utenti](/links/community).