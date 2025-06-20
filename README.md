# Microsoft Azure Fundamentals (AZ-900) Study Guide

## 1. Cloud Computing Fundamentals

### 1.1 What is Cloud Computing?
**Definition**: 
> "Using remote servers hosted on the internet to store, manage, and process data rather than local servers or personal computers."

**Key Comparison**:
| Aspect | On-Premises | Cloud |
|--------|-------------|-------|
| Hardware Ownership | You buy/maintain | Provider manages |
| Staff Responsibility | Your IT team | Provider's team |
| Cost Model | Capital Expenditure (CapEx) | Operational Expenditure (OpEx) |
| Scalability | Physically limited | On-demand resources |

### 1.2 Evolution of Hosting Models
#### Four Key Stages:
1. **Dedicated Servers (1990s)**
   - 1 physical server = 1 business
   - Pros: Maximum security
   - Cons: High cost ($10,000+/server)

2. **Virtual Private Servers (VPS)**
   - Virtualization divides 1 physical server into multiple VMs
   - Pros: Better resource utilization
   - Cons: Still requires capacity planning

3. **Shared Hosting (2000s)**
   - Hundreds of websites on one server (e.g., GoDaddy)
   - Pros: Very cheap (~$5/month)
   - Cons: No isolation, performance issues

4. **Modern Cloud (Present)**
   - Distributed across thousands of servers
   - Key Advantages:
     - Pay-per-use pricing
     - Automatic scaling
     - 99.9%+ uptime SLAs

### 1.3 Cloud Characteristics (Exam Focus)
- **Elasticity**: Scale up/down automatically
- **Fault Tolerance**: Built-in redundancy
- **Global Reach**: Deploy in any Azure region
- **Resource Pooling**: Multi-tenant efficiency

## 2. Azure Deployment Models

### 2.1 Core Deployment Models
| Model | Description | Azure Terminology | Example Components |
|-------|-------------|-------------------|---------------------|
| **Public Cloud** | Fully hosted on Azure | "Cloud Native" | Azure VMs, Cosmos DB |
| **Private Cloud** | On-premises infrastructure | "On-Premises" | OpenStack, Local Hyper-V |
| **Hybrid Cloud** | Combines public + private | "Hybrid" | Azure Stack, ExpressRoute |

### 2.2 Key Comparisons
#### Feature Analysis:
| Characteristic | Public Cloud | Private Cloud | Hybrid Cloud |
|----------------|--------------|---------------|--------------|
| **Cost** | Pay-as-you-go | High CapEx | Balanced |
| **Security** | Strong defaults | Customizable | Mixed approach |
| **Compliance** | Standard certs | Tailored solutions | Flexible |
| **Maintenance** | Microsoft manages | Your team manages | Shared |
| **Connectivity** | Internet | Local network | ExpressRoute/VPN |

### 2.3 Hybrid Cloud Components
**ExpressRoute**:
- Dedicated private fiber connection
- Bypasses public internet
- Typical speeds: 50Mbps-10Gbps

**Azure Arc**:
- Manage resources across clouds/on-prem
- Supports:
  - Kubernetes clusters
  - Windows/Linux servers
  - Azure data services

### 2.4 Cross-Cloud (Multi-Cloud)
**Key Points**:
- Not officially in AZ-900 exam but good to know
- Uses services like Azure Arc for management
- Common in enterprises using:
  - Azure + AWS
  - Azure + GCP
  - All three major providers

### Exam Tips:
1. **Public Cloud Focus**: AZ-900 emphasizes public cloud (Azure) scenarios
2. **Hybrid Keywords**: Watch for "ExpressRoute" and "VPN" in questions
3. **Compliance**: Know that public cloud meets most compliance needs except specific government cases

## 3. Cloud Economics: Total Cost of Ownership (TCO)

### 3.1 TCO Iceberg Concept
**Visual Representation**:

### 3.2 Cost Comparison Breakdown
| Cost Factor | On-Premises | Azure Cloud |
|-------------|-------------|-------------|
| **Upfront Costs** | High (CapEx) | Low/None (OpEx) |
| **Ongoing Costs** | Maintenance contracts | Pay-as-you-go |
| **Hardware** | Purchased outright | Microsoft's responsibility |
| **Personnel** | Dedicated IT staff | Shared Microsoft staff |
| **Scalability** | Manual procurement | Automatic scaling |
| **Maintenance** | Your responsibility | Azure handles updates |

### 3.3 Key Savings Metrics
- **Typical Savings**: 75% reduction when moving to cloud
- **Hidden Cost Elimination**:
  - No physical data center costs
  - No hardware refresh cycles
  - Reduced staffing requirements

### 3.4 Azure TCO Calculator
[Official TCO Tool](https://azure.microsoft.com/pricing/tco/) helps compare:
- Server workloads
- Storage needs
- Networking requirements

### Exam Tips:
1. **CapEx vs OpEx**:
   - CapEx = Large upfront purchases (on-prem)
   - OpEx = Recurring operational costs (cloud)

2. **TCO Questions**:
   - Always consider hidden costs in comparisons
   - Cloud becomes cheaper at scale due to shared resources

3. **Key Percentage**:
   - Remember "75% savings" as benchmark (but actual may vary)

   ## 4. High Availability and Scalability

### 4.1 High Availability (HA)
**Definition**: 
> "Ability to maintain service availability by eliminating single points of failure"

#### Key Components:
| Component | Purpose | Azure Example |
|-----------|---------|---------------|
| **Availability Zones** | Physically separate datacenters | 3+ zones per region |
| **Load Balancer** | Distributes traffic evenly | Azure Load Balancer |
| **Health Probes** | Detects unhealthy instances | HTTP/TCP checks |

**Implementation Pattern**:
mermaid
graph TD
    A[User] --> B[Azure Load Balancer]
    B --> C[VM in Zone 1]
    B --> D[VM in Zone 2]
    B --> E[VM in Zone 3]

SLA Examples:

Single VM: 99.9%

VMs across Availability Zones: 99.99%

### 4.2 Scaling Methods
#### Vertical Scaling ("Scale Up")
What: Increase server capacity (CPU/RAM)

When: Applications can't be distributed

Limits: Physical hardware ceilings

Azure Example: Resizing VM from D2s_v3 to D4s_v3

#### Horizontal Scaling ("Scale Out")
 - What: Add more servers of same size
 - When: Stateless applications
 - Advantage: No theoretical limit
 - Azure Example: VM Scale Sets

### Scaling Methods Comparison
| Characteristic       | Vertical Scaling       | Horizontal Scaling     |
|----------------------|------------------------|------------------------|
| **Complexity**       | Low                    | Medium                 |
| **Downtime**         | Requires restart       | None                   |
| **Cost**            | Expensive upgrades     | Linear growth          |
| **Azure Tool**      | VM Resize              | Scale Sets             |

### 4.3 Availability vs Scalability
| Goal                          | Solution               | Key Azure Service               |
|-------------------------------|------------------------|----------------------------------|
| Stay online during failures   | High Availability      | Availability Zones              |
| Handle more traffic           | Scalability            | VM Scale Sets                   |
| Both                          | Combined approach      | Load Balancer + Zones + Scale Sets |

#### Exam Tips:
Availability Zones:

Always recommend for production workloads

Remember "3 zones" as default configuration

Scaling Questions:

"Scale up" = vertical (bigger servers)

"Scale out" = horizontal (more servers)

SLA Numbers:

Single instance: 99.9%

Multi-zone: 99.99% (extra "9" matters)

### High Elasticity

- **Definition**:  
  - Ability to automatically increase or decrease capacity based on current demand (traffic, memory, computing power).  
  - Key difference from scalability: it's **automatic** and includes **decreasing** capacity, not just increasing.  

- **Implementation**:  
  - Uses **horizontal scaling** (adding/removing servers of the same size):  
    - **Scaling out**: Adding more servers.  
    - **Scaling in**: Removing servers.  
  - **Vertical scaling** is generally **not used** for elasticity due to risks (e.g., data loss when resizing storage).  

- **Azure Tools for Elasticity**:  
  1. **VM Scale Sets**:  
     - Automatically adjust server count based on demand or a schedule.  
  2. **SQL Server Stretch Database**:  
     - Dynamically moves "warm/cold" transactional data between SQL Server 2016 and Azure.  
     - Similar concept to scale sets (not covered in detail in this course).  

### High Fault Tolerance

- **Definition**:  
  - Ensures **no single point of failure** to minimize the chance of service disruption.  
  - Goes beyond **high availability** by explicitly focusing on **failure prevention** (embedded in the term "fault tolerant").  

- **Key Mechanism**: **Failover**  
  - Plan to shift traffic to a **redundant system** if the primary system fails.  
  - Example:  
    - **Primary database** syncs data to a **secondary (standby) database** in real time.  
    - If the primary fails (hardware/software issue), the system:  
      1. Detects the failure.  
      2. Fails over to the secondary.  
      3. Promotes the secondary to **primary**.  

- **Azure Tool for Fault Tolerance**:  
  - **Azure Traffic Manager**:  
    - Operates at the **DNS level** to redirect traffic from a failed primary system to a standby.  
    - Ideal for **regional failures**.  
  - *Note*: Load balancers can also be used, but Traffic Manager is highlighted here.

### High Durability & Disaster Recovery (DR)

#### **High Durability**  
- **Definition**:  
  - Ability to **recover from disasters** and **prevent data loss**.  
  - Key questions to ensure durability:  
    - Do backups exist?  
    - How fast can backups be restored?  
    - Are backups functional?  
    - How is live data corruption prevented?  

#### **Disaster Recovery (DR) Fundamentals**  
1. **Business Continuity Plan (BCP)**:  
   - Document outlining how a business operates during unplanned disruptions.  
2. **Key Metrics**:  
   - **Recovery Point Objective (RPO)**:  
     - Maximum acceptable **data loss** (measured in time).  
   - **Recovery Time Objective (RTO)**:  
     - Maximum acceptable **downtime** before financial impact.  

#### **Disaster Recovery Options**  
*(Trade-off: Cost vs. Recovery Speed)*  

| **Option**          | **Description**                                                                 | **RPO/RTO**       | **Use Case**                     | **Cost**            |  
|---------------------|---------------------------------------------------------------------------------|-------------------|----------------------------------|---------------------|  
| **Backup & Restore** | Data backed up; restored to new infrastructure after disaster.                  | Hours             | Low-priority services            | Most cost-effective |  
| **Pilot Light**     | Minimal services replicate data to another region; scale up post-disaster.      | ~10 minutes       | Moderate RTO/RPO needs           | Moderate            |  
| **Warm Standby**    | Scaled-down copy of infrastructure; scale to full capacity post-disaster.       | Minutes           | Business-critical services       | High                |  
| **Multi-Site Active/Active** | Fully replicated, identical infrastructure in another region.               | Near-zero/Real-time | Mission-critical services     | Highest (2x cost)   |  

#### **Key Takeaways**  
- **Higher cost** → **Faster recovery** (lower RTO/RPO).  
- **Mission-critical systems** typically use **multi-site active/active** for near-zero downtime.  
- **Backup & restore** is suitable for non-urgent, low-budget scenarios.  

### Part 8: Evolution of Computing - Dedicated Servers vs. Virtual Machines (VMs)

#### **1. Dedicated Servers**  
- **Definition**:  
  - Physical server **wholly used by a single customer** (no resource sharing).  
  - Also called **"bare metal"** (mimics on-premise servers).  

- **Pros**:  
  ✅ **Full control** over hardware/resources.  
  ✅ **Security/privacy guarantee** (no multi-tenancy).  
  ✅ Predictable performance (no noisy neighbors).  

- **Cons**:  
  ❌ **Capacity guessing**: Must pre-purchase hardware (capital cost).  
  ❌ **Underutilization**: Wasted space until app scales.  
  ❌ **Upgrades**: Slow/expensive (requires buying new hardware).  
  ❌ **OS Limitation**: Stuck with the installed OS.  
  ❌ **App Conflicts**: Multiple apps on one server may compete for resources.  

#### **2. Virtual Machines (VMs)**  
- **Definition**:  
  - Software-emulated machines running on a **shared physical server** (via **hypervisor**).  
  - Multiple VMs can run on a single physical server.  

- **Pros**:  
  ✅ **Cost-effective**: Pay a fraction of the physical server cost.  
  ✅ **Multi-tenancy**: Isolated from other customers' VMs on the same hardware.  
  ✅ **Flexibility**: Run multiple VMs with different OSes/apps.  

- **Cons**:  
  ❌ **Underutilization**: Still pay for unused VM capacity (fixed sizing).  
  ❌ **Guest OS Limitation**: Bound to the chosen VM OS.  
  ❌ **App Conflicts**: Multiple apps on the **same VM** may conflict (but apps on separate VMs won’t).  

#### **Key Takeaways**  
- **Dedicated servers** → Best for **full control/security** but inefficient for scaling.  
- **VMs** → **More economical** but still suffer from sizing rigidity.  
- **Hypervisor**: Software enabling VM isolation on shared hardware.  

### Evolution of Computing - Containers & Serverless Functions

#### **1. Containers**  
- **Definition**:  
  - Lightweight, isolated processes running on a **shared OS** (via a **Docker daemon** or similar).  
  - Further subdivides resources compared to VMs for **better efficiency**.  

- **Pros**:  
  ✅ **Maximized utilization**: More cost-effective than VMs (no OS overhead per container).  
  ✅ **Flexibility**: Each container can run a **different OS/user space** on the same host.  
  ✅ **Portability**: Consistent runtime environment across systems.  

- **Cons**:  
  ❌ **Shared OS**: All containers on a host use the **same underlying OS kernel**.  

#### **2. Serverless Functions**  
- **Definition**:  
  - Event-driven, **single-purpose code snippets** executed in ephemeral environments.  
  - Part of **Function-as-a-Service (FaaS)** offerings (e.g., Azure Functions).  

- **Pros**:  
  ✅ **No infrastructure management**: Fully managed by the cloud provider ("serverless").  
  ✅ **Extreme cost efficiency**: Pay **only for execution time/memory used**.  
  ✅ **Automatic scaling**: Handles traffic spikes seamlessly.  

- **Cons**:  
  ❌ **Cold starts**: Delay when initializing a function after inactivity.  
  ❌ **Limited execution duration**: Functions time out after a set period.  

#### **Key Takeaways**  
- **Containers** → Ideal for **microservices** with flexible OS needs.  
- **Serverless** → Best for **event-driven tasks** (e.g., APIs, data processing).  
- **Evolution**:  
  Dedicated Servers → VMs → Containers → Functions  
  *(Increasing abstraction, cost efficiency, and scalability)* 

### Part 10: Cloud Computing Evolution - Final Comparison

#### **Compute Options Comparison**

| Feature            | Dedicated Servers | Virtual Machines (VMs) | Containers       | Serverless Functions |
|--------------------|------------------|----------------------|-----------------|----------------------|
| **Isolation**      | Physical         | Hypervisor-level     | Process-level   | Code-level            |
| **Overhead**       | Highest          | High                 | Low             | None                  |
| **Boot Time**      | Minutes          | 1-2 minutes          | Seconds         | Milliseconds*         |
| **Scaling**        | Manual           | Manual/Auto-scale    | Auto-scale      | Fully Automatic       |
| **Cost Model**     | CapEx            | Pay-per-VM           | Pay-per-use     | Pay-per-execution     |
| **Management**     | Full             | OS & Apps            | Apps only       | Code only             |

*Note: Serverless functions may experience cold starts (2-5s delay) when inactive*

#### **When to Use Each**

**1. Dedicated Servers:**
- Regulatory compliance requiring physical isolation
- Legacy applications requiring specific hardware
- Maximum performance needs (e.g., HPC)

**2. Virtual Machines:**
- Traditional application migration  
- Mixed OS environments (Windows + Linux)  
- When you need full OS control  

**3. Containers:**
- Microservices architectures  
- CI/CD pipelines  
- Hybrid cloud deployments  
- Kubernetes orchestration  

**4. Serverless:**
- Event processing (e.g., file uploads)  
- Scheduled tasks (cron jobs)  
- API backends  
- Low-traffic services  

#### **Advanced Considerations**

**Cold Start Mitigation:**
- Provisioned concurrency (keep warm)  
- Minimum instance count  
- Function bundling  

**Container Optimization:**
- Multi-stage builds  
- Lightweight base images (Alpine)  
- Proper resource limits  

#### **Evolution Path**

1. **Dedicated Servers** (Bare Metal)  
   ↓  
2. **Virtual Machines** (Hypervisor-based)  
   ↓  
3. **Containers** (OS-level Virtualization)  
   ↓  
4. **Serverless** (Event-driven Execution)  

**Key Trend:** Each evolution step brings:  
- Higher abstraction level  
- Better cost efficiency  
- Improved scalability  
- Reduced management overhead  

#### **Study Tips**

- Remember: Containers share the host OS kernel  
- Serverless isn't truly "no server" - just no visible server management  
- VMs provide stronger isolation than containers  
- Dedicated servers are still needed for some compliance scenarios  

### Part 11: Azure Regions and Geographies

#### **Key Concepts**
- **Region**: Grouping of data centers (called Availability Zones in Azure)
  - 58 regions across 140 countries (Azure has the most regions among cloud providers)
- **Geography**: Discrete market containing 2+ regions that maintain:
  - Data residency (data stays within defined boundaries)
  - Compliance with local regulations

#### **Geographies Examples**
1. **Standard Geographies**:
   - United States
   - Canada
   - Brazil
   - Mexico
   - Europe/Asia/Africa regions

2. **Special Geographies**:
   - Azure Government US (exclusive to US government)

#### **Why Geographies Matter**
- Ensures data remains within required boundaries (e.g., Canadian data never leaves Canada)
- Helps meet regulatory requirements (privacy laws, industry compliance)

#### **Region Pairs**
- Each Azure region is paired with another ~300 miles away
- **Purposes**:
  - Enable updates without downtime
  - Provide disaster recovery options
  - Some services auto-replicate to paired regions

#### **Key Services Using Region Pairs**
- **Geo-Redundant Storage (GRS)**: 
  - Automatically replicates data to secondary region
  - Example pairs:
    - Canada Central ↔ Canada East
    - East US ↔ West US
    - Germany Central ↔ Germany Northeast

#### **Practical Notes**
- You select a region when creating resources (e.g., VMs)
- View all regions via Azure's "Global Infrastructure" page
- Not all services are available in all regions

### Part 12: Azure Region Types and Service Availability

#### **Azure Region Types**
1. **Recommended Regions**:
   - Provide the broadest range of service capabilities
   - Designed to support Availability Zones
   - Majority of Azure services available here

2. **Alternate Regions**:
   - Extend Azure's footprint within data residency boundaries
   - **Do not** support Availability Zones
   - Labeled as "Other" in Azure portal
   - Still allow resource deployment (just without zone redundancy)

#### **Service Availability Categories**
| Category      | Availability in Recommended Regions | Availability in Alternate Regions |
|---------------|------------------------------------|-----------------------------------|
| **Foundational** | Immediately at GA (or within 12 months) | Same as recommended regions |
| **Mainstream**   | Immediately at GA (or within 12 months) | Based on customer demand |
| **Specialized**  | Based on customer demand | Based on customer demand |

#### **Key Terms**
- **General Availability (GA)**: When a service is ready for public use
- **Availability Zones**: Physically separate datacenters within a region
- **Data Residency**: Keeping data within specified geographic boundaries

#### **Important Notes**
- Not all services are available in all regions
- Service availability depends on:
  - Infrastructure readiness
  - Compliance requirements
  - Customer demand
- Always check current service availability before architecture planning

### Azure Special Regions and Availability Zones

#### **Special Azure Regions**
1. **US Government Regions**:
   - US DoD Central
   - US Gov Virginia
   - US Gov Iowa
   - 3 additional undisclosed locations
   - *Purpose*: Meet strict government compliance requirements

2. **China Regions** (operated by 21Vianet):
   - China East
   - China North
   - *Key Point*: Microsoft doesn't directly maintain these datacenters

#### **Availability Zones (AZs)**
- **Definition**: Physically separate datacenters within an Azure region
  - Each AZ has independent power, cooling, and networking
  - Typically 3 AZs per region (some exceptions exist)

**Key Characteristics**:
- Physical separation (different buildings)
- Low-latency connections (< milliseconds)
- Designed for high availability

**Why Three AZs?**
- Ensures redundancy if 1-2 zones fail
- Common practice for mission-critical workloads

#### **Using Availability Zones**
- When creating resources:
  1. Select region (e.g., East US)
  2. Choose AZ option (Zone 1, 2, or 3)
  3. For high availability: Distribute across multiple AZs

### Part 14: AZ Supported Regions and Fault/Update Domains

#### **Availability Zone Supported Regions**
- **Recommended Regions**:
  - Typically have 3 AZs (some newer regions may add them later)
  - Example regions with 3 AZs:
    - Central US
    - East US 2  
    - West US 2
    - West Europe
    - France Central  
    - North Europe
    - Southeast Asia

- **Alternate/Other Regions**:
  - Do not support AZs
  - Interface shows "No infrastructure redundancy required" option

#### **Fault Domains vs Update Domains**

**Fault Domain (FD)**
- Logical group of hardware sharing power/network
- Prevents single point of failure (e.g., rack failure)
- Think: Physical separation

**Update Domain (UD)**
- Logical group for staggered updates
- Prevents downtime during maintenance
- Think: Maintenance sequencing

#### **Availability Sets**
- **Purpose**: Distribute VMs across:
  - Multiple fault domains (different physical racks)
  - Multiple update domains (staggered maintenance)

- **Configuration Example**:
  - 3 Fault Domains = VMs spread across 3 racks
  - 5 Update Domains = Updates affect max 20% of VMs at once

#### **Azure Portal Implementation**
1. When creating a VM:
   - Under "Availability options" → Select "Availability set"
   - Create new set with:
     - Fault domain count (physical separation)
     - Update domain count (maintenance sequencing)

2. Key behaviors:
   - VMs in same availability set won't share fault/update domains
   - Default is 3 FDs and 5 UDs (can be customized)

#### **Key Takeaways**
- Use AZs when possible (regions with 3 AZs)
- Use Availability Sets when AZs aren't available
- FDs protect against hardware failures
- UDs prevent downtime during updates
- Always distribute critical workloads across multiple domains

### Part 15: Azure Compute Services

#### **1. Azure Virtual Machines (VMs)**
- **Description**: 
  - Most common compute type (Windows/Linux OS)
  - Full control over configuration (CPU, memory, storage)
  - Shared hardware (dedicated options available)
- **Use Cases**:
  - Traditional server workloads
  - Lift-and-shift migrations
  - Custom software environments

#### **2. Azure Container Instances (ACI)**
- **Description**:
  - "Docker as a service"
  - Runs containerized apps without managing VMs
  - Supports both Windows and Linux containers
- **Use Cases**:
  - Simple container deployments
  - Task automation
  - CI/CD pipelines

#### **3. Azure Kubernetes Service (AKS)**
- **Description**:
  - Managed Kubernetes orchestration
  - Industry-standard for container management
  - Auto-scaling and self-healing
- **Use Cases**:
  - Microservices architectures
  - Complex container deployments
  - Production workloads

#### **4. Azure Service Fabric**
- **Description**:
  - Enterprise-grade microservices platform
  - Runs on Azure or on-premises
  - Supports both containers and traditional apps
- **Use Cases**:
  - Distributed systems
  - Stateful services
  - Large-scale mission-critical apps

#### **5. Azure Functions**
- **Description**:
  - Event-driven serverless compute
  - Pay-per-execution model
  - Automatic scaling
- **Use Cases**:
  - Event processing
  - APIs
  - Scheduled tasks

#### **6. Azure Batch**
- **Description**:
  - Parallel batch processing
  - Supports low-priority/Spot VMs
  - Manages job scheduling
- **Use Cases**:
  - Scientific computing
  - Video rendering
  - Financial modeling

#### **Comparison Table**
| Service | Management Level | Best For | Billing Model |
|---------|-----------------|----------|--------------|
| VMs | Infrastructure | Full control | Per-second |
| ACI | Containers | Simple apps | Per-second |
| AKS | Orchestration | Production containers | Cluster + resources |
| Service Fabric | Platform | Enterprise microservices | Resource-based |
| Functions | Code | Event processing | Per-execution |
| Batch | Jobs | Parallel workloads | Job-based |

#### **Key Takeaways**
- **VMs** provide most control but most management
- **Containers** (ACI/AKS) offer better density and portability
- **Serverless** (Functions) maximizes cost efficiency
- **Batch** optimizes parallel workloads
- Choose based on: control needs, scalability, and cost model

### Azure Compute Services

#### **1. Azure Virtual Machines (VMs)**
- **Description**: 
  - Most common compute type (Windows/Linux OS)
  - Full control over configuration (CPU, memory, storage)
  - Shared hardware (dedicated options available)
- **Use Cases**:
  - Traditional server workloads
  - Lift-and-shift migrations
  - Custom software environments

#### **2. Azure Container Instances (ACI)**
- **Description**:
  - "Docker as a service"
  - Runs containerized apps without managing VMs
  - Supports both Windows and Linux containers
- **Use Cases**:
  - Simple container deployments
  - Task automation
  - CI/CD pipelines

#### **3. Azure Kubernetes Service (AKS)**
- **Description**:
  - Managed Kubernetes orchestration
  - Industry-standard for container management
  - Auto-scaling and self-healing
- **Use Cases**:
  - Microservices architectures
  - Complex container deployments
  - Production workloads

#### **4. Azure Service Fabric**
- **Description**:
  - Enterprise-grade microservices platform
  - Runs on Azure or on-premises
  - Supports both containers and traditional apps
- **Use Cases**:
  - Distributed systems
  - Stateful services
  - Large-scale mission-critical apps

#### **5. Azure Functions**
- **Description**:
  - Event-driven serverless compute
  - Pay-per-execution model
  - Automatic scaling
- **Use Cases**:
  - Event processing
  - APIs
  - Scheduled tasks

#### **6. Azure Batch**
- **Description**:
  - Parallel batch processing
  - Supports low-priority/Spot VMs
  - Manages job scheduling
- **Use Cases**:
  - Scientific computing
  - Video rendering
  - Financial modeling

#### **Comparison Table**
| Service | Management Level | Best For | Billing Model |
|---------|-----------------|----------|--------------|
| VMs | Infrastructure | Full control | Per-second |
| ACI | Containers | Simple apps | Per-second |
| AKS | Orchestration | Production containers | Cluster + resources |
| Service Fabric | Platform | Enterprise microservices | Resource-based |
| Functions | Code | Event processing | Per-execution |
| Batch | Jobs | Parallel workloads | Job-based |

#### **Key Takeaways**
- **VMs** provide most control but most management
- **Containers** (ACI/AKS) offer better density and portability
- **Serverless** (Functions) maximizes cost efficiency
- **Batch** optimizes parallel workloads
- Choose based on: control needs, scalability, and cost model

### Part 16: Azure Virtual Machines and Related Services

#### **Azure Virtual Machines (VMs)**
- **Key Features**:
  - Fully configurable (OS, CPU, memory, storage)
  - Supports Windows and Linux
  - Hourly billing (per-second granularity)
  - 99.9% SLA with premium disks (single instance)
  - 99.95% SLA with two+ instances in availability sets

- **Components Created Automatically**:
  - Network Security Group (firewall)
  - Network Interface (IP management)
  - Public IP Address
  - Virtual Network (VNet)

- **Limits**:
  - 20 VMs per region per subscription (can request increase)
  - Size determined by Azure image (vCPU/memory/storage combo)

#### **Supported Operating Systems**
- **Marketplace Options**:
  - Windows Server
  - SUS, Red Hat, Ubuntu, Debian, FreeBSD
  - Container-optimized: Flatcar, RancherOS
  - Pre-configured: Bitnami (e.g., WordPress), Jenkins

- **Custom Images**:
  - Upload VHD format (not VHDX)
  - Create using Hyper-V (Windows) or conversion tools

#### **Virtual Machine Scale Sets**
- **Purpose**: Automatically scale VM instances
- **Key Capabilities**:
  - Scale based on metrics (CPU, network, disk)
  - Health monitoring and auto-repair
  - Supports 100-1000 VMs
  - Integrates with load balancers

- **Scaling Policies**:
  - **Scale Out**: Add VMs when threshold exceeded
  - **Scale In**: Remove VMs when demand drops
  - Advanced options: Percentage-based scaling, custom metrics

- **Health Monitoring**:
  - Application health extension (HTTP checks)
  - Load balancer probes (more robust)
  - Automatic unhealthy instance replacement

#### **Load Balancer Options**
1. **Application Gateway**:
   - Layer 7 (HTTP/HTTPS)
   - Web traffic optimization

2. **Azure Load Balancer**:
   - Layer 4 (TCP/UDP)
   - General network traffic

#### **Azure Virtual Desktop (AVD)**
- **Formerly**: Windows Virtual Desktop
- **Key Features**:
  - Cloud-hosted virtual desktops and apps
  - Access from any device (Windows, Mac, iOS, Android, Linux)
  - Built-in security (data stays in cloud)
  - Integration with Microsoft 365/Teams

- **Benefits**:
  - Reduced infrastructure costs
  - Built-in disaster recovery
  - Simplified management (no VDI hardware)
  - Conditional access via Azure AD

### Azure App Services

#### **Overview**
- **Type**: Platform-as-a-Service (PaaS)
- **Purpose**: Host web apps, REST APIs, and mobile backends
- **Key Features**:
  - Automatic OS/language patching
  - Built-in load balancing and auto-scaling
  - CI/CD integrations (Azure DevOps, GitHub, Docker Hub)
  - Custom domains and SSL certificates
  - Staging environments (deployment slots)

#### **Supported Runtimes**
| Language/Framework | Notes |
|--------------------|-------|
| .NET/.NET Core | Multiple versions available |
| Java | Enterprise support |
| Node.js | LTS and current versions |
| PHP | Wide version support |
| Python | 2.x and 3.x variants |
| Ruby | Limited monitoring support |
| Custom Containers | Docker support for unsupported stacks |

#### **Deployment Slots**
- **Functionality**: Create isolated environments (staging, QA, prod)
- **Blue-Green Deployments**: 
  - Test in staging slot
  - Swap with production instantly
- **Benefits**: Zero-downtime deployments

#### **App Service Environments (ASE)**
- **Purpose**: Isolated, high-scale deployments
- **Types**:
  1. **External ASE**: Internet-facing apps
  2. **ILB ASE**: Internal Load Balancer for private networks
- **Use Cases**:
  - High security requirements
  - Extreme scaling needs
  - Network isolation

#### **Pricing Tiers**
| Tier | Characteristics | Best For |
|------|----------------|----------|
| **Free (F1)** | 1GB storage, 60 min/day compute | Testing only |
| **Shared** | 100 apps, no SLA | Dev environments |
| **Basic** | Dedicated VMs, 99.95% SLA | Small production workloads |
| **Standard** | Auto-scale to 3 instances | Medium traffic apps |
| **Premium** | Scale to 10 instances | High-traffic apps |
| **Isolated** | VNet integration, 100 instances | Enterprise ASE deployments |

#### **Key Considerations**
- **Linux Limitations**: No shared tier support
- **Version Management**: Older runtime versions get deprecated
- **Customization**: Use Docker for unsupported stacks
- **Scaling**: Combine with Traffic Manager for global distribution

### Part 18: Azure Storage Services

#### **Core Storage Services**
| Service | Type | Description | Key Use Cases |
|---------|------|-------------|--------------|
| **Blob Storage** | Object | Serverless storage for unstructured data | Large files, backups, media |
| **Disk Storage** | Block | Virtual hard drives for VMs | OS disks, persistent storage |
| **File Storage** | File | Managed file shares (SMB/NFS) | Shared drives across VMs |
| **Queue Storage** | Messaging* | Application message queuing | Decoupling app components |
| **Table Storage** | NoSQL* | Schema-less key-value store | Structured non-relational data |
| **Archive Storage** | Cold | Lowest-cost long-term storage | Compliance, backups (>180 days) |
| **Data Lake Storage** | Analytics | Unified data repository | Big data processing |

*Note: Queue/Table storage are technically data services but categorized under storage accounts

#### **Storage Account Types**
1. **General Purpose v2**:
   - Supports all storage types
   - Recommended for most scenarios
   - Zone-redundant options available

2. **Blob Storage**:
   - Legacy account type
   - Only supports blob containers
   - Limited to standard performance

3. **Block Blob Storage**:
   - Premium performance (SSD)
   - Optimized for high transaction rates

4. **File Storage**:
   - Dedicated for Azure Files
   - Premium performance options

#### **Performance Tiers**
| Tier | Media | Best For | Latency | Cost |
|------|-------|----------|---------|------|
| **Standard** | HDD | Backup, archives | Higher | Lower |
| **Premium** | SSD | Transactional workloads | Low | Higher |

#### **Access Tiers**
| Tier | Min Retention | Access Cost | Storage Cost | Use Case |
|------|--------------|-------------|--------------|----------|
| **Hot** | N/A | Low | High | Frequently accessed |
| **Cool** | 30 days | Medium | Medium | Infrequent access |
| **Archive** | 180 days | High | Very Low | Rarely accessed |

#### **Replication Options**
1. **Primary Region**:
   - **LRS (Local)**: 3 copies in one datacenter
   - **ZRS (Zone)**: 3 copies across AZs

2. **Secondary Region**:
   - **GRS (Geo)**: LRS + async copy to secondary region
   - **GZRS (Geo-Zone)**: ZRS + async geo-replication

3. **Read Access**:
   - **RA-GRS**: GRS with read access to secondary
   - **RA-GZRS**: GZRS with read access

#### **Key Concepts**
- **Blob Lifecycle Management**: Auto-tiering rules
- **Rehydration**: Moving from Archive → Cool/Hot (hours)
- **Early Deletion Fees**: Cool (30d), Archive (180d)
- **IOPS**: Critical metric for performance-sensitive workloads

#### **Specialized Services**
- **Azure Data Box**: Physical data transfer device
- **Data Lake Storage Gen2**: Unified analytics storage

### Azure Storage Key Concepts (Exam Focus)

#### **Replication Types**
1. **Primary Region**:
   - **LRS** (Local): 
     - 3 sync copies in 1 datacenter
     - 11 nines durability
     - Cheapest option
   - **ZRS** (Zone):
     - 3 sync copies across AZs
     - 12 nines durability
     - Protects against AZ failure

2. **Secondary Region**:
   - **GRS**: LRS + async copy to paired region
   - **GZRS**: ZRS + async geo-replication
   - 16 nines durability
   - Secondary only accessible during failover

3. **Read Access Secondary**:
   - **RA-GRS/RA-GZRS**: 
     - Sync copies in secondary region
     - Allows read access to secondary

#### **Blob Storage Essentials**
- **Types**:
  - **Block blobs**: Standard files (4.7TB max)
  - **Append blobs**: Log files (append-only)
  - **Page blobs**: VHDs (8TB max)

- **Access Tools**:
  - **AZCopy**: CLI utility (needs RBAC roles)
  - **Storage Explorer**: GUI management

#### **Azure Files**
- Managed SMB/NFS shares in cloud
- Use cases:
  - Replace on-prem file servers
  - Centralized app settings
  - Container persistent storage
  - Hybrid cloud deployments

#### **Azure File Sync**
- Caches Azure file shares on local servers
- Enables:
  - Cloud tiering (hot/cold files)
  - Multi-site sync
  - Protocol flexibility (SMB/NFS/FTP)

#### **Key Exam Notes**
- **Sync vs Async**:
  - Sync = immediate consistency (LRS/ZRS)
  - Async = eventual consistency (GRS/GZRS)
- **Naming**: Storage account names must be globally unique (DNS-based)
- **Performance**: Premium = SSD (low latency), Standard = HDD
- **Access Tiers**: Hot (frequent), Cool (30d+), Archive (180d+)

### Azure Active Directory (Key Exam Concepts)

#### **Azure AD Editions**
| Tier | Key Features |
|------|-------------|
| **Free** | Basic MFA, SSO, user management |
| **Office 365 Apps** | Company branding, on-prem sync |
| **Premium P1** | Hybrid architectures, conditional access |
| **Premium P2** | Identity protection, governance |

#### **Core Components**
- **Identity Providers**: Cloud-based authentication service
- **AD Domain Services**: Managed domain controllers (LDAP/Kerberos/NTLM)
- **External Identities**: B2B (business partners) and B2C (consumer) scenarios

#### **Single Sign-On (SSO) Protocols**
| Protocol | Use Case | Notes |
|----------|---------|-------|
| **OpenID Connect** | Modern web apps | Built on OAuth 2.0 |
| **SAML** | Enterprise federation | XML-based |
| **Password-based** | Legacy apps | Credential replay |
| **IWA** | On-prem Windows | Uses domain credentials |
| **Header-based** | Custom apps | Token in HTTP headers |

#### **Multi-Factor Authentication (MFA)**
- Requires 2+ verification methods
- Protects against credential theft
- Enabled by default in P1/P2 tiers

#### **Conditional Access**
- **Policy Components**:
  - Signals (user/device/location)
  - Conditions (apps/risk levels)
  - Controls (block/require MFA)
- **Key Scenarios**:
  - Require MFA for admins
  - Block access from risky locations
  - Device compliance enforcement

#### **Terminology**
- **Domain Controller**: Auth server (on-prem/cloud)
- **GPO**: Security policy container
- **Organizational Unit (OU)**: AD object container
- **Hybrid Identity**: Sync between on-prem AD and Azure AD

#### **Exam Notes**
- Azure AD ≠ On-prem AD (complementary services)
- P1/P2 required for advanced features
- Conditional access evaluates signals in real-time
- B2B vs B2C external identities have different use cases

### Zero Trust & Defense in Depth

#### **Microsoft Zero Trust Model**
**Core Principles**:
1. **Verify Explicitly**  
   - Authenticate/authorize using all available signals (user, device, location, etc.)
   
2. **Least Privilege Access**  
   - JIT (Just-In-Time) access  
   - JEA (Just-Enough-Access) policies  
   - Risk-based adaptive controls

3. **Assume Breach**  
   - Micro-segmentation  
   - End-to-end encryption  
   - Continuous monitoring

**Six Pillars**:
1. **Identities** (Azure AD/Microsoft Entra)  
2. **Endpoints** (Devices)  
3. **Applications**  
4. **Data**  
5. **Infrastructure**  
6. **Networks**

#### **Defense in Depth (7 Layers)**
| Layer | Focus | Example Controls |
|-------|-------|------------------|
| **Data** | Encryption & access | Azure Storage Service Encryption |
| **Application** | Secure development | Web Application Firewall |
| **Compute** | VM/endpoint security | Azure Security Center monitoring |
| **Network** | Segmentation | NSGs, Azure Firewall |
| **Perimeter** | DDoS protection | Azure DDoS Protection |
| **Identity** | Access control | Conditional Access, MFA |
| **Physical** | Datacenter security | Biometric access controls |

#### **Key Exam Takeaways**
- Zero Trust replaces traditional perimeter-based security
- Identity is the new security perimeter (Azure AD focus)
- Defense in Depth provides layered protection
- Microsoft's model aligns with NIST SP 800-207 standard
- All principles apply across all Azure services

### Azure Defender & Multi-Factor Authentication

#### **Azure Defender**
1. **Core Components**:
   - **Coverage**: Protects multiple resource types (VMs, SQL, Key Vaults, Storage, etc.)
   - **Security Alerts**: Real-time threat notifications with remediation steps
   - **Insights**: Security recommendations and priority alerts
   - **Advanced Protection**: Additional security features (see below)

2. **Key Features**:
   - VM vulnerability assessments
   - Just-in-Time VM access
   - Container image scanning
   - Adaptive network hardening
   - Network map visualization

3. **Protection Scope**:
   - Works across Azure, hybrid, and multi-cloud (via Azure Arc)
   - Covers AWS/GCP resources when integrated
   - Unified security management plane

#### **Multi-Factor Authentication (MFA)**
1. **How It Works**:
   - Requires two or more verification methods:
     - Something you know (password)
     - Something you have (phone/app)
     - Something you are (biometrics)

2. **Azure MFA Methods**:
   - Microsoft Authenticator app
   - SMS/text verification
   - Phone call verification
   - OAuth hardware tokens

3. **Why Use MFA**:
   - Mitigates credential theft
   - Required for Conditional Access policies
   - Complies with most security frameworks

4. **Implementation**:
   - Enabled by default in Azure AD Premium tiers
   - Can enforce via Conditional Access policies
   - Applies to both cloud and hybrid identities

#### **Exam Notes**
- Azure Defender is part of Microsoft Defender for Cloud
- MFA is a core Zero Trust requirement
- Network maps provide visual security topology
- JIT VM access reduces attack surface
- Azure Arc enables cross-cloud security management

### Azure Security & Management Services

#### **Azure Security Center**
- **Purpose**: Unified security management for hybrid cloud
- **Key Features**:
  - Continuous compliance monitoring
  - Security posture scoring
  - Integrated with Azure Defender (advanced threat protection)

#### **Azure Key Vault**
- **Functions**:
  - Secrets management (passwords, API keys)
  - Key management (encryption keys)
  - Certificate management (SSL/TLS)
  - HSM-backed storage (FIPS 140-2 validated)

#### **DDoS Protection**
| Tier | Features | Cost |
|------|----------|------|
| **Basic** | Always-on traffic monitoring | Free |
| **Standard** | Metrics/alerts, SLA guarantee | ~$3k/month |

**Attack Types**:
1. Volumetric (bandwidth exhaustion)
2. Protocol (TCP/UDP floods)
3. Application layer (HTTP/SQL attacks)

#### **Azure Firewall**
- Stateful firewall-as-a-service
- Features:
  - Threat intelligence feeds
  - Network traffic filtering
  - Azure Monitor integration
  - Static public IP support

#### **Application Gateway**
- Layer 7 load balancer
- **Routing Rules**:
  - Basic (catch-all)
  - Multi-site (host header-based)
- **Backend Pool Options**:
  - VMs, VMSS, IPs, App Services

#### **RBAC (Role-Based Access Control)**
| Role | Permissions |
|------|------------|
| Owner | Full access + grant rights |
| Contributor | Create/manage (no grants) |
| Reader | View-only |
| User Admin | Manage user access |

**RBAC Components**:
1. Security Principal (who)
2. Role Definition (what)
3. Scope (where - mgmt group/sub/RG/resource)

#### **Management Groups**
- Hierarchical organization of subscriptions
- Inheritance: Policies apply downward
- Root MG → Child MGs → Subscriptions

#### **Azure Service Health**
- **Three Components**:
  1. Azure Status (global outages)
  2. Service Health (personalized view)
  3. Resource Health (per-resource status)

#### **Key Exam Notes**
- Key Vault uses HSMs for FIPS compliance
- App Gateway supports SSL termination
- RBAC scope hierarchy: MG > Sub > RG > Resource
- DDoS Standard required for SLA protection
- Security Center provides unified security posture

### Part 25: Azure Optimization & Development Services

#### **Azure Advisor**
- **Purpose**: Personalized cloud optimization recommendations
- **Categories**:
  1. Cost (e.g., idle resources)
  2. Security (e.g., MFA enablement)
  3. Performance (e.g., VM sizing)
  4. High Availability (e.g., backup configuration)
  5. Operational Excellence (e.g., activity log alerts)

#### **Azure Database Services**
| Service | Type | Key Feature |
|---------|------|-------------|
| **Cosmos DB** | NoSQL | 99.999% SLA, multi-model |
| **SQL Database** | Relational (MS SQL) | Fully managed PaaS |
| **Database for MySQL/PostgreSQL** | Relational | Open-source RDBMS |
| **SQL Server on VMs** | Relational (MS SQL) | Lift-and-shift IaaS |
| **Synapse Analytics** | Data Warehouse | Integrated analytics |
| **Cache for Redis** | In-memory | Low-latency caching |
| **Table Storage** | NoSQL | Key-value store |

#### **Application Integration Services**
1. **Notification Hub**: Cross-platform push notifications
2. **API Apps**: Cloud-hosted API endpoints
3. **Service Bus**: Enterprise messaging (pub/sub)
4. **Stream Analytics**: Real-time event processing
5. **Logic Apps**: Workflow automation (low-code)
6. **API Management**: API gateway with analytics
7. **Queue Storage**: App-to-app messaging

#### **Developer Tools**
- **SignalR**: Real-time web functionality
- **App Service**: Fully managed web apps (PaaS)
- **Visual Studio**: Azure-integrated IDE
- **Xamarin**: Mobile app development framework

#### **Key Exam Notes**
- Cosmos DB offers 5 nines availability
- SQL Database vs SQL on VMs: PaaS vs IaaS
- Service Bus vs Queue Storage: Enterprise vs simple messaging
- Logic Apps use connectors for SaaS integration
- Advisor recommendations are subscription-scoped

### Part 26: Azure DevOps, Networking & IoT Services

#### **Azure DevOps Services**
| Service | Purpose | Key Feature |
|---------|---------|-------------|
| **Boards** | Agile planning | Kanban boards, sprint tracking |
| **Pipelines** | CI/CD | Multi-cloud deployments |
| **Repos** | Code management | Git repositories (like GitHub) |
| **Test Plans** | QA testing | Manual/exploratory testing tools |
| **Artifacts** | Package management | NuGet/npm feeds |
| **DevTest Labs** | Environment mgmt | Quick dev/test sandboxes |

#### **Cloud-Native Networking**
1. **Azure DNS**: Ultra-fast domain management
2. **VNETs**: Isolated network segments
3. **Load Balancer (L4)**: TCP/UDP traffic distribution
4. **Application Gateway (L7)**: HTTP routing + WAF
5. **NSGs**: Virtual firewall for subnets/VMs

#### **Enterprise/Hybrid Networking**
| Service | Use Case | Throughput |
|---------|----------|------------|
| **Front Door** | Global entry point | HTTP acceleration |
| **ExpressRoute** | Private cloud connection | 50Mbps-10Gbps |
| **Virtual WAN** | Hub-spoke networking | Unified management |
| **VPN Gateway** | Site-to-site VPN | Lower bandwidth |

#### **Azure Traffic Manager**
- **DNS-level** load balancing
- **Routing Methods**:
  - Performance (latency-based)
  - Priority (failover)
  - Geographic (location-based)
  - Weighted (A/B testing)

#### **IoT Services**
| Service | Purpose | Key Feature |
|---------|---------|-------------|
| **IoT Central** | SaaS IoT solution | No-code device mgmt |
| **IoT Hub** | Device-cloud comms | Bi-directional messaging |
| **IoT Edge** | Edge computing | Local data processing |
| **Win10 IoT Core** | Embedded OS | Long-term support |

#### **Key Exam Notes**
- ExpressRoute provides **private** (not Internet) connectivity
- Traffic Manager vs Load Balancer: DNS vs IP routing
- IoT Edge enables offline-capable devices
- DevOps Pipelines support multi-cloud deployments
- Application Gateway includes WAF capability

### Part 27: Azure Big Data & AI Services

#### **Big Data & Analytics**
| Service | Type | Key Feature |
|---------|------|-------------|
| **Synapse Analytics** | Data Warehouse | SQL-based analytics at scale |
| **HDInsight** | Managed Clusters | Open-source (Hadoop/Spark/Kafka) |
| **Databricks** | Spark Platform | Optimized Spark environment |
| **Data Lake Analytics** | On-demand Jobs | Serverless query processing |

**Key Concepts**:
- **Data Lake**: Raw data storage in native format
- **ETL vs ELT**: Synapse supports both patterns
- **Serverless Options**: Data Lake Analytics, Synapse serverless

#### **AI/ML Hierarchy**
1. **Artificial Intelligence (AI)**: Human-like tasks
2. **Machine Learning (ML)**: Improves without explicit programming
3. **Deep Learning**: Neural networks for complex problems

#### **Machine Learning Services**
- **Azure ML Service**:
  - Full ML lifecycle management
  - Supports Python/R/TensorFlow
  - Pipeline automation
- **Azure ML Studio (Classic)**:
  - Legacy drag-and-drop interface
  - Limited functionality

#### **Cognitive Services (Pre-built AI)**
| Category | Example Services | Use Case |
|----------|-----------------|----------|
| **Language** | Translator, LUIS | Text translation, NLP |
| **Vision** | Computer Vision, Face | Image recognition |
| **Decision** | Anomaly Detector | Pattern analysis |
| **Web Search** | Bing API | Search integration |
| **Speech** | Speech-to-Text | Voice interfaces |

#### **Key Exam Notes**
- Synapse replaces SQL Data Warehouse
- HDInsight vs Databricks: OSS vs optimized Spark
- Cognitive Services require no ML expertise
- Always choose ML Service over ML Studio (classic)
- Data Lakes store raw, unstructured data

### Part 28: Azure Serverless & Resource Management

#### **Serverless Computing Characteristics**
- **Event-driven execution**: Functions triggered by events (HTTP, timers, etc.)
- **No infrastructure management**: Azure handles scaling/availability
- **Micro-billing**: Pay per execution (100ms granularity)
- **Polyglot support**: Multiple runtime languages (Node.js, Python, C#, etc.)

#### **Key Serverless Services**
| Service | Purpose | Key Feature |
|---------|---------|-------------|
| **Azure Functions** | Event-driven compute | Supports triggers/bindings |
| **Blob Storage** | Serverless object storage | Auto-scaling capacity |
| **Logic Apps** | Workflow automation | Low-code visual designer |
| **Event Grid** | Event routing | Pub/sub messaging |

#### **Resource Groups Essentials**
- **Logical containers** for Azure resources
- **Key attributes**:
  - Region-scoped (but can contain cross-region resources)
  - No cost for the group itself
  - Mandatory for resource deployment
- **Management benefits**:
  - Unified lifecycle management
  - Role-based access control (RBAC) boundary
  - Billing/tagging organization

#### **Function App Components**
1. **Function App**: Container for functions (shared context)
2. **Triggers**: Event types that invoke functions (HTTP, queue, timer)
3. **Bindings**: Declarative connections to other services
4. **Authorization Levels**:
   - Function (key required)
   - Anonymous (no key)
   - Admin (master key)

#### **Exam Critical Notes**
- Serverless ≠ No servers (just abstracted)
- Cold starts affect latency (mitigate with premium plans)
- Always use resource groups for organization
- Functions scale automatically (up to 200 instances by default)
- Blob Storage supports triggers for serverless workflows

### Part 29: Azure SLAs, Pricing & Licensing

#### **Service Level Agreements (SLAs)**
- **Definition**: Azure's uptime/connectivity guarantees per service
- **Key Points**:
  - Expressed as "nines" (99.9% = three nines)
  - Free/shared tiers have no SLA
  - Varies by service (e.g., Cosmos DB offers 99.999%)
  - Check official SLA docs for each service

#### **Service Credits**
- **Compensation** for missed SLA targets
- **Example VM Credits**:
  - <99.9% uptime → 10% credit
  - <99% → 25% credit
  - <95% → 100% credit

#### **Composite SLAs**
- **Calculation**: Multiply individual SLAs (e.g., Web App 99.95% × SQL 99.99% = 99.94%)
- **Improvement Strategies**:
  - Add redundant components (queues/failovers)
  - Design for resiliency

#### **TCO Calculator**
- **Purpose**: Compare on-prem vs. cloud costs
- **Inputs**:
  - Server specs (CPU/RAM/storage)
  - Network bandwidth
  - Labor/maintenance costs
- **Output**: Detailed 1-5 year savings report

#### **Azure Marketplace**
- **Third-party solutions**: VMs, apps, SaaS
- **Pricing Models**:
  - Free
  - BYOL (Bring Your Own License)
  - Pay-as-you-go
  - Free trials

#### **Azure Hybrid Benefit (AHB)**
- **Applies to**: Windows Server & SQL Server VMs
- **Key Benefits**:
  - Reuse on-prem licenses in Azure
  - Significant cost savings (up to 85%)
  - Enable during VM creation or after

#### **Exam Notes**
- Composite SLAs always ≤ weakest component SLA
- AHB requires Software Assurance
- Marketplace offers pre-configured solutions
- Credits apply to service costs (not refunds)

# AZ-900 Study Notes: Azure Subscriptions, Pricing, Cost Management, and Tags

## Azure Subscriptions
- **Definition**: Equivalent to an "Azure account"; used to manage and pay for Azure services.
- **Subscription Tiers**:
  - **Free Subscription**:
    - Requires a credit card for sign-up.
    - Includes $200 USD free credits for 30 days.
    - Some Azure products free for 12 months.
    - Limitations (e.g., restricted user access).
    - Possible charges if exceeding free tier limits.
  - **Pay-as-you-go (PAYG)**:
    - Credit card required.
    - Charged monthly based on resource usage.
  - **Enterprise Agreement**:
    - Discounted pricing for enterprises.
    - Requires negotiation with Azure.
  - **Student Subscription**:
    - No credit card required.
    - $100 USD credits for 12 months.
    - Requires valid student email.

## Managing Azure Spend
- **Track Spend**:
  - Navigate to **Subscriptions** in the Azure portal.
  - View remaining credits and usage.
  - Upgrade subscription when needed (e.g., from free to PAYG).
- **Support Options**:
  - Basic support included; premium support available for additional fees.

## Azure Pricing Calculator
- **Purpose**: Estimate costs for Azure products before deployment.
- **Features**:
  - No sign-in required.
  - Downloadable Excel spreadsheets for sharing estimates.
  - Example scenarios (e.g., CI/CD pipelines, virtual machines).
  - Customizable inputs (region, OS, configuration).
- **Usage**:
  - Access via [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator).
  - Adjust parameters (e.g., storage type, operations) to refine estimates.

## Azure Cost Management
- **Features**:
  - **Cost Analysis**: Visualize spending with graphs and filters.
  - **Budgets**: Set thresholds and receive alerts for overspending.
- **Use Case**: Monitor and optimize cloud resource expenditures.

## Resource Tags
- **Definition**: Key-value pairs assigned to Azure resources for organization.
- **Common Tag Examples**:
  - Department (e.g., `Finance`, `IT`).
  - Environment (e.g., `Dev`, `Prod`).
  - Status (e.g., `Approved`, `Pending`).
  - Project or team names.
  - Compliance/security classifications.
- **Benefits**:
  - **Resource Management**: Group by workload/environment.
  - **Cost Tracking**: Allocate costs by department/project.
  - **Operations**: Identify mission-critical services.
  - **Security**: Classify data for compliance (e.g., `PCI-DSS`).
- **Best Practice**: Use tags consistently in production workloads.

# AZ-900 Study Notes: Microsoft Purview, Azure Policies, Locks, Blueprints, and Portal

## Microsoft Purview Information Protection
- **Purpose**: Discover, classify, and protect sensitive data across hybrid environments.
- **Four Domains**:
  1. **Know Your Data**:
     - **Sensitive Information Types**: Identifies data using regex or custom rules (e.g., keywords, confidence levels).
     - **Trainable Classifiers**: Uses examples (not patterns) to classify data (built-in or custom).
     - **Data Classification**: Visualizes labeled/retained items and user actions (via **Context/Activity Explorer**).
  2. **Protect Your Data**:
     - Tools: Encryption, access restrictions, visual markings (e.g., **Sensitivity Labels**, **Azure Information Protection**).
  3. **Prevent Data Loss (DLP)**:
     - Prevents accidental sharing (e.g., **Microsoft Purview DLP**, browser extensions for compliance).
  4. **Govern Your Data**:
     - **Data Lifecycle Management**: Retain/delete data per compliance needs (e.g., retention policies, labels).
     - **Records Management**: Manages high-value items (e.g., legal/regulatory records) via file plans/disposition reviews.

## Azure Policies
- **Purpose**: Enforce organizational standards and assess compliance (no access restrictions).
- **Components**:
  - **Policy Definition**: JSON file with business rules.
  - **Policy Assignment**: Scope (user/resource group/management group).
  - **Initiative Definitions**: Groups of policies (e.g., PCI-DSS compliance).
- **Use Case**: Compliance with standards like NIST, HIPAA, FedRAMP.

## Resource Locks
- **Purpose**: Prevent accidental deletion/modification of critical resources.
- **Lock Types**:
  - **Cannot Delete**: Allows read/modify but blocks deletion.
  - **Read-Only**: Blocks updates/deletions (read-only access).

## Azure Blueprints
- **Purpose**: Deploy governed subscriptions with predefined patterns.
- **Features**:
  - **Declarative**: Predefined resources (ARM templates, policies, role assignments).
  - **Relationship Tracking**: Links blueprint definitions to assignments.
  - **Multi-Subscription Updates**: Upgrade multiple subscriptions simultaneously.
- **vs. ARM Templates**:
  - Blueprints maintain active relationships and support auditing/tracking.

## Azure Portal
- **Overview**: Web-based console for managing Azure resources (portal.azure.com).
- **Preview Portal**:
  - Access beta/pre-release features (preview.portal.azure.com).
  - **Caution**: Avoid preview features in production (potential rollbacks).
- **Accessing Previews**:
  - Register features under **Subscriptions** > **Preview Features**.
  - Example: Microsoft Fabric (requires organizational account).

## Key Takeaways
- **Purview**: Classify/protect data via labels, DLP, and governance.
- **Policies**: Monitor compliance; initiatives group related policies.
- **Locks**: Safeguard critical resources.
- **Blueprints**: Standardize deployments with governance.
- **Portal**: Use preview features cautiously; prefer stable releases for production.

# AZ-900 Study Notes: Azure Cloud Shell, PowerShell, and CLI

## Azure Cloud Shell
- **Purpose**: Browser-accessible shell (Bash/PowerShell) for managing Azure resources.
- **Features**:
  - **Access**: Click the Cloud Shell icon in Azure Portal header.
  - **Setup**: Requires a storage account (auto-created on first use).
  - **Pre-installed Tools**: Includes Azure CLI (`az`) and PowerShell modules.
- **Usage**:
  - **Bash**: Linux-based commands (e.g., `pwd`, `ls`).
  - **Azure CLI**: Run `az` commands (e.g., `az account list` to view subscriptions).
- **Resource Providers**: Ensure `Microsoft.CloudShell` is registered (via **Subscriptions** > **Resource Providers**).

## Azure PowerShell
- **What is PowerShell?**:
  - Task automation tool (command-line shell + scripting language).
  - Built on .NET, returns objects (not just text).
- **Azure PowerShell**:
  - **Cmdlets**: Commands for managing Azure resources (e.g., `New-AzResourceGroup`).
  - **Access**: Via Cloud Shell or local installation (Windows/macOS/Linux).

## Azure Files
    - Fully managed file share in cloud
    - Network protocols can be used
        - Server Message Block (SMB)
        - Network File System (NFS)
    - Use cases
        - Replace or supplement on-prem file servers Network Attach Storage(NAS)
        - Lift-and-Shift
            - Classic  - Move both application and data to Azure
            - Hybrid - Move data and keep application on prem
        - Simplify cloud development
            - Shared application settings
            - Diagnostic share - All logs in one place
            - Dev/Test/Debug - Shared tools for developer needed for local environments
        - Containerization
            - Persist volumes for stateful containers
    - Why use Azure Files instread of own file share
        - Shared access
        - Fully managed
        - Scripting and tooling - Can automate management and creation with Azure API and PowerShell
        - Resiliency

## Azure File Sync

    - Cache Azure file shares

## Azure Migrate
    -   Streamlined service for migration, modernization and optimization on Azure
    -   Simplifies pre-migration processes like discovering, assessing and sizing on prem resources 
    -   Easily integrates with third party tools
        -   Unified Migration Platform - Centralized portal to initiate, execute and monitor migration
        -   Diverse Toolset - Provide tools seamlessly integrate with other Azure services, tools and third party offerings from independant software vendors(ISVs)
    -   Comprehensive Migration and Modernization capabilities that can assess, migrate and modernize Servers, Db's and Web Apps
    -   Databases -> Azure SQL on a VM, Azure SQL Managed Instance or Azure SQL Database
    -   Web Apps -> App Service or Azure Kubernates
    -   Virtual Desktops -> Azure Virtual Desktop
    -   Integrated tools
        -   Azure Migrate: Discovery and assessment - Discover and assess VMware, Hyper-V and physical servers
        -   Migration and modernisation - Migrate VMware VMs, Hyper-V VMs, Physical servers, Virtual servers etc
        -   Data migration Assistant - Data migration assistant for SQL servers, identify problems, unsupported features
        -   Azure Database Migration Service - Managed service for seamless migration to Azure data platforms
        -   Movere - Saas platform that enhances business intelligence by accuraely depcting IT environments
        -   Web app migration assistant - Stnadalone tool to assesss on-prem websites for migration to App Service
        -   Azure Data Box - Move large amount of offline data to Azure

## Azure Databox

    -   Send terabytes of data into and out of Azure
    -   Can use SMB or NFS
    -   Each device max 80TB
    -   Import Use cases
        -   One-time migrations - Offline tapes, Relocate VM's, Historical data
        -   Initial bulk transfers - Moving vast backups
        -   Periodic uploads - Video content from oil rigs, windmill farms
    -   Export use cases
        -   Disaster recovery - Restoring data on-prem 
        -   Security requirments
        -   Migration data back to on-prem or different cloud provider

## Azure Entra ID ( Active Directory )
    -   Microsoft's identify and access managment service
    -   Four editions
        -   Free - MFA, SSO, Basic security, Usage reports, User managment
        -   Office 365 Apps - Company branding, SLA, Two Sync between On-Prem and Cloud
        -   Premium 1 - Hybrid Architecture, Advanced Group Access, Conditional Access
        -   Premium 2 - Identify Protection, Identity Governance

## Azure AD - Terminology

    -   Domain - Area of a network organized by a single authentication database
    -   Active directory domain - Logical grouping of AD objects
    -   Domain controller - Server that authenticates user identities and authorizes their access to resources
    -   Domain Computer - Computer that is registered with a central authentication database
    -   AD Object - Basic element such as Users, Groups, Printers, Computers
    -   Group Policy Object(GPO) - Virtual collection of policy settings. Controls what AD Objects have access to
    -   Organisation Units(OU) - Subdivision with in AD
    -   Directory Service - Provides the methods for storing directory data and making available to network users ( eg Active Directory Domain Service, AD DS)

## Azure AD - Azure Active Directory Domain Services(AD DS)
    -   Provides managed domain service
        -   Domain joins
        -   Group policies
        -   Lightweight directory access protocal(LDAP)
        -   Kerboeros/NTLM authentication

## Azure AD - SSO in Entra ID

    -   Support MS 365, Salesforce, Dropbox
    -   Support SAML, OpeID Connect, OAuth
    -   Cloud apps - OpenID Connect, OAuth, SAML, password-based or linked
    -   On-Prem - password-based, Integrated Windows Auth, Header based or linked

## Azure AD - External Identities
    -   Bring own identities like Google or Facebook
    -   Share apps with external users ( B2B collaboratoin )
    -   Develop apps intended for other Azure AD tenants ( Single tenant or Multi tenant )
    -   Develop white labeled apps ( Azure AD B2C )

## Conditional Access
    -   Extra layer of security before allowing authenticated users to access data or assets
    -   Implemented via Conditional Access policies( Set of rules that specify the conditions under which sign-ins are evaluated and allowed)
    -   Eg certain users need MFA
    -   Signals
        -   User or group membership
        -   Named location information / IP location information
        -   Device
        -   Application
        -   Real time sign in risk detection
        -   Cloud apps or actions
        -   User risk
    -   Decisions
        -   Block access
        -   Grant access
            -   Require multi factor authentication
            -   Require device to be marked as complient
            -   Require approved client app

## Zero trust model
    -   Trust no one, verify everything
    -   Principles
        -   Verify explicity - Always authenticate based on all available data points
        -   Least privileged access/Principle of Least Privilege (PoLP) - Limit user access with Just-In-Time and Just-Enough-Access risk-based adaptive policies, and data protection
        -   Assume breach - Minimize blast radius and segment access, verify end-to-end encryption and use analytics to get visibility, drive threat detection, improve defenses

## Defense in Depth

    -   7 layers of security
        -   Data - Access to business and customer data, encryption to protect data
        -   Application - Secure and free of security vulnerabilities
        -   Compute - Access to VM's
        -   Network - Limit communication between resources
        -   Perimeter - DDos protection
        -   Identify and access
        -   Physical - Access to data center

## MS Defender for Cloud ( Azure Defender )

    -   Coverate
    -   Security Alerts
    -   Insights - Suggested reading, high priority alerts
    -   Advanced Protection
        -   VM vulnerabilty assessment
        -   Just-in-time VM access
        -   Adaptative application control
        -   Container image scanning
        -   Adaptive network hardening
        -   SQL vulnerabilty assessment
        -   File integrity monitoring
        -   Network map
        -   IOT security
    -   Hybrid cloud protection
        -   Can protect virtual machines residing in other cloud servic providers
        -   Azure Arc is a control pane that manage compute resources in other cloud service providers

## Azure Security center
    -   Unified infrastructure security management system

## Key vault
    -   Helps safehard cryptographic keys and other secrets
    -   tokens, passwords, certificates etc
    -   Hardware security module(HSM)
        -   Multi tenant -Multiple customers virtually isolated on an HSM
        -   Single customer on a dedicated HSM

## Azure DDoS Protection
    -   Types of DDoS
        -   Volumetric attacks
            -   Volume based attacks that flood the network
            -   Exhausts bandwidth
            -   Measured in bps
        -   Protocol attacks
            -   Exhaust server reosurces with false protocal requets ( UDP TCP flooding on Layer 3/4)
            -   Measured in packages per second ( psp)
        -   Application layer attacks
            -   HTTP floods, SQL injection, cross-site scripting(XSS), parameter tampering
            -   WAF for protection
    -   Two tiers of DDos Protection
        -   Basic
        -   Standard
            -   Metrics, Alerts, Reporting
            -   Export support
            -   Application and Cost Protection SLAs

## Azure Firewall
    -   Managed, cloud-based network security service protects Azure VNets
    -   Fully stateful Firewall as a Service
        -   Built in high availability
        -   Unrestricted cloud scalability
    -   Use static public IP address
    -   Integrated with Azure Monitor

## Application Gateway
    -   Application level routing and load balancing service
    -   Operate on OSI Layer 7

## Routing Rules
    -   Listerns
        -   Basic - forward all requets for any domain to backend pools
        -   Multi-site - forward requets to different backend pools based on host header and host name
    - Requests are matched based on order of the rules and type of listener
    -   Backend targest
        -   Backend Pools or Redirection
    -   HTTP Settings
        -   Allow define how we want to handle cookies, connection draining, port request time out

## Role based access control (RBAC)
    -   Who has access to Azure resoruces, what they can do with them, and what areas they have access to
    -   Role assignment
        -   Security principle
            - Represents the identities eg User, Group, Service Principle, Managed Identity
        -   Role defenition
            -   Collection of permissions
        -   Scope
            -   Set of resoruces that access for the Role assignment applies to
            -   Scope access controls at the Management, Subscription or Resource group level

## Management Groups
    -   Manage multiple subscriptions into a hierarchal structure

## Service Health
    -   Azure Status
    -   Azure service health
    -   Azure resource health

## Azure Advisor
    -   Personalized cloud consultant that helps to follow best practices to optimize azure deployments
    -   Display recommendations for all following categories
        -   High availability
        -   Security
        -   Performance
        -   Cost
        -   Operational Excellence    

## Database services
    -   Azure Cosmos DB
        -   Fully managed NoSQL database
    -   Azure SQL Database
        -   MS SQL fully managed
    -   Azure Database for MySQL/PSQL, MariaDB
    - SQL server on VMs ( MS SQL )
    -   Azure Synapse Analytics ( Azure SQL Data warehouse)
        -   Fully managed data warehouse
    -   Azure Database Migration service
    -   Azure Cache for Redis
    -   Azure Table Storage
        -   Wide Column NoSQL Database

## Application Integration
    -   Azure notification hub
        -   Pub/Sub push notification
    -   Azure API Apps
        -   API gateway
    -   Azure Service Bus
        -   Coud messaging as a service (MaaS)
    -   Azure stream Analytics
        -   Realtime analytics
    -   Azure Logics Apps
        -   Schedule, automate and orchestrate tasks, business processes and workflows
    -   Azure API Management
        -   Hybrid, multi-cloud management platform for APIs across all envs
        -   Put in front of existing APIs to add additional functionality
    -   Azure Queue Storage
        -   Messaging Queue

## Developer and Mobile Tools
    -   Azure SignalR Service
        -   Real-Time Messaging
    -   Azure app service
    -   Visual Studio
    -   Xamarin
        -   Mobile-App Framework

## Azure DevOps Services
    -   Azure DevOps
        -   Azure Boards(Kanban)
        -   Azure pipelines
        -   Azure Repos
        -   Azure Test Plans
        -   Azure artifacts
        -   Azure DevTest Labs

## Azure Cloud-Native Networking Services
    -   Azure DNS
    -   Azure Virtual Networks
    -   Azure Load Balancer (Level 4)
    -   Azure Application Gateway (Level 7)
    -   Network Security Groups

## Enterprise/Hybrid networking services
    -   Azure Front Door
        -   Scalable and secure entry pint for fast delivery of your global applications
    -   Azure Express Route
        -   Connection between on-prem to Azure cloud(50Mbps to 10Gbps)
    -   Virtual WAN
        -   Networking service that brings networking, security, routing functionality
    -   Azure Connection
        -   VPN connection secuirely connects two Azure local networks via IPsec
    -   Virtual Network Gateway
        -   Site to site VPN between Azure virtual network and local network

## Azure Traffic Manager
    -   Operates at DNS layers and reroute traffic
    -   Fail over 
    -   Route to random VM to simulate A/B testing

## IoT Services
    -   IoT central - Connect IoT to cloud
    -   IoT Hub - Enable secure and reliable communication between IoT app and devices
    -   IoT Edge - Fully managed servie built on Azure IoT Hub. Allow data processing and analysis nearest the IoT devices. Offload compting from cloud to IoT.
    -   Windows 10 IOT COre Services
        -   A cloud services subscription provides essential services needed to commercialize  a device on WIndows 10 IoT Core.

## Big Data and Analytics Services
    -   Azure Synapse Analytics - Data warehousing and Big Data analytics
    -   HDInsight - Run open source analytics software like Hadoop, Kafka and Spark
    -   Azure Databriks - Apache Spark based analytics platform optimized for Azure cloud services
    -   Data Lake Analytics - On demand analytics job service that simplifies big data.

## AI/ML Services
    -   Azure Machine Lerning service - Simplifies running AI/ML related workloads. Use Pthon, R and DL workloads such as Tensorflow.
    -   Azure Machine Learning Studio - Old service, No pipleline and other limitations

    - AI based services
        -   Personalizer
        -   Translator
        -   Anomaly detector
        -   Azure Bot Service- Intelligent, serverless bot service that scales on demand
        -   Form Recogniser - Automate the extraction of text, key/values pairs and tables from books
        -   Computer Vision
        -   Language Understanding - Natural language understanding into apps
        -   Q/A Maker
        -   Text Analytics
        -   Content moderator
        -   Face
        -   Ink Recogniser - Handwriting, shapes and document layout

## Serverless services
    -   Features
        -   Event driven scale
        -   Abstrction of Servers
        -   Micro Billing
    -   Azure Functions
    -   Blob Storage
    -   Logic apps
    -   Event Grid

## Service Level Agreemnts (SLA)
    -   Azure commitments for uptime and connectivity
    -   Performance target - in %

## Service Credits
    -   Complensation for under performing azure product

## Composite SLA
    -   When combine SLAs across different service offerings

## TCO Calculator ( Total cost of ownership )
    -   Estimate the cost savings

## Azure Hybrid Benefit
    -   Repurpose windows server licences on Azure

## Azure Cost analysis
    -   Perform cost analysis, visualize spendings, create budgets, create alerts

## MS Purview Information Protection
    -   Collection of features to help discover, classify, and protect sensitive information
    -   Know your data
        -   Understand data landscape
        -   Sensitive information types
            -   Identify sensitive data by using built-in or custom regular expressions or functions
        -   Trainable classifiers
            -   Identify sensitive data by using examples of data
        -   Data classification
            -   Graphical Identificatoin of items
    -   Protect your data
        -   Apply flexible protectoin actions that include encryption, access restrictions, visual markings
        -   Sensitivity labels
        -   Azure Information Protection unified labeling client
        -   Double Key Encryption
        -   Office 365 Message Encription
        -   Service encryption with Customer Key
        -   SharePoint Information RightsManagement(IRM)
        -   Rights Management connector
        -   Azure Information Protection unified labeling scanner
        -   Microsoft Defender for cloud apps
        -   Microsoft Information Protection SDK
    -   Prevent data loss
        -   Prevent accidental oversharing of sensitive information
        -   Microsoft Purview Data loss prevention(DLP)
        -   Endpoint data loss prevention
        -   Microsoft Compliance Extension - Chrome extension
        -   Microsoft Purview data loss prevention on-prem scanner
    -   Govern your data
        -   Microsoft Purview Data Lifecycle Management - Collection of features to govern your data for compliance or regulatory
        -   MS Purview Data Lifecycle Management
            -   Retentionn policies
            -   Inactive mailboxes
            -   Archive mailboxes
            -   Import service for PST files

## Azure policies
    -   Enforce organizational standards and to assess compliance ( do not restrict, but observe )
    -   Policy definitions - JSON file describe business rules
    -   Policy Assignment - Scope of a policy can effect
    -   Policy Parameters - Values can pass into policy definition
    -   Initiative Definitions - Collection

## Resource Locks
    -   Prevent accidentally deleting or modifying critical resources

### Lock levels
        -   CanNotDelete(Delete)
        -   ReadOnly(Read-only)

## Azure Blueprints
    -   Quick creation of governed subscriptions
    -   Compose artifacts based on common or organisation based patterns into reusable blueprints
    -   Backed by Azure Cosmos DB
    -   ARM Templates vs Azure Blueprints
        -   ARM Template 
            -   Stored locally or in source control
            -   No active connection or relationship to ARM template
        -   Azure Blueprints
            -   Relationship between blueprint definition and blueprint assignment
            -   Can also upgrade several subscriptions at once  
            -   Suppports improved tracking and auditing of deployments

## Azure Resource Manager (ARM)

    -   Manage azure resources

### Use cases
    -   A gate keeper where all requests flow through and decides whether that request can be performed

### Scoping
    -   Boundary control for azure resources
    -   Govern resources by placing resources
        -   within a logical group
        -   applying logical restrictions in the form of rules
    -   Management groups - A logical group of multiple subscriptions

### ARM templates
    -   Management and provisioning infrastructure via machine readable files(JSON)
    -   Types
        -   Declarative - Define exactly what you want and get exactly that
        -   Imperative - Define what you generally want and service will guess what you want
    -   ARM templates are declarative

## Azure Monitor
    -   Solution for collecting, analyzing and acting on telemetry

## The pillars of observabilty
    -   Observability - Ability to measure and understand how internal systems work
    -   To obtain observability need to use Metrics, Logs and Traces
    -   Metrics - A number that is measured over a period of time
    -   Logs -  A log file
    -   Traces - History of requests travel thorough to pinpoint a failure

## Anatomy of Azure Monitor

### Sources of common monitoring data
    -   Application
    -   OS
    -   Azure Resources
    -   Azure Subscription
    -   Azure Tenant
    -   Custom Sources

### Functions Azure monitor can perform

#### Insights
    -   Application
    -   Containers
    -   VMs
    -   Monitoring Solutions

#### Visualize
    -   Dashboard
    -   Views
    -   Power BI
    -   Workbooks

#### Analyze
    -   Metric Analytics
    -   Log Analytics

#### Respond
    -   Alerts
    -   Autoscale

#### Integrate
    -   Logic Apps
    -   Export APIs

## Log Analytics
    -   Edit and run log queries with data in Azure Monitor Logs

## Log Analytics workspaces
    -   Unique environment for Azure monitor log data

## Azure Alerts
    -   Notify when issues are found

### Types of Alerts
    -   Metric Alerts
    -   Log Alerts
    -   Activity Log Alerts

### Parts
    -   Alert Rule
    -   Action Group/Monitor condition

## Application Insights
    -   Application Performance Management(APM)
    -   Performance and availability