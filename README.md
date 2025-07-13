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

*Figure 19: Download Docker Script Command* <br>
<img width="1111" height="159" alt="Screenshot 2025-07-11 114804" src="https://github.com/user-attachments/assets/3d7a8071-d191-4022-83aa-ffe3574ae79a" />

*Figure 20: Script File in Directory* <br>
<img width="1121" height="160" alt="Screenshot 2025-07-11 114856" src="https://github.com/user-attachments/assets/bcb2ef6d-5c59-4be3-8629-1d934f18e09e" />

*Figure 21: Script File Content Preview* <br>
<img width="1112" height="623" alt="Screenshot 2025-07-11 114923" src="https://github.com/user-attachments/assets/ecca322e-da7e-4528-8f60-0c1145dc8d21" />


Run the script:

```bash
sudo sh get-docker.sh
```

*Figure 22: Run Installation Script* <br>
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

*Figure 23: Poste.io Container Running* <br>
<img width="1107" height="253" alt="Screenshot 2025-07-11 115240" src="https://github.com/user-attachments/assets/ad39b5f1-55ef-4a62-abf3-8d338d5fda7b" />

*Figure 24: Poste.io Ready Message* <br>
<img width="1094" height="482" alt="Screenshot 2025-07-11 125631" src="https://github.com/user-attachments/assets/593dbe5a-1e74-40b7-abf1-04912369279b" />

For more advanced configuration, refer to the official guide:  
[https://poste.io/doc/getting-started](https://poste.io/doc/getting-started)

Also, note that Poste.io opens the following ports:

*Figure 25: Poste.io Ports* <br>
<img width="807" height="438" alt="Screenshot 2025-07-11 130300" src="https://github.com/user-attachments/assets/766e6db2-53de-4dd1-a3f6-d872f92e9e75" />

#### 3. Test Poste.io

On the top righ corner click on the mail icon.
*Figure 26: Accesing Web Mail* <br>
<img width="247" height="47" alt="Screenshot 2025-07-11 130353" src="https://github.com/user-attachments/assets/d355ce41-db71-4cad-b5d9-7c97c9d1808e" />

Compose and email.
*Figure 27: Web Mail Interface* <br>
<img width="1474" height="651" alt="Screenshot 2025-07-11 130707" src="https://github.com/user-attachments/assets/19665fe0-1576-481b-9773-2c9e472f65cc" />

Open on a browser tab MailTemp and get a disposable email address.
*Figure 28: TempMail Website <br>
<img width="1572" height="921" alt="Screenshot 2025-07-11 130809" src="https://github.com/user-attachments/assets/a8e4ec95-339d-4e33-9c4c-de6ed5327571" />

Send an email to the disposable address.
*Figure 29: Sending email <br>
<img width="1191" height="635" alt="Screenshot 2025-07-11 130754" src="https://github.com/user-attachments/assets/dba79eaf-45a2-40a0-b293-c1375d014f25" />

Check the inbox of the disposable email.
*Figure 30: Inbox <br>
<img width="1572" height="925" alt="Screenshot 2025-07-11 130822" src="https://github.com/user-attachments/assets/102223c1-d709-4fc7-a1f2-c0e363e75fde" />

Now we can confirm that our mail server is working correctly and delivering emails with our fake domain (spoof).
*Figure 31: Email with fake spoof domain <br>
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

*Figure 32: Poste.io First-Time Setup Form* <br>
<img width="1593" height="772" alt="Screenshot 2025-07-11 130037" src="https://github.com/user-attachments/assets/2d6ed2f8-a140-4be8-bfd9-2dfd1096c5f4" />

---

## Phase 5: Gophish Installation and Configuration

---

### Step 5.1: Gophish Installation

#### 1. Download Gophish

- Go to [https://getgophish.com](https://getgophish.com) and download version 0.12.1  
  *Figure 33: Gophish Website*  
  <img width="1671" height="326" alt="Screenshot 2025-07-11 010507" src="https://github.com/user-attachments/assets/05fca0e6-9f10-492b-b2cb-9932f74e3c8c" />

- Copy the download link:  
  `https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip`  
  *Figure 34: Gophish Package Link*  
  <img width="934" height="297" alt="Screenshot 2025-07-11 010704" src="https://github.com/user-attachments/assets/29584779-e0de-457c-8687-2539a2f5f5cd" />

- Download the package using `wget`:  
  ```bash
  wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
  ```
  *Figure 35: Gophish Download Command*  
  <img width="1117" height="122" alt="Screenshot 2025-07-11 010948" src="https://github.com/user-attachments/assets/2f492aa2-1b3a-4553-ae1b-0a49d9a10f62" />  
  *Figure 36: Gophish Downloaded*  
  <img width="1107" height="560" alt="Screenshot 2025-07-11 011004" src="https://github.com/user-attachments/assets/1b997808-47ae-47cb-a8e9-efcf44458af3" />  
  *Figure 37: Gophish File Check*  
  <img width="1107" height="124" alt="Screenshot 2025-07-11 011035" src="https://github.com/user-attachments/assets/c4013ffe-21e3-4ac8-918e-2930257dcd7e" />

#### 2. Create Gophish Folder and Unzip

- Create a directory:
  ```bash
  sudo mkdir /opt/gophish
  ```
  *Figure 38: Create Folder*  
  <img width="1090" height="133" alt="Screenshot 2025-07-11 011114" src="https://github.com/user-attachments/assets/bcdcb5dc-280a-45ea-a34a-195e97e04985" />

- Unzip the downloaded file:
  ```bash
  unzip gophish-v0.12.1-linux-64bit.zip -d /opt/gophish
  ```
  *Figure 39: Unzip Command*  
  <img width="1108" height="83" alt="Screenshot 2025-07-11 011205" src="https://github.com/user-attachments/assets/8a8dc6c1-ab66-4f11-97b2-614e5db4a868" />  
  *Figure 40: Folder Content*  
  <img width="1113" height="141" alt="Screenshot 2025-07-11 011244" src="https://github.com/user-attachments/assets/73d3347d-2b7a-453f-a3a6-13f0e6ac8243" />

#### 3. Change Permissions and Configure Gophish

- Make the binary executable:
  ```bash
  cd /opt/gophish
  sudo chmod +x gophish
  ```
  *Figure 41: Navigate to Folder*  
  <img width="1109" height="100" alt="Screenshot 2025-07-11 011335" src="https://github.com/user-attachments/assets/3029baac-b377-4d5e-959c-dfce65a1069e" />  
  *Figure 42: Modify Permissions*  
  <img width="1110" height="121" alt="Screenshot 2025-07-11 011415" src="https://github.com/user-attachments/assets/081e35a3-db64-44df-8a48-923435b7f602" />

- Edit the `config.json` file:
  ```bash
  sudo nano config.json
  ```
  *Figure 43: Modify File*  
  <img width="1118" height="109" alt="Screenshot 2025-07-11 011449" src="https://github.com/user-attachments/assets/7ae41b98-28a0-4473-894e-9a7ea43eeee5" />

- Change the line:
  `"listen_url": "127.0.0.0:3333"`  
  to  
  `"listen_url": "0.0.0.0:3333"`  
  *Figure 44: Modified File*  
  <img width="1109" height="606" alt="Screenshot 2025-07-11 011546" src="https://github.com/user-attachments/assets/a1085982-3bbf-4862-a640-7ea053148fc2" />

#### 4. Run Gophish Framework

Start the Gophish service:
```bash
sudo ./gophish
```

*Figure 45: Run Gophish*  
<img width="1122" height="126" alt="Screenshot 2025-07-11 011629" src="https://github.com/user-attachments/assets/a29c36bd-224b-4eef-babd-c6fc0ad34c7d" />  
*Figure 46: Gophish Running*  
<img width="1115" height="776" alt="Screenshot 2025-07-11 011644" src="https://github.com/user-attachments/assets/62547ab2-c15d-4e84-827c-c37f0f37e0ef" />

#### 5. Gophish Initial Credentials

- The initial credentials are displayed in the terminal on the first run. You'll be prompted to set a new password.

*Figure 47: Gophish Initial Credentials*  
<img width="1115" height="776" alt="Screenshot 2025-07-11 011739" src="https://github.com/user-attachments/assets/6eeb3c77-c957-46ce-bddb-900152e0d70e" />

---

### Step 5.2: Gophish Configuration

#### 1. Access the Web Interface

- Open a browser and visit:  
  `https://<SERVER_PUBLIC_IP>:3333`

*Figure 48: Access Gophish Web Interface*  
<img width="1512" height="711" alt="Screenshot 2025-07-11 012038" src="https://github.com/user-attachments/assets/cfcc9f3f-d29e-43cc-bf45-aacc9a9ae034" />

#### 2. Change Default Credentials

- Log in using the temporary credentials shown earlier.
- You will be prompted to change the default password.

*Figure 49: Initial Credentials Login*  
<img width="529" height="278" alt="Screenshot 2025-07-11 012148" src="https://github.com/user-attachments/assets/d7e53527-3526-4d2e-bb77-eb6a48b9acd4" />  
*Figure 50: Change Default Password*  
<img width="634" height="460" alt="Screenshot 2025-07-11 012214" src="https://github.com/user-attachments/assets/12c205ff-8280-4657-8bb6-165515015637" />  
*Figure 51: Gophish Dashboard*  
<img width="1493" height="741" alt="Screenshot 2025-07-11 012241" src="https://github.com/user-attachments/assets/c6125d9b-a574-4441-a5cd-e69096eb345b" />

-----------------------------------------------------------


## Phase 6: Client VMs Deployment

---

### Step 6.1: Lightweight Linux VM 

For this project, we will deploy four lightweight Linux VM flavours, which will serve the purpose of simulating four clients, accessing disposable emails on the TempMail website. Will will be using Lubuntu, which is a lightweight Linux distribution. I have created a template on my Proxmox Home Lab and cloned it to get four separate VMs. I am not showing this process because I'm hoping you know. If you don't use Proxmpx, you can use any other Hypervisor, such as VirtualBox or VMware.

*Figure 52: Lubuntu Client VMs*  
<img width="1378" height="732" alt="image" src="https://github.com/user-attachments/assets/6d69e9a8-3c80-4690-80f7-8d48939e3ab3" />



Phase 7: Campaign Development and Testing




