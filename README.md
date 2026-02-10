# Active Directory

## Objective

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned



### Tools Used

- VirtualBox as a vitual machine host
- Windows 10, Ubuntu server, Kali Linux, and Windows server 2022 as Operating systems
- Splunk is used as the SIEM

## Steps
1. Create a Network Diagram to plan out the structure of the lab environment

<img width="1011" height="809" alt="Screenshot 2026-02-10 165157" src="https://github.com/user-attachments/assets/fa5ead9b-8c5d-41a7-bb24-16eb3b4ded6d" />


2. Download and install all necessary VM Systems
   
<img width="951" height="747" alt="Screenshot 2026-02-10 183533" src="https://github.com/user-attachments/assets/dac76541-4181-4b34-8d9f-a4bf901518b5" />

   2.5. Sudo apt-get update && Sudo apt-get upgrade -y on ubuntu server
   
3. Set up a NAT Network with planned IP address and connect all VMs to that network

<img width="959" height="741" alt="Screenshot 2026-02-10 183804" src="https://github.com/user-attachments/assets/ffefe516-927d-41d9-9f29-1a53f1dd339f" />

4. configure splunk server to the designated ip address by changing the .yaml file

<img width="797" height="661" alt="Screenshot 2026-02-10 183854" src="https://github.com/user-attachments/assets/594cea97-85a7-47fb-b9d9-4fa0f9bcbd4d" />

5. Install virtualbox packages, add a shared directory and add a new user to vbox
(sudo apt-get install virtualbox-guest-additions-iso)(sudo apt-get install virtualbox-guest-utils)(sudo adduser *username* vboxsf)

6. Make a new directory and mount the shared directory to the newly created one
(sudo mount -t vboxsf -o uid=1000,gid=1000 *shared directory* *new directory*

7. move to the new directory and install splunk package
(cd *new directory*) (sudo dpkg -i splunk-*verions of splunk*)

8. Set up splunk server by moving to splunk directory and change user to splunk to gain permissions
(cd /opt/splunk) (sudo -u splunk bash)

9. move to bin directory and run the installer
(cd bin) (./splunk start)

10. automate splunk server startup by changing back to default user and moving to bin directory
(exit) (cd bin) (sudo ./splunk enable boot-start -user splunk)

11. Configure target vm and windows server by installing splunk universal fowarder and sysmon


12. find olaf sysmon config and save the .xml file

13. create a new inputs.conf file in \Program Files\SplunkUniversalForwarder\etc\system\local and save new config

<img width="745" height="508" alt="Screenshot 2026-02-10 193425" src="https://github.com/user-attachments/assets/af6821fa-a6ed-4ab5-a519-f0f178907742" />

14. go to services, change Log On As to Local system and restart splunk universal forwarding


15. log into splunk server and create a new index called endpoint

16. activate splunk server by adding a new port (9997) to configure receiving setting


17. Create  user accounts though windows server under organisational units


18. configure kali linux using the set ip address and install crowbar


19. enabe rdp on the target vm


20. 
