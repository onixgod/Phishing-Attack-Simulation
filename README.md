# Phishing Attack Simulation with Gophish and Poste.io

## Objective

This project showcases the setup and execution of a **controlled phishing simulation lab** using **Gophish** and **Poste.io**. The goal is to safely explore how phishing attacks work and strengthen cybersecurity skills in a hands-on environment.

**Key Objectives:**
- Conduct realistic phishing campaigns in a controlled lab setting  
- Understand the functionality and capabilities of phishing tools  
- Learn how phishing attacks are implemented in real-world scenarios  
- Enhance cybersecurity and technical skillsets through practical experience  

---

## Acknowledgments

Special thanks to **@Sandra (With.Sandra's YouTube Channel)** for the inspiration and guidance that helped shape this project.  
Additional gratitude to **hailbytes.com** for their advanced tutorials, which enabled the transition from an introductory lab to a **live email testing environment**.

---

## Skills Developed

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
- Enable firewall and add custom rules to allow TCP/UDP from your local IP

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

## Phase 4: Gophish Installation and Configuration

### Step 4.1: Gophish Installation

1. **Download Gophish**:
   - Go to https://getgophish.com and download version 0.12.1  
     *Figure 19: Gophish Website*  
     <img width="1671" height="326" alt="Screenshot 2025-07-11 010507" src="https://github.com/user-attachments/assets/05fca0e6-9f10-492b-b2cb-9932f74e3c8c" />
   - Copy the download link:  
     `https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip`  
     *Figure 20: Gophish Package Link*  
     <img width="934" height="297" alt="Screenshot 2025-07-11 010704" src="https://github.com/user-attachments/assets/29584779-e0de-457c-8687-2539a2f5f5cd" />
   - Download the package using `wget`:  
     `wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip`  
     *Figure 21: Gophish Download Command*  
     <img width="1117" height="122" alt="Screenshot 2025-07-11 010948" src="https://github.com/user-attachments/assets/2f492aa2-1b3a-4553-ae1b-0a49d9a10f62" />  
     *Figure 22: Gophish Downloaded*  
     <img width="1107" height="560" alt="Screenshot 2025-07-11 011004" src="https://github.com/user-attachments/assets/1b997808-47ae-47cb-a8e9-efcf44458af3" />  
     *Figure 23: Gophish File Check*  
     <img width="1107" height="124" alt="Screenshot 2025-07-11 011035" src="https://github.com/user-attachments/assets/c4013ffe-21e3-4ac8-918e-2930257dcd7e" />

2. **Create Gophish folder and unzip package**:
   - Create a directory to hold Gophish:  
     `sudo mkdir /opt/gophish`  
     *Figure 24: Command*  
     <img width="1090" height="133" alt="Screenshot 2025-07-11 011114" src="https://github.com/user-attachments/assets/bcdcb5dc-280a-45ea-a34a-195e97e04985" />
   - Unzip the package:  
     `unzip gophish-v0.12.1-linux-64bit.zip -d /opt/gophish`  
     *Figure 25: Command*  
     <img width="1108" height="83" alt="Screenshot 2025-07-11 011205" src="https://github.com/user-attachments/assets/8a8dc6c1-ab66-4f11-97b2-614e5db4a868" />  
     *Figure 26: Folder Content*  
     <img width="1113" height="141" alt="Screenshot 2025-07-11 011244" src="https://github.com/user-attachments/assets/73d3347d-2b7a-453f-a3a6-13f0e6ac8243" />

3. **Change Permissions and Configure Settings**:
   - Make the binary executable:  
     ```bash
     cd /opt/gophish
     sudo chmod +x gophish
     ```  
     *Figure 27: Navigate to Folder*  
     <img width="1109" height="100" alt="Screenshot 2025-07-11 011335" src="https://github.com/user-attachments/assets/3029baac-b377-4d5e-959c-dfce65a1069e" />  
     *Figure 28: Modify Permissions*  
     <img width="1110" height="121" alt="Screenshot 2025-07-11 011415" src="https://github.com/user-attachments/assets/081e35a3-db64-44df-8a48-923435b7f602" />
   - Edit `config.json`:  
     `sudo nano config.json`  
     *Figure 29: Modify File*  
     <img width="1118" height="109" alt="Screenshot 2025-07-11 011449" src="https://github.com/user-attachments/assets/7ae41b98-28a0-4473-894e-9a7ea43eeee5" />
   - Change the `"listen_url"` value from `"127.0.0.0:3333"` to `"0.0.0.0:3333"` to allow external access.  
     *Figure 30: Modified File*  
     <img width="1109" height="606" alt="Screenshot 2025-07-11 011546" src="https://github.com/user-attachments/assets/a1085982-3bbf-4862-a640-7ea053148fc2" />









