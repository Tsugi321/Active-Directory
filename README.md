# Active Directory

## Objective

The Detection Lab project aimed to establish a realistic, enterprise‑style environment for simulating cyber attacks and analysing defensive telemetry. By deploying Active Directory, configuring endpoint logging, and integrating Splunk as the SIEM, the lab provided a controlled space to generate, ingest, and investigate security events. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned

- Designed and deployed a multi‑VM cybersecurity lab environment using VirtualBox, including network planning, NAT configuration, and static IP assignment
- Installed, configured, and managed multiple operating systems (Windows 10, Windows Server 2022, Ubuntu Server, Kali Linux) for enterprise‑style testing
- Deployed Splunk Enterprise and Splunk Universal Forwarder, including index creation, data ingestion setup, and log forwarding configuration
- Implemented Sysmon with a custom configuration to enrich endpoint telemetry and improve visibility into system activity
- Analyzed Windows Security Event Logs (e.g., 4624, 4625) to identify authentication attempts, brute‑force activity, and attacker behavior
- Built and administered an Active Directory domain, including domain controller promotion, DNS configuration, OU structuring, and user account management
- Conducted adversary simulation using Hydra for brute‑force attacks and Atomic Red Team for MITRE ATT&CK‑aligned test execution
- Investigated and validated attack telemetry within Splunk to understand detection logic, event patterns, and SOC triage workflows
- Strengthened troubleshooting skills across networking, OS configuration, permissions, and SIEM ingestion pipelines
- Documented technical processes clearly and accurately to support repeatability and knowledge sharing


### Tools Used

- VirtualBox as a vitual machine host
- Windows 10, Ubuntu server, Kali Linux, and Windows server 2022 as Operating systems
- Splunk is used as the SIEM for log ingestion, indexing, searching, and detection analysis
- Splunk Universal Forwarder to forward Windows and Linux logs to the Splunk server
- Sysmon (with Olaf’s configuration) as an endpoint telemetry tool providing detailed process, network, and authentication logging
- Hydra to simulate a brute-force password‑guessing attacks over RDP
- Atomic Red Team (ART) for executing MITRE ATT&CK‑aligned adversary techniques
- PowerShell & Bash for configuration, automation, and attack execution

## Steps
1. Create a Network Diagram to plan out the structure of the lab environment.

<img width="1011" height="809" alt="Screenshot 2026-02-10 165157" src="https://github.com/user-attachments/assets/fa5ead9b-8c5d-41a7-bb24-16eb3b4ded6d" />


2. Download and install all necessary VM Systems.
   
<img width="951" height="747" alt="Screenshot 2026-02-10 183533" src="https://github.com/user-attachments/assets/dac76541-4181-4b34-8d9f-a4bf901518b5" />

2.5 Make sure ubuntu is updated.
(Sudo apt-get update && Sudo apt-get upgrade -y on ubuntu server)
   
3. Set up a NAT Network with planned IP address and connect all VMs to that network

<img width="959" height="741" alt="Screenshot 2026-02-10 183804" src="https://github.com/user-attachments/assets/ffefe516-927d-41d9-9f29-1a53f1dd339f" />

4. Configure splunk server to the designated ip address by changing the .yaml file
(sudo nano /etc/netplan/50-cloud-init.yaml > configure file to set designated ip address and gateway)

<img width="320" height="178" alt="Screenshot 2026-02-12 180832" src="https://github.com/user-attachments/assets/e8260e1c-e819-4081-a6d9-cdf80c98ae31" />

<img width="797" height="661" alt="Screenshot 2026-02-10 183854" src="https://github.com/user-attachments/assets/594cea97-85a7-47fb-b9d9-4fa0f9bcbd4d" />

5. Install virtualbox packages, add a shared directory and add a new user to vbox
(sudo apt-get install virtualbox-guest-additions-iso)(sudo apt-get install virtualbox-guest-utils)(sudo adduser *username* vboxsf)

6. Make a new directory and mount the shared directory to the newly created one
(sudo mount -t vboxsf -o uid=1000,gid=1000 *shared directory* *new directory*

7. Move to the new directory and install splunk package
(cd *new directory*) (sudo dpkg -i splunk-*verions of splunk*)

8. Set up splunk server by moving to splunk directory and change user to splunk to gain permissions
(cd /opt/splunk) (sudo -u splunk bash)

9. Move to bin directory and run the installer
(cd bin) (./splunk start)

10. Automate splunk server startup by changing back to default user and moving to bin directory
(exit) (cd bin) (sudo ./splunk enable boot-start -user splunk)

11. Configure target vm and windows server by installing splunk universal fowarder and sysmon


12. Find olaf sysmon config and save the .xml file

13. Create a new inputs.conf file in \Program Files\SplunkUniversalForwarder\etc\system\local and save new config

<img width="745" height="508" alt="Screenshot 2026-02-10 193425" src="https://github.com/user-attachments/assets/af6821fa-a6ed-4ab5-a519-f0f178907742" />

14. Go to services, change Log On As to Local system and restart splunk universal forwarding

15. Log into splunk server and create a new index called endpoint

16. Activate splunk server by adding a new port (9997) to configure receiving setting

17. Install Active Directory Domain Services(ADDS) on the windows server
(Manage > Add roles and features > install Role-based or feature-based > Target server > select ADDS and add features > Install)

18. Promote server to domain controller
 (Add a new forest > add *domain name* > choose password > install)

19. Create organisational units and add users
(tools > active directory users and computers > right click the domain > new > organisational unit > add name > within the organisational unit rightclick > new > user > add name > add password)

20. Change DNS server on target PC
(Rightclick network icon > open network & internet settings > change adapter options > rightclick internet connection > properties > double click ipv4 > change prefered DNS server to domain controller)

21. Join target pc to the domain
(search pc > rightclick ThisPC > properties > advanced system settings > computer name > change > domain > *domain name* > login with administrator login)

22. Restart target vm and log into newly made user

23. Configure kali linux using the set ip address 
(rightclick network icon > edit connections > select first profile > select cog icon > select ipv4 settings > change method to manual > add planned ip address > dns server 8.8.8.8 > save > disconect the internet > connect back to the same internet)

24. Update kali, make new directory and install hydra
(Open terminal on the desktop > sudo apt-get update && sudo apt-get upgrade -y > mkdir ad-project > sudo apt-get install -y hydra

25. Access rockyou wordlist and move it to the new directory
(cd /usr/share/wordlists/ > sudo gunzip rockyou.txt.gz > cp rockyou.txt ~/Desktop/*directory name* > cd ~/Desktop/*directory name*)

26. Copy the first 20 lines into a new file and add the targeted password into the new file
("head -n 20 rockyou.txt > passwords.txt" > nano passwords.txt > add target password)

27. Make a new file called users.txt and add the targeted username
(echo "username" > users.txt)

28. On the target pc, enable Remote Desktop Protocol
(search this pc > click properties > select advanced system settings > log in using ADministrator account > select remote tab > sellect allow remote connections to this computer > select users > add > add users > apply changes)

29. Begin a brute force attack on the target machine
(hydra -L users.txt -P passwords.txt rdp://*target's IP*)

30. Check data on splunk server
Results: found 26 events under eventCode 4625 and 1 under 4624

<img width="999" height="377" alt="Screenshot 2026-02-12 170648" src="https://github.com/user-attachments/assets/4b15c01f-52f9-4515-9e3c-5c5b5a3074e3" />

<img width="880" height="458" alt="Screenshot 2026-02-12 170709" src="https://github.com/user-attachments/assets/fdacc0e8-7f48-46c9-9fe4-3f4bc7cec9c9" />

Event code 4625 corrresponds to "An account failed to log on" and code 4624 corresnponds to "An account was successfully logged on"

<img width="712" height="558" alt="Screenshot 2026-02-12 171205" src="https://github.com/user-attachments/assets/71ac958f-5872-4325-883a-bd056474b7f0" />

Attacker machine name and ip is also shown

32. Install Atomic Red Team (ART)
(run powershell as administrator > Set-ExecutionPolicy Bypass CurrentUser > Y > Open windows security > Virus & threat protection > Manage settings > Add or remove exclusion > Add exclusion > folder > select C:\ drive> Go back to powershell and run IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing); > Install-AtomicRedTeam -getAtomics)

33. (on powershell Invoke-AtomicTest T1136.001 (corresponds to create new local account)
    
<img width="1002" height="690" alt="Screenshot 2026-02-12 173022" src="https://github.com/user-attachments/assets/6a98ac9f-6e9d-4573-98f4-6237502b7b9c" />


Results: A new local user was detected.

<img width="1003" height="547" alt="Screenshot 2026-02-12 173359" src="https://github.com/user-attachments/assets/8043c09f-2c4d-4db5-a30c-e26b240cf7e9" />

