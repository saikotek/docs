---
title: Enterprise File Storage - Zachowaj automatyczny snapshot
excerpt: "Dowiedz się, jak przechowywać automatyczne snapshoty rozwiązania Enterprise File Storage za pomocą API OVHcloud"
updated: 2024-11-28
---

## Wprowadzenie

Snapshoty **automatyczne** są tworzone przez [Politykę snapshotów](/pages/storage_and_backup/file_storage/enterprise_file_storage/netapp_snapshot_policy) i działają zgodnie z regułami z nimi związanymi.

Zachowanie **automatycznej** kopii zapasowej snapshot zapobiega jej rotacji za pomocą polityki wykonywania snapshotów, a zatem jej usuwania. Snapshot zmienia się w `manual`.

**Dowiedz się, jak przechowywać automatyczny snapshot rozwiązania Enterprise File Storage za pomocą API OVHcloud.**

## Wymagania początkowe

- Wykupienie usługi OVHcloud [Enterprise File Storage](/links/storage/enterprise-file-storage)
- Połączenie z [API OVHcloud](/links/api)
- Posiadanie wolumenu Enterprise File Storage z `automatycznym` snapshotem

> [!success]
> Jeśli nie wiesz, jak korzystać z API OVHcloud, zapoznaj się z naszym przewodnikiem "[Pierwsze kroki z API OVHcloud](/pages/manage_and_operate/api/first-steps)".

## W praktyce

1\. Zidentyfikuj `id` snapshota za pomocą następującego wywołania API:

> [!api]
>
> @api {v1} /storage GET /storage/netapp/{serviceName}/share/{shareId}/snapshot
>

- `{serviceName}` to unikalny identyfikator usługi
- `{shareId}` jest identyfikatorem wolumenu, do którego należy snapshot

![HoldSnapshot](images/hold_snapshot_step_1.png){.thumbnail}

2\. Zachowaj snapshot, używając następującego wywołania API:

> [!api]
>
> @api {v1} /storage POST /storage/netapp/{serviceName}/share/{shareId}/snapshot/{snapshotId}/hold

- `{serviceName}` to unikalny identyfikator usługi
- `{shareId}` jest identyfikatorem wolumenu, do którego należy snapshot
- `{snapshotID}` to identyfikator snapshota uzyskany na poprzednim etapie

> [!warning]
>
> Po wykonaniu operacji zachowywania danych (`hold`), `id` oraz `type` kopii snapshot zostaną zmienione. Jednak jego właściwości `name`, `createdAt` i `path` zostaną zachowane.
> Zapisz informacje o nowym `id`, jeśli chcesz kontynuować wykonywanie operacji na snapshocie.

![RevertSnapshot](images/hold_snapshot_step_2.png){.thumbnail}

**Zrzut *automatyczny* jest teraz zapisany jako *ręczny* snapshot.**

## Sprawdź również

Jeśli potrzebujesz szkolenia lub pomocy technicznej w celu wdrożenia naszych rozwiązań, skontaktuj się z przedstawicielem handlowym lub kliknij [ten link](/links/professional-services), aby uzyskać wycenę i poprosić o spersonalizowaną analizę projektu od naszych ekspertów z zespołu Professional Services.

Dołącz do [grona naszych użytkowników](/links/community).