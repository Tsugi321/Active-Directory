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
4. configure splunk server to the designated ip address
5. Set up splunk using a shared directory
6. Configure target vm and windows server by installing splunk universal fowarder and sysmon
7. Create  user accounts though windows server under organisational units
8. configure kali linux using the set ip address and install crowbar
9. enabe rdp on the target vm
10. 
