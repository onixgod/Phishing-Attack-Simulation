# Phishing Attack Simulation Lab with Gophish & Poste.io

## Overview

This comprehensive lab guide demonstrates how to simulate a **real-world phishing attack** in a safe and isolated environment. The objective is to understand phishing tactics, learn how malicious actors operate, and develop skills for detecting and preventing such attacks using **Gophish** and **Poste.io**.

## Learning Goals

- Design and execute realistic phishing campaigns
- Explore phishing infrastructure capabilities (Gophish + Mail server)
- Simulate user interactions with phishing emails and landing pages
- Improve incident response and detection skills
- Analyse campaign results and extract key insights from captured credentials and user interactions

## Skills Gained

### Technical Skills
- **Linux System Administration**: Ubuntu server setup and hardening
- **Virtualisation Management**: Proxmox VE setup and VM provisioning
- **Cloud Infrastructure**: Configuration and deployment using Kamatera
- **Containerization**: Docker setup and container management
- **Email Server Administration**: Installing and configuring Poste.io with SMTP
- **Network Security**: Firewall configuration and secure port management

### Cybersecurity Skills
- **Phishing Campaign Design**: Crafting convincing emails and attack scenarios
- **Security Awareness Testing**: Designing tests and defining evaluation metrics
- **Threat Simulation**: Recreating real-world phishing attacks for training purposes
- **Red Team Operations**: Understanding attack methodologies and execution

## Tools and Technologies

### Primary Tools
- **Gophish** – Open-source phishing simulation framework
- **Poste.io** – All-in-one email server with web-based interface
- **Proxmox VE** – Virtualization platform for lab environment
- **Kamatera** – Cloud provider for hosting simulation infrastructure

### Supporting Tools
- **Ubuntu Server 24.04 LTS** – Base operating system for mail and phishing servers
- **UFW (Uncomplicated Firewall)** – Host-based firewall management
- **Docker** – Container platform for Poste.io deployment
- **SQLite** – Lightweight database for Gophish campaign data

### Target Environment
- **Lubuntu Desktop** – Lightweight Linux desktop for testing client interactions
- **TempMail** – A Disposable email service for receiving phishing emails safely

## Phase 1: Infrastructure Planning and Preparation

### 1.1 Network Architecture Design

Before implementation, you'll need to create a comprehensive diagram to visualise the project architecture and understand data flow between components.

**Architecture Components:**
- **Virtual Machines**: Lubuntu clients hosted in Proxmox home lab
- **Cloud Services**: Kamatera-hosted Ubuntu server running Gophish and Poste.io
- **Network Infrastructure**: Routing, firewall rules, and port forwarding

**Figure 1: Lab Architecture Overview**  
<img width="1442" height="861" alt="Phishing Attack Simulation Architecture" src="https://github.com/user-attachments/assets/eea1dd4a-06ea-47aa-88d1-51c87f054894" />

## Phase 2: Phishing Campaign Workflow

The following diagram outlines the end-to-end workflow for executing a phishing campaign using Gophish and Poste.io, including configuration steps and execution lifecycle.

**Figure 2: Campaign Workflow**  
<img width="671" height="562" alt="Phishing Simulation Workflow" src="https://github.com/user-attachments/assets/b8554c28-d7df-413f-8b34-c92d6ec8a893" />

### Workflow Summary

1. **Initiation**: Manager launches the phishing simulation via the Gophish dashboard (port 3333)
2. **Configuration**: Email templates, landing pages (port 8081), and recipient lists are created; sending profile configured using Poste.io as SMTP server (port 465)
3. **Execution**: Campaign launches, Gophish sends phishing emails through Poste.io to TempMail inboxes
4. **User Interaction**: Targets receive emails and interact with landing pages; Gophish records clicks and form submissions
5. **Analysis**: Campaign results monitored in the Gophish dashboard to evaluate engagement and identify improvement areas

## Phase 3: Cloud Infrastructure Setup

### 3.1 Kamatera Cloud VM Deployment

Kamatera offers a generous $100 free trial credit, making it ideal for this project.

#### 3.1.1 Create Kamatera Account
- Sign up at [Kamatera.com](https://www.kamatera.com/)
- The free trial provides sufficient credit for complete deployment

#### 3.1.2 Deploy Ubuntu Server 24.04 LTS

1. Navigate to **My Cloud** and click **Create New Server**
2. Configure the following settings:
   - **Zone**: Select the closest to your region
   - **Image**: Ubuntu 24.04 LTS
   - **Server Type**: General Purpose

**Figure 3: Kamatera Server Deployment**  
<img width="1712" height="1177" alt="Kamatera Server Configuration" src="https://github.com/user-attachments/assets/268fde08-75a1-49a1-9736-7004a47ae33a" />

3. Set recommended specifications:
   - **CPU**: 2 vCPUs
   - **RAM**: 4 GB
   - **Storage**: 50 GB SSD
   - **Networking**: Public and private networking enabled

**Figure 4: Server Configuration Options**  
<img width="1265" height="933" alt="Server Specs Configuration" src="https://github.com/user-attachments/assets/23e5b241-269e-4848-8cb6-d5ab0ca2e392" />

4. Set server credentials:
   - Create a strong root password
   - Name the instance: `MyLab-PhishLab`
   - Estimated cost: ~$20/month

**Figure 5: Server Credentials Configuration**  
<img width="1335" height="826" alt="Server Name and Password" src="https://github.com/user-attachments/assets/ba355d0a-6b97-4872-9618-0c1cbb897a9d" />

#### 3.1.3 Verify Server Status

1. Navigate to **Server List** and locate your new instance

**Figure 6: Server Status Dashboard**  
<img width="1681" height="508" alt="Server Status" src="https://github.com/user-attachments/assets/4c5e5e85-ee58-4911-9707-b83573247cb5" />

**Figure 7: Server Details**  
<img width="1408" height="686" alt="Server Information" src="https://github.com/user-attachments/assets/a4b612c7-95d0-4658-a36c-31a831fc90df" />

2. Test connectivity from your local terminal:
```bash
ping <SERVER_PUBLIC_IP>
```

**Figure 8: Connectivity Test**  
<img width="1109" height="345" alt="Ping Test Results" src="https://github.com/user-attachments/assets/431390e7-5cd7-462e-956d-f4935da3c001" />

#### 3.1.4 Configure Kamatera Firewall

1. Navigate to **Firewall** under server settings
2. Enable the firewall and add custom rules:
   - Allow TCP/UDP traffic from your local IP address
   - Use an IP lookup tool (e.g., whatismyip.com) to identify your public IP

**Figure 9: Firewall Configuration**  
<img width="1440" height="988" alt="Firewall Rules" src="https://github.com/user-attachments/assets/25b7da53-74e9-48d1-b70e-51e1350c8a60" />

**Figure 10: UDP Rule Configuration**  
<img width="604" height="680" alt="UDP Rules" src="https://github.com/user-attachments/assets/03f02881-70a4-46ce-a973-a7f601814d4d" />

**Figure 11: TCP Rule Configuration**  
<img width="599" height="678" alt="TCP Rules" src="https://github.com/user-attachments/assets/b4d1ffd9-c6ec-45bf-b01d-29ff5f230926" />

**Figure 12: IP Address Lookup**  
<img width="1467" height="563" alt="IP Lookup Tool" src="https://github.com/user-attachments/assets/6c275c50-32b9-4e64-bea4-f2eb03510ebb" />

#### 3.1.5 Establish SSH Connection

Connect to your Ubuntu server from your local machine:
```bash
ssh root@<SERVER_PUBLIC_IP>
```

**Figure 13: SSH Connection**  
<img width="1107" height="216" alt="SSH Command" src="https://github.com/user-attachments/assets/128d5092-16a3-4f06-a424-f6559f604d37" />

**Figure 14: SSH Session Established**  
<img width="1108" height="769" alt="SSH Connected" src="https://github.com/user-attachments/assets/d38d2638-62bb-44b7-ae6f-29d08a443405" />

#### 3.1.6 System Updates and Package Installation

1. Update the system:
```bash
apt update && apt upgrade -y
```

**Figure 15: System Update Command**  
<img width="1111" height="124" alt="Update Command" src="https://github.com/user-attachments/assets/32d55335-998c-4a6e-9d3a-2242a9936c83" />

**Figure 16: Update Process**  
<img width="1117" height="475" alt="Update Output" src="https://github.com/user-attachments/assets/20372622-ad74-49ce-8723-c47e36fe3c4b" />

2. Install required packages:
```bash
sudo apt install unzip -y
```

**Figure 17: Installing Unzip**  
<img width="1108" height="126" alt="Unzip Installation" src="https://github.com/user-attachments/assets/cee61116-d4b2-4c9f-aea0-fd283fc13a7d" />

**Figure 18: Installation Complete**  
<img width="1112" height="400" alt="Installation Output" src="https://github.com/user-attachments/assets/ddd59499-49fa-4662-ab45-c51303ad86fe" />

## Phase 4: Email Infrastructure Setup (Poste.io)

> **Important Note:**  
> This mail server setup is designed for **testing and learning purposes only** in a disposable email environment. It does **not** include MX records, real domains, TLS certificates, SPF, DKIM, or DMARC configuration. Consequently, it **will not deliver to trusted email providers** (Gmail, Outlook, etc.). **Do not use this setup for malicious purposes.**

### 4.1 Poste.io Installation

#### 4.1.1 Install Docker Engine

1. Download the Docker installation script:
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```

**Figure 19: Download Docker Script**  
<img width="1111" height="159" alt="Docker Download" src="https://github.com/user-attachments/assets/3d7a8071-d191-4022-83aa-ffe3574ae79a" />

**Figure 20: Script File Created**  
<img width="1121" height="160" alt="Script File" src="https://github.com/user-attachments/assets/bcb2ef6d-5c59-4be3-8629-1d934f18e09e" />

**Figure 21: Script Content Preview**  
<img width="1112" height="623" alt="Script Content" src="https://github.com/user-attachments/assets/ecca322e-da7e-4528-8f60-0c1145dc8d21" />

2. Execute the installation script:
```bash
sudo sh get-docker.sh
```

**Figure 22: Docker Installation**  
<img width="1113" height="133" alt="Docker Install" src="https://github.com/user-attachments/assets/6d46e30c-5970-4119-8e99-f3e69b69210a" />

3. Verify Docker installation:
```bash
sudo docker run hello-world
```
This command should display a "Hello from Docker" message.

#### 4.1.2 Deploy Poste.io Container

Execute the following Docker command with your specific configuration:

```bash
docker run \
    --net=host \
    -e TZ=Europe/Prague \
    -v /your-data-dir/data:/data \
    --name "mailserver" \
    -h "campaign.com.au" \
    -t analogic/poste.io
```

**Command Parameters Explained:**
- `--net=host`: Uses host networking for simplified access
- `-e TZ=Europe/Prague`: Sets timezone (adjust as needed)
- `-v /your-data-dir/data:/data`: Mounts data directory for persistence
- `--name "mailserver"`: Names the Docker container
- `-h "mail.example.com"`: Sets mailserver hostname (replace with your domain)
- `-t analogic/poste.io`: Specifies the Poste.io Docker image

**Figure 23: Poste.io Container Running**  
<img width="1107" height="253" alt="Container Running" src="https://github.com/user-attachments/assets/ad39b5f1-55ef-4a62-abf3-8d338d5fda7b" />

**Figure 24: Poste.io Ready**  
<img width="1094" height="482" alt="Poste.io Ready" src="https://github.com/user-attachments/assets/593dbe5a-1e74-40b7-abf1-04912369279b" />

**Figure 25: Poste.io Port Configuration**  
<img width="807" height="438" alt="Port Configuration" src="https://github.com/user-attachments/assets/766e6db2-53de-4dd1-a3f6-d872f92e9e75" />

For advanced configuration options, refer to the official documentation: [https://poste.io/doc/getting-started](https://poste.io/doc/getting-started)

#### 4.1.3 Test Email Functionality

1. Access the webmail interface by clicking the mail icon in the top-right corner

**Figure 26: Accessing Webmail**  
<img width="247" height="47" alt="Webmail Access" src="https://github.com/user-attachments/assets/d355ce41-db71-4cad-b5d9-7c97c9d1808e" />

**Figure 27: Webmail Interface**  
<img width="1474" height="651" alt="Webmail Interface" src="https://github.com/user-attachments/assets/19665fe0-1576-481b-9773-2c9e472f65cc" />

2. Obtain a disposable email address from TempMail

**Figure 28: TempMail Service**  
<img width="1572" height="921" alt="TempMail Website" src="https://github.com/user-attachments/assets/a8e4ec95-339d-4e33-9c4c-de6ed5327571" />

3. Send a test email to the disposable address

**Figure 29: Sending Test Email**  
<img width="1191" height="635" alt="Test Email" src="https://github.com/user-attachments/assets/dba79eaf-45a2-40a0-b293-c1375d014f25" />

4. Verify email delivery in the TempMail inbox

**Figure 30: Email Received**  
<img width="1572" height="925" alt="Email Inbox" src="https://github.com/user-attachments/assets/102223c1-d709-4fc7-a1f2-c0e363e75fde" />

**Figure 31: Email with Spoofed Domain**  
<img width="829" height="385" alt="Spoofed Domain Email" src="https://github.com/user-attachments/assets/aa680ff7-5e71-4e25-955d-b8fe022578f7" />

This confirms that the mail server is operational and can deliver emails with the configured domain.

### 4.2 Poste.io Configuration

#### 4.2.1 Complete Initial Setup

1. Access the web interface at: `https://<SERVER_PUBLIC_IP>`
2. If the default page doesn't load, navigate directly to: `https://<SERVER_PUBLIC_IP>/admin/install/server`
3. Complete the setup wizard with the following information:
   - **Mailserver hostname**: `campaign.com.au`
   - **Administrator email**: `admin@campaign.com.au`
   - **Password**: Create a strong administrator password

**Figure 32: Poste.io Setup Form**  
<img width="1593" height="774" alt="Initial Setup" src="https://github.com/user-attachments/assets/5a2084c2-df66-42c0-9123-ed339325b6e0" />

## Phase 5: Gophish Installation and Configuration

### 5.1 Gophish Installation

#### 5.1.1 Download Gophish

1. Visit [https://getgophish.com](https://getgophish.com) and locate version 0.12.1

**Figure 33: Gophish Website**  
<img width="1671" height="326" alt="Gophish Download" src="https://github.com/user-attachments/assets/05fca0e6-9f10-492b-b2cb-9932f74e3c8c" />

2. Copy the download link for Linux 64-bit:
   `https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip`

**Figure 34: Download Link**  
<img width="934" height="297" alt="Download Link" src="https://github.com/user-attachments/assets/29584779-e0de-457c-8687-2539a2f5f5cd" />

3. Download using wget:
```bash
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
```

**Figure 35: Download Command**  
<img width="1117" height="122" alt="Download Command" src="https://github.com/user-attachments/assets/2f492aa2-1b3a-4553-ae1b-0a49d9a10f62" />

**Figure 36: Download Complete**  
<img width="1107" height="560" alt="Download Complete" src="https://github.com/user-attachments/assets/1b997808-47ae-47cb-a8e9-efcf44458af3" />

**Figure 37: File Verification**  
<img width="1107" height="124" alt="File Check" src="https://github.com/user-attachments/assets/c4013ffe-21e3-4ac8-918e-2930257dcd7e" />

#### 5.1.2 Installation and Setup

1. Create installation directory:
```bash
sudo mkdir /opt/gophish
```

**Figure 38: Create Directory**  
<img width="1090" height="133" alt="Create Directory" src="https://github.com/user-attachments/assets/bcdcb5dc-280a-45ea-a34a-195e97e04985" />

2. Extract the archive:
```bash
unzip gophish-v0.12.1-linux-64bit.zip -d /opt/gophish
```

**Figure 39: Extract Files**  
<img width="1108" height="83" alt="Unzip Command" src="https://github.com/user-attachments/assets/8a8dc6c1-ab66-4f11-97b2-614e5db4a868" />

**Figure 40: Directory Contents**  
<img width="1113" height="141" alt="Directory Contents" src="https://github.com/user-attachments/assets/73d3347d-2b7a-453f-a3a6-13f0e6ac8243" />

3. Set executable permissions:
```bash
cd /opt/gophish
sudo chmod +x gophish
```

**Figure 41: Navigate to Directory**  
<img width="1109" height="100" alt="Navigate Directory" src="https://github.com/user-attachments/assets/3029baac-b377-4d5e-959c-dfce65a1069e" />

**Figure 42: Set Permissions**  
<img width="1110" height="121" alt="Set Permissions" src="https://github.com/user-attachments/assets/081e35a3-db64-44df-8a48-923435b7f602" />

#### 5.1.3 Configuration

1. Edit the configuration file:
```bash
sudo nano config.json
```

**Figure 43: Edit Configuration**  
<img width="1118" height="109" alt="Edit Config" src="https://github.com/user-attachments/assets/7ae41b98-28a0-4473-894e-9a7ea43eeee5" />

2. Modify the listen URL:
   - Change: `"listen_url": "127.0.0.1:3333"`
   - To: `"listen_url": "0.0.0.0:3333"`

**Figure 44: Configuration File**  
<img width="1109" height="606" alt="Config File" src="https://github.com/user-attachments/assets/a1085982-3bbf-4862-a640-7ea053148fc2" />

#### 5.1.4 Launch Gophish

1. Start the Gophish service:
```bash
sudo ./gophish
```

**Figure 45: Start Gophish**  
<img width="1122" height="126" alt="Start Gophish" src="https://github.com/user-attachments/assets/a29c36bd-224b-4eef-babd-c6fc0ad34c7d" />

**Figure 46: Gophish Running**  
<img width="1115" height="776" alt="Gophish Running" src="https://github.com/user-attachments/assets/62547ab2-c15d-4e84-827c-c37f0f37e0ef" />

2. Note the initial credentials displayed in the terminal

**Figure 47: Initial Credentials**  
<img width="1115" height="776" alt="Initial Credentials" src="https://github.com/user-attachments/assets/6eeb3c77-c957-46ce-bddb-900152e0d70e" />

### 5.2 Gophish Configuration

#### 5.2.1 Access Web Interface

1. Open a browser and navigate to: `https://<SERVER_PUBLIC_IP>:3333`

**Figure 48: Gophish Web Interface**  
<img width="1512" height="711" alt="Web Interface" src="https://github.com/user-attachments/assets/cfcc9f3f-d29e-43cc-bf45-aacc9a9ae034" />

#### 5.2.2 Initial Login and Password Change

1. Log in using the temporary credentials from the terminal

**Figure 49: Login Screen**  
<img width="529" height="278" alt="Login Screen" src="https://github.com/user-attachments/assets/d7e53527-3526-4d2e-bb77-eb6a48b9acd4" />

2. Change the default password when prompted

**Figure 50: Password Change**  
<img width="634" height="460" alt="Change Password" src="https://github.com/user-attachments/assets/12c205ff-8280-4657-8bb6-165515015637" />

**Figure 51: Gophish Dashboard**  
<img width="1493" height="741" alt="Dashboard" src="https://github.com/user-attachments/assets/c6125d9b-a574-4441-a5cd-e69096eb345b" />

## Phase 6: Client Environment Setup

### 6.1 Virtual Machine Deployment

Deploy four lightweight Linux VMs to simulate client targets. This guide uses Lubuntu for its minimal resource requirements.

**Note**: The VM deployment process using Proxmox, VirtualBox, or VMware is not detailed here as it's assumed you have virtualisation experience.

**Figure 52: Lubuntu Client VMs**  
<img width="1378" height="732" alt="Client VMs" src="https://github.com/user-attachments/assets/6d69e9a8-3c80-4690-80f7-8d48939e3ab3" />

## Phase 7: Campaign Development and Execution

### 7.1 Virtual Domain Creation

#### 7.1.1 Create Target Domain

1. In the Poste.io admin interface, navigate to **Virtual Domains**
2. Click **Create a new virtual domain**

**Figure 54: Virtual Domains**  
<img width="1666" height="536" alt="Virtual Domains" src="https://github.com/user-attachments/assets/685ebc33-e336-4330-bfcb-499d4eb6e8f6" />

3. Create a domain using: `mailer.last.fm` (matching your email template)

**Figure 55: New Virtual Domain**  
<img width="912" height="352" alt="New Domain" src="https://github.com/user-attachments/assets/c59a303f-fa65-4065-87ae-60feeb72b5ca" />

#### 7.1.2 Create Email Account

1. Create a new email address for the campaign domain

**Figure 56: New Email Address**  
<img width="1342" height="868" alt="New Email" src="https://github.com/user-attachments/assets/98085605-7243-4783-bed1-892df86c28c6" />

2. Configure the email account details

**Figure 57: Email Configuration**  
<img width="1146" height="689" alt="Email Config" src="https://github.com/user-attachments/assets/bc0bd9b3-71ea-43f2-85b0-4f74c85346af" />

**Figure 58: Email Account Created**  
<img width="1426" height="1033" alt="Email Created" src="https://github.com/user-attachments/assets/ead884cd-f2da-492e-81ce-c9e92ea7e974" />

#### 7.1.3 Test Virtual Domain

1. Access the webmail portal

**Figure 59: Webmail Portal**  
<img width="485" height="36" alt="Webmail Portal" src="https://github.com/user-attachments/assets/4907565e-0458-43a1-8647-7b68b7e5ab4d" />

2. Log in with the campaign email credentials

**Figure 60: Webmail Login**  
<img width="819" height="512" alt="Webmail Credentials" src="https://github.com/user-attachments/assets/0a614025-98fb-4125-ad72-42c493f1cb89" />

3. Send a test email to verify functionality

**Figure 61: Test Email**  
<img width="1208" height="655" alt="Test Email" src="https://github.com/user-attachments/assets/bb260bef-f1c1-43b7-aea7-2b4b400422fc" />

4. Confirm delivery to a disposable email

**Figure 62: Email Delivery**  
<img width="1299" height="530" alt="Email Delivery" src="https://github.com/user-attachments/assets/1316955d-09c9-47f4-8b24-a5c4ac500e6a" />

**Figure 63: Email Content**  
<img width="746" height="472" alt="Email Content" src="https://github.com/user-attachments/assets/19f38acb-fd77-440d-a898-4e12ee1d8a4f" />

### 7.2 Gophish Campaign Configuration

#### 7.2.1 Email Template Creation

1. Navigate to **Email Templates** and click **New Template**

**Figure 64: Email Templates**  
<img width="1680" height="468" alt="Email Templates" src="https://github.com/user-attachments/assets/2b5e54c9-8ea9-45da-ad7e-1ab1f742432e" />

2. Configure template details and import the original email

**Figure 65: Template Configuration**  
<img width="701" height="494" alt="Template Config" src="https://github.com/user-attachments/assets/0bf2896a-51ba-4acc-bdef-46740b29e3f3" />

3. Obtain email source code (in Gmail: three dots → Show Original)

**Figure 66: Email Source**  
<img width="1301" height="909" alt="Email Source" src="https://github.com/user-attachments/assets/99308790-692b-403d-b946-2cbddd055831" />

**Figure 67: Copy Email Source**  
<img width="1586" height="589" alt="Copy Source" src="https://github.com/user-attachments/assets/a7e4ba57-f421-44f4-ae6f-a5df8f159a40" />

4. Import email and configure settings

**Figure 68: Import Email**  
<img width="711" height="499" alt="Import Email" src="https://github.com/user-attachments/assets/59ae8291-1a15-4186-a754-7afd6fbdb28e" />

5. Save the template

**Figure 69: Save Template**  
<img width="694" height="1248" alt="Save Template" src="https://github.com/user-attachments/assets/586096fc-7198-4f1b-b548-59c5b6bccb5a" />

**Figure 70: Template Saved**  
<img width="1413" height="396" alt="Template Saved" src="https://github.com/user-attachments/assets/e11e168b-098b-48a8-b079-ccb13155c7eb" />

#### 7.2.2 User Group Configuration

1. Boot your Lubuntu VMs and obtain disposable email addresses for each

**Figure 71: VM1 Email**  
<img width="1275" height="548" alt="VM1 Email" src="https://github.com/user-attachments/assets/d5e08802-4a3a-4ef6-a28c-c19ef0038166" />

**Figure 72: VM2 Email**  
<img width="1265" height="481" alt="VM2 Email" src="https://github.com/user-attachments/assets/932fb45c-a295-41d7-a736-7cc38c1c4355" />

**Figure 73: VM3 Email**  
<img width="1270" height="487" alt="VM3 Email" src="https://github.com/user-attachments/assets/4d1d314b-b3b5-44e0-b52f-783396dcd99e" />

**Figure 74: VM4 Email**  
<img width="1200" height="464" alt="VM4 Email" src="https://github.com/user-attachments/assets/ec950ae0-9d3c-400c-8aff-3b60ae86021d" />

2. Navigate to **Users & Groups** and click **New Group**

**Figure 75: Users & Groups**  
<img width="1676" height="396" alt="Users & Groups" src="https://github.com/user-attachments/assets/e8cfe1f8-331b-48d3-95db-d1595c809121" />

3. Download the CSV template for easier bulk import

**Figure 76: CSV Template**  
<img width="694" height="241" alt="CSV Template" src="https://github.com/user-attachments/assets/71fcd397-31ee-4e00-b2cb-245edfe823a6" />

4. Fill in the CSV with target information (emails from VMs, names, positions)

**Figure 77: Completed CSV**  
<img width="994" height="394" alt="CSV Data" src="https://github.com/user-attachments/assets/1eadf130-e1fd-4539-beb4-0a7e73d2e5e1" />

5. Use **Bulk Import Users** to upload the CSV

**Figure 78: Bulk Import**  
<img width="693" height="677" alt="Bulk Import" src="https://github.com/user-attachments/assets/ba99e002-62d9-47eb-a8f5-c6fde437d455" />

#### 7.2.3 Landing Page Development

1. Navigate to **Landing Pages** and click **New Page**

**Figure 79: Landing Pages**  
<img width="1692" height="536" alt="Landing Pages" src="https://github.com/user-attachments/assets/87f90c20-9949-4e1a-abc9-c0b73bfc77c8" />

2. Configure landing page name and import target site (Last.fm login page)

**Figure 80: Landing Page Configuration**  
<img width="700" height="260" alt="Landing Config" src="https://github.com/user-attachments/assets/be85738f-9a90-4488-864b-1045d8ac6ee2" />

**Figure 81: Import Last.fm**  
<img width="693" height="271" alt="Import Site" src="https://github.com/user-attachments/assets/f540f4de-c2f4-418c-b4ac-d1db23a97d75" />

3. Configure data capture settings and redirect URL

**Figure 82: Landing Page Settings**  
<img width="700" height="983" alt="Landing Settings" src="https://github.com/user-attachments/assets/e24fd7ac-61cd-4d7e-9e67-1060894f04b9" />

**Figure 83: Landing Page Saved**  
<img width="1441" height="427" alt="Landing Saved" src="https://github.com/user-attachments/assets/1aebe9f3-e0cb-4d64-9c17-ef2fb089f2f5" />

#### 7.2.4 Sending Profile Configuration

1. Navigate to **Sending Profiles** and click **New Profile**

**Figure 84: Sending Profiles**  
<img width="1705" height="630" alt="Sending Profiles" src="https://github.com/user-attachments/assets/c5ba4eea-7063-4321-8d24-5c58d15b294f" />

2. Configure SMTP settings using Poste.io virtual domain
   - **Host**: Server public IP with port 465
   - **Username/Password**: Virtual domain email credentials
   - Test email delivery before saving

**Figure 85: SMTP Configuration**  
<img width="707" height="1057" alt="SMTP Config" src="https://github.com/user-attachments/assets/7b10072a-3a7b-4c3a-9b12-61cfb2329d59" />

**Figure 86: Profile Saved**  
<img width="1406" height="441" alt="Profile Saved" src="https://github.com/user-attachments/assets/17c33129-029d-4d33-9bd5-94cab374eed6" />

#### 7.2.5 Campaign Creation and Launch

1. Navigate to **Campaigns** and click **New Campaign**

**Figure 87: New Campaign**  
<img width="1275" height="495" alt="New Campaign" src="https://github.com/user-attachments/assets/cab1ed59-230d-42fd-99d7-3c4a3db98fff" />

2. Configure campaign settings:
   - **URL**: Server public IP with port 8081 (Gophish listener)
   - Select previously created templates, groups, and sending profiles
   - Launch the campaign

**Figure 88: Campaign Configuration**  
<img width="701" height="771" alt="Campaign Config" src="https://github.com/user-attachments/assets/3bdfff1b-6a70-4365-b769-d097a9f83407" />

### 7.3 Campaign Execution and Monitoring

#### 7.3.1 Real-time Campaign Monitoring

Monitor campaign progress in the Gophish dashboard:

**Figure 89: Campaign Monitoring**  
<img width="1688" height="1057" alt="Campaign Monitor" src="https://github.com/user-attachments/assets/019e7424-548c-4aed-a3aa-5ac091fa7681" />

**Figure 90: Campaign Responses**  
<img width="1420" height="662" alt="Campaign Responses" src="https://github.com/user-attachments/assets/d75f8e77-1a38-4eac-b8e2-2c04edc5406a" />

#### 7.3.2 User Interaction Simulation

1. Monitor individual user responses

**Figure 91: Individual Response**  
<img width="1370" height="339" alt="User Response" src="https://github.com/user-attachments/assets/14d1feaa-34df-450e-a478-d119e474b7e2" />

2. Simulate credential entry on the landing page

**Figure 92: Credential Entry**  
<img width="1148" height="581" alt="Credential Entry" src="https://github.com/user-attachments/assets/4a903b00-6800-47c6-94cd-2e0151daf4fd" />

3. Verify credential capture in Gophish

**Figure 93: Credentials Captured**  
<img width="1414" height="655" alt="Credentials Captured" src="https://github.com/user-attachments/assets/d4763dba-3ad4-4dac-ba9d-f1fdb2782eac" />

**Figure 94: Credential Details**  
<img width="1395" height="834" alt="Credential Details" src="https://github.com/user-attachments/assets/f8eff93d-961a-43e2-96f6-4bde2a3500e7" />

#### 7.3.3 Complete Campaign Results

After simulating all user interactions:

**Figure 95: All Submissions**  
<img width="1416" height="728" alt="All Submissions" src="https://github.com/user-attachments/assets/a548f59f-3d18-4eda-8e15-09135f8d3e92" />

**Figure 96: Captured Credentials 1**  
<img width="1350" height="791" alt="Credentials 1" src="https://github.com/user-attachments/assets/6409502a-c2de-403e-b3b1-bd74e0a485cc" />

**Figure 97: Captured Credentials 2**  
<img width="1342" height="776" alt="Credentials 2" src="https://github.com/user-attachments/assets/ffbf9e29-c482-4861-829d-359f9f1c1695" />

**Figure 98: Captured Credentials 3**  
<img width="1295" height="802" alt="Credentials 3" src="https://github.com/user-attachments/assets/9bfe7a52-bb56-458f-b465-4c3bcf257d0b" />

**Figure 99: Campaign Completion**  
<img width="1417" height="788" alt="Campaign Complete" src="https://github.com/user-attachments/assets/0299cce3-515e-48e1-800b-8c480252f8d2" />

## Project Conclusion

This comprehensive phishing simulation lab successfully demonstrates the complete lifecycle of a phishing attack in a controlled environment. By integrating Gophish with Poste.io and deploying virtual client machines, we've replicated the core phases of real-world phishing campaigns:

### Key Achievements
- **Infrastructure Setup**: Successfully deployed cloud-based phishing infrastructure using Kamatera, Docker, and Ubuntu Server
- **Email Spoofing**: Configured Poste.io to send convincing phishing emails with spoofed domains
- **Campaign Execution**: Created realistic phishing templates, landing pages, and user groups
- **Data Capture**: Demonstrated credential harvesting and user interaction tracking
- **Security Awareness**: Highlighted vulnerabilities in human behaviour and email security

### Learning Outcomes
This lab provides hands-on experience with:
- **Attack Methodologies**: Understanding how threat actors design and execute phishing campaigns
- **Infrastructure Components**: Learning the technical requirements for phishing operations
- **Detection Opportunities**: Identifying points where security controls could intervene
- **User Behaviour**: Observing how users interact with malicious content
- **Defensive Strategies**: Developing awareness of protection mechanisms and training needs

### Practical Applications
The skills and knowledge gained from this lab apply to:
- **Security Awareness Training**: Designing effective user education programs
- **Red Team Operations**: Conducting authorized penetration testing
- **Blue Team Defense**: Improving detection and response capabilities
- **Risk Assessment**: Evaluating organisational vulnerability to social engineering
- **Incident Response**: Understanding attack vectors and evidence collection

## Ethical Use and Legal Disclaimer

> **Critical Warning:**  
> This guide is intended **exclusively for educational and authorised testing purposes** within **controlled environments**. The techniques demonstrated must only be used with explicit written permission from system owners and within the scope of legitimate security testing or training programs.

### Legal Requirements
- **Authorisation**: Always obtain proper written authorisation before conducting any phishing simulations
- **Scope Limitation**: Only target systems and users explicitly included in the authorised testing scope
- **Data Protection**: Ensure all captured data is handled according to applicable privacy laws and regulations
- **Documentation**: Maintain detailed records of all testing activities for audit purposes

### Prohibited Uses
The following activities are strictly forbidden:
- Conducting unauthorised phishing attacks against any individual or organisation
- Using these techniques for financial gain, identity theft, or other criminal purposes
- Deploying phishing infrastructure without proper authorisation and oversight
- Sharing captured credentials or personal information outside the authorised testing team
- Using spoofed domains that could damage legitimate organisations' reputations

## Troubleshooting Guide

### Common Issues and Solutions

#### Email Delivery Problems
**Issue**: Emails not reaching target inboxes
- **Cause**: Missing DNS records, blacklisted IP, or blocked ports
- **Solution**: Use disposable email services for testing; verify Poste.io configuration
- **Note**: This setup intentionally lacks proper email authentication for educational purposes

#### Gophish Interface Accessibility
**Issue**: Cannot access Gophish web interface
- **Cause**: Firewall blocking port 3333 or incorrect listen configuration
- **Solution**: 
  - Verify firewall rules allow traffic on port 3333
  - Confirm `config.json` uses `"listen_url": "0.0.0.0:3333"`
  - Check server security groups in the cloud provider console

#### Docker Container Issues
**Issue**: Poste.io container fails to start
- **Cause**: Port conflicts or insufficient permissions
- **Solution**:
  - Stop conflicting services using ports 25, 80, 443, 465, 993, 995
  - Remove existing container: `docker rm -f mailserver`
  - Restart with proper permissions and unique ports

#### Landing Page Display Problems
**Issue**: Landing page doesn't render correctly
- **Cause**: Missing CSS/JavaScript resources or HTTPS/HTTP conflicts
- **Solution**:
  - Use simple HTML templates without complex JavaScript
  - Ensure all resources are properly imported
  - Test with basic forms before adding complexity

## Additional Resources

### Documentation and Guides
- **Gophish Documentation**: [https://docs.getgophish.com](https://docs.getgophish.com)
- **Poste.io Setup Guide**: [https://poste.io/doc](https://poste.io/doc)
- **Docker Best Practices**: [https://docs.docker.com/develop/best-practices](https://docs.docker.com/develop/best-practices)

### Security Frameworks
- **NIST Cybersecurity Framework**: Guidelines for security assessment and improvement
- **OWASP Testing Guide**: Web application security testing methodologies
- **SANS Security Awareness**: Resources for security training program development

### Community Support
- **Gophish Community**: GitHub issues and discussions for technical support
- **Security Forums**: Professional communities for sharing best practices
- **Training Programs**: Certified ethical hacking and penetration testing courses

---

*This guide represents a comprehensive approach to understanding phishing attack methodologies through safe, controlled simulation. You can use this knowledge responsibly to improve cybersecurity awareness and defensive capabilities.*
