# Performing an On-Path (AitM) Attack

## Overview
This lab simulates a real-world penetration testing scenario for the client **Structureality**. The objective is to evaluate network security by implementing an adversary-in-the-middle (AitM) attack to intercept web authentication credentials. This simulation utilizes business email compromise (BEC) tactics and social engineering to determine if users are vulnerable to phishing scams and if insecure protocols are in use within the network.

---

##  Technical Toolkit

* **Burp Suite:** Configured as an unauthorized web proxy to intercept, inspect, and manipulate HTTP/S traffic.
* **Kali Linux (KALI VM):** The primary attacker workstation used to host the intercepting tools.
* **Windows Server 2016 (MS VM):** The target/victim environment used to simulate end-user behavior.
* **Target Web Application:** `juiceshop.local`, a known vulnerable web application used for security training.
* **Phishing/BEC Frameworks:** Tactics used to craft and deliver the deceptive message to the victim.

---

##  Key Accomplishments & Skills Demonstrated

* **AitM Attack Execution:** Configured Burp Suite as an unauthorized proxy to intercept and monitor live web traffic between a victim and server
* **Credential Harvesting:** Successfully captured and analyzed sensitive web authentication data during active sessions
* **BEC Simulation:** Engineered a realistic Business Email Compromise scenario to test user vulnerability to phishing
* **Social Engineering Tactics:** Applied psychological triggers to influence victim behavior and facilitate a successful compromise
* **Network Path Exploitation:** Navigated across internal and screened subnets to identify and exploit architectural communication weaknesses
* **Vulnerability Validation:** Confirmed the presence of insecure protocols and configurations susceptible to session hijacking
* **Red Team Methodology:** Integrated technical exploits with social engineering to simulate multi-stage, real-world cyberattacks
* **Traffic Manipulation:** Utilized professional-grade intercepting tools to inspect and modify HTTP/S requests in real-time

---

##  Lab Analysis

### Section 1: Configure Burp Suite as a Proxy
The attacker workstation (Kali Linux) was prepared to act as an interceptor. Burp Suite was configured as an unauthorized web proxy by adding a new proxy listener bound to a specific IP address (**10.1.16.66**) and port (**8080**). This setup ensures that any traffic directed to this address can be inspected and manipulated.
<p align="center">
  <img src="path/to/Section1.PNG" width="45%" alt="pics"/>
</p>

### Section 2: Create an Attack Script
The attacker created a malicious batch file named `newproxy.bat` using the **vim** editor. This script targets Windows registry settings (`HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings`) to force the victim's system to use the attacker's IP as its **ProxyServer** and sets **ProxyEnable** to true. The **Apache2** service was started to host and deliver the file.
<p align="center">
  <img src="path/to/Section2.PNG" width="45%" alt="pics"/>
</p>

### Section 3: Play the Victim
This section simulates the human element of the attack through social engineering. The victim followed unsolicited instructions to download and run the `newproxy.bat` file. Despite a security warning stating the publisher could not be verified, the victim clicked **"Run,"** which successfully rerouted their web traffic through the attacker's proxy.
<p align="center">
  <img src="path/to/Section3.PNG" width="45%" alt="pics"/>
</p>

### Section 4: Discover AitM Captured Credentials
With the proxy active, the attacker monitored the **HTTP history** in Burp Suite as the victim attempted to log in to `juiceshop.local`. Because the victim used an insecure protocol, the attacker captured a **POST** request to `/rest/user/login`. The intercepted request revealed the victim’s plain-text credentials:
* **Email:** `jaime@structureality.com`
* **Password:** `Pa55w0rd!`
<p align="center">
  <img src="path/to/Section4.PNG" width="45%" alt="pics"/>
</p>
