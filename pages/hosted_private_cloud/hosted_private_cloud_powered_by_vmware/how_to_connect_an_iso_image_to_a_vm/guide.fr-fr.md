---
title: "Comment connecter une image ISO à une VM"
excerpt: "Découvrez comment connecter une image ISO à une machine virtuelle ?"
updated: 2024-11-05
---

> [!success]
> Vous pouvez consulter le guide « [Téléverser un ISO dans un datastore](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/vmware_datastore_upload) » pour plus d'informations sur le téléversement d'éléments (ISO, fichiers, etc..) dans votre environnement VMware on OVHcloud.


## Objectif

Vous pouvez créer une librairie de fichiers ISO à utiliser pour vos déploiements de systèmes et de logiciels dans votre infrastructure.

**Ce guide vous accompagne tout au long du processus de connexion d'une image ISO à une VM.**

## Prérequis

- Être contact administrateur de l'infrastructure [Hosted Private Cloud](/links/hosted-private-cloud/vmware), afin de recevoir les identifiants de connexion.
- Avoir un identifiant utilisateur actif (créé dans l'[espace client OVHcloud](/links/manager))

## En pratique

### Création de la librairie

Dans l'interface vSphere, allez dans la section `Stockage`{.action}.<br>
Choisissez le Datastore qui abritera la librairie (préférez les espaces de stockage partagés aux stockage locaux afin d'éviter les problèmes d'accès).<br>
Dans l'onglet `Fichiers`{.action}, cliquez sur `Nouveau Dossier`{.action}.

![FOLDER](images/en01newfolder.png){.thumbnail}

Nommez votre dossier (dans notre exemple : ISOs) puis selectionnez-le et cliquez sur `Télécharger des fichiers`{.action}.

![UPLOAD](images/en02upload.png){.thumbnail}

Naviguez jusqu'aux fichiers ISO que vous souhaitez uploader et cliquez sur `Ouvrir`{.action}.

![BROWSE](images/en03browse.png){.thumbnail}

Votre librairie est prête. Vous pouvez ajouter des images ISO selon vos besoins et dans la limite de l'espace de stockage disponible.

![LIBRARY](images/en04library.png){.thumbnail}

### Connecter une image à une VM

Dans l'interface vSphere, allez dans la section `Hôtes & clusters`{.action}.<br>
Faites un clic droit sur la VM qui a besoin de l'image ISO attachée puis cliquez sur `Modifier les paramètres`{.action}.<br>

![EDIT](images/en05edit.png){.thumbnail}

Changez le paramètre du lecteur CD/DVD en "Fichier ISO banque de données".

![ISO](images/en06dataiso.png){.thumbnail}

Dans la fenêtre de navigation qui apparait, allez dans la librairie créée précédement et selectionnez l'image à utiliser.<br>
Cliquez sur `OK`{.action}.

![SELECT](images/en07choose.png){.thumbnail}

De retour dans la fenêtre de paramétrage, assurez-vous que l'option "Connecter" est cochée avant de cliquer `OK`{.action}.

![CONNECT](images/en08connect.png){.thumbnail}

L'image est désormais connectée et disponible pour votre VM comme si c'était un media physique directement attaché.

## Aller plus loin

Pour plus d'informations sur le téléversement au sein de votre environnement Hosted Private Cloud - VMware on OVHcloud, consultez le guide « [Téléverser un ISO dans un datastore](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/vmware_datastore_upload) ».

En effet, vous pouvez utiliser votre client web HTML sécurisé vCenter on OVHcloud mais aussi `govc` (voir la procédure dans le guide).

Échangez avec notre [communauté d'utilisateurs](/links/community).
