---
title: "Enterprise File Storage - Automatische Snapshots beibehalten"
excerpt: Erfahren Sie hier, wie Sie mithilfe der OVHcloud API automatische Snapshots für Enterprise File Storage bewahren können
updated: 2024-11-28
---

## Ziel

**Automatische** Snapshots werden von einer [Snapshot-Richtlinie](/pages/storage_and_backup/file_storage/enterprise_file_storage/netapp_snapshot_policy) gemäß den Regeln erstellt, die in dieser Richtlinie festgelegt sind.

Das Beibehalten eines **automatischen** Snapshots verhindert dessen Rotation durch die Snapshot-Richtlinie und somit dessen Löschung. Der Snapshot wird damit zu einem Snapshot vom Typ `manual` geändert.

**Diese Anleitung erklärt, wie Sie mithilfe der OVHcloud API einen automatischen Snapshot für Enterprise File Storage beibehalten.**

## Voraussetzungen

- Sie nutzen [OVHcloud Enterprise File Storage](/links/storage/enterprise-file-storage).
- Sie können sich in der [OVHcloud API-Konsole](/links/api) einloggen.
- Sie verfügen über ein Enterprise File Storage Volume mit einem Snapshot vom Typ `automatic`.

> [!success]
> Wenn Sie mit der Verwendung der OVHcloud API nicht vertraut sind, finden Sie [hier unsere Anleitung zur OVHcloud API](/pages/manage_and_operate/api/first-steps).

## In der praktischen Anwendung

1\. Identifizieren Sie die `id` des Snapshots mithilfe des folgenden API-Aufrufs:

> [!api]
>
> @api {v1} /storage GET /storage/netapp/{serviceName}/share/{shareId}/snapshot
>

- `{serviceName}` ist die eindeutige Kennung des Dienstes.
- `{shareId}` ist die Kennung des Volumes, zu dem der Snapshot gehört.

![HoldSnapshot](images/hold_snapshot_step_1.png){.thumbnail}

2\. Bewahren Sie den Snapshot mithilfe des folgenden API-Aufrufs:

> [!api]
>
> @api {v1} /storage POST /storage/netapp/{serviceName}/share/{shareId}/snapshot/{snapshotId}/hold

- `{serviceName}` ist die eindeutige Kennung des Dienstes.
- `{shareId}` ist die Kennung des Volumes, zu dem der Snapshot gehört.
- `{snapshotID}` ist die im vorherigen Schritt abgerufene Snapshot-ID.

> [!warning]
>
> Nach Abschluss des Aufbewahrungsvorgangs (`hold`) werden `id` und `type` des Snapshots geändert. Die Eigenschaften `name`, `createdAt` und `path` werden jedoch beibehalten.
>
> Beachten Sie die neue `id`, wenn Sie weitere Operationen mit dem Snapshot durchführen möchten.

![RevertSnapshot](images/hold_snapshot_step_2.png){.thumbnail}

**Der *automatische* Snapshot wird beibehalten und zu einem *manuellen* Snapshot umgewandelt.**

## Weiterführende Informationen

Wenn Sie Schulungen oder technische Unterstützung bei der Implementierung unserer Lösungen benötigen, wenden Sie sich an Ihren Vertriebsmitarbeiter oder klicken Sie auf [diesen Link](/links/professional-services), um einen Kostenvoranschlag zu erhalten und eine persönliche Analyse Ihres Projekts durch unsere Experten des Professional Services Teams anzufordern.

Treten Sie unserer [User Community](/links/community) bei.