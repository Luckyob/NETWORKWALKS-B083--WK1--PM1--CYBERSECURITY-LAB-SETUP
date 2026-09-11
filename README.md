# Cybersecurity Virtual Lab Setup

Building an isolated cybersecurity laboratory using VirtualBox and Kali Linux for ethical hacking and security testing.

## Project Overview

This project documents the setup of an isolated virtual cybersecurity laboratory using VirtualBox and Kali Linux.

The lab is designed as a controlled environment for learning cybersecurity concepts, network reconnaissance, vulnerability assessment, penetration testing techniques, and security tool usage.

A private virtual network is used to allow additional virtual machines to be connected later as authorized targets for testing.

## Objectives

The main objectives of this project are to:

- Install and configure VirtualBox
- Install and configure Kali Linux
- Create a private NAT Network
- Configure Kali Linux network connectivity
- Configure IPv4 addressing
- Verify network communication
- Test Internet and DNS connectivity
- Create a clean VM snapshot
- Document the laboratory setup
- Prepare the environment for future penetration testing exercises

## Purpose of the Lab

The laboratory provides an isolated environment for practicing cybersecurity and ethical hacking techniques.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Network analysis
- Vulnerability assessment
- Web security testing
- Packet analysis
- Exploitation practice
- Security tool experimentation

> **Important:** All security testing should only be performed against systems that you own or have explicit authorization to test.

## Lab Architecture



<img width="1366" height="662" alt="Screenshot_2026-09-10_23-54-29" src="https://github.com/user-attachments/assets/4a1600e1-c5fd-470d-ad03-a46403b4b335" />

                
## Lab Configuration

| Component | Configuration |
|---|---|
| Host OS | Windows 10 |
| Hypervisor | VirtualBox 7.2 |
| Security OS | Kali Linux 2026.2 |
| Virtual Network | NAT Network |
| Network Address | `10.0.0.0/24` |
| Gateway | `10.0.0.1` |
| DNS Server | `8.8.8.8` |
| Future Target Range | `10.0.0.3 - 10.0.0.99` |


## Lab Setup Procedure

### Step 1. Install 7-Zip and VirtualBox 
7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a .7z archive.

Tool: 7-Zip

VirtualBox was installed and configured as the hypervisor for the cybersecurity laboratory.

VirtualBox allows multiple operating systems to run as virtual machines on the host computer.
<img width="1366" height="728" alt="image" src="https://github.com/user-attachments/assets/adcd5183-c9a2-4549-ae2d-06c7851e8394" />

### Step 2. Install Kali Linux

Kali Linux was installed as the primary security testing virtual machine.

The VM was configured with the required system resources and network adapter.

### Step 3. Create the NAT Network

A dedicated NAT Network was created in VirtualBox.

**Configuration:**


<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/288cd556-7ddf-4a5e-b32a-50f45156c025" />



The NAT Network allows virtual machines connected to the same network to communicate with each other while providing external network connectivity through NAT.

This makes it suitable for creating an isolated multi-machine cybersecurity laboratory.


### Step 4. Import Kali Linux

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

<img width="1366" height="728" alt="image" src="https://github.com/user-attachments/assets/4eb48c10-172f-4672-856a-6a2afea15ffe" />


### Step 5. Configure the Kali Linux Network
The network configuration was checked and configured with a consistent IPv4 address.


<img width="701" height="550" alt="Screenshot_2026-09-10_23-32-02" src="https://github.com/user-attachments/assets/2003ba37-a7a0-4237-91ab-687cb06a759b" />


### Step 6. Create a VM Snapshot

After completing the initial configuration, a clean VirtualBox snapshot was created.

**Example snapshot name:**

```text
Kali - Initial Setup
```

The snapshot provides a known-good recovery point before performing future cybersecurity experiments.

## Lab Verification

| Test | Command | Expected Result |
|---|---|---|
| IP configuration | `ip a` | Kali IP displayed |
| Routing | `ip route` | Default route displayed |
| Gateway | `ping 10.0.0.1` | Successful replies |
| Internet | `ping 8.8.8.8` | Successful replies |
| DNS | `nslookup google.com` | Domain resolves |
| Nmap | `nmap --version` | Nmap version displayed |
| Snapshot | Restore snapshot | Baseline restored |

## Problem Encountered: eth0 Network Interface Disconnected

During the lab setup, the `eth0` network interface was not connecting to the VirtualBox NAT Network.

### Troubleshooting

I first checked the status of the network interfaces using:

```bash
nmcli device status
```
The VirtualBox adapter configuration and Kali network connection were then reviewed to identify the cause.

This demonstrated the importance of checking both the virtual network configuration and the operating system network configuration when troubleshooting connectivity.
```


The output showed that `eth0` was disconnected, while the `lo` (loopback) interface was connected.

I restarted the NetworkManager service to refresh the network configuration:

```bash
sudo systemctl restart NetworkManager
```

I then checked the IPv4 configuration of `eth0`:

```bash
ip -4 addr show eth0

After restarting NetworkManager, I rechecked the network interface status:
nmcli device status
This time, eth0 showed as connected, confirming that the network interface had successfully established a connection.
Resolution
The issue was resolved by restarting NetworkManager, which allowed eth0 to reconnect and obtain its network configuration from the VirtualBox NAT Network.
Commands Used
nmcli device status
sudo systemctl restart NetworkManager
ip -4 addr show eth0
nmcli device status
Result: eth0 successfully connected to the VirtualBox NAT Network.

```
## Screenshots

### 1. VirtualBox NAT Network

**VirtualBox NAT Network** 

This screenshot shows the NAT Network configuration used for the cybersecurity laboratory.

![VirtualBox NAT Network](images/1-nat-network.png)

### 2. Kali Linux Network Configuration

**Kali Network Configuration** 

This screenshot shows the network configuration of the Kali Linux virtual machine.

<img width="1366" height="662" alt="Screenshot_2026-09-10_23_31_22" src="https://github.com/user-attachments/assets/e0a27de8-94d4-4b09-a692-e30f645cf599" />

### 3. Network Verification

**Network Verification** 

This screenshot shows the network verification commands and results.

<img width="1366" height="627" alt="Screenshot_2026-09-11_00-04-16" src="https://github.com/user-attachments/assets/a9fe0362-0495-4a38-b125-519aa8f275d2" />

<img width="1366" height="627" alt="Screenshot_2026-09-10_23-35-38" src="https://github.com/user-attachments/assets/be605ce0-bc1d-4994-9710-859564426bb5" />


## What I Learned

Through this project, I learned how to build and configure a virtual environment for cybersecurity practice.

### 1. VirtualBox Networking

I learned how VirtualBox network modes affect communication between virtual machines and external networks.

### 2. NAT Network

I learned that a NAT Network allows multiple virtual machines to communicate with each other while also providing outbound connectivity.

### 3. IP Addressing

I learned how IPv4 addresses, subnet masks, gateways, and DNS servers work together to provide network connectivity.

### 4. Kali Linux Networking

I learned how to inspect network interfaces, routing information, and connectivity from the Kali Linux command line.

### 5. Network Troubleshooting

I learned how to troubleshoot network problems by checking the interface, IP address, routing table, gateway, and DNS separately.

### 6. Virtual Machine Snapshots

I learned the importance of creating a clean snapshot before conducting security experiments.

### 7. Cybersecurity Lab Design

I learned how to create an isolated environment where cybersecurity tools and techniques can be practiced safely.

## Security and Ethical Use

This laboratory is intended strictly for educational and authorized cybersecurity testing.

All scanning, vulnerability assessment, exploitation, and other security testing activities should only be performed against systems that I own or have explicit permission to test.

The laboratory provides a controlled environment for developing practical cybersecurity skills without targeting unauthorized systems.

## Conclusion

The virtual cybersecurity laboratory was successfully configured using VirtualBox and Kali Linux.

The environment provides a controlled platform for practicing cybersecurity concepts, testing security tools, and performing authorized penetration testing exercises.

The laboratory can be expanded in the future by adding additional virtual machines, vulnerable applications, and intentionally vulnerable target systems.

## 🔗 Tools & Resources

- **7-Zip:** https://7-zip.org/download.html
- **VirtualBox:** https://virtualbox.org/wiki/Downloads
- **Kali Linux:** https://kali.org/get-kali

## 👤 Author

**Samuel Lucky**  
Cybersecurity Professional B083

**LinkedIn:** https://www.linkedin.com/in/lucky-samuel-4bb397296

## 📌 Project Information

- **Program Name:** Cybersecurity at Networkwalks
- **Week:** 01
- **Project:** Cybersecurity & Pentesting Lab Setup
- **Repository:** GitHub
