---
title: Enterprise File Storage - Hold an automatic snapshot
excerpt: "Hold automatic snapshots from Enterprise File Storage offer using the OVHcloud API"
updated: 2024-11-28
---

## Objective 

**Automatic** snapshots are created by a [Snapshot Policy](/pages/storage_and_backup/file_storage/enterprise_file_storage/netapp_snapshot_policy) which takes and keeps snapshot copies of a volume as defined by the rules associated with the policy. 

Holding an **automatic** snapshot prevents it from being rotated by the snapshot policy and makes it a **manual** snapshot.

**Learn how to hold an automatic snapshot from your Enterprise File Storage offer using the OVHcloud API.**

## Requirements

- An active OVHcloud [Enterprise File Storage](/links/storage/enterprise-file-storage) service
- Access to the [OVHcloud API](/links/api)
- An Enterprise File Storage volume with an `automatic` snapshot

> [!success]
> If you are not familiar with using the OVHcloud API, please refer to our guide on [Getting started with the OVHcloud API](/pages/manage_and_operate/api/first-steps).

## Instructions

1\. Identify the snapshot `id` using the following API call:

> [!api]
>
> @api {v1} /storage GET /storage/netapp/{serviceName}/share/{shareId}/snapshot
>

- `{serviceName}` is the service unique ID
- `{shareId}` is the share ID to which the snapshot belongs

![HoldSnapshot](images/hold_snapshot_step_1.png){.thumbnail}

2\. Hold the snapshot using the following API call:

> [!api]
>
> @api {v1} /storage POST /storage/netapp/{serviceName}/share/{shareId}/snapshot/{snapshotId}/hold

- `{serviceName}` is the service unique ID
- `{shareId}` is the share ID to which the snapshot belongs
- `{snapshotID}` is the snapshot ID

> [!warning]
>
> After the hold operation is performed, the snapshot `id` and `type`  will change. However, its `name`, `createdAt` and `path` properties will be kept.
> Please take note of the new `id` if you want to perform further operations with the snapshot.

![RevertSnapshot](images/hold_snapshot_step_2.png){.thumbnail}

**The *automatic* snapshot has now become a *manual* snapshot.**

## Go further

If you need training or technical assistance to implement our solutions, contact your sales representative or click on [this link](/links/professional-services) to get a quote and ask our Professional Services experts for assisting you on your specific use case of your project.

Join our [community of users](/links/community).