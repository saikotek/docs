---
title: Enterprise File Storage - Conservar uma snapshot automática
excerpt: "Descubra como conservar as snapshots automáticas da sua solução Enterprise File Storage com a ajuda da API OVHcloud"
updated: 2024-11-28
---

## Objetivo

As snapshots **automáticas** são criadas por uma [Política de Snapshots](/pages/storage_and_backup/file_storage/enterprise_file_storage/netapp_snapshot_policy) de acordo com as regras associadas a esta última.

Manter uma snapshot **automática** impede a sua rotação pela política de snapshots e, portanto, a sua eliminação. A snapshot será `manual`.

**Saiba como conservar uma snapshot automática da sua solução Enterprise File Storage através da API OVHcloud.**

## Requisitos

- Ter uma oferta OVHcloud [Enterprise File Storage](/links/storage/enterprise-file-storage)
- Estar ligado à [API OVHcloud](/links/api)
- Dispor de um volume Enterprise File Storage com uma snapshot `automática`

> [!success]
> Se não está familiarizado com a utilização da API OVHcloud, consulte o nosso guia "[Primeiros passos com as API OVHcloud](/pages/manage_and_operate/api/first-steps)".

## Instruções

1\. Identifique o `id` da snapshot através da seguinte chamada API:

> [!api]
>
> @api {v1} /storage GET /storage/netapp/{serviceName}/share/{shareId}/snapshot
>

- `{serviceName}` é o identificador único do serviço
- `{shareId}` é o identificador do volume a que pertence a snapshot

![HoldSnapshot](images/hold_snapshot_step_1.png){.thumbnail}

2\. Guarde a snapshot utilizando a seguinte chamada API:

> [!api]
>
> @api {v1} /storage POST /storage/netapp/{serviceName}/share/{shareId}/snapshot/{snapshotId}/hold

- `{serviceName}` é o identificador único do serviço
- `{shareId}` é o identificador do volume a que pertence a snapshot
- `{snapshotID}` é o identificador da snapshot recuperada na etapa anterior

> [!warning]
>
> Depois de efetuada a operação de conservação (`hold`), o `id` e o `type` da snapshot serão alterados. No entanto, as suas propriedades `name`, `createdAt` e `path` serão conservadas.
> Tome nota do novo `id` se deseja continuar a efetuar operações na snapshot.

![RevertSnapshot](images/hold_snapshot_step_2.png){.thumbnail}

**A snapshot *automática* é agora conservada e torna-se uma snapshot *manual*.**

## Quer saber mais?

Se precisar de formação ou de assistência técnica para implementar as nossas soluções, contacte o seu representante comercial ou clique em [esta ligação](/links/professional-services) para obter um orçamento e solicitar uma análise personalizada do seu projecto aos nossos especialistas da equipa de Serviços Profissionais.

Fale com nossa [comunidade de utilizadores](/links/community).