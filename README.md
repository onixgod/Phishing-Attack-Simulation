---
title: "Phishing Attack Simulation Lab"
description: "A step-by-step phishing lab using Gophish, Poste.io, and Kamatera cloud"
author: "Your Name"
date: 2025-07-13
layout: default
---

# Phishing Attack Simulation Lab with Gophish & Poste.io

## Overview

This lab simulates a **real-world phishing attack** in a safe and isolated environment. The objective is to understand phishing tactics, how malicious actors operate, and how defenders can detect and prevent such attacks using **Gophish** and **Poste.io**.

---

## Learning Goals

- Design and run realistic phishing campaigns
- Explore the capabilities of phishing infrastructure (Gophish + Mail server)
- Simulate user interactions with phishing emails and landing pages
- Improve your incident response and detection skills
- Analyze results and extract key insights from captured credentials and clicks

---

## Skills Gained

### 🛠Technical Skills
- Linux server setup and hardening
- Docker containerization and networking
- Cloud VM provisioning (Kamatera)
- Mail server configuration with Poste.io
- Firewall and network rule management

### Cybersecurity Skills
- Phishing campaign design
- Security awareness simulation
- Threat emulation and red team testing
- Detection strategy validation


---


### Technical Skills
- **Virtualisation Management**: Proxmox VE setup and VM provisioning  
- **Cloud Infrastructure**: Configuration and deployment using Kamatera  
- **Linux System Administration**: Hardening and managing Ubuntu servers  
- **Email Server Administration**: Installing and configuring Poste.io, SMTP setup  
- **Network Security**: Firewall setup and secure port management  

### Cybersecurity Skills
- **Phishing Campaign Design**: Crafting convincing emails and attack scenarios  
- **Security Awareness Testing**: Designing tests and defining evaluation metrics  
- **Threat Simulation**: Recreating real-world phishing attacks for training purposes  

---

## Tools Used

### Primary Tools
- **Gophish** – Open-source phishing simulation framework  
- **Poste.io** – All-in-one email server with web-based interface  
- **Proxmox VE** – Virtualisation platform used for lab environment  
- **Kamatera** – Cloud provider used to host the simulation infrastructure  

### Supporting Tools
- **Ubuntu Server 24.04 LTS** – Base OS for mail and phishing servers  
- **UFW (Uncomplicated Firewall)** – Host-based firewall tool  
- **Postfix** – Mail transfer agent used by Poste.io  
- **SQLite** – Lightweight database for Gophish campaign data  

---

## Target Environment

- **Lubuntu Desktop** – Lightweight Linux desktop for testing client interactions  
- **Disposable Email Clients** – Services like TempMail for receiving phishing emails in a safe, isolated manner

## Detailed Steps

### Phase 1: Infrastructure Planning and Preparation

The first step in this project is to create a comprehensive diagram to guide the deployment process. This planning phase is essential to understand the data flow and system interactions before implementation.

#### Step 1.1: Network Architecture Design

To visualize the project architecture, I used **Draw.io** to create a network diagram. It illustrates how each component — from virtual machines to cloud services — interacts during the phishing simulation setup.

**Diagram Components:**

- **Virtual Machines**: Lubuntu clients hosted in a Proxmox home lab
- **Cloud Services**: Kamatera-hosted Ubuntu server running Gophish and Poste.io
- **Network Infrastructure**: Routing, firewall rules, and port forwarding

**Figure 1: Lab Architecture Overview**  
<img width="1442" height="861" alt="Phishing Attack Simulation drawio (5)" src="https://github.com/user-attachments/assets/eea1dd4a-06ea-47aa-88d1-51c87f054894" />

---

### Phase 2: Phishing Campaign Workflow

The following diagram outlines the end-to-end workflow for executing a phishing campaign using Gophish and Poste.io. It includes the configuration steps and the execution lifecycle—from email creation to result analysis.

**Figure 2: Campaign Workflow**  
<img width="671" height="562" alt="phishing_simulation_workflow drawio (1)" src="https://github.com/user-attachments/assets/b8554c28-d7df-413f-8b34-c92d6ec8a893" />

#### Workflow Summary

1. **Initiation**
   - The manager launches the phishing simulation via the Gophish dashboard (port 3333).

2. **Configuration Phase**
   - Email templates, landing pages (port 8081), and recipient lists are created.
   - A sending profile is configured using Poste.io as the internal SMTP server (port 465).

3. **Execution**
   - The campaign is launched.
   - Gophish sends phishing emails through Poste.io.
   - Emails are delivered to TempMail inboxes used by the Lubuntu clients.

4. **User Interaction**
   - Targets receive the phishing email and interact with the landing page.
   - Gophish records user actions such as clicks and form submissions.

5. **Analysis**
   - The campaign results are monitored in the Gophish dashboard to evaluate engagement levels and identify areas for user awareness improvement.

## Phase 3: Cloud Infrastructure Setup

### Step 3.1: Kamatera Cloud VM Deployment

Kamatera was selected as the cloud provider due to its generous $100 free trial credit, which is sufficient for this project.

#### 1. Create a Kamatera Account
- Sign up at [Kamatera.com](https://www.kamatera.com/).
- The free trial provides enough credit to complete the full deployment.

#### 2. Deploy Ubuntu Server 24.04 LTS

- Navigate to **My Cloud** and click **Create New Server**.
- Select the following:
  - **Zone**: Closest to your region
  - **Image**: Ubuntu 24.04 LTS
  - **Server Type**: General Purpose

**Figure 3: Kamatera Server Deployment Page**  
<img width="1712" height="1177" alt="Screenshot 2025-07-11 000422" src="https://github.com/user-attachments/assets/268fde08-75a1-49a1-9736-7004a47ae33a" />

- Recommended specs:
  - 2 vCPUs
  - 4 GB RAM
  - 50 GB SSD
  - Public and private networking enabled

**Figure 4: Server Configuration Options**  
<img width="1265" height="933" alt="Screenshot 2025-07-12 115541" src="https://github.com/user-attachments/assets/23e5b241-269e-4848-8cb6-d5ab0ca2e392" />

- Set a root password
- Name the instance `MyLab-PhishLab`
- Estimated cost: ~$20/month

**Figure 5: Server Name and Password Configuration**  
<img width="1335" height="826" alt="Screenshot 2025-07-12 120615" src="https://github.com/user-attachments/assets/ba355d0a-6b97-4872-9618-0c1cbb897a9d" />

#### 3. Check Server Status

- Go to **Server List** and locate your new instance.

**Figure 6: Server Status Dashboard**  
<img width="1681" height="508" alt="Screenshot 2025-07-12 121141" src="https://github.com/user-attachments/assets/4c5e5e85-ee58-4911-9707-b83573247cb5" />

**Figure 7: Server Details**  
<img width="1408" height="686" alt="Screenshot 2025-07-12 121649" src="https://github.com/user-attachments/assets/a4b612c7-95d0-4658-a36c-31a831fc90df" />

- From your local terminal, test connectivity using:

```bash
ping <SERVER_PUBLIC_IP>
```

**Figure 8: Ping Test Output**  
<img width="1109" height="345" alt="Screenshot 2025-07-11 001820" src="https://github.com/user-attachments/assets/431390e7-5cd7-462e-956d-f4935da3c001" />

#### 4. Configure Kamatera Firewall

- Navigate to **Firewall** under the server’s settings
- Enable the firewall and add custom rules to allow TCP/UDP from your local IP

**Figure 9: Firewall Rule Settings**  
<img width="1440" height="988" alt="image" src="https://github.com/user-attachments/assets/25b7da53-74e9-48d1-b70e-51e1350c8a60" />

**Figure 10: UDP Rule Settings**  
<img width="604" height="680" alt="Screenshot 2025-07-11 003513" src="https://github.com/user-attachments/assets/03f02881-70a4-46ce-a973-a7f601814d4d" />

**Figure 11: TCP Rule Settings**  
<img width="599" height="678" alt="Screenshot 2025-07-11 003630" src="https://github.com/user-attachments/assets/b4d1ffd9-c6ec-45bf-b01d-29ff5f230926" />

- Use an IP lookup tool (e.g., whatismyip.com) to identify your current public IP.

**Figure 12: IP Lookup Tool Example**  
<img width="1467" height="563" alt="image" src="https://github.com/user-attachments/assets/6c275c50-32b9-4e64-bea4-f2eb03510ebb" />

#### 5. SSH into the Ubuntu Server

From your local machine:

```bash
ssh root@<SERVER_PUBLIC_IP>
```

**Figure 13: SSH Connection Terminal Output**  
<img width="1107" height="216" alt="Screenshot 2025-07-11 005850" src="https://github.com/user-attachments/assets/128d5092-16a3-4f06-a424-f6559f604d37" />

**Figure 14: SSH Connection Established**  
<img width="1108" height="769" alt="Screenshot 2025-07-11 005956" src="https://github.com/user-attachments/assets/d38d2638-62bb-44b7-ae6f-29d08a443405" />

#### 6. Update and Install Required Packages

Run the following commands after login:

```bash
apt update && apt upgrade -y
```

**Figure 15: System Update Command**  
<img width="1111" height="124" alt="Screenshot 2025-07-11 010048" src="https://github.com/user-attachments/assets/32d55335-998c-4a6e-9d3a-2242a9936c83" />

**Figure 16: System Update Output**  
<img width="1117" height="475" alt="Screenshot 2025-07-11 010122" src="https://github.com/user-attachments/assets/20372622-ad74-49ce-8723-c47e36fe3c4b" />

Install unzip:

```bash
sudo apt install unzip -y
```

**Figure 17: Unzip Installation Command**  
<img width="1108" height="126" alt="Screenshot 2025-07-11 010304" src="https://github.com/user-attachments/assets/cee61116-d4b2-4c9f-aea0-fd283fc13a7d" />

**Figure 18: Unzip Installation Output**  
<img width="1112" height="400" alt="Screenshot 2025-07-11 010318" src="https://github.com/user-attachments/assets/ddd59499-49fa-4662-ab45-c51303ad86fe" />

## Phase 4: Email Infrastructure Setup (Poste.io)

> **Note:**  
> This mail server setup is designed to send emails to a disposable email environment for **testing and learning purposes only**. It does **not** include the setup of MX records, real domains, TLS, SPF, DKIM, or DMARC. As a result, it **will not deliver to trusted email providers** (e.g., Gmail, Outlook). Do **not** use this setup for malicious purposes.

---

### Step 4.1: Poste.io Installation

#### 1. Install Docker Engine

Download the Docker installation script:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```

**Figure 19: Download Docker Script Command** <br>
<img width="1111" height="159" alt="Screenshot 2025-07-11 114804" src="https://github.com/user-attachments/assets/3d7a8071-d191-4022-83aa-ffe3574ae79a" />

**Figure 20: Script File in Directory** <br>
<img width="1121" height="160" alt="Screenshot 2025-07-11 114856" src="https://github.com/user-attachments/assets/bcb2ef6d-5c59-4be3-8629-1d934f18e09e" />

*Figure 21: Script File Content Preview* <br>
<img width="1112" height="623" alt="Screenshot 2025-07-11 114923" src="https://github.com/user-attachments/assets/ecca322e-da7e-4528-8f60-0c1145dc8d21" />


Run the script:

```bash
sudo sh get-docker.sh
```

**Figure 22: Run Installation Script** <br>
<img width="1113" height="133" alt="Screenshot 2025-07-11 115056" src="https://github.com/user-attachments/assets/6d46e30c-5970-4119-8e99-f3e69b69210a" />


Verify Docker Engine is working correctly:

```bash
sudo docker run hello-world
```

This command should output a "Hello from Docker" message and exit.  

---

#### 2. Download and Run the Poste.io Docker Container

Before executing the command, here's a breakdown of each flag used:

- `--net=host`: Uses host networking (simplifies access).
- `-e TZ=Europe/Prague`: Set your timezone.
- `-v /your-data-dir/data:/data`: Mounts your data directory (user accounts, logs, emails).
- `--name "mailserver"`: Names the Docker container.
- `-h "mail.example.com"`: Sets your mailserver hostname (replace accordingly).
- `-t analogic/poste.io`: Specifies the Poste.io image (free version).

> **Note:** Replace `mail.example.com` with your own project-related hostname.

**Final Command:**

```bash
docker run \
    --net=host \
    -e TZ=Europe/Prague \
    -v /your-data-dir/data:/data \
    --name "mailserver" \
    -h "campaign.com.au" \
    -t analogic/poste.io
```

**Figure 23: Poste.io Container Running** <br>
<img width="1107" height="253" alt="Screenshot 2025-07-11 115240" src="https://github.com/user-attachments/assets/ad39b5f1-55ef-4a62-abf3-8d338d5fda7b" />

**Figure 24: Poste.io Ready Message** <br>
<img width="1094" height="482" alt="Screenshot 2025-07-11 125631" src="https://github.com/user-attachments/assets/593dbe5a-1e74-40b7-abf1-04912369279b" />

For more advanced configuration, refer to the official guide:  
[https://poste.io/doc/getting-started](https://poste.io/doc/getting-started)

Also, note that Poste.io opens the following ports:

**Figure 25: Poste.io Ports** <br>
<img width="807" height="438" alt="Screenshot 2025-07-11 130300" src="https://github.com/user-attachments/assets/766e6db2-53de-4dd1-a3f6-d872f92e9e75" />

#### 3. Test Poste.io

On the top righ corner click on the mail icon.
**Figure 26: Accesing Web Mail** <br>
<img width="247" height="47" alt="Screenshot 2025-07-11 130353" src="https://github.com/user-attachments/assets/d355ce41-db71-4cad-b5d9-7c97c9d1808e" />

Compose and email.<br>
**Figure 27: Web Mail Interface** <br>
<img width="1474" height="651" alt="Screenshot 2025-07-11 130707" src="https://github.com/user-attachments/assets/19665fe0-1576-481b-9773-2c9e472f65cc" />

Open on a browser tab MailTemp and get a disposable email address.,br>
**Figure 28: TempMail Website** <br>
<img width="1572" height="921" alt="Screenshot 2025-07-11 130809" src="https://github.com/user-attachments/assets/a8e4ec95-339d-4e33-9c4c-de6ed5327571" />

Send an email to the disposable address. <br>
**Figure 29: Sending email** <br>
<img width="1191" height="635" alt="Screenshot 2025-07-11 130754" src="https://github.com/user-attachments/assets/dba79eaf-45a2-40a0-b293-c1375d014f25" />

Check the inbox of the disposable email. <br>
**Figure 30: Inbox** <br>
<img width="1572" height="925" alt="Screenshot 2025-07-11 130822" src="https://github.com/user-attachments/assets/102223c1-d709-4fc7-a1f2-c0e363e75fde" />

Now we can confirm that our mail server is working correctly and delivering emails with our fake domain (spoof). <br>
**Figure 31: Email with fake spoof domain** <br>
<img width="829" height="385" alt="Screenshot 2025-07-11 130926" src="https://github.com/user-attachments/assets/aa680ff7-5e71-4e25-955d-b8fe022578f7" />

---

#### 3. Verify Installation and Access the Web Interface

- Open your browser and navigate to:  
  `https://<SERVER_PUBLIC_IP>`

- If the default login page doesn't load, access the install path directly:  
  `https://<SERVER_PUBLIC_IP>/admin/install/server`

---

### Step 4.2: Poste.io Configuration

#### 1. Complete Initial Setup Wizard via Web Interface

Fill in the following configuration fields:

- **Mailserver hostname:** `campaign.com.au`
- **Administrator email:** `admin@campaign.com.au`
- **Password:** A strong password for mailserver access

**Figure 32: Poste.io First-Time Setup Form** <br>
<img width="1593" height="774" alt="image" src="https://github.com/user-attachments/assets/5a2084c2-df66-42c0-9123-ed339325b6e0" />

---

## Phase 5: Gophish Installation and Configuration

---

### Step 5.1: Gophish Installation

#### 1. Download Gophish

- Go to [https://getgophish.com](https://getgophish.com) and download version 0.12.1  
  **Figure 33: Gophish Website** 
  <img width="1671" height="326" alt="Screenshot 2025-07-11 010507" src="https://github.com/user-attachments/assets/05fca0e6-9f10-492b-b2cb-9932f74e3c8c" />

- Copy the download link:  
  `https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip`  
  *Figure 34: Gophish Package Link*  
  <img width="934" height="297" alt="Screenshot 2025-07-11 010704" src="https://github.com/user-attachments/assets/29584779-e0de-457c-8687-2539a2f5f5cd" />

- Download the package using `wget`:  
  ```bash
  wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
  ```
  **Figure 35: Gophish Download Command**
  <img width="1117" height="122" alt="Screenshot 2025-07-11 010948" src="https://github.com/user-attachments/assets/2f492aa2-1b3a-4553-ae1b-0a49d9a10f62" />  
  **Figure 36: Gophish Downloaded**  
  <img width="1107" height="560" alt="Screenshot 2025-07-11 011004" src="https://github.com/user-attachments/assets/1b997808-47ae-47cb-a8e9-efcf44458af3" />  
  **Figure 37: Gophish File Check**  
  <img width="1107" height="124" alt="Screenshot 2025-07-11 011035" src="https://github.com/user-attachments/assets/c4013ffe-21e3-4ac8-918e-2930257dcd7e" />

#### 2. Create Gophish Folder and Unzip

- Create a directory:
  ```bash
  sudo mkdir /opt/gophish
  ```
  **Figure 38: Create Folder**  
  <img width="1090" height="133" alt="Screenshot 2025-07-11 011114" src="https://github.com/user-attachments/assets/bcdcb5dc-280a-45ea-a34a-195e97e04985" />

- Unzip the downloaded file:
  ```bash
  unzip gophish-v0.12.1-linux-64bit.zip -d /opt/gophish
  ```
  **Figure 39: Unzip Command**  
  <img width="1108" height="83" alt="Screenshot 2025-07-11 011205" src="https://github.com/user-attachments/assets/8a8dc6c1-ab66-4f11-97b2-614e5db4a868" />  
  **Figure 40: Folder Content**  
  <img width="1113" height="141" alt="Screenshot 2025-07-11 011244" src="https://github.com/user-attachments/assets/73d3347d-2b7a-453f-a3a6-13f0e6ac8243" />

#### 3. Change Permissions and Configure Gophish

- Make the binary executable:
  ```bash
  cd /opt/gophish
  sudo chmod +x gophish
  ```
  **Figure 41: Navigate to Folder**  
  <img width="1109" height="100" alt="Screenshot 2025-07-11 011335" src="https://github.com/user-attachments/assets/3029baac-b377-4d5e-959c-dfce65a1069e" />  
  *Figure 42: Modify Permissions*  
  <img width="1110" height="121" alt="Screenshot 2025-07-11 011415" src="https://github.com/user-attachments/assets/081e35a3-db64-44df-8a48-923435b7f602" />

- Edit the `config.json` file:
  ```bash
  sudo nano config.json
  ```
  **Figure 43: Modify File**  
  <img width="1118" height="109" alt="Screenshot 2025-07-11 011449" src="https://github.com/user-attachments/assets/7ae41b98-28a0-4473-894e-9a7ea43eeee5" />

- Change the line:
  `"listen_url": "127.0.0.0:3333"`  
  to  
  `"listen_url": "0.0.0.0:3333"`  
  **Figure 44: Modified File**  
  <img width="1109" height="606" alt="Screenshot 2025-07-11 011546" src="https://github.com/user-attachments/assets/a1085982-3bbf-4862-a640-7ea053148fc2" />

#### 4. Run Gophish Framework

Start the Gophish service:
```bash
sudo ./gophish
```

**Figure 45: Run Gophish**  
<img width="1122" height="126" alt="Screenshot 2025-07-11 011629" src="https://github.com/user-attachments/assets/a29c36bd-224b-4eef-babd-c6fc0ad34c7d" />  
**Figure 46: Gophish Running**  
<img width="1115" height="776" alt="Screenshot 2025-07-11 011644" src="https://github.com/user-attachments/assets/62547ab2-c15d-4e84-827c-c37f0f37e0ef" />

#### 5. Gophish Initial Credentials

- The initial credentials are displayed in the terminal on the first run. You'll be prompted to set a new password.

**Figure 47: Gophish Initial Credentials**  
<img width="1115" height="776" alt="Screenshot 2025-07-11 011739" src="https://github.com/user-attachments/assets/6eeb3c77-c957-46ce-bddb-900152e0d70e" />

---

### Step 5.2: Gophish Configuration

#### 1. Access the Web Interface

- Open a browser and visit:  
  `https://<SERVER_PUBLIC_IP>:3333`

**Figure 48: Access Gophish Web Interface**  
<img width="1512" height="711" alt="Screenshot 2025-07-11 012038" src="https://github.com/user-attachments/assets/cfcc9f3f-d29e-43cc-bf45-aacc9a9ae034" />

#### 2. Change Default Credentials

- Log in using the temporary credentials shown earlier.
- You will be prompted to change the default password.

**Figure 49: Initial Credentials Login**  
<img width="529" height="278" alt="Screenshot 2025-07-11 012148" src="https://github.com/user-attachments/assets/d7e53527-3526-4d2e-bb77-eb6a48b9acd4" />  
**Figure 50: Change Default Password**  
<img width="634" height="460" alt="Screenshot 2025-07-11 012214" src="https://github.com/user-attachments/assets/12c205ff-8280-4657-8bb6-165515015637" />  
**Figure 51: Gophish Dashboard**  
<img width="1493" height="741" alt="Screenshot 2025-07-11 012241" src="https://github.com/user-attachments/assets/c6125d9b-a574-4441-a5cd-e69096eb345b" />

-----------------------------------------------------------


## Phase 6: Client VMs Deployment

---

### Step 6.1: Lightweight Linux VM 

For this project, we will deploy four lightweight Linux VM flavours, which will serve the purpose of simulating four clients, accessing disposable emails on the TempMail website. Will will be using Lubuntu, which is a lightweight Linux distribution. I have created a template on my Proxmox Home Lab and cloned it to get four separate VMs. I am not showing this process because I'm hoping you know. If you don't use Proxmpx, you can use any other Hypervisor, such as VirtualBox or VMware.

**Figure 52: Lubuntu Client VMs**  
<img width="1378" height="732" alt="image" src="https://github.com/user-attachments/assets/6d69e9a8-3c80-4690-80f7-8d48939e3ab3" />



Phase 7: Campaign Development and Testing

Now, it is time to develop a campaign, and we need to source a good email template and an appropriate landing page for the test. For this project, I will use the Last.fm website. I have an email template from this website that will fit perfectly for this project. We will need to create a Virtual domain for the campaign on Poste.io.

**Figure 53: Email Template** <br>
<img width="1314" height="1113" alt="image" src="https://github.com/user-attachments/assets/ac57e9c3-684a-434f-9c77-e36cb47c8655" />

### Step 7.1: Virtual Domain Creation on Poste.io

On the Poste.io admin site, go to Virtual domains and click on Create a new virtual domain. <br>
**Figure 54: Virtual domains** <br>
<img width="1666" height="536" alt="image" src="https://github.com/user-attachments/assets/685ebc33-e336-4330-bfcb-499d4eb6e8f6" />

Create the domain using the domain address from the email template, in my case `mailer.last.fm`, and submit it. <br>
**Figure 55: New Virtual domain** 
<img width="912" height="352" alt="image" src="https://github.com/user-attachments/assets/c59a303f-fa65-4065-87ae-60feeb72b5ca" />

Now, let's create a new email address for this domain, using the email address from the template. <br>
**Figure 56: New email address** 
<img width="1342" height="868" alt="image" src="https://github.com/user-attachments/assets/98085605-7243-4783-bed1-892df86c28c6" />

Fill in the info for the new email account and submit. <br>
**Figure 57: New email filled out** 
<img width="1146" height="689" alt="image" src="https://github.com/user-attachments/assets/bc0bd9b3-71ea-43f2-85b0-4f74c85346af" />

**Figure 58: New email created** 
<img width="1426" height="1033" alt="image" src="https://github.com/user-attachments/assets/ead884cd-f2da-492e-81ce-c9e92ea7e974" />

### Step 7.2: Test Email Delivery from new Virtual Domain

First, log in to the Webmail. <br>

**Figure 59: Webmail portal** <br>
<img width="485" height="36" alt="image" src="https://github.com/user-attachments/assets/4907565e-0458-43a1-8647-7b68b7e5ab4d" />

Use the new email created for the target domain campaign. <br>
**Figure 60: Webmail Credentials** <br> 
<img width="819" height="512" alt="image" src="https://github.com/user-attachments/assets/0a614025-98fb-4125-ad72-42c493f1cb89" />

Compose an email and send to a disposable email address on TempEmail.

**Figure 60: Temp email** <br>
<img width="1310" height="297" alt="image" src="https://github.com/user-attachments/assets/81d0a20c-36af-4c41-947c-d667f6b21d8f" /><br>

**Figure 61: Composed email** <br>
<img width="1208" height="655" alt="image" src="https://github.com/user-attachments/assets/bb260bef-f1c1-43b7-aea7-2b4b400422fc" /><br>

Check if the email was received.
**Figure 62: Inbox** <br>
<img width="1299" height="530" alt="image" src="https://github.com/user-attachments/assets/1316955d-09c9-47f4-8b24-a5c4ac500e6a" /> <br>
**Figure 63: Email body** <br>
<img width="746" height="472" alt="image" src="https://github.com/user-attachments/assets/19f38acb-fd77-440d-a898-4e12ee1d8a4f" /> <br>

Now, we are sure that our email server is delivering emails with the Virtual Domain created by it, and we are ready for the next step.

### Step 7.2: Gophish Campaign Setup

1. Email Template Creation

Navigate to Email Templates and click on New Template
**Figure 64: Email Templates**
<img width="1680" height="468" alt="image" src="https://github.com/user-attachments/assets/2b5e54c9-8ea9-45da-ad7e-1ab1f742432e" />

Fill in the info, and as I have a sample email for my template, I will use it, and click on Import Email.
**Figure 65: Template Email info**
<img width="701" height="494" alt="image" src="https://github.com/user-attachments/assets/0bf2896a-51ba-4acc-bdef-46740b29e3f3" />

I'm trying to access the email sample, but since I'm in Gmail, I need the source code. On Gmail, you can access it by clicking on the three dots on the right-hand side corner, then clicking on Show Original.
**Figure 66: Template Email**
<img width="1301" height="909" alt="image" src="https://github.com/user-attachments/assets/99308790-692b-403d-b946-2cbddd055831" />

Click on  Copy to Clipboard
**Figure 67: Copy original Email**
<img width="1586" height="589" alt="image" src="https://github.com/user-attachments/assets/a7e4ba57-f421-44f4-ae6f-a5df8f159a40" />

Now paste the Original mail into the Import Email window on Gophish, and check Change Links to Point to Landing Page and then click on import.
**Figure 68: Import Email**
<img width="711" height="499" alt="image" src="https://github.com/user-attachments/assets/59ae8291-1a15-4186-a754-7afd6fbdb28e" />

Now that you have all fill in you cna save the template
**Figure 69: Saving Email Template**
<img width="694" height="1248" alt="image" src="https://github.com/user-attachments/assets/586096fc-7198-4f1b-b548-59c5b6bccb5a" />

**Figure 69: Saved Email Template**
<img width="1413" height="396" alt="image" src="https://github.com/user-attachments/assets/e11e168b-098b-48a8-b079-ccb13155c7eb" />

2. User Group Configuration

For this, we need to run our 4 Lubuntu VMs clients, open the browser and navigate to TempEmail and get an email account for each VM.

*Figure 70: Proxmox VMs running*
<img width="1111" height="563" alt="Screenshot 2025-07-11 140534" src="https://github.com/user-attachments/assets/1fb12a3d-482e-4045-a20c-370e7332c78a" />

*Figure 71: VM1 Disposable Email*
<img width="1275" height="548" alt="Screenshot 2025-07-11 140810" src="https://github.com/user-attachments/assets/d5e08802-4a3a-4ef6-a28c-c19ef0038166" />

*Figure 72: VM2 Disposable Email*
<img width="1265" height="481" alt="Screenshot 2025-07-11 140907" src="https://github.com/user-attachments/assets/932fb45c-a295-41d7-a736-7cc38c1c4355" />

*Figure 73: VM3 Disposable Email*
<img width="1270" height="487" alt="Screenshot 2025-07-11 140955" src="https://github.com/user-attachments/assets/4d1d314b-b3b5-44e0-b52f-783396dcd99e" />

*Figure 74: VM4 Disposable Email*
<img width="1200" height="464" alt="Screenshot 2025-07-11 141133" src="https://github.com/user-attachments/assets/ec950ae0-9d3c-400c-8aff-3b60ae86021d" />

Navigate to Users & Groups and click on New Group
*Figure 75: Users & Groups*
<img width="1676" height="396" alt="Screenshot 2025-07-11 140441" src="https://github.com/user-attachments/assets/e8cfe1f8-331b-48d3-95db-d1595c809121" />

On New Group, click on download the CSV template, it will be easier to do it this way.
*Figure 76: Use CSV*
<img width="694" height="241" alt="Screenshot 2025-07-11 141253" src="https://github.com/user-attachments/assets/71fcd397-31ee-4e00-b2cb-245edfe823a6" />

Fill in the disposable emails from VM1 to VM4 along with their first name, last name and position and save the CSV.
*Figure 77: CSV Filled In*
<img width="994" height="394" alt="Screenshot 2025-07-11 141310" src="https://github.com/user-attachments/assets/1eadf130-e1fd-4539-beb4-0a7e73d2e5e1" />

Click on Bulk Import Users and select the CSV you filled in.
*Figure 78: Bulk Import*
<img width="693" height="677" alt="Screenshot 2025-07-11 141343" src="https://github.com/user-attachments/assets/ba99e002-62d9-47eb-a8f5-c6fde437d455" />

3. Landing Page Development

As we are using the Last.fm email template, we need to source a page from the original website where we can collect credentials.

*Figure 79: Last.fm Login Page*
<img width="1712" height="678" alt="image" src="https://github.com/user-attachments/assets/2e94f5e5-6b51-4116-a96c-8217597ab031" />

Navigate to Landing Pages and click on New Page.
*Figure 80: Landing pages*
<img width="1692" height="536" alt="image" src="https://github.com/user-attachments/assets/87f90c20-9949-4e1a-abc9-c0b73bfc77c8" />

Give a name and click on Import Site.
*Figure 81: Landing Fill in*
<img width="700" height="260" alt="image" src="https://github.com/user-attachments/assets/be85738f-9a90-4488-864b-1045d8ac6ee2" />

Import Last.fm login page.
*Figure 82: Importin Last.fm*
<img width="693" height="271" alt="Screenshot 2025-07-11 135312" src="https://github.com/user-attachments/assets/f540f4de-c2f4-418c-b4ac-d1db23a97d75" />

Check Capture Submited Data, Capture Passwords and on Redirect to put the original Last.From the login page, click on Save Page.
*Figure 83: Landing Page Filled In*
<img width="700" height="983" alt="Screenshot 2025-07-11 135530" src="https://github.com/user-attachments/assets/e24fd7ac-61cd-4d7e-9e67-1060894f04b9" />

*Figure 84: Landing Page Saved*
<img width="1441" height="427" alt="Screenshot 2025-07-11 135641" src="https://github.com/user-attachments/assets/1aebe9f3-e0cb-4d64-9c17-ef2fb089f2f5" />

4. Sending Profiles Configuration

Now we need to configure Gophish to use Poste.io to send the emails for our campaign. Go to Sending Profiles and then click on New Profile.
*Figure 85: Create a New Sending Profile*
<img width="1705" height="630" alt="image" src="https://github.com/user-attachments/assets/c5ba4eea-7063-4321-8d24-5c58d15b294f" />

Fill in the details, remember we will use the Virtual domain we created on Poste.io for our campaign, and for Host we need to use the public IP of the server and the port 465. When that is done before saving the profile, click on Send Test email to see if Gophish is able to use our SMTP server, then click on Save Profile.
*Figure 86: Sending Profile Filled in*
<img width="707" height="1057" alt="image" src="https://github.com/user-attachments/assets/7b10072a-3a7b-4c3a-9b12-61cfb2329d59" />

*Figure 87: Sending Profile Saved*
<img width="1406" height="441" alt="image" src="https://github.com/user-attachments/assets/17c33129-029d-4d33-9bd5-94cab374eed6" />

5. Campaign Creation

Now that we have all the other parts set up it is time to create the campaign, navigate to Campaigns and then click on New Campaign.
*Figure 88: Create a new campaign*
<img width="1275" height="495" alt="Screenshot 2025-07-11 141418" src="https://github.com/user-attachments/assets/cab1ed59-230d-42fd-99d7-3c4a3db98fff" />

Fill in the details. For the URL which is the Gophish listener, use the Server Public IP and port 8081. By default, it's port 80, but we've changed it to port 8081 for Poste.io's UI, now and click on Launch Campaign
*Figure 89: Campaign Launch*
<img width="701" height="771" alt="image" src="https://github.com/user-attachments/assets/3bdfff1b-6a70-4365-b769-d097a9f83407" />

6. Real-time Monitoring

We will simulate the clients by opening the emails received and clicking on the links.

After the campaign launch, we start monitoring for events. 
*Figure 89: Campaign Monitoring*
<img width="1688" height="1057" alt="Screenshot 2025-07-11 141741" src="https://github.com/user-attachments/assets/019e7424-548c-4aed-a3aa-5ac091fa7681" />

We have sent four emails, one of which is open, and a link was clicked.
*Figure 90: Campaign Responses*
<img width="1420" height="662" alt="image" src="https://github.com/user-attachments/assets/d75f8e77-1a38-4eac-b8e2-2c04edc5406a" />

Let's check who clicked on the link.
*Figure 91: First Response*
<img width="1370" height="339" alt="image" src="https://github.com/user-attachments/assets/14d1feaa-34df-450e-a478-d119e474b7e2" />

Let's simulate that the client enters the credentials.
*Figure 92: User Credentials*
<img width="1148" height="581" alt="image" src="https://github.com/user-attachments/assets/4a903b00-6800-47c6-94cd-2e0151daf4fd" />

On Gophish, we can see that the credentials were recorded.
*Figure 93: Credentials Recorded*
<img width="1414" height="655" alt="Screenshot 2025-07-11 150854" src="https://github.com/user-attachments/assets/d4763dba-3ad4-4dac-ba9d-f1fdb2782eac" />

Let's check the credentials, as you can see Gophish successfully recorded the client credentials, proving that a successful phishing attack.
*Figure 94: Credentials*
<img width="1395" height="834" alt="Screenshot 2025-07-11 150922" src="https://github.com/user-attachments/assets/f8eff93d-961a-43e2-96f6-4bde2a3500e7" />

Now let's do the same for the rest of the clients.
*Figure 95: All clients' data submitted*
<img width="1416" height="728" alt="Screenshot 2025-07-11 152258" src="https://github.com/user-attachments/assets/a548f59f-3d18-4eda-8e15-09135f8d3e92" />

*Figure 96: Credentials Recorded*
<img width="1350" height="791" alt="Screenshot 2025-07-11 152319" src="https://github.com/user-attachments/assets/6409502a-c2de-403e-b3b1-bd74e0a485cc" />
*Figure 97: Credentials Recorded*
<img width="1342" height="776" alt="Screenshot 2025-07-11 152336" src="https://github.com/user-attachments/assets/ffbf9e29-c482-4861-829d-359f9f1c1695" />
*Figure 98: Credentials Recorded*
<img width="1295" height="802" alt="Screenshot 2025-07-11 152400" src="https://github.com/user-attachments/assets/9bfe7a52-bb56-458f-b465-4c3bcf257d0b" />

After success, we can complete the campaign.
*Figure 99: Campaign Completion*
<img width="1417" height="788" alt="Screenshot 2025-07-11 152534" src="https://github.com/user-attachments/assets/0299cce3-515e-48e1-800b-8c480252f8d2" />

---

## Project Conclusion

This project successfully demonstrates the end-to-end process of setting up and executing a phishing simulation lab. By integrating Gophish, Poste.io, and virtual clients in a safe environment, it replicates the core phases of real-world phishing campaigns — from email crafting to credential harvesting and post-campaign analysis. This hands-on experience highlights how threat actors operate and how blue teams can detect and mitigate such attacks.

---

## Disclaimer

> This guide is intended **strictly for educational and ethical testing purposes** within **controlled environments**.  
> Unauthorised deployment of phishing simulations or email spoofing in real environments or against unsuspecting individuals is illegal and unethical. Please always get the proper authorisation before conducting simulations.

---

## Troubleshooting Guide

### Poste.io Doesn't Send to Gmail/Outlook
- These providers block messages from servers without proper DNS (PTR, SPF, DKIM) records.
- This setup lacks domain verification and is intended only for **internal/disposable email testing**.

### Gophish Interface Doesn’t Load
- Ensure port `3333` is open in your firewall rules and accessible.
- Verify `config.json` contains `"listen_url": "0.0.0.0:3333"`

### Docker Mail Server Container Fails to Start
- Check for conflicting ports (e.g., another service using 25, 443, or 80)
- Re-run with `--rm` flag for cleanup: `docker rm -f mailserver`

### Campaign Emails Not Delivered
- Ensure Poste.io is running and the sending profile in Gophish uses correct SMTP and port `465`.
- Use TempMail or any disposable service to confirm delivery.

### Landing Page Doesn’t Render Correctly
- Ensure imported source HTML is clean and all required assets (CSS, JS) are reachable.
- Use “Import Site” only for basic HTML — modern JavaScript-heavy sites may fail to import.
