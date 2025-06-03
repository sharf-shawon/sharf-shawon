---
draft: true
date: '2025-06-03'
title: 'Can You Run A Proxmox HA Cluster On Dell Wyse 5070? Real-World Insights'
description: "Is the Dell Wyse 5070 suitable for running a Proxmox VE High Availability cluster? Here's a practical evaluation covering storage, networking, and performance considerations for your homelab."
tags: ["proxmox", "homelab", "dell wyse 5070", "high availability", "low power server"]
seo_keywords: "Proxmox VE HA Cluster, Dell Wyse 5070 Proxmox, Low Power Homelab Server, Proxmox Thin Client Setup, Sharfuddin Shawon"
showToc: true
TocOpen: false
hideSummary: false
searchHidden: false
ShowBreadCrumbs: true
canonicalURL: 'https://shawon.me/posts/dell-wyse-5070-proxmox-high-availability-cluster'
aliases: [ "/dell-wyse-5070-proxmox-ha"]
slug: "dell-wyse-5070-proxmox-high-availability-cluster"
cover:
  image: "/images/posts/proxmox-wyse-5070-ha-cover.jpg"
  alt: "Dell Wyse 5070 running Proxmox VE"
  caption: "Testing Proxmox VE HA on Dell Wyse 5070 Thin Clients"
  relative: true
  hidden: false
---

# Can You Run a Proxmox HA Cluster on Dell Wyse 5070? Let's find out.

If you're building a **low-power Proxmox VE cluster** and eyeing the **Dell Wyse 5070** as a cost-effective node, you're not alone. I got 3 Dell Wyse 5070 Thinclients with 4 Core **Intel J4105 processor** and 8GB ram each. These thin clients, are popular among homelab enthusiasts thanks to their affordability and energy efficiency. However, my question is, how well do they hold up in a **Proxmox HA (High Availability)** cluster setup?

Here’s what I discovered after testing a 3 node Wyse 5070-based cluster with **Proxmox VE 8** and attempting to enable **HA and Ceph**.

---

## eMMC Storage: Not Detected in Proxmox GUI

The internal **eMMC storage** on the Dell Wyse 5070 is **not recognized in the Proxmox GUI** by default. While it’s technically possible to access and use it through CLI-based setup tweaks, it's **not recommended for HA deployments**. eMMC is not designed for the I/O demands and reliability expectations of enterprise-grade or even enthusiast-grade HA storage.

### ➤ Verdict: Avoid using eMMC for critical storage or clustering.

---

## SATA Support: Limited to One Drive

Each Wyse 5070 has **only one SATA port** available, meaning:

- You can install **a single 2.5" SSD/HDD**.
- No internal room for a second drive.
- **USB disks** can be used, but they’re not ideal for redundancy or performance in HA or Ceph setups.

### ➤ Verdict: **Not viable for HA**, which requires at least two local disks per node (OS + data).

---

## Networking: Limited but Expandable

By default, the Wyse 5070 includes:

- **1x Gigabit Ethernet**
- **Wi-Fi (5GHz)**

While this setup works for a basic Proxmox node, it’s not sufficient for HA clusters or Ceph networking, where **dedicated bandwidth** is crucial.

### Recommended Options:

- Add a **USB Ethernet adapter**.
- Use the **M.2 A+E slot** (if available) for a second internal NIC.
- Consider a **VLAN-capable switch** if you're aggregating traffic across nodes.

### ➤ Verdict: Needs additional Ethernet interface for any serious HA or Ceph workload.

---

## Power Efficiency vs. Performance

One of the key selling points of the Wyse 5070 is its **power efficiency**. With a TDP under 10W, these units are perfect for:

- **Always-on services**
- **Learning environments**
- **Lightweight VMs/containers**

However, the **Intel J4105 CPU** is not ideal for compute-heavy workloads or high IOPS environments like those involved in Ceph clustering.

### ➤ Verdict: Ideal for **light homelab tasks**, not for performance-heavy use.

---

## Final Verdict: Proxmox HA Cluster Is Not Practical on Wyse 5070

While the **Dell Wyse 5070** makes for a great **low-cost Proxmox node**, it simply **lacks the hardware required for a proper HA cluster**:

| Criteria              | Result                     |
|-----------------------|----------------------------|
| Dual Disk Support     | ❌ Not available            |
| Reliable Local Storage| ❌ eMMC not suitable        |
| Dual NICs             | ❌ Only one onboard Ethernet|
| Ceph Ready            | ❌ Additional NICs needed   |
| Power Efficiency      | ✅ Excellent                |
| General Usability     | ✅ Good for lightweight setups |

> **HA Setup is NOT recommended** on Wyse 5070 unless major hardware mods are made.  
> For Ceph, **at least one dedicated Ethernet interface per node is essential**.

---

## Alternative Use Cases for Wyse 5070 in a Homelab

If you already have Dell Wyse 5070 units, here are some great uses:

- **Standalone Proxmox VE node**
- **Backup/replication node**
- **Docker Swarm or Kubernetes node (for lightweight services)**
- **Home assistant or Pi-hole server**
- **NFS/SMB client for shared storage environments**

---

## Final Thoughts

The Dell Wyse 5070 is a **great choice for power-conscious homelabbers**, but not a silver bullet. While it offers enough for basic virtualization and container orchestration, **don’t count on it for HA, Ceph, or enterprise-level clustering**.

For true high availability, look for nodes with:

- Dual SATA/NVMe support
- Dual NICs
- ECC memory (if possible)
- Higher IOPS storage options

---

If you're setting up your homelab or planning a Proxmox cluster, subscribe to my blog for more real-world experiments, practical tips, and cost-effective setups.

Got questions or suggestions? Drop a comment below or [contact me here](/contact).

