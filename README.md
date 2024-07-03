# 📖 Introduction

Azure Site Recovery (ASR) is a Disaster recovery as a service by Azure for your virtual machines (VMs), both in the cloud (Azure) and on-premise. It continuously copies your VMs to a separate Azure region, acting like a secure off-site backup. This ensures your business keeps running even if disaster strikes your main location, like a fire, flood, or cyberattack. ASR constantly updates these backups (called replication), so they're always in sync with your original VMs. If something goes wrong, you can easily switch over (failover) to the backed-up VMs in Azure, minimizing downtime and data loss. By using ASR for your VMs, you're building a more resilient infrastructure, protecting your critical applications, and giving your business peace of mind in case of the unexpected.

# 📖 Fundamentals

**Key differences between High Availability and Disaster Recovery**

  * High availability (HA) within a region uses techniques like availability zones, fault domains, and load balancers.
  * HA protects against node, rack, or facility failures.
  * Synchronous replication and active-active configurations ensure data consistency and availability.
  * Disaster recovery involves a larger distance between regions for added protection.
  * Azure regions are defined by a two-millisecond latency envelope and may consist of multiple physical facilities.
  * Availability zones within a region provide independent cooling, power, networking, and communications.
  * HA techniques like synchronous replication and active-active configurations are used within a region.
  * Disaster recovery focuses on failover between regions for greater resilience.

**How Azure recovery Typically works**

  * Site Recovery installs the Mobility service on source VMs, 
  * Mobility service then copies data to a cache storage account in the same region.
  * The cache data is then used to replicate VM data to another region.
  * Failover to the target region can be done without paying for compute resources on Azure.
  * Failback to the source environment or reprotection of the target environment is possible.

# 🛠️ Configuring and Testing Disaster Recovery

To set up Azure Site Recovery (ASR) for a cloud-based Azure VM and ensure a smooth disaster recovery process, the following steps ensure best practice:

  * Region based Replication Selection
  * Running a test Disaster recovery
  * Cleanup, Commit, Re-Protect, and Changing Recovery Point

This three-step process creates a robust disaster recovery plan for your infrastructure, including setting up replication, testing recovery, switching to the backup, and returning to the original location with minimal disruption.

the following components are required for the completion of the Disaster recovery plan

  * Azure Site Recovery
  * Recovery Vault Service
  * Storage Accounts
  * Virtual Machines
  * Virtual Network

# 🚀 Procedures to Execute Disaster Recovery

**🛠️ Creating a Virtual Machine for Replication**
  * We need create the follwing
     * A resource group named **prodRG**
     * The virtual machine is named **prod"**.

**🛠️ Configuring Site Recovery**

  * Site Recovery can be enabled using the **Disaster Recovery** tab for the virtual machine created in the Azure portal.
  * The target region can be changed in the tab, here we switch it to Brazil south.
  * We review the settings and start the replication by confirming it.
  * The process of creating the necessary resources on Azure would take around 30 minutes.
  * *Additional Info - * Advanced settings include target settings, storage settings, replication settings, and extension settings.
  * *Additional Info - * Target settings allow configuration of the subscription, resource group, virtual network, and availability settings for the target environment.
  * *Additional Info - * Storage settings allow configuration of the cache storage account, including its type (premium SSD or standard SSD).
  * *Additional Info - * Replication settings include the Recovery Services Vault, resource group, and automation account for managing site recovery extension updates.

**🛠️ Replicated Resources Go Through**

  * Two new resource groups were created.
  * *ProdASR* Resource Group contains the virtual network for the target region.
  * Site Recovery Vault Resource Group contains the cache storage account, automation account, and Recovery Services Vault.
  * Replication status for the app server VM is healthy.
  * RPO would appear in a few minutes after the creation process as it takes time to calculate this value.

**🛠️ Test Failover Phase**

  * When we go over to the **prodRG-asr** resource group we would see an option to Failover, When we attempt to do a test failover.
  * A new virtual machine would be created in the target region.
  * In order to test the recovered virtual machine in the target region we would need to give it a public address.
  * Using the the public IP address we can access an ISS app server on the Windows server VM to verify functionality.

**🛠️ Cleanup, Commit, Re-Protect, Change Recovery Points**

  * After a test failover, you can clean up the test environment by deleting the virtual machine created during the test failover.
  * After a successful failover, you can:
     * Shut down the machine before beginning the failover.
     * Change recovery points until you commit to a specific recovery point.
     * Commit to a recovery point to prevent further changes.
     * Re-protect the target environment, which has now become the primary environment.

# Conclusion
This implementation guide has provided a comprehensive introduction to Azure Site Recovery, a powerful disaster recovery solution for virtual machines (VMs). We explored how Site Recovery replicates VMs from various sources (Azure, on-premises, or physical servers) to a secure target environment, ensuring business continuity during outages. The execution showcased the configuration process through the Azure portal, including target region selection, advanced settings for resources, storage, and replication, and initiating replication. We then set up a web server on the VM for demonstration purposes. Following successful replication, a test failover to the target region was performed, creating a new VM, assigning a public IP, and verifying accessibility. Finally, we explored post-failover options like cleaning up the test environment, managing recovery points (committing or changing), and re-protecting the now-primary target environment. This hands-on experience provided valuable insights into Azure Site Recovery's capabilities and its potential to strengthen your disaster recovery strategy.
