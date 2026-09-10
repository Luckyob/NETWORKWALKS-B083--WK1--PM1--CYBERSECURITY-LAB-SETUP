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

image

### Step 5. Configure the Kali Linux Network
The network configuration was checked and configured with a consistent IPv4 address.

![Uploading Screenshot_2026-09-10_23-35-38.png…]()
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

## Problems Encountered and Solutions

### Problem 1. Kali Network Interface Not Showing the Expected IP

During the network configuration process, the Kali VM did not initially display the expected IPv4 address on the `eth0` interface.

The network configuration was checked using:

```bash
ip a
```

The VirtualBox adapter configuration and Kali network connection were then reviewed to identify the cause.

This demonstrated the importance of checking both the virtual network configuration and the operating system network configuration when troubleshooting connectivity.

### Problem 2. Hotspot Connectivity

The Kali VM was also tested using the host computer's Internet connection through a mobile hotspot.

When connectivity did not work as expected, the network adapter, IP configuration, and routing information were checked using:

```bash
ip a
ip route
```

Connectivity was then tested using:

```bash
ping 8.8.8.8
```

This helped determine whether the problem was related to the VM interface, routing, DNS, or the VirtualBox network configuration.

## Screenshots

### 1. VirtualBox NAT Network

**VirtualBox NAT Network** (`1-nat-network.png`)

This screenshot shows the NAT Network configuration used for the cybersecurity laboratory.

![VirtualBox NAT Network](images/1-nat-network.png)

### 2. Kali Linux Virtual Machine

**Kali Linux** (`2-kali-linux.png`)

This screenshot shows the Kali Linux virtual machine running inside VirtualBox.

![Kali Linux](images/2-kali-linux.png)

### 3. Kali Linux Network Configuration

**Kali Network Configuration** (`3-kali-network.png`)

This screenshot shows the network configuration of the Kali Linux virtual machine.

![Kali Network Configuration](images/3-kali-network.png)

### 4. Network Verification

**Network Verification** (`4-network-verification.png`)

This screenshot shows the network verification commands and results.

![Network Verification](images/4-network-verification.png)

### 5. Virtual Machine Snapshot

**VirtualBox Snapshot** (`5-vm-snapshot.png`)

This screenshot shows the clean snapshot created after completing the initial laboratory setup.

![VirtualBox Snapshot](images/5-vm-snapshot.png)

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
