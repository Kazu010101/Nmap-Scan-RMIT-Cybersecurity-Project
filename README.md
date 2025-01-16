# Nmap-Scan-RMIT-Cybersecurity-Project
One of the red teaming activities for my RMIT Cybersecurity Project

## Objective

As part of implementing cybersecurity testing concepts and procedures, nmap scan was conducted using Kali Linux VM launched from the XYZ Company's Office network, simulating a malicious guest. The idea is to demonstrate to the client that having unsegmented network between internal staff and the guest improves the risk of cyber attacks, especially in the initial environment without any IPS or cybersecurity tools in place. Nmap is a popular network scanning tool which is crucial for any attackers to collect information from the target and detect potential vulnerabilities in the network. 

![red team lab nmap](https://github.com/user-attachments/assets/092e32ce-cdae-4509-8172-231a3503be58)

*Figure 1: In this scenario, the attacker has successfully gained Wifi access to the network to conduct active reconnaisance using nmap scan.*

## Lab Setup

![nmap scan red team](https://github.com/user-attachments/assets/b2a83336-6849-4f89-84b0-6fa195d3352a)

*Figure 2: To simulate this lab, 2 Virtual Machines were used: Windows 10 (the victim) and Kali Linux (the attacker). Both virtual machine's network configuration are set to "internal network" and class C private IP address are statically configured on both machines, simulating a private IP address network.*

![red team nmap ping](https://github.com/user-attachments/assets/15c140a0-bbf8-4309-bdb3-959d8a875737)

*Figure 3: Both Windows 10 (192.168.1.5) and Kali Linux (192.168.1.33) are verified can ping with each other.*

## Nmap Scan commands

Once verified that both machines could ping each other, the following nmap scan commands were launched:

- nmap -sP 192.168.1.0/24

![nmap scan 2](https://github.com/user-attachments/assets/54266725-36b4-4e84-a004-762370df1211)

*Figure 4: Scanning the 192.168.1.0/24 network allows the attacker to detect the presence of Windows 10 VM (192.168.1.5).*

- nmap -sT -v -p0 192.168.1.5
  
![nmap scan 4](https://github.com/user-attachments/assets/fb9b12fb-1620-4160-a881-e612c702cc80)

*Figure 5: Further scan against 192.168.1.5 discovers open ports on the host.*

-nmap -O 192.168.1.5

![nmap scan 5](https://github.com/user-attachments/assets/12e2ede9-be25-49bd-b7c1-1ccda79c81d0)

*Figure 6: This command scans for the Operating System of the host machine; it identifies the host's OS is Windows 10.*

## Result

The most important information from the nmap scan is that there are 3 open TCP ports, which are 135, 139, and 445. Considering that the target also uses Windows 10 OS, these information suggest that the host is running a file sharing service such as SMB protocol, which can be further exploited by the attacker.

## Mitigation

- The Office Network needs to be subnetted into at least two subnets, each seperately for the internal staff and the guest.
- Additional security tools such as IPS and firewalls are required to protect internal staff network from malicious traffic originiating from outside and guest network.
- Additions of network devices such as pfSense Router is required so that ACL can be set up to prevent the flow of traffic from guest network entering the internal staff network.

