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

<img width="959" height="806" alt="image" src="https://github.com/user-attachments/assets/a0d74d37-8f99-4832-8366-f472c7ccc0f9](https://github.com/Tsugi321/Active-Directory/blob/main/Screenshot%202026-02-10%20165157.png" />

2. Download and install all necessary VM Systems

   2.5. Sudo apt-get update && Sudo apt-get upgrade -y on ubuntu server
4. Set up a NAT Network with planned IP address and connect all VMs to that network
5. configure splunk server to the designated ip address
6. Set up splunk using a shared directory
7. Configure target vm and windows server by installing splunk universal fowarder and sysmon
8. Create  user accounts though windows server under organisational units
9. configure kali linux using the set ip address and install crowbar
10. enabe rdp on the target vm
11. 
