---
title: "Comment migrer les données Veeam Cloud Connect vers Object Storage ?"
excerpt: "Découvrez deux solutions pour migrer vos données Veeam Cloud Connect vers Object Storage avec Veeam Backup & Replication Enterprise Edition."
updated: 2024-12-11
---

## Objectif

**Ce guide vous détaille comment migrer vos données depuis Veeam Cloud Connect vers Object Storage.**  
Vous y trouverez deux approches : l'une sans nouveau serveur Veeam Enterprise et l'autre avec un nouveau serveur.

## Prérequis

- Accès à l'interface de gestion Veeam Cloud Connect.
- Une installation de Veeam Backup & Replication Enterprise Edition compatible avec votre infrastructure actuelle.
- Les droits administratifs nécessaires pour configurer les repositories de sauvegarde et gérer les jobs.

## En pratique

### Option 1 - Migration sans nouveau serveur Veeam Enterprise

1. **Créer un espace de stockage Object Storage (bucket).**  
   Suivez les étapes ici : [Créer un bucket Object Storage](/pages/storage_and_backup/object_storage/s3_create_bucket).

2. **Configurer un nouveau repository de sauvegarde.**  
   Consultez : [Configurer S3 sur Veeam](https://help.ovhcloud.com/csm/fr-public-cloud-storage-s3-veeam?id=kb_article_view&sysparm_article=KB0047499).

3. **Exporter les données de backup depuis Veeam Cloud Connect.**  
   Utilisez l'option "Export Entire Backup Chain" dans la console Cloud Connect.  
   Voir la documentation officielle : [Déplacer les sauvegardes](https://helpcenter.veeam.com/docs/backup/vsphere/move_backup.html?ver=120#repo).

4. **Importer les fichiers de sauvegarde dans le nouveau repository.**  
   Utilisez l'option "Add Existing Backup" dans la console Veeam Backup & Replication Enterprise Edition.

5. **Configurer ou modifier un job de sauvegarde.**  
   Incluez les données migrées dans un job existant ou créez un nouveau job.

> **Note** : Cette procédure peut varier selon votre configuration. Référez-vous aux guides officiels de Veeam pour des instructions détaillées.


### Étape 2 : Migration avec un nouveau serveur Veeam Enterprise

1. **Créer un espace de stockage Object Storage (bucket).**  
   Suivez les étapes ici : [Créer un bucket Object Storage](https://help.ovhcloud.com/csm/fr-public-cloud-storage-s3-create-bucket?id=kb_article_view&sysparm_article=KB0047313).

2. **Installer et configurer Veeam Backup & Replication sur le nouveau serveur.**  
   Vérifiez que la version est compatible avec votre installation actuelle de Veeam Cloud Connect.

3. **Configurer un nouveau repository de sauvegarde sur le serveur.**  
   Consultez : [Configurer S3 sur Veeam](https://help.ovhcloud.com/csm/fr-public-cloud-storage-s3-veeam?id=kb_article_view&sysparm_article=KB0047499).

4. **Exporter les données de backup depuis Veeam Cloud Connect.**  
   Utilisez l'option "Export Entire Backup Chain".  
   Voir la documentation officielle : [Déplacer les sauvegardes](https://helpcenter.veeam.com/docs/backup/vsphere/move_backup.html?ver=120#repo).

5. **Importer les fichiers de sauvegarde dans le nouveau repository.**  
   Utilisez l'option "Add Existing Backup" dans la console Veeam Backup & Replication Enterprise Edition.

6. **Configurer ou modifier un job de sauvegarde.**  
   Incluez les données migrées dans un job existant ou créez un nouveau job.

> **Note** : Cette procédure peut varier selon votre configuration. Référez-vous aux guides officiels de Veeam pour des instructions détaillées.

---

## Aller plus loin

Échangez avec notre [communauté d'utilisateurs](/links/community).
