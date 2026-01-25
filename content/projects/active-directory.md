+++
date = '2026-01-24T21:50:51-05:00'
draft = false
title = 'Active Directory Setup'
description = "Setup for Active Directory using VMware Workstation Pro"
authors = ["Logan Wright"]
series = ["Part 1"]
+++

## Objective

* Install and configure **Active Directory Domain Services (AD DS)** on a virtual machine.
* Configure the VM as a **Domain Controller** and a **DNS Server**.
* Domain join a client VM to the `logan.local` domain.

## Why?

* Educational purposes and for further testing with **Group Policy Objects (GPOs)** and additional AD administrative tasks.

## Tasks Completed

* **Installation:** Set up Microsoft Server 2025 Evaluation using VMware Workstation and installed AD DS/DNS tools.
* **Maintenance:** Installed all updates for both the client and server, utilizing **snapshots** throughout the process.
* **Networking:** Configured static IPv4 addresses and pointed the client to the server for DNS.
* **Verification:** Tested connectivity between both machines using `ping`.
* **Domain Join:** Successfully joined a client VM to the domain using administrative credentials.

## Issues

* **"WHEA_UNCORRECTABLE_ERROR" BSOD**
    * A known error that occurs when using NVMe virtual disks during Windows updates inside VMware.
    * See [Troubleshooting Notes](#troubleshooting-notes) for the resolution.

## Outcome

* Successfully domain joined a Windows 11 client VM to a Microsoft Server 2025 Evaluation domain controller.

## Images 

<details>
  <summary>Show / hide images</summary>

  <div style="display: flex; flex-wrap: wrap; gap: 10px; margin-top: 20px;">
    
<a data-fslightbox="ad-setup" href="/images/projectimages/active-directory-setup/client.jpg">
    <img src="/images/projectimages/active-directory-setup/client.jpg" alt="Client VM" style="width:48%; height:auto; border-radius: 8px; cursor: pointer;">
</a>

<a data-fslightbox="ad-setup" href="/images/projectimages/active-directory-setup/server.png">
    <img src="/images/projectimages/active-directory-setup/server.png" alt="Server VM" style="width:48%; height:auto; border-radius: 8px; cursor: pointer;">
</a>

  </div>
</details>

## Troubleshooting Notes

After a quick search for the BSOD error, it appeared that VMware’s NVMe controller was the culprit. I took the following steps to resolve it:

1. **Removed** the NVMe Controller from the Server VM settings (while keeping the existing `.vmdk` files).
2. **Added** a new virtual hard drive using the **SATA** controller.
3. **Attached** the previous `.vmdk` files to the SATA controller.
4. Successfully booted the server and completed the update/restart process without further crashes.