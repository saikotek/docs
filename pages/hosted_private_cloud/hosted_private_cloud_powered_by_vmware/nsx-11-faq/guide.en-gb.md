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