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

#### Step 2.1: Workflow Summary

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

