Build-Measure-Learn principle
============================
* Build ( Deliver on a hypothesis based on customer empathy . Build an MVP to meet a defined customer need)
* Measure ( Test the hypothesis based on customer observations . Build a growth mindset by candidly testing assumptions)
* Learn ( Apply a growth mindset through continous learning. Turn fast fails into impactful change )

Formula for innovation
======================

Innovation = invention + adoption


Growth mindset
==============
* Customer first. We have to meet customers where they are.
* Continous learning. Methodology learn-it-all not know-it-all.
* Beginner mindset. Demonstrate empathy by approaching every conversation with a beginner mindset.
* Listen mode. Speak less and listen more
* Encourage others. Use the thins you do say to encourage others. Pull diverse perspectivs from others
* Share the code. Focus on owning the outcome, share the code to invite the diverse perspective.  

Azure networking overview
=========================
* DC Hardware
    * SmartNIC
    * FPGA
    * Sonic
* Services
    * Virtual Networking
    * Load Balancing
    * VPN Services
    * Firewall
    * DDos Protection
    * DNS and Traffic Management
* Intra-region
    * DC Networks
    * Regional Networks
    * Optical Modules
* WAN Backbone
    * Software WAN
    * Subsea Cables
    * Terrestrial Fiber
    * National Clouds
* CDN
    * Acceleration for application and content
* Edge and ExpressRoute
    * Internet Peering and ExpressRoute
* Last Mile
    * E2E monitoring
        * Network Watcher
        * Network Performance monitoring

Inside Azure Region
===================
* Edge (Connects Region to Internet and Enterprise peers)
* *Regional Network Gateway* 
    * Connects Regions to Regions, DC to DC
    * Contiguous geographical area ~ 100km in diameter
    * T-shirt sized (28 to 528MWatts region scale)
* Data Centers
    * AZ to AZ latency - 1.0 ms
    * Network latency perimeter ~ 2.0 ms

Availablity Zones
=================
* Miniumum 3 ( independent power,cooling)
* Unique physical locationw within Azure Region
* Each zone made from >=1 DC
* Fault-tolerant to protect from DC failure
* To serve quorum-based workloads

Paired Regions
==============
* Region usually srart from the definition of Data sovereignty boundary
  * Data sovereignty is the idea that data are subject to the laws and governance structures within the nation it is collected. 
* Disaster Recovery on top of Azure, so environmental disasters are not affect ( hurricanes, floods )

Azure Region Connectivity
=========================
* Azure Region connected to teh MS WAN via two *Rings*
* Each DC(=AZ) connected to both rings
* Express Route and Internet Peers connected to MS WAN
* Redundant connectivity = Connectivity to WAN and between AZ is preserved

Technology used in backbone
===========================
* DWDM 15 Terabit per second
* Connectivity to very remote locations - Azure Orbital

Software Defined Network
========================
* SDN policies applied via agents on host
* SDN stack coupled to Azure Hosts and VMs
* Azure Host servers multiple needs such as compute, network and storage

Azure Host 
==========
* Each VM connected to Virtual Filtering Platform (VFP) by 10Gbps
* [VMs] -> [Virtual Filtering Platform(VFP)] -> [NICs -- policy] -> SDN Agents -> pNIC(50 Gbps NIC + FPGA)

Main Network topologies in Cloud
================================
* Mesh
* Hub and Spoke

Advances in Networking 
======================
* **Centralized Network Management**
* Build and manage complex network topologies (mesh , hub and spoke)
* Create network scopes to group networks by org/function
* Apply connectivity, security, and routing configurations across regions and subscriptions
* Safe deployment of policy changes with defined frequency across regions
* Demo by Mark Russinovich 

Azure Resource Manager
======================
* Azure Resorce Manager is an universal control plane for all Azure Services

Architecture of Azure Resource Manager
======================================
1. Rest API
2. SDK, CLI and PowerShell, AzurePortal
3. ARM
    1. RBAC
    2. Activity logs and telemetry
    3. ARM Configurations
        1. Resrouce metadata
        2. Resource groups
        3. Subscriptions
        4. Management groups
        5. Tags
    4. ARM Resource Proviers (ARM is a front door to Resource Providers)
            * Bot framework
            * IoT hub
            * App Services
            * Key vaults
            * ARC for servers
            * Service fabric
            * AKS
            * SQL
            * Azure functions
            * Event grid
            * ARC for Kubernetes
            * Compute RPs
            * Networking RPs
            * Storage RPs
            * ARC for data services
    5. Built on top of 
        1. Azure Fabric Controller
        2. Hardware Manager
        3. Azure infrastructure
        4. Edge infrastructure
        5. On-prem infrastructure
    6. ARM Strength : Declarative JSON Definitions ( Verbose )
        1. Projcet Bicep -> Simple declarative language to provision infrastructure on Azure
            * Intuitive
            * Transpiles to ARM Templates
            * Modular
            * OpenSource
            * Bicep language -> ARM Templates -> Azure Resource Manager -> ResouceProviders,ARC,Kubernetes,GitHub,3rd party extensions
            * Much more consice vs ARM JSON definitions
            * More user friendly resource name refrences
            * bicep build -> create JSON

Microservice applications in enterprise
=======================================
1. Stateful/Stateless function as a service
1. Pub/Sub
1. Triggers


API Models
==========
1. REST
1. gRPC
1. OpenAPI

Azure API Management
====================
* API Security
* Legacy services transformation
* Decoupling Front-end from Back-end

Service Mesh
============
* Service Mesh is a dedicated infrastructure layer for facilitating service-to-service commnitcations between microservices, often using a sidecar proxy
* Istio, Linkerd, Consul, NGINX
* Observability, Security and Reliability
* Service Discovery, Load Balancing, Health Checks, Access Control
* Mutual TLS

Azure 2020
==========
* 160k miles of fiber and undersea calbles
* 170+ Edge Sites
* 500+ Network Partner
* 1M+ miles of fiber cable per dc
* 61 Azure region

Servers
=======
* Optimized for high-memory / high-compute ( SAP ) workloads
  * 24 TB, 448 Cores
* Deep Learning workloads(Multi-GPU)

Azure FrontDoor
===============
* Works on Layer 7 (HTTP/HTTPS) using Anycast
* Route to the fastest and most available backend
  * Traffic routing methods
  * Backend health monitoring options

Delivery methods comparsion
===========================
* Questions to ask
  * Global or regionial
  * HTTP(s) vs non-HTTP(s)
  * SLA
  * Features
  * Internet-facing ?
* Azure FrontDoor | Global / HTTPs
* DNS-based global routing -> Traffic Manager | Global/non-HTTPs
* Load balance between servers in a region at application layer -> Application Gateway | Regional / HTTPs
* Network Load balancing -> Load Balancer | Global / non/HTTPs

Azure Edge Zone (preview)
=========================
* Enables data processing close to the user

Storage offerings
=================
* Disk Storage (Ultra,Premium,Standard)
* Object Storage (Azure Blob)
* File Storage (Azure Files)
* Backup (Azure Backup)
* Data Transport (Azure Data Box)
* Hybrid Storage (Azure File Sync,Stack Edge)
  
Azure Storage Architecture
==========================
>             Location Services  -----> DNS
>                     |
>                     V
>                    VIP
>                     |
>                     V
> REST API: ADSL,Blob,File,Table,Queue  File:NFS,SMB
> |
> | FrontEnd Layer: Request Handling, Partition Map, AAA
> |
> | Partition Layer: Blobs, Tables & Queues, Load Balancign, Cacing, Strong Consistency (All accesses are seen by all parallel processes (or nodes, processors, etc.) in the same order (sequentially))  ** REPLICATION HERE - across regions / Cluster Group **
> | 
> | Stream Layer: Streams, Extents, Blobs, Intra-Stamp Replication
> | ------------------------------------------------------------
> |                   HARDWARE : SSD,HDD, Archive

Azure Storage Directions
========================
* Using DNA for storage
* Holographic storage

Azure Traffic Manager
=====================
* Working on DNS Layer ; Design to working with ANY Service
* Enable geographically disperse regions
* CNAME -> ____.trafficmanager.net
* 6 routing methods
  * Performance ( closest one )
  * Weighted ( prefer one ) in rollout scenarios
  * Priority
  * Geographic - Based on origin
  * Muti-value - return multiple values
  * Subnet - source based
* Set Custom header value
* Expected Range of responses ( health check )
* Endpoints
  * Internal
  * External
  * Nested -> Anoter TM

Azure Service Matrix
====================
* Connect
  * Virtual Network
  * Virtual WAN
  * Express Route
  * VPN
  * DNS
* Protect
  * DDOS Protection
  * Firewall
  * NSG
  * Web Application Firewall
  * Virtual Network Endpoints
* Monitor
  * Network Watcher
  * Express Route Monitor
  * Azure Monitor
  * Virtual Network TAP
* Deliver
  * CDN
  * FrontDoor
  * TrafficManager
  * Application Gateway
  * Load Balancer

Azure Delivery methods comparison
=================================

Azure Load Balancer|Azure Application Gateway|Azure Traffic Manager|Azure Front Door
-------------------|-------------------------|---------------------|----------------
Works on L4 OSI    | Works on L7 OSI         | DNS bsed LB (only at domain level) | Offers L7 capabilities
Health probes TCP/HTTP | Health probes as HTTP/HTTPS | HTTP/HTTPS/TCP | synthetic HTTP/HTTPS in form of GET/HEAD
Standart/Basic SKU|Standart/Basic SKU|NA|NA
Recently becomes Global LB | Regional LB | Global | Global
Azure VM | Any IP Address | Public DNS CNAME | Various(App service,cloud service, storage, App GW, API Mgmt, Public IP)
TCP&UDP|HTTP,HTTPS,HTTP/2 & WebSocket|DNS Resolution|HTTP,HTTPS, HTTP/2
Sticky sessions supported|Sticky sessions supported|Sticky sessions supported|Sticky sessions supported
NSG provide traffic control|NSG|Geo-traffic replication|
NA|WAF|NA|WAF


Difference between HTTP and HTTP/2
==================================
HTTP1.1 keep all requests and responses in text format, HTTP/2 using binary encoding


Azure Load Balancer
===================
* Solve problem of high-availablity
* Layer 4 resource ( FrontDoor is on Layer 7)
* Public or Inernal
* SKU difference
  * Scale
  * HTTPS for health checks
  * HA Ports

Microsoft Well-Architected framework
============================================
* Cost Optimization ( Managing costs to maximize the value delivered )
* Operational Excellence ( Operations processes that keep a system running in production )
* Performance Efficience ( The ability of a system to adapts to changes in load )
* Reiliability ( The ability of a system to recover from failures and continue to function )
* Security ( Protecting applications and data from threats )

Cost Optimization
=================
* What Actions are you taking to optimize cloud costs ?
  * Identify opportunities to reduce overall cost
  * Use cost management tools to plan and track costs
  * Tag my resources and track that back to costs
* How do you ensure that cloud resources are appropriately provisioned ?
  * Automate based on the application lifespan
  * Use DevOps and deployment automation
  * Configue auto-scale policies for my workloads
  * Select the right resource offering size (VM,disk, database)
  * Choose appropriate services that match my business requirements
* How is your organization modelling cloud costs ?
  * Estimate and track my costs
  * Educate the employees about the cloud and various pricing models
  * Teach employers about expences
* How do you manage the storage footprint of your digital assets ?
  * Track data flows in/out Azure
  * Define and enforce data retention and archival requirements
  * Use proper storage model for storing data
* How you monitoring your cost ?
  * Watch my cloud costs
  * Create and respond to cost alerts
  * Perform cost reviews on a regular cadence ( Azure Advisor )
* What trade-offs have you made to optimize for cost ?
  * Analyze ROI regularly
  * Use different Azure datacenter locations to optimize cost
  * Use Azure Marketplace
  * Take advantage of offers

Operational Excellence
======================
* Understanding critical system flows. 
  * Define SLA ( Service Level Agreement ), SLI ( Service Level Indicator ) and SLO ( Service Level Objective )
    * SLA - agreement wit client
    * SLO - objective that team must hit to meet SLA
    * SLI - real numbers on performance
  * Define RTO, RPO
    * RPO - Measure how often you take backup (indicates amount of data will be lost in the event of outage)
    * RTO - Time that app can be down and not cause significant damage to a business
  * Define critical system flows
  * Define performance requirements for applications and key scenarios
* Monitoring of resources
  * Use APM - Application Performance Management
  * Use Azure Appicatons Insights ( to collect logs )
  * Logs indexed and searchable
  * Enable events correlation
  * End-to-end performance of critical system flows is monitored
* Collected data interpretation
  * Azure Log Analytics or Splunk to collect logs and metrics
  * Azure Activity Logs are collected
  * Resource level monitoring are enforced 
  * External dependancies are monitored
  * Enable workload data/monitoring visualization
* Alerting and notification
  * Azure Monitor or Grafana to visualize
  * Create tailored dashboards 
  * Integrate alerting with ITSM such as ServiceNow
  * PagerDuty & DataDog
* Recovery and Failover
  * Define Recovery Steps
  * Define fallback
  * Health model to classify situations
  * Automated recovery procedures are in-place 
  * Automated recovery procedures are tested 
* Scale
  * Define scale model
  * Enable Auto-Scaling
  * Codify Auto-Scale
* Configuration Managment
  * Store sensitive information in Azure Key Vault
  * Define key rotation
  * Define identities
  * Define SSL certs management/expiration dates
  * Version control for software 
* Deployment considerations
  * Deployment process without manual operations
  * HotFix process
  * Blue/Green deployments or canary releases
  * Feature flags testing
* Infrastructure as code
  * The entire infrastructure defined as code
  * No operational changes performed outside of IAC
  * Configuration drift is tracked and addressed
  * 1:1 test environment with production
* Testing and validations
  * Tests for perfomance
  * Tests for scalability
  * Tests for resilieny
  * Tests as part of each major change
  * Fault test injections
  
Performance Efficiency
======================

* Design workloads to scale
  * Choose the right data store type
  * Use Dynamic service discovery for microservices application
  * Use Locks to ensure consistancy
  * Use Async calls / waits to prevent Locks
  * Use queues
  * Use pub/sub models
  * Avoid sticky sessions and client affinity
  * Use background jobs
* Performance
  * Use horizontal scaling
  * Scale down when load decreases
  * Use idempotent operations
* Load handling
  * Test under load
  * Measure scale up time
  * Use predictive scaling ( based on trends/events )
* Capacity planning
  * Use CDN if applicable
  * Strategy to manage events that may cause a spike in load
  * Optimize resource SKUs selection ( vm , database sizing )

Reliability
===========
* Reliabiliy targets
  * Define RTO, RPO
  * Define SLA, SLO, SLI
  * Define MTTR, MTBF
  * Use composite SLA
  * Define recovery targets
* Design appliation to be resiliant to failures
  * Deploy across multiple regions
  * Remove all single point of failures by running multiple instances
  * Deploy across multiple AZ
  * Plan for component level failure
  * Plan for dependancy failure

Whats happenend after user types url in the browser ?
=====================================================
1. User types a URL in the Browser
2. A DNS requiest is made
3. A browser received an IP address and needs to contact it
4. CDN copies this data in strategic geolocations around the word
5. Browser will call for the Edge Server within CDN nework nearer to the end-user
6. CDN always return the best possible IP address
7. If content cant be found in the Edge Server cache , the edge server sends request to the Origing Server to retrieve this information
8. Nature of dynamic content requires repeated back and forth calls to the Origin Server
   1. Same request provide different results - personalized content for users
   2. It rely more on teh contnet provider origin
9. DSA, comes into play - optimize latency and varying round-trip time of the desired content
10. DSA uses advanced DNS mapping, better TCP algorithms
11. On-the-fly compression
12. Will identify cacheable content form dynamic content


# Azure Security Products
## Users and Devices
1. Azure Active Directory
   >The Azure Active Directory (Azure AD) its an enterprise identity service provides singel sign-on and MFA 
2. Azure IOT Central
   >Secure IOT Provider
3. Azure Sphere
   >Azure Sphere is a secured, high-level applicatoin platform with built-in communication and security features for internet-connected devices
4. Microsoft Authenticator
   >App that provide additional layer of security on top of the fingerprint or PIN
5. Microsoft Intune
   >Mobile Device Management and Mobile Application Managment. 
6. Windows 10
   >Flagship operation system and released as a part of Windows NT. Seamless experience across multiple deivces
## Data and Apps
1. Azure Dedicated HSM Gateway ( Hardware Security Module )
   >Maintain full administrative and cryptographic contol of your HSM
   >Validated for FIPS 140-2 Level 3 and eIDAS Common Criteria EAL4+
   >Migrate HSM applications to Azure with minimal changes and improved latency
2. Control and secure data and document within organization within and outside of the company.
   >Classification, protection, visibility, control, secure collaboration 
3. Azure Key Vault
   >Azure Key Valut is a cloud service that provides a secure store for secrets. ( Keys, passwords, certificates, etc)
4. Microsoft Cloud App Security
   >Posture validateion, Monitoring, Compliance, Protect against cyberthreats and anomalies
## Threat protection
1. Azure Advance Threat protection - Azure ATP = Defender for Identity
   >Cloud-based security solution that leverages on-prem AD signals to identify, detect and investigate advanced threats, compromised identities and insider actions
   * Prevent
   * Detect
   * Investigate
   * Respondd
2. Azure Sentinel
   >Security Information and Event Management
   * **Collect** Data across Users, Devices, Applicatoins and Infrastructure in multiple clouds
   * **Detect** new(!) threats and minimize false positives
   * **Investigate** threats with AI and hunt suspicious activities at scale
   * **Respond** to incidents rapidly
3. Microsoft Defender for endpoint
   >Host-based protection
4. Office 365 Advanced Threat Protection
5. Microsoft Secure Score
   >Security Posture assecment across M365 workloads
## Infrastructure
1. Azure Application Gateway
2. Azure DDoS Protection
3. Azure Security Center
4. Azure VPN Gateway 
