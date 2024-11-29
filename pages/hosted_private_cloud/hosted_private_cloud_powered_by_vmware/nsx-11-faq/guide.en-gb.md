---
title: "NSX - FAQ"
excerpt: "Find frequently asked questions about the most common scenarios concerning the use of NSX within the Hosted Private Cloud ecosystem"
updated: 2024-11-05
---

## Objective

**Find below frequently asked questions and answers to your NSX usage**.

## Frequently asked questions - FAQ

> [!faq]
> What are the differences between <a name="diffencepack"></a> support packs
> > All packs are based on a day/hour count, e.g.: 1 day = 8 hours, 2 days = 16 hours (sometimes more).
> > The first approach is the same for all packs with a discovery phase, but the duration of the pack will depend on the complexity of the environment and the maturity of your current managed offer.
> > This issue will be explored with the [Professional Services](/links/professional-services) team in a first evaluation call.
> >
> How can I protect my virtual machines directly exposed on the internet with a Public IP? <a name="public ip"></a>
> > You can position the external interface of your virtual machines in an `ovh-t0-public` segment and then secure your flows with the NSX Distributed Firewall.
> >
> What is the end-of-life date for NSX-V? <a name="eofnsxv"></a>
> > VMware has decided to initiate the end of life (EOL) of NSX-V since January 2022. OVHcloud has been granted an extension of support until 31st July 2024.
> >
> What is the end-of-support date for NSX-T migration requests?
> > NSX-V’s end of life occurred on July 31, 2024. Since this date, the migration can no longer be carried out.
> >
> What is the maximum date on which to request migration support? <a name="deadlineassistance"></a>
> > This migration is no longer possible. However, you can [contact support](https://help.ovhcloud.com/csm?id=csm_get_help) or your technical account manager (TAM) if you need more information about your current options.
> >
> What happens if we haven’t migrated? <a name="nsxvmigrationend"></a>
> > OVHcloud does not delete the service, but we cannot guarantee the same level of service commitment (SLA). A document must therefore be signed in the form of a contractual clause setting out the liability on NSX-V's end of life since July 31, 2024 in the event of any problems.
> >
> Is it possible to do Border Gateway Protocol (BGP)? <a name="bgp"></a>
> > It is impossible to do public BGP (peer with OVHcloud internet routers).
> > However, it is possible to do (private) BGP with a vRack via a Tier-0 gateway or a VRF level 0 gateway, or in an IPsec tunnel via a Tier-0 only.
> >
> Is NSX-T BGP compatible across IPSEC? <a name="bgpoveripsec"></a>
> > Currently, BGP over IPSEC functionality is only available from a Tier-0 gateway (version earlier than 4.1.1). It is not possible to complete a VPN tunnel on a VRF level 0 gateway.
> > This operation requires specific rights with the Tier-0 gateway to create the tunnel.
> > If you have a specific use case, you can [open a ticket](https://help.ovhcloud.com/csm?id=csm_get_help) so that we can assist you in this configuration.
> >
> What is the change regarding the BGP autonomous system (AS)?
> > It is possible to position different AS numbers according to Tier-0 gateways or VRF level 0 gateways.
> >
> Can we put a virtual firewall in front of the Tier-0 in the same managed vSphere?
> > You can completely disconnect the public interfaces of the T0 and interconnect them via a private network or a security appliance exposed live on the internet.
> >
> What is the difference between a Tier-0 gateway and a Tier-1? <a name="t0vst1">
> > In VMware design, a Tier-1 is always attached to a Tier-0.
> > Flows pass through a Tier-0 to go to the external network.
> > All elements that need to remain inside (locally) the managed Vsphere platform are routed by the Tier-1.
> >
> How can I add another Tier-0 Gateway? <a name="addt0gw"></a>
> > It is currently not possible to add a new functional Tier-0 Gateway.
> > Depending on your needs, you can create a virtual Tier-0 instance called VRF. This VRF will not be able to be connected on the internet.
> >
> The "Edit" button in NSX for a Tier-0 is disabled, how can I configure the public Gateway? <a name="publicgateway"></a>
> > This is not possible by default. The Tier-0 Gateways are each hosted on a different host, HA (High Availability) is activated and a virtual IP (VIP) is configured between the 2 EDGES to maintain service continuity. The HA section is already preconfigured by OVHcloud.
> > This is no longer the case in version `4.1.1`.
> >
> Can I configure an active-active Tier-0 Gateway to have double bandwidth ("guaranteed" 10+10=20Gb/s and "theoretical" 25+25=50Gb/s)?
> > No, this is not possible by default. The configuration is managed by OVHcloud and is active/passive with a VIP (10 Gbps guaranteed bandwidth).
> >
> Is it possible to connect to the Tier-0 in the command line to perform diagnostics or packet capture? <a name="t0gwdoublebw"></a>
> > No, it is impossible for the Tier-0.
> >
> What is the maximum number of interfaces (connected segments) on a Tier-1 Gateway? <a name="t1interface capacity"></a>
> > This information can be found in the NSX-T `NSX > Inventory > Capacity`{.action} interface. To see how to log in to the NSX-T web interface, please refer to the following guide: [Enable NSX-T in a VMware on OVHcloud Hosted Private Cloud](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/nsx_add_user_rights).
> >
> > For Edges, we refer to Gateways and Tier-0 and Tier-1. The Tier-0 is already deployed and uses 3 public IPs to route between active/standby Gateways and uses the concept of a VIP that is upstream of the 2 internal public IPs. This device is used for failover and redundancy.
> > NSX and NSX-v are different, and at this time you cannot interrupt the current Tier-0 configuration and deploy more.
> >
> Is it possible to connect to Tier-1 at the command line to perform diagnostics or packet capture? <a name="t1commandline"></a>
> > No, it is impossible for the Tier-1. Different tools are available in NSX to meet these needs.
> >
> How do I add public IPs? <a name="addpublicicip"></a>
> > Additional public IPs can be added via "next hop" routing, specifying the managed VMware vSphere environment (pcc) as a resource, and the public virtual IP (VIP) of the T0 as the `next hop`.
> >
> Can IP address blocks be used/distributed between two VMware DCs in the same managed vSphere? <a name="ipblockdistribution"></a>
> > IP address blocks are dependent on the VMware vSphere managed environment (pcc) and not on the vDC. It is therefore possible to use the same IP address block between several virtual datacentres (without any modification).
> > A block of public IPs routed on the virtual IP (VIP) of your T0 cannot be used in another VMnetwork vDC. The subnet defined on the T0 interface can be used on other vDCs of the same vSphere managed via the NSX `ovh-t0-public` segment.
> >
> Do we need to update the clusters in order to use NSX-T in a Vsphere `7.0.3` environment? <a name="updatensxtvsphere703"></a>
> > In this case, you do not need to update the clusters.
> >
> How are IPs managed during the migration? <a name="managemigrationip"></a>
> > You can find out how to move your existing IP from your NSX-V platform, and route it to the IP attached to the T0 section in the [migration guide](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/service-migration-vdc).
> > When an NSX-T vDC is delivered, we deploy and configure a new IP block for NSX T0 (VIP + NSX EDGES). You can reuse the IP attached to the NSX-V DC and point it to the new vDC.
> >
> For vDC migration, you need to switch the DS to global. Can we rollback this configuration? <a name="vdcmigration"></a>
> > The global datastore is managed via the OVHcloud Control Panel or API.
> > This allows you to globalize your datastore, which will be visible from your new vDC. It allows you to make a vMotion "Compute" and not a vMotion "Storage" of the virtual machines.
> > In this case, you cannot restore your data. You will need to order a new datastore and apply a vMotion to free it up globally.
> >
> What is the impact of migrating to NSX-T `4.1.1`? <a name="nsxmigrationimpact"></a>
> > There is normally no downtime, a maintenance task will be initiated, including a move of the Edges with a vMotion.
> > No specific tasks need to be scheduled on your managed environments.
> >
> Will you provide training and documentation to improve NSX-T skills? <a name="docandtrainingnsxt"></a>
> >
> > - [Getting started with NSX](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/nsx-01-first-steps)
> > - [VMware on OVHcloud](/products/hosted-private-cloud-hosted-private-cloud-powered-by-vmware)
> >
> If an NSX-V migration has been planned to a third-party pfSense solution, should we restart with a request to create a new vDC without NSX-V? Can it be done on the existing vDC? <a name="nsxtmigrationpfsense"></a>
> > In this case, you do not need to order a new vDC, but make sure to disable all your NSX-V features so that OVHcloud can disable the component.
> >
> Can I configure Internet output? In other words, is it possible to deploy the interface? <a name="internetoutput"></a>
> > It is not possible to manage internet output in NSX as Edge is managed by OVHcloud, but you can configure the network on your VM (managed vSphere).
>
> Can IP migration be done IP by IP or IP block? <a name="ipmigrationperblock"></a>
> > IP migration is done by block, you change the *next stop* of the IP block, the global block is transitioned to the NSX part.
> >
> Does this migration interrupt the service? If so, how long? <a name="ipmigrationinterruption"></a>
> > This will depend on the services you use. For example, if you use IPSEC tunnels and public IPs, you will need to move your workloads and reconfigure the IP block you had on your NSX-V infrastructure to your NSX-T infrastructure.
> > When moving an IP, a short service outage may occur. Depending on your network topology, you can have continuity via the vRack service of the flows between the different workloads supported by an exposure of the NSX-V fronts, you move the different machines to the second DC and through the vRack the flow continues to go back to your previous NSX-V fronts.
> > Downtime depends on the complexity of your environment.
> >
> How much bandwidth will the edge-node cards have, knowing that the T0 will be shared? <a name="bandwidthedgenode"></a>
> > This will depend on which services are enabled (LoadBalancer/NAT/Firewall, etc.)
> >
> Does the vRack work with NSX-T?  <a name="vrackwithnsxt"></a>
> > Yes, the vRack works with NSX-T.
> > You can access it from groups of ports in vSphere or VLAN segments using NSX.
> >
> Will the VM cluster have access to the OVHcloud vRack? Or will the vRack be connected to the edge nodes? <a name="vrackaccess"></a>
> > The NSX cluster is compatible with an OVHcloud vRack. You can add the NSX service in the vRack of your managed VMware vSphere (pcc). Find more information on [this page](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/vrack_and_hosted_private_cloud).
> >
> Can I configure High Availability (HA)? <a name="ha"></a>
> > No, the NSX Edge routers are configured by OVHcloud following the official VMware high availability (HA) private infrastructure management best practices.
> >
> Is it possible to have multiple edge clusters? <a name="multipleedgeclusters"></a>
> > Today, only 1 Edge NSX-T cluster is required.
> >
> Currently, we have 300 edges and around 5000 simultaneous RDPs. Will the average configuration "4 vcpu / 8 GB RAM / 200 GB" hold for flows? <a name="averageconfiguration"></a>
> > Sizing will depend on the services you enable or consume on your edges (firewall or load balancing).
> > Today, the Medium size edge node may not be suitable for you, the `4.1.1` version will grant you new features such as “Edge nodes scale up”, allowing you to switch to L or XL profiles.
> > It all depends on your use cases and the metrics you have on your platform.
> >
> If we don’t want a VRF to split the T0, what would be the solution other than training or buying a new managed vSphere? <a name="VRF"></a>
> > It is possible not to use VRF and to use T1.
> > You can use a T1, which hosts the workloads that support it. In this case, the T1 is used as a "mini" VRF but the flows will be mixed inside the T0.
> > The advantage of doing a VRF in T0 is maintaining the partitioning of the routing table of the elements going to the external network of your managed VMware vSphere platform.
> >
> Can I use the OVHcloud API to configure and use NSX? <a name="api"></a>
> > Yes, it is possible to do this. Here is an example of an API v1 call that you can use within the **/dedicatedcloud** universe:
> >
> > > [!api]
> > >
> > > @api {v1} /dedicatedCloud PUT /dedicatedCloud/{serviceName}/datacenter/{datacenterId}/cluster/{clusterId}/nsxt
> > >
> >
> > > **Settings**:
> > >
> > > - `clusterId`: ID of the managed vSphere cluster (example: 2010).
> > > - `datacenterId`: ID of the managed vSphere datastore (example: 1254)
> > > - `serviceName` : Name of the managed vSphere (example: pcc-XXX-XXX-XXX).
> > >
> How do I migrate with Zerto solutions? <a name="migrationzerto"></a>
> > Simply follow the steps in the documentation provided by OVHcloud:
> >
> > - [Use Zerto between OVHcloud and a third-party platform](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/zerto_virtual_replication_as_a_service)
> > - [Use Zerto Virtual Replication between two OVHcloud datacentres](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/zerto_vm_replica_deletion)
> >
> What do I do with my Veeam backup and Zerto replication options? Are they still compatible with NSX? <a name="veeamzerto"></a>
> > Yes, but you will need to reconfigure them after migrating your virtual datacentre (vDC).
> >
> Is it possible to combine our NSX-V and NSX-T managed vSphere during the transition phase? <a name="nsxtwithnsxv"></a>
> > You can get NSX-T if you order a new vDC.
> > Please note that ordering the new vDC will automatically trigger the refund mechanism for the coming month.
> >
> How long will the migration take? <a name="nsxvtonsxtmigration"></a>
> > This will depend primarily on the NSX-V infrastructure discovery/assessment phase and the NSX-T side design phase.
> > The migration itself is short, it is a reconfirmation of the VMware stack.
> > It is possible to create a wide area network, a VPN between the two environments, vxLAN for NSX-V and segments with NSX-T, allowing to move VMs from one vDC to another and then perform the migration steps. This will limit service downtime during the transition.
> > You can also include Terraform in your NSX-T design to push your Terraform configuration directly into the environment you just ordered.
> >
> Can we use "migration coordinator" for migration between nsx-v and nsx? <a name="nsxmigrationcoordinator"></a>
> > This tool requires very strong administrative rights on the environment. The Professional Services team can validate the execution and the duplication. In this tool, it is important to note that many elements are not supported (options, existing rules in NSX-V).
> > The reproduction phase would require a lot of adaptations on your part, so it is not a recommended tool in the migration.
> >
> Why is NSX management through Terraform done via a separate `https://nsxt` endpoint? <a name="nsxterraform"></a>
> > The NSX API is independent and not linked to the vSphere API. This is why we have created a dedicated endpoint to reach it.
> >
> Is it possible to connect an NSX Edge router between 2 managed VMware vSphere environments? <a name="nsxedge"></a>
> > Yes, it is possible.
> >
> Do you carry out backups of the NSX configurations, including manual client configuration? <a name="nsxbackupmanualconfiguration"></a>
> > Yes, OVHcloud performs backups. You can find them in your NSX-T control panel.
> > This backup is not intended for restoration when it is improperly handled, but for support in the event of corruption of the various NSX-T controllers.
> >
> Is it possible to have the delivery of a vDC NSX-T in a VMware vSphere managed of the year 2016, will there be problems during the delivery? <a name="nsxtinto2016pcc"></a>
> > Yes, it is possible, there are no constraints currently.
> >
> Are there any additional limitations in a SecNumCloud context? <a name="sncliitations"></a>
> > There are no additional limitations compared to an unqualified SecNumCloud environment.
> >
> In a SecNumCloud context, is the migration going the same way? <a name="sncmigration"></a>
> > Yes, both migrations are identical.
> >
> Is there a backup outside of SecNumCloud? <a name="semnumcloudbackupoutside"></a>
> > There is no difference between backups in SecNumCloud and non-SecNumCloud qualified environments.
> >
> Why is there a price change for NSX-T and its version `4.1.1`? <a name="pricingnsxton411version"></a>
> > The price increase for NSX solutions is based on:
> >
> > - inflation-based cost increases for all of our services in 2022 and 2023.
> > - NSX-T license fees.
> > - Costs related to the NSX management infrastructure.
> >
> Will the dates and initial price of managed environments be retained during a migration for the duration of the engagement? <a name="pricemigrationpcc"></a>
> > The commitment and conditions will not be automatically maintained.
> > We invite you to contact your preferred contact at OVHcloud in order to set up new commercial conditions.
> >
> During the migration phase, will we have to pay twice for our platform for one month, and then be reimbursed the following month? <a name="priceduringmigration"></a>
> > OVHcloud will refund 1 month of NSX hosting and management fees on your next bill after ordering your new virtual datacentre (vDC) (1 month = 30 days).
> >
> Is there an additional cost to using the Advanced Load Balancer (with WAF) and a distributed IPS/IDS? <a name="pricealbandipsids"></a>
> > Yes, the basic version of the load balancer application with firewall (ALB + WAF) is not included in the NSX-T license. We will offer it as an additional option.

## Go further

[Getting started with NSX](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/nsx-01-first-steps).

If you require training or technical support to implement our solutions, please contact your sales representative or click [this link](/links/professional-services) to get a quote and request a custom analysis of your project from our Professional Services team experts.

Join our [community of users](/links/community).
=======
**Find below the frequently asked questions about NSX.**

## FAQ

<a name="diffencepack"></a>

### What are the different assistance packs? What are the differences between the packs?

All packs are based on days (1 day = 8 hours); 1 day, 2 days or more.

The first approach is the same for all packs with a discovery phase but the duration of the pack will depend on the complexity of the environment and the customer maturity.

This would be discussed with the PS team during a first assessment call.

<a name="public ip"></a>

### How can I protect my virtual machines exposed on the internet directly, with a Public IP?

You can create virtual machines in the ovh-t0-public segment, and then secure your flows with the NSX Distributed Firewall.

<a name="eofnsxv"></a>

### What is the deadline for the NSX-T migration? What is NSX-V End of Life date?

NSX-V End of Life is planned for the 16th of January 2024, the migration has to be performed before this date. 

<a name="deadlineassistance"></a>

### What is the last date on which you can request migration support?

NSX-V End of Life is planned for January 16th of 2024, so the sooner you take action, the more time to perform your migration.

<a name="nsxvmigrationend"></a>

### What happens if we have not migrated before the 16th of January 2023?

OVhcloud will not cut the service but won't be able to guarantee any SLA. Customers will have to sign a document committing to leave NSX-V at a certain given date by OVHcloud. 

VMware has decided the NSX-V End of Life in January 2024. Discussions are still on-going with them regarding the NSX-V extension of support, OVHcloud will communicate as soon as possible an official statement.

<a name="bgp"></a>

### Is it possible to do BGP?

It is not possible to do Public BGP.

Though it is possible to do BGP in the vRack, a documentation will be available soon to detail this workaround.

<a name="bgpoveripsec"></a>

### Is NSX-T compatible with BGP over IPSEC?

Currently, the BGP over IPEC feature is only available from a T0 (version before 4.1.1 release).

This operation requires specific rights at T0 to create the tunnel.

If you have a specific use case, you can open a ticket so we can support you in this configuration.

<a name="changeas"></a>

### What are the change on the AS?

Before the 4.1.1 version, there is one AS number per environmen coming from the T0.

Opening a ticket with the Support, you can request a modification on the AS number.

With the 4.1.1 version, you will be able to set up different AS on the VRF and not have necessarily the AS number from the T0.

<a name="virtualfirewallt0pcc"></a>

### Can we put a virtual firewall in front of the T0 in the same PCC?

Today it is not possible. The T0 already has a gateway firewall feature so we recommend to configure the firewall with the T0.

<a name="t0vst1">

### Can you explain the difference between T0 and T1?

In the VMware conception, a T1 is always attached to a T0.

Flows go through the T0 to go to the external network.

All the elements that have to stay insinde the Vsphere platform are routed by the T1.

<a name="addt0gw"></a>

### How can I add another Tier-0 Gateway?

It is currently not possible to add a new working tier-0 Gateway.

<a name="publicgateway"></a>

### The "Edit" button in NSX for Tier-0 is disabled, how do I configure the public gateway?

It is not possible by default. The Tier-0 gateways are each hosted in a different host, HA (High Availability) is enabled and a VIP is configured between the 2 EDGES in order to maintain service continuity. The HA part is already preconfigured by OVHCloud.

<a name="t0gwdoublebw"></a>

### Can I configure an active-active Tier-0 Gateway in order to have a double bandwidth (10+10=20Gb/s guarantee and 25+25Gb/s "theoretical")?

No, it is not possible by default, the configuration is managed by OVHcloud and is done in active/passive mode with a VIP (10 Gbp/s guaranteed bandwidth).

<a name="t0commandline"></a>

### Is it possible to connect to the Tier-0 from the command line to perform debugging or packet capture?

No, this is not possible for Tier-0.

<a name="t1interfacecapacity"></a>

### What is the maximum number of interfaces (connected segments) on a Tier-1 Gateway?

This information can be found in NSX > Inventory > Capacity.

Regarding the Edges, we refer to the Gateways and the Tier-0 and Tier-1. Tier-0 is already deployed and uses 3 public IPs to route between the active/backup Gateways and uses the concept of a VIP that is in front of the 2 internal public IPs. This is used for failover and redundancy.

NSX and NSX-v are different and at the moment you cannot break the current Tier-0 configuration and deploy others.

<a name="t1commandline"></a>

### Is it possible to connect to the Tier-1 from the command line to perform debugging or packet capture?

No, this is not possible for Tier-1. Different tools are available in NSX to address these needs.

<a name="addpublicip"></a>

### How can I add more Public IPs?

As indicated in [this guide](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/nsx-01-first-steps#displaying-the-ha-vip-virtual-ip-address), at the moment it is not possible to create new virtual IP addresses, but this feature should be available soon.

<a name="ipblockdistribution"></a>

### Can IP address blocks be used/distributed between two VMware DCs in the same PCC?

IP address blocks are PCC-dependent, not vDC-dependent. Therefore it is possible to use the same IP address block between multiple virtual data centres (without any changes).

<a name="updatensxtvsphere703"></a>

### Do we need to update the clusters in order to use NSX-T in a Vsphere 7.0.3 environment?

In this case you don't have to update the clusters.

<a name="managemigrationip"></a>

### How do we manage the IPs during the migration?

You will find into [the migration guide](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/service-migration-vdc/), how to move your existing IP from your NSX-V platform and route them to the IP attached to the T0 part.

When a NSX-T vDC is delivered, we deploy and configure a new IP Block for NSX T0 (VIP + NSX EDGES). You will be able to re-use the IP attached to the NSX-V DC and point them to the new vDC.

<a name="vdcmigration"></a>

### For the vDC migration, the data store has to go global, is a roll back possible on this configuration?

The global data store is managed at the manager or API level.

This allows you to globalise your data store which will be visible from your new vDC. It allows you to do a compute Vmotion and not a storage Vmotion of the VMs.

In this case a roll back is not possible, you would have to order a new data store and apply on it a Vmotion to free the global one.

<a name="nsxmigrationimpact"></a>

### What is the customer impact of the NSX 4.1.1 migration?

There is normally no downtime, a maintenance task will be initiated, including a move of the edges with a Vmotion.

From your user side, there is no specific task to plan.

<a name="docandtrainingnsxt"></a>

### Will you provide trainings and documentation to improve NSX-T skills?

- [Getting Started with NSX](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/nsx-01-first-steps)
- [VMware on OVHcloud](products/hosted-private-cloud-hosted-private-cloud-powered-by-vmware)


<a name="nsxtmigrationpfsense"></a>

### If we have anticipated the NSX-T migration and chose a PfSense tier solution, do we still have to request a new vDC creation without NSX-T? Can we do it on the existing vDC?

In this case you don't have to order a new vDC but make sure you deactivate all your NSX-V features so OVHcloud can disable the component.

<a name="internetoutput"></a>

### Is the Internet output configurable? In other words, can I deploy the interface?

It is not possible to manage the Internet output in NSX as the Edge is managed by OVHcloud, but you can configure the network on your VM (vSPHERE).

<a name="ipmigrationperblock"></a>

### Can the IP migration be done IP per IP or by block?

The IP migration is performed by block, you will change the next stop of the IP block, the global block is transitioned to the NSX part.

<a name="ipmigrationinterruption"></a>

### Will this migration cut the service and if yes, how long?

This will depend on the used services. For example, if you are using IPSEC tunnels and public IPs, you will have to move your workloads and reconfigure the IP block you had on your NSX-V insfrastructure to your NSX-T one.

During this IP move, a short service cut can happen. Depending on your network topology, you can have a continuity via the vRack service of the flows among the different workloads carried by an exposition of the NSX-V edges. You move the different machines to the second DC and through the vRack the flow keep rising to your previous NSX-V edges.

The downtime will thus depend on your environment's complexity.

<a name="bandwidthedgenode"></a>

### What will be the bandwidth of the edge node's cards, knowing T0 will be mutualised?

This will depend on the activated services (LB/NAT/Firewall, etc.)

<a name="vrackwithnsxt"></a>

### Does vRack work with NSX-T ?

Yes, vRack works with NSX-T.

You can access it from port groups in vSphere or vLAN segments inside NSX.

<a name="vrackaccess"></a>

### Will the compute cluster have access to vRack? Or will the vRack be connected only to edge node?

The NSX cluster is fully compatible with vRack. You can add the NSX service in your PCC vRack. Find more information about vRack on [this page](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/vrack_and_hosted_private_cloud).

<a name="ha"></a>

### Can I configure High Availability (HA)?

No, NSX Edges are configured by OVHcloud following VMware best practices regarding HA.

<a name="multipleedgeclusters"></a>

### Can we have multiple edge clusters?

Today, 1 single NSX-T Edge cluster is necessary.

<a name="averageconfiguration"></a>

### We currently have 300 edges and about 5000 simultaneous RDP, will the average configuration "4 vcpu / 8 Go RAM / 200 Go" manage the flows?

The sizing will depend on the services you activate or consume on your edges (firewalling or loadbalancing).

Today the size M edge node might not fit for you. The 4.1.1 release will grant you new features like "edge nodes scale up", allowing you to raise to L or XL profiles.

All this will depend on your use cases and the metrics you have on your platform.

<a name="VRF"></a>

### If we don't want to have a VRF to split the T0, what would be the solution besides training or buying a new PCC?

It is possible not to use the VRF and use the T1.

You can use a T1, hosting the workloads behind it. In this case the T1 is used as a "mini" VRF but the flows will be mixed inside the T0.

The advantage of doing a VRF in T0 is to maintain the partitioning of the routing table of the elements going to the external network of the vSphere platform.

<a name="api"></a>

### Can I use the OVHcloud API to configure and use NSX?

Yes, it is possible to do so.

<a name="migrationzerto"></a>

### What about Zerto in the migration phase?

There are no complexities in this part, you can follow step by step the documentation OVHcloud provides.

<a name="veeamzerto"></a>

### What about my Veeam and Zerto options? Are they still compatible with NSX?

Yes but you will have to reconfigure them after vDC migration.

<a name="nsxtwithnsxv"></a>

### Is it possible to have on our PCC NSX-V and NSX-T at the same time to perform tests?

It is possible if you order a new vDC to get NSX-T.

Please note that ordering the new vDC will automatically initiate the refund mechanism for the coming month.

<a name="nsxvtonsxtmigration"></a>

### How long will the migration take?

This will mainly depend on the discovery/assessment phase of the NSX-V insfrastructure and the design phase on the NSX-T side.

The migration itself is short, it is a re-confirmation of the VMware stack.

It is possible to create an extended network, a VPN between the two environments, vxLAN for NSX-V and segments with NSX-T, allowing to move VMs from a vDC to another and then to perform the migrations steps. This will ease the service cut during the transition.

You can also include Terraform into your NSX-T design in order to push your Terraform configuration directly into the environment your just ordered.

<a name="nsxmigrationcoordinator"></a>

### Can we use "migration coordinator" for the migration between NSX-V and NSX-T?

This tool requires very strong administration rights on the environment, our Professional Services team can execute and duplicate the confirmation. In this tool, it is important to notice that many elements are not supported (options, existing rules in NSX-V).

The reproduction phase would require lots of adaptation from your part so it is not a recommended tool in the migration.

<a name="nsxterraform"></a>

### Why is NSX management via Terraform done via a separate `https://nsxt` endpoint?

The NSX API is dedicated and not linked to the vSphere API. That's why we created a dedicated endpoint to reach it.

<a name="nsxedge"></a>

### Is it possible to communicate an NSX edge between 2 PCC?

Yes, it's possible.

<a name="nsxbackupmanualconfiguration"></a>

### Do you take NSX configuration backups, including for the customer manual configuration?

Yes, OVHcloud is performing some backups, you can see them into your NSX-T control plane.

This backup is not aimed to allow you to do a roll back in case of wrong configuration from your end but exist in case of corruption of the different NSX-T controllers.

<a name="nsxtinto2016pcc"></a>

### Is it possible to have the delivery of an NSX-T vDC in a 2016 PCC or are there delivery issues?

Yes, it is possible, there are no current constraints.

<a name="etarelease"></a>

### What is the ETA for the NSX 4.1.1 release?

ETA is planned for the end of October 2023.

<a name="snclimitations"></a>

### Are there additional limitations in a SecNumCloud context?

There are no additional limitations compared to a non-SNC environment.

<a name="sncmigration"></a>

### Is a SecNumCloud migration the same as a non SNC migration?

Yes both migrations are the same.

<a name="sncbackupoutside"></a>

### Is there any backup outside SecNumCloud?

There is no difference between SNC and non-SNC regarding the backup.

<a name="pricingnsxton411version"></a>

### Why is there a pricing modification for NSX-T and its 4.1.1 version?

The price increase on the NSX offers is based on: 

    - The raise in our costs based on the inflation on all our services in 2022 and 2023.
    - The NSX-T licensing costs.
    - The costs linked to the NSX management insfrastructure.

Waiting for the availability of the NSX 4.1.1 version, physical ressources dedicated the to NSX Edge VM hosting have been assumed by OVHcloud and have not been charged to you.

In consequence, the transition to the 4.1.1 version won't have any pricing impact.

<a name="pricemigrationpcc"></a>

### Will the commitments dates and initial prices be maintained after the migration?

Commitment and conditions won't be automatically maintened.

Please get in contact with your preferred OVHcloud contact in order to set up new commercial conditions.

<a name="priceduringmigration"></a>

### During the migration phase, we will have to pay twice for our platform for one month, and then get reimbursed next month?

OVHcloud will refund 1 month of hosts and NSX management fees on the next invoice following the order of your new vDC (1 month considered as 30 days).

<a name="pricealbandipsids"></a>

### Is there an additional cost to use Advanced LB (with WAF) and a distributed IPS/IDS?

The basic version of ALB is already included in the NSX-T licence version, without additional cost.

IPS/IDS is planned to be released in the future without precise ETA for now, with additional cost.

## Go further <a name="gofurther"></a>

[Getting started with NSX](/pages/hosted_private_cloud/hosted_private_cloud_powered_by_vmware/nsx-01-first-steps)

If you need training or technical assistance to implement our solutions, contact your sales representative or click on [this link](https://www.ovhcloud.com/en-gb/professional-services/) to get a quote and ask our Professional Services experts for a custom analysis of your project.

Join our community of users on <https://community.ovh.com/en/>.

