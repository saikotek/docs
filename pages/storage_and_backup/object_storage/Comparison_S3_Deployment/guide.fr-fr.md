---
title: "Comparaison des modes de déploiement S3 : Présentation des régions 3-AZ, 1-AZ et des zones locales"  
excerpt: "Découvrez les modes de déploiement du stockage objet S3 d'OVHcloud"  
updated: "2024-10-24"  
---

## Objectif

OVHcloud propose plusieurs modes de déploiement pour son service de stockage objet S3, chacun adapté à des besoins spécifiques en matière de résilience, disponibilité, performance et latence. Ce document fournit une explication détaillée des caractéristiques de chaque mode de déploiement, suivie d'une comparaison pour aider les utilisateurs à choisir l'option la plus adaptée à leurs besoins.

## Prérequis

- Comprendre les cas d'utilisation des différents modes de déploiement : 1-AZ, 3-AZ, et Local Zones.
- Familiarité avec le service OVHcloud Object Storage - S3 API.

## Concepts

Le service de stockage objet d'OVHcloud propose trois principaux modes de déploiement, chacun optimisé pour des cas d'utilisation spécifiques et offrant divers niveaux de redondance et de tolérance aux pannes :

1. **Région 1-AZ** : Pour les besoins généraux de stockage et de sauvegarde, offrant une résilience de base avec un coût optimisé.
2. **Région 3-AZ** : Adaptée aux applications critiques nécessitant une haute disponibilité, avec une tolérance aux pannes accrue.
3. **Local Zones** : Conçues pour rapprocher les données des utilisateurs finaux, réduisant la latence et garantissant la conformité locale.

## Modes de déploiement

> **Note:**  
> Les informations suivantes concernent les différents modes de déploiement disponibles pour le service. Sélectionnez le mode qui répond le mieux à vos besoins en termes de résilience, de disponibilité et de performance. Vous pouvez identifier le mode de déploiement disponible pour une région donnée sur le [document Object Storage - Endpoints et géo-disponibilité de l’Object Storage.](https://help.ovhcloud.com/csm/en-gb-public-cloud-storage-s3-location?id=kb_article_view&sysparm_article=KB0047382)

### 1. Introduction

OVHcloud propose plusieurs modes déploiement adaptés à différents besoins en termes de résilience, de disponibilité et de performance. Chaque mode est optimisé pour des cas d'utilisation spécifiques et offre des niveaux différents de redondance et de tolérance aux pannes. Ce document explore en détail ces modes et présente une comparaison pour faciliter votre choix.

### 2. Région 1-AZ

#### Infrastructure et redondance

Une région 1-AZ se compose d'une **seule zone de disponibilité qui couvre plusieurs datacenters dans la même région**, utilisant une conception redondante 2N+1. Cette configuration offre une résilience contre les défaillances de rack de serveurs et de disques durs, mais elle peut être vulnérable à une panne plus global d'un datacenter. Notez que dans une région 1-AZ, le service Object Storage S3 est situé dans un datacentre spécifique, et en cas de panne dans ce datacenter, l'accès aux données pourrait être impacté, même si les autres datacenters de la zone restent opérationnels.

#### Caractéristiques

- **Erasure Coding :** Fournit une redondance des données sur différents serveurs,  garantissant ainsi une continuité en cas de défaillances matérielles, et ce, en répartissant des morceaux de données sur plusieurs disques et serveurs au sein de la zone de disponibilité. 
- **Coût optimisé :** idéal pour les sauvegardes et applications générales où le budget est prioritaire.

#### Limites

- **Risque de panne** : En cas de panne d'un datacenter, les données peuvent devenir indisponibles ou être potentiellement perdues si ;celui hébergeant le service Object Storage est touché. Toutefois, la protection contre les défaillances de serveurs et de disques durs est maintenue.

**Remarque :**
Pour renforcer la résilience des applications critiques dans une région 1-AZ, [la réplication asynchrone](https://help.ovhcloud.com/csm/fr-public-cloud-storage-s3-asynchronous-replication-buckets?id=kb_article_view&sysparm_article=KB0062418) peut être utilisée, offrant une protection supplémentaire sans compromettre votre coût global. Cela peut aider à renforcer la résilience des applications et des données. Une autre approche pour réduire ce risque est d'utiliser un [**mode de déploiement 3-AZ**](#3-region-3-AZ).

**Spécifications de redondance - Région 1-AZ :**

| Paramètre              | Description                                           |
|------------------------|-------------------------------------------------------|
| **Type de redondance** | 2N+1 entre plusieurs datacentres               |
| **Tolérance aux pannes** | Niveau serveur et disque ; risque de panne du centre de données |
| **Cas d'utilisation**  | Applications générales, sauvegardes                   |

### 3. Région 3-AZ

#### Infrastructure et redondance 

Les régions 3-AZ se composent de **trois zones de disponibilité indépendantes**, offrant une isolation complète pour l'alimentation, le refroidissement et les réseaux. Ce mode garantit la **disponibilité du service**, même en cas de panne d'une zone de disponibilité.

#### Caractéristiques

- **Haute disponibilité :** les données restent accessibles pour les opération de lecture et d'écriture, même si une zone est défaillante. Cette configuration est idéale pour les applications exigeant une haute disponibilité.

#### Cas d'usages

Les régions 3-AZ sont idéales pour les applications critiques  où la gouvernance des données exige une disponibilité continue des données, telles que les plateformes de e-commerce, e-santé, les services financiers ou services de media streaming.

**Remarque :**  
Bien que proposant une protection accrue, ce mode de déploiement peut ne pas être totalement résistant à une panne, très improbable, panne régionale. Une protection additionnelle comme [la réplication asynchrone](https://help.ovhcloud.com/csm/fr-public-cloud-storage-s3-asynchronous-replication-buckets?id=kb_article_view&sysparm_article=KB0062418) peut être considérée pour améliorer la résilience des données.

**Spécifications de performance :**

| Paramètre              | Description                                           |
|------------------------|-------------------------------------------------------|
| **Connectivité**       | Faible latence entre zones de disponibilité           |
| **Haute disponibilité**| Maintien de l'accès malgré une panne de zone           |
| **Cas d'utilisation**  | Applications critiques, streaming, e-commerce, e-santé        |

### 4. Local Zones

#### Design et flexibilité

Les Local Zones rapprochent les services d'OVHcloud des utilisateurs finaux, minimisant la latence et garantissant la conformité aux réglementations locales. Ces zones sont idéales pour des performances maximales et des besoins de stockage localisés.

**Avantages en matière de coûts et de conformité**

- **Réduction des coûts de réseau :** aident à réduire les coûts en minimisant la distance que les données doivent parcourir.
- **Stockage localisé :** Prend en charge les exigences de localisation des données, ce qui en fait une option idéale pour la conformité réglementaire.

**Limites :**

- **Limitation à une seule zone :** Les Local Zones sont limitées à une seule zone de disponibilité et ne fournissent pas de redondance entre zones, ce qui restreint les options de récupération de données en cas de sinistre."
- 
**Cas d'utilisation :**

| Avantage               | Description                                           |
|------------------------|-------------------------------------------------------|
| **Performance**        | Latence ultra-faible                                  |
| **Conformité des données** | Localisation des données pour la conformité       |
| **Cas d'utilisation**  | Gaming, visioconférences, applications régionales |

## Comparaison des modes de déploiement

| Caractéristiques          | Région 1-AZ                              | Région 3-AZ                            | Local Zones                             |
|---------------------------|------------------------------------------|----------------------------------------|-------------------------------------------|
| **Structure de déploiement** | Zone de disponibilité unique               | Trois zones indépendantes              | Localisé pour faible latence              |
| **Redondance**             | 2N+1 interne                               | Redondance inter-zones                 | Pas de redondance entre zones             |
| **Disponibilité des données** | Limité si panne d'un datacenter, mais résilience à la panne de serveurs/disques | Maintenue entre zones                  | Limitée à la zone locale                  |
| **Latence**               | Modérée                                   | Faible entre zones                     | Ultra-faible pour les utilisateurs finaux |
| **Cas d'utilisation**     | Applications générales, sauvegardes       | Applications critiques                 | Applications sensibles à la latence       |
| **Coût**                  | Optimisé                                  | Plus élevé pour résilience accrue      | Dépend de la zone et des besoins          |


## Aller plus loin

Pour des détails supplémentaires et de l’assistance sur les modes de déploiement S3, consultez [ce guide](/pages/storage_and_backup/object_storage/cold_archive_getting_started) et notre communauté sur [Discord](https://discord.gg/ovhcloud) ou <https://community.ovh.com/fr/>.

Si vous avez besoin d'une formation ou d'une assistance technique pour la mise en œuvre de nos solutions, contactez votre commercial ou cliquez sur [ce lien](https://www.ovhcloud.com/fr/professional-services/) pour obtenir un devis et une analyse personnalisée de votre projet.
