---
title: "Comparaison des modes de déploiement S3 : Présentation des régions 3-AZ, 1-AZ et des zones locales"  
excerpt: "Découvrez les modes de déploiement du stockage objet S3 d'OVHcloud"  
updated: "2024-10-24"  
---

## Objectif

OVHcloud propose plusieurs modes de déploiement pour son service de stockage objet S3, chacun adapté à des besoins spécifiques en matière de résilience, disponibilité, performance et latence. Ce document fournit une explication détaillée des caractéristiques de chaque mode de déploiement, suivie d'une comparaison pour aider les utilisateurs à choisir l'option la plus adaptée à leurs besoins.

## Concepts

Le service de stockage objet S3 d'OVHcloud propose trois principaux modes de déploiement, chacun optimisé pour des cas d'utilisation spécifiques et offrant divers niveaux de redondance et de tolérance aux pannes :

1. **Région 1-AZ** : Pour les besoins généraux de stockage et de sauvegarde, offrant une résilience de base avec un coût optimisé.
2. **Région 3-AZ** : Adaptée aux applications critiques nécessitant une haute disponibilité, avec une tolérance aux pannes accrue.
3. **Zones locales** : Conçues pour rapprocher les données des utilisateurs finaux, réduisant la latence et garantissant la conformité locale.

**Ce guide vous aidera à comprendre les modes de déploiement S3 et à choisir celui qui répond le mieux à vos besoins en termes de résilience, disponibilité et performance.**

## Modes de déploiement

### Région 1-AZ

#### Infrastructure et redondance

Une région 1-AZ se compose d'une seule zone de disponibilité, couvrant plusieurs centres de données dans une région donnée. La redondance 2N+1 garantit la résilience contre les pannes de rack de serveurs, bien que ce mode reste vulnérable en cas de panne complète d’un centre de données.

**Caractéristiques :**

- **Codage par dispersion (Erasure Coding)** pour garantir la redondance des données en cas de défaillances matérielles.
- **Coût optimisé**, idéal pour les sauvegardes et applications générales où le budget est prioritaire.

**Limites :**

- **Risque de panne de centre de données**, avec des données qui peuvent devenir temporairement inaccessibles.

**Spécifications de redondance :**

| Paramètre              | Description                                           |
|------------------------|-------------------------------------------------------|
| **Type de redondance** | 2N+1 entre plusieurs centres de données               |
| **Tolérance aux pannes** | Niveau serveur et disque ; risque de panne du centre de données |
| **Cas d'utilisation**  | Applications générales, sauvegardes                   |

### Région 3-AZ

#### Structure et disponibilité

Les régions 3-AZ se composent de trois zones de disponibilité indépendantes, offrant une isolation complète pour l'alimentation, le refroidissement et les réseaux. Ce mode garantit la disponibilité des données, même en cas de panne de zone.

**Caractéristiques :**

- **Haute disponibilité**, les données restent accessibles même si une zone est défaillante.
- Idéal pour les applications exigeant une disponibilité continue, telles que le e-commerce et les services financiers.

**Limites :**

- Peut nécessiter une protection supplémentaire, comme la **réplication asynchrone multi-régions**, pour une résilience optimale face aux pannes improbables de la région.

**Spécifications de performance :**

| Paramètre              | Description                                           |
|------------------------|-------------------------------------------------------|
| **Connectivité**       | Faible latence entre zones de disponibilité           |
| **Haute disponibilité**| Maintien de l'accès malgré une panne de zone           |
| **Cas d'utilisation**  | Applications critiques, streaming, e-commerce         |

### Zones locales

#### Design et flexibilité

Les zones locales rapprochent les services d'OVHcloud des utilisateurs finaux, minimisant la latence et garantissant la conformité aux réglementations locales. Ces zones sont idéales pour des performances maximales et des besoins de stockage localisés.

**Caractéristiques :**

- **Faible latence** pour une performance optimale.
- Conforme aux exigences locales en matière de réglementation des données.

**Limites :**

- Limitées à une seule zone de disponibilité, sans redondance inter-zones.

**Cas d'utilisation :**

| Avantage               | Description                                           |
|------------------------|-------------------------------------------------------|
| **Performance**        | Latence ultra-faible                                  |
| **Conformité des données** | Localisation des données pour la conformité       |
| **Cas d'utilisation**  | Jeux en ligne, visioconférences, applications régionales |

## Comparaison des modes de déploiement

| Caractéristiques          | Région 1-AZ                              | Région 3-AZ                            | Zones locales                             |
|---------------------------|------------------------------------------|----------------------------------------|-------------------------------------------|
| **Structure de déploiement** | Zone de disponibilité unique               | Trois zones indépendantes              | Localisé pour faible latence              |
| **Redondance**             | 2N+1 interne                               | Redondance inter-zones                 | Pas de redondance entre zones             |
| **Disponibilité des données** | Risque de panne de centre de données, mais résilience au niveau du serveur | Maintenue entre zones                  | Limitée à la zone locale                  |
| **Latence**               | Modérée                                   | Faible entre zones                     | Ultra-faible pour les utilisateurs finaux |
| **Cas d'utilisation**     | Applications générales, sauvegardes       | Applications critiques                 | Applications sensibles à la latence       |
| **Coût**                  | Optimisé                                  | Plus élevé pour résilience accrue      | Dépend de la zone et des besoins          |

## Performances réseau, téléchargement et récupération

Le stockage objet S3 est basé sur l’API S3 d’OVHcloud, avec des performances et des limites comme le nombre de buckets, la bande passante et la taille maximale des objets disponibles [ici](/pages/storage_and_backup/object_storage/s3_limitations).

Pour télécharger vos données, la bande passante maximale est de **1 Gbps par connexion** avec un nombre illimité de connexions parallèles. Le temps de téléchargement dépend de votre connexion Internet.

**Exemples de temps de téléchargement :**

- **1 Gbps** : 1 To en ~2,2 heures.
- **5 Gbps** : 1 To en ~26 minutes.

## Tarification

La facturation est basée sur l'espace de stockage utilisé et l’espace Object Storage avec une granularité de 1 Go. En cas de suppression anticipée (moins de 180 jours), un supplément peut être appliqué pour respecter la durée minimale d'archivage.

## Aller plus loin

Pour des détails supplémentaires et de l’assistance sur les modes de déploiement S3, consultez [ce guide](/pages/storage_and_backup/object_storage/cold_archive_getting_started) et notre communauté sur [Discord](https://discord.gg/ovhcloud) ou <https://community.ovh.com/fr/>.

Si vous avez besoin d'une formation ou d'une assistance technique pour la mise en œuvre de nos solutions, contactez votre commercial ou cliquez sur [ce lien](https://www.ovhcloud.com/fr/professional-services/) pour obtenir un devis et une analyse personnalisée de votre projet.
