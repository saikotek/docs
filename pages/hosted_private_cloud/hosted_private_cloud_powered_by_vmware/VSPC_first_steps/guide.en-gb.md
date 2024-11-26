---
title: Getting started with VSCP
excerpt: Discover VSCP, a cloud-enabled platform provided by Veeam that helps you manage backups and data protection.
updated: 2024-11-21
---
## Objective

The **Veeam Service Provider Console (VSPC)** is a cloud-enabled platform for centralized management and monitoring of data protection operations and services. With VSPC, you can monitor backups, create custom backup policies, and make sure your servers are always protected, all from one central dashboard.

**This guide is an introduction to VSPC.** 

It will walk you through the first steps to get started with VSPC, including:

- Accessing the VSPC portal with your OVHcloud credentials.  
- Downloading and installing the management agent to connect your servers to VSPC.  
- Verifying that your servers are connected and showing up in VSPC.  
- Setting up and customizing backup policies for your servers.

> **[!Warning]**  
> OVHcloud provides services for which you are responsible, with regard to their configuration and management. It is therefore your responsibility to ensure that they work properly.  
> This guide is designed to assist you as much as possible with common tasks. However, we recommend contacting a specialist provider if you experience any difficulties or doubts when it comes to managing, using, or setting up a service on a server.
>
## Requirements
- A [Hosted Private Cloud infrastructure](https://www.ovhcloud.com) from OVHcloud to enable access to the Veeam Service Provider Console.
- Administrative permissions for the [OVHcloud Control Panel](https://www.ovhcloud.com/control-panel) to manage resources.
- A server compatible with the Veeam Backup Agents, running a supported [operating system](https://helpcenter.veeam.com).
- A firewall configured to allow communication between the VSPC and your managed servers.

## Instructions

### Step 1: Accessing the VSPC portal
1. Visit the VSPC portal link provided by OVHcloud (e.g., `https://...`).
2. Log in using the administrative credentials assigned to your Hosted Private Cloud infrastructure.
   - If credentials are missing, contact OVHcloud support or your account manager.
3. Upon login, you’ll see the VSPC dashboard. Key elements include:
   - **Active alarms**: Manage predefined alarms and customize them as needed.
   - **Dashboard overview**: Displays:
     - Protected workloads in your backup and cloud infrastructures.
     - Cloud resources consumed by your organization.
     - Job session statuses and data protection efficiency.
   - **Backup jobs**: Lists configured backup jobs, where you can create, run, or modify them.
   - **Data overview**: Provides a clear summary of backed-up data.
   - **Host discovery rules**: Configure rules for discovering hosts.
   - **Managed computers**: Lists all computers managed by the VSPC.
   - **Reports**: Access detailed reports on backup job completion.

*(Placeholder for screenshots of the VSPC dashboard)*

---

### Step 2: Downloading the Management Agent
1. Navigate to the **Discovered Computers** section in the VSPC.
2. Click `Download Management Agent`, then select `Create Download Link`.
3. Options available:
   - Copy the download link.
   - Download the agent directly.

> **Warning**: Check firewall rules to allow the VSPC to communicate with the target server before downloading.

---

### Step 3: Installing the Management Agent
1. Open the generated link on the target server to download the management agent.
2. Run the downloaded file on the target server.
3. Follow the installation prompts to complete the setup.
4. Verify the server appears in the **Discovered Computers** list with an installation progress bar.

*(Placeholder for screenshots of the installation process and “Discovered Computers” section with progress bar)*

---

### Step 4: Verifying the Agent installation
- Confirm the agent status in the **Discovered Computers** section.
- Check for successful connection and registration with the VSPC.

*(Placeholder for confirmation screenshots or verification steps)*

---

### Step 5: Changing backup policies
- OVHcloud provides a default backup policy, including a 2TB S3 bucket.
1. To review or configure the policy:
   - Navigate to the **Backup Job** section.
   - Click the value under `Successful Jobs` to view the default policy.
   - Select the backup policy you want to assign.
   - Modify components such as:
     - **Operation mode**: Select the type of host to back up.
     - **Backup mode**: Choose data to back up.
     - **Destination**: Define the backup storage location (e.g., 1TB S3 bucket).
     - **Repository credentials**: Configure authentication.
     - **Retention policy**: Set backup retention duration (default: 7 days).
     - **Guest processing mode**: Enable advanced options like file indexing and application-aware processing.
     - **Schedule**: Configure automatic backups (default: 10 PM daily, with retries for failures).

> **Warning**: Verify available storage space before starting backups or restorations. Insufficient space can result in failures.

---

### Policy customization scenarios

#### **Windows example: Partition-level backup**
- Configure the policy to back up only the `C:` drive.
1. Navigate to **Backup Jobs** and select the server.
2. Modify the backup policy by selecting `Partition Backup`.
3. Choose the `C:` partition and exclude others.

*(Placeholder for screenshots of the partition selection screen for Windows)*

#### **Linux example: Directory-level backup**
- Target critical directories like `/var/www`, excluding `/tmp`.
1. Navigate to **Backup Jobs** and select the Linux server.
2. Assign or modify a policy to include `/var/www` and exclude `/tmp`.

*(Placeholder for screenshots of the directory selection screen for Linux)*

---

### Step 6: Assigning policies to servers
1. Navigate to **Managed Computers** and select **Backup Agents**.
2. Choose the server from the list.
3. Click `Assign`, select the desired policy, and confirm.
4. View the summary of assigned policies by clicking `Show`.

*(Placeholder for screenshots of the policy assignment process)*

---

### Step 7: Managing backup jobs

#### **Scheduled backups**
- Backups run automatically as per the configured schedule.

#### **On-demand backups**
1. In the **Backup Jobs** section, select the server.
2. Click `Start` to initiate a backup immediately.

---

### Step 8: Logs and reporting
1. Generate reports from the **Reports** section in the VSPC.
2. Review logs to troubleshoot any issues during backup or restoration.

---

### Step 9: Restoring data
1. Use the VSPC interface to browse backups and select files for restoration.
2. Modify or erase files as needed during the restoration process.

*(Placeholder for screenshots of the restoration interface)*

---

## Go Further
- Join our [community of users](https://community.ovhcloud.com) to connect with other VSPC users.


