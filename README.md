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

The first step in this project is to create a comprehensive diagram that will guide our deployment process. This planning phase is crucial for understanding the data flow and system interactions before we begin the actual implementation.

#### Step 1.1: Network Architecture Design

To visualise the project architecture, I used **Draw.io** to create the following network diagram. This helps clarify how each component, from virtual machines to cloud services, interacts during the phishing simulation setup.

**1. Diagram Components**

* **Virtual Machines**: Lubuntu clients hosted on a Proxmox home lab
* **Cloud Services**: Kamatera-hosted Ubuntu server running Gophish and Poste.io
* **Network Infrastructure**: Routing, firewall, and port forwarding configuration

*Figure 1: Lab Architecture Overview*
<img width="1442" height="861" alt="Phishing Attack Simulation drawio (5)" src="https://github.com/user-attachments/assets/eea1dd4a-06ea-47aa-88d1-51c87f054894" />

### Phase 2: Campaign Workflow

The following diagram outlines the step-by-step **workflow for executing a phishing campaign** using Gophish and Poste.io. It captures both the configuration phase and the execution lifecycle, from email creation to result analysis.

*Figure 2: Campaign Workflow* <br>
<img width="671" height="562" alt="phishing_simulation_workflow drawio (1)" src="https://github.com/user-attachments/assets/b8554c28-d7df-413f-8b34-c92d6ec8a893" />

#### Workflow Summary

1. **Initiation**
   * The manager starts the phishing simulation from the Gophish dashboard (port 3333).

2. **Configuration Phase**
   * Templates, landing pages (port 8081), and target lists are configured.
   * A sending profile is created using the internal SMTP server (Poste.io on port 465).

3. **Execution**
   * The campaign is launched.
   * Gophish sends phishing emails through Poste.io.
   * Emails are delivered to TempMail disposable inboxes used by Lubuntu clients.

4. **User Interaction**
   * Targets receive the phishing email and interact with the landing page.
   * Gophish tracks these interactions (clicks, submissions, etc.).

5. **Analysis**
   * The manager monitors results directly in the Gophish dashboard to assess engagement and awareness levels.

## Phase 3: Cloud Infrastructure Setup

### Step 3.1: Kamatera Cloud VM Deployment

Kamatera was selected as the cloud provider due to its generous $100 free credit.

1. **Create a Kamatera account**: The free trial credit is sufficient for this project.

2. **Deploy Ubuntu Server 24.04 LTS VM**:

   * Navigate to *My Cloud* and click **Create New Server**.
   * Select your zone, image (Ubuntu 24.04 LTS), and server type. <br> *Figure 3: Kamatera Server Deployment Page* <br> <img width="1712" height="1177" alt="Screenshot 2025-07-11 000422" src="https://github.com/user-attachments/assets/268fde08-75a1-49a1-9736-7004a47ae33a" />
   * Use the following specs: 2 vCPUs, 4GB RAM, 50GB SSD, public and private network enabled. <br> *Figure 4: Server Configuration Options* <br> <img width="1265" height="933" alt="Screenshot 2025-07-12 115541" src="https://github.com/user-attachments/assets/23e5b241-269e-4848-8cb6-d5ab0ca2e392" />
   * Set a root password and name the instance "MyLab-PhishLab". Monthly cost: ~$20.
     
*Figure 5: Server Name and Password Configuration* <br> <img width="1335" height="826" alt="Screenshot 2025-07-12 120615" src="https://github.com/user-attachments/assets/ba355d0a-6b97-4872-9618-0c1cbb897a9d" />

3. **Check server status**:
   * Navigate to *Server List* and select your newly created server. <br> *Figure 6: Server Status Dashboard* <br> <img width="1681" height="508" alt="Screenshot 2025-07-12 121141" src="https://github.com/user-attachments/assets/4c5e5e85-ee58-4911-9707-b83573247cb5" /> <br> *Figure 7: Server Details* <br> <img width="1408" height="686" alt="Screenshot 2025-07-12 121649" src="https://github.com/user-attachments/assets/a4b612c7-95d0-4658-a36c-31a831fc90df" />
   * From your local host, ping the public IP to confirm connectivity `ping <SERVER_PUBLIC_IP>`. <br> *Figure 8: Ping Test Output* <br> <img width="1109" height="345" alt="Screenshot 2025-07-11 001820" src="https://github.com/user-attachments/assets/431390e7-5cd7-462e-956d-f4935da3c001" />

4. **Configure Kamatera firewall**:
   * Navigate to *Firewall* under server settings.
   * Enable firewall and add rules to allow TCP/UDP from your host IP. <br> *Figure 9: Firewall Rule Settings* <br> <img width="1440" height="988" alt="image" src="https://github.com/user-attachments/assets/25b7da53-74e9-48d1-b70e-51e1350c8a60" /> <br> *Figure 10: UDP Rule Settings* <br> <img width="604" height="680" alt="Screenshot 2025-07-11 003513" src="https://github.com/user-attachments/assets/03f02881-70a4-46ce-a973-a7f601814d4d" /> <br> *Figure 11: TCP Rule Settings* <br> <img width="599" height="678" alt="Screenshot 2025-07-11 003630" src="https://github.com/user-attachments/assets/b4d1ffd9-c6ec-45bf-b01d-29ff5f230926" />
   * Use a public IP checker tool to identify your IP. <br> *Figure 12: IP Lookup Tool Example* <br> <img width="1467" height="563" alt="image" src="https://github.com/user-attachments/assets/6c275c50-32b9-4e64-bea4-f2eb03510ebb" />

5. **SSH into the Ubuntu server**:
   * On your local terminal: `ssh root@<SERVER_PUBLIC_IP>` <br> *Figure 13: SSH Connection Terminal Output* <br>  <img width="1107" height="216" alt="Screenshot 2025-07-11 005850" src="https://github.com/user-attachments/assets/128d5092-16a3-4f06-a424-f6559f604d37" /> <br> *Figure 14: SSH Connection Stablished* <br> <img width="1108" height="769" alt="Screenshot 2025-07-11 005956" src="https://github.com/user-attachments/assets/d38d2638-62bb-44b7-ae6f-29d08a443405" />
   * Update packages: `apt update && apt upgrade -y` <br> *Figure 15: System Command* <br> <img width="1111" height="124" alt="Screenshot 2025-07-11 010048" src="https://github.com/user-attachments/assets/32d55335-998c-4a6e-9d3a-2242a9936c83" /> <br> *Figure 16: System Update Output* <br> <img width="1117" height="475" alt="Screenshot 2025-07-11 010122" src="https://github.com/user-attachments/assets/20372622-ad74-49ce-8723-c47e36fe3c4b" />
   * Install unzip: `sudo apt install unzip -y` <br> *Figure 16: Unzip Installation Command* <br> <img width="1108" height="126" alt="Screenshot 2025-07-11 010304" src="https://github.com/user-attachments/assets/cee61116-d4b2-4c9f-aea0-fd283fc13a7d" /> <br> *Figure 17: Unzip Installation Output* <br> <img width="1112" height="400" alt="Screenshot 2025-07-11 010318" src="https://github.com/user-attachments/assets/ddd59499-49fa-4662-ab45-c51303ad86fe" />

## Phase 4: Gophish Installation and Configuration

### Step 4.1: Gophish Installation

1. **Download Gophish**:
   * Go to https://getgophish.com and download v0.12.1. <br> *Figure 18: Gophish Website* <br> <img width="1671" height="326" alt="Screenshot 2025-07-11 010507" src="https://github.com/user-attachments/assets/05fca0e6-9f10-492b-b2cb-9932f74e3c8c" />
   * Click on download and copy the package link `https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip`. <br> *Figure 19: Gophish Package Link* <br> <img width="934" height="297" alt="Screenshot 2025-07-11 010704" src="https://github.com/user-attachments/assets/29584779-e0de-457c-8687-2539a2f5f5cd" />
   * Go to the terminal and use: `wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip` <br> *Figure 20: Gophish Download Command* <br> <img width="1117" height="122" alt="Screenshot 2025-07-11 010948" src="https://github.com/user-attachments/assets/2f492aa2-1b3a-4553-ae1b-0a49d9a10f62" /> <br> *Figure 21: Gophish Downloaded* <br> <img width="1107" height="560" alt="Screenshot 2025-07-11 011004" src="https://github.com/user-attachments/assets/1b997808-47ae-47cb-a8e9-efcf44458af3" /> <br> *Figure 22: Gophish File Check* <br> <img width="1107" height="124" alt="Screenshot 2025-07-11 011035" src="https://github.com/user-attachments/assets/c4013ffe-21e3-4ac8-918e-2930257dcd7e" />

2. **Create Gophish folder and unzip Gophish package**:
  * Let's create a local directory to unzip the Gophish package content `sudo mkdir /opt/gophish`. <br> *Figure 23: Command* <br> <img width="1090" height="133" alt="Screenshot 2025-07-11 011114" src="https://github.com/user-attachments/assets/bcdcb5dc-280a-45ea-a34a-195e97e04985" />
  * Unzip the Gophish package within the folder `unzip gophish-v0.12.1-linux-64bit.zip -d /opt/gophish`. <br> *Figure 24: Command* <br> <img width="1108" height="83" alt="Screenshot 2025-07-11 011205" src="https://github.com/user-attachments/assets/8a8dc6c1-ab66-4f11-97b2-614e5db4a868" /> <br> *Figure 24: Folder Content* <br> <img width="1113" height="141" alt="Screenshot 2025-07-11 011244" src="https://github.com/user-attachments/assets/73d3347d-2b7a-453f-a3a6-13f0e6ac8243" />
3. ** Changing Permissions and Gophish Initial Settings **:
  * Change Gophish permission and make it executable, first navigate to the Gophish folder `cd /opt/gophish`, then type `sudo chmod +x gophish`. <br> *Figure 25: Naviagte to Folder* <br> <img width="1109" height="100" alt="Screenshot 2025-07-11 011335" src="https://github.com/user-attachments/assets/3029baac-b377-4d5e-959c-dfce65a1069e" />  <br> *Figure 26: Modify Permisions* <br> <img width="1110" height="121" alt="Screenshot 2025-07-11 011415" src="https://github.com/user-attachments/assets/081e35a3-db64-44df-8a48-923435b7f602" />
  * Now we need to edit `config.json` to modify the initial settings, `sudo nano config. json`. <br> *Figure 26: Modify File* <br> <img width="1118" height="109" alt="Screenshot 2025-07-11 011449" src="https://github.com/user-attachments/assets/7ae41b98-28a0-4473-894e-9a7ea43eeee5" />
  * Navigate to `"listen_url": "127.0.0.0:3333"` and change it to `"listen_url": "0.0.0.0:3333"`. We need to perform this change to allow access from external machines. <br> *Figure 27: Modified File* <br> <img width="1109" height="606" alt="Screenshot 2025-07-11 011546" src="https://github.com/user-attachments/assets/a1085982-3bbf-4862-a640-7ea053148fc2" />








