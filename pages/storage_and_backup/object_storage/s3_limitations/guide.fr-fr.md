---
title: Object Storage - Limites techniques
excerpt: "Retrouvez ici les limites techniques de l'offre S3 Object Storage"
updated: 2024-08-22
---

<style>
td:nth-of-type(2) {
  white-space:nowrap;
}
</style>

## Objectif

Retrouvez ici les limites techniques relatives à l'offre S3 Object Storage OVHcloud.

## Performance

### Bande passante maximale par connexion

1 Gbps / connexion.

Étant donné que la solution **S3 Object Storage OVHcloud** est un système hautement distribué, l’utilisation de **requêtes parallèles** vous aidera à surmonter cette limitation. En fonction de votre application et de votre cas d'usage, cette opération peut être effectuée en initiant simultanément des requêtes (également appelées *concurrent requests*).

Découvrez comment maximiser vos performances avec [ce guide](/pages/storage_and_backup/object_storage/s3_performance_optimization).

### Nombre maximum de requêtes par seconde en écriture sur un bucket

300 (au-delà de ce nombre, la qualité de service n'est plus garantie).

Cette valeur maximale est une limite souple qui peut être facilement dépassée en adoptant les bonnes pratiques pour répartir les E/S le plus largement possible dans le cluster de stockage objet, en tirant parti du **mécanisme de *sharding***.

Découvrez comment maximiser vos performances avec [ce guide](/pages/storage_and_backup/object_storage/s3_performance_optimization).

## Limitations du bucket

### Nombre maximum de buckets par projet

- 100 (par défaut)
- 1000 (nécessite une intervenion manuelle, veuillez [contacter notre support](https://help.ovhcloud.com/csm?id=csm_get_help) à cet effet)

### Nombre maximum d'objets dans un bucket

Illimité

### Attribution de noms

- Doit comporter entre 3 et 63 caractères.
- Doit commencer et se terminer par des caractères alphanumériques minuscules (de a à z et de 0 à 9).
- Doit être unique au sein d'OVHcloud.
- Peut comporter les signes de ponctuation suivants : « . » et « - ».
- Ne peut comporter plusieurs signes de ponctuation à la suite (« .. » ou « -. » ou « .- » ou « -- »).
- Ne peut ressembler à une adresse IP (192.168.1.1).

> [!warning]
>
> Pour une meilleure compatibilité, nous vous recommandons d'éviter d'utiliser des points (.) dans les noms de bucket, sauf pour les buckets qui sont utilisés uniquement pour l'hébergement de sites web statiques. Si vous incluez des points dans le nom d'un bucket, vous ne pouvez pas utiliser l'adressage de type *virtual host* en HTTPS, à moins d'effectuer votre propre validation de certificat. En effet, les certificats de sécurité utilisés pour l'hébergement virtuel des buckets ne fonctionnent pas pour les buckets dont le nom comporte des points.
>

## Limitations des objets

### Taille maximum par object / mpu / part

#### Via un seule requête PUT

Maximum 5 Go par objet (pour un objet dont la taille est supérieure à 5 Go, procédez à un *multi-part upload*).

#### Via un multi-part upload (MPU)

- La taille pour une seule *part* doit être comprise entre 5 Mo (minimum) et 5 Go (maximum)
- 10000 *parts* maximum en mpu

La taille théorique maximale d’un seul *Large Object* uploadé via MPU est donc de 48To.

### Nombre maximum de comptes utilisateurs par projet

1000

### Attribution de noms

- Doit comporter entre 3 et 63 caractères.
- Doit commencer et se terminer par des caractères alphanumériques minuscules (de a à z et de 0 à 9).
- Doit être unique au sein d'OVHcloud.
- Peut comporter les signes de ponctuation suivants : « . » et « - ».
- Ne peut comporter plusieurs signes de ponctuation à la suite (« .. » ou « -. » ou « .- » ou « -- »).
- Ne peut ressembler à une adresse IP (192.168.1.1).

<a name="features-matrix"></a>

### Disponibilité des fonctionnalités

<table>
    <tr>
        <th> Thème </th>
        <th> Fonctionnalité </th>
        <th> Operation </th>
        <th> Regions </th>
        <th> Local&nbsp;Zones </th>
    </tr>
    <tr>
        <td rowspan="8">Bucket management</td>
        <td rowspan="8">Bucket creation</td>
        <td> create bucket</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>delete bucket</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>list buckets</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>get bucket location</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>head bucket</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>put bucket tagging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket tagging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete bucket tagging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="7">Lifecycle operations</td>
        <td rowspan="4">Intelligent tiering</td>
        <td>delete intelligent tiering conf</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>put intelligent tiering conf</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>list intelligent tiering conf</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get intelligent tiering conf</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="3">Lifecycle policy</td>
        <td>put bucket lifecycle conf</td>
        <td>no</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>get bucket lifecycle conf</td>
        <td>no</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>delete bucket lifecycle conf</td>
        <td>no</td>
        <td>yes</td>
    </tr>
    <tr>
        <td rowspan="17">Access control</td>
        <td rowspan="4">ACL</td>
        <td>put bucket ACL</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>get bucket ACL</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>put object ACL</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get object ACL</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td rowspan="3">Block public access</td>
        <td>put public block</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get public access block</td>
        <td>no</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>delete public block status</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="4">Bucket policy</td>
        <td>put bucket policy</td>
        <td>no</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>delete bucket policy</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket policy status</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket policy</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="3">CORS</td>
        <td>put bucket cors</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>get bucket cors</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>delete bucket cors</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td rowspan="3">Object ownership</td>
        <td>put ownership controls</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get ownership controls</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete ownership controls</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="8">Immutability</td>
        <td rowspan="2">Versioning</td>
        <td>get bucket versioning</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>put bucket versioning</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td rowspan="6">Object lock</td>
        <td>put object lock configuration</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>get object lock configuration</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>put object legal hold</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get object legal hold</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>put object retention</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get object retention</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="7">Encryption at rest</td>
        <td>SSE-C</td>
        <td>n/c</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td rowspan="3">SSE-S3</td>
        <td>put bucket encryption</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete bucket encryption</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket encryption</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="3">SSE-KMS</td>
        <td>put bucket encryption</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete bucket encryption</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket encryption</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="18">Object management</td>
        <td rowspan="9">Single object creation</td>
        <td>put object</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>delete object</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>list objects v2</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>get object</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>delete objects</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>copy object</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>put object tagging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get object tagging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete object tagging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="6">Multipart upload</td>
        <td>create mpu</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>upload part</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>list mpus</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>complete mpu</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>abort mpu</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>list parts</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td rowspan="3">Metadata mgt</td>
        <td>get attributes</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>head object</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>list object versions</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td rowspan="2">Event driven architectures</td>
        <td rowspan="2">Event notification</td>
        <td>put bucket notification configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket notification configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="3">Resiliency</td>
        <td rowspan="3">Async replication</td>
        <td>get bucket replication</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete bucket replication</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>put bucket replication</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="15">Observability</td>
        <td rowspan="3">Server access logging</td>
        <td>get bucket logging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete bucket logging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td>put bucket logging</td>
        <td>yes</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="4">Bucket metrics</td>
        <td>put bucket metrics configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket metrics configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>list bucket metrics configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete bucket metrics configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="4">Storage class analytics</td>
        <td>put bucket analytics configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket analytics configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>list bucket analytics configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete bucket analytics configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="4">Bucket inventory</td>
        <td>put bucket inventory configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>get bucket inventory configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>list bucket inventory configurations</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td>delete bucket inventory configuration</td>
        <td>no</td>
        <td>no</td>
    </tr>
    <tr>
        <td rowspan="6">Web content</td>
        <td rowspan="3">Static web site</td>
        <td>put bucket website</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>get bucket website</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>delete bucket website</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td rowspan="3">Pre-signed urls</td>
        <td>GET</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>PUT</td>
        <td>yes</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>POST</td>
        <td>no</td>
        <td>yes</td>
    </tr>
    <tr>
        <td>Data analytics</td>
        <td>S3 Select</td>
        <td>select object content</td>
        <td>no</td>
        <td>no</td>
    </tr>
</table>

## Aller plus loin

Si vous avez besoin d'une formation ou d'une assistance technique pour la mise en oeuvre de nos solutions, contactez votre commercial ou cliquez sur [ce lien](/links/professional-services) pour obtenir un devis et demander une analyse personnalisée de votre projet à nos experts de l’équipe Professional Services.

Échangez avec notre [communauté d'utilisateurs](/links/community).
