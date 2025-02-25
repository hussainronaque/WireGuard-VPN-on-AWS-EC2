# 🔒 **WireGuard VPN on AWS EC2**

A complete guide and implementation of a secure Virtual Private Network (VPN) using **WireGuard** on an **AWS EC2** instance. This project explores modern network security practices with a focus on high performance, ease of configuration, and robust encryption.  

📄 **[Read our full research paper here](./paper/Security-at-Network-Layer-IPSec-and-VPNs.pdf)**

---

## 🌐 **Overview of the Project**

This project demonstrates how to deploy a WireGuard VPN server on an AWS EC2 instance. The VPN allows secure, encrypted connections over public networks, ensuring data privacy and protection from cyber threats.  

It includes:  
- A server setup on AWS EC2 running **Ubuntu 20.04**  
- End-to-end encrypted connections using **WireGuard**  
- A thorough comparison between **IPSec** and **WireGuard** protocols  
- Automated configuration scripts for easy deployment  

---

## 🔑 **Why WireGuard?**

WireGuard is a next-generation VPN protocol designed to replace older protocols like IPSec and OpenVPN. Here’s why it stands out:

- ⚡ **High Performance**: Uses state-of-the-art cryptographic primitives (e.g., ChaCha20 for encryption) that are faster than traditional algorithms used in IPSec.  
- 🔒 **Robust Security**: Simpler codebase (~4000 lines) reduces the chances of security flaws.  
- 🛠️ **Easy Configuration**: Straightforward setup with minimal configuration needed.  
- 📱 **Cross-Platform Support**: Compatible with Linux, macOS, Windows, iOS, and Android.  
- 🌍 **Seamless Roaming**: Maintains connection across network changes without interruptions.  

---

## 🚀 **Features of the VPN Setup**

- ✅ **Secure tunneling of internet traffic through AWS EC2**  
- 🔐 **End-to-end encryption with modern cryptographic techniques**  
- 🌍 **Bypass geographical restrictions**  
- 🔧 **Minimalistic, efficient configuration**  
- 📡 **Easy client setup with pre-configured scripts**  

---

## ⚙️ **How to Set Up**

### 🖥️ **Server Setup (AWS EC2)**

1. Launch an EC2 instance with **Ubuntu 20.04**.
2. Allow inbound traffic on **UDP port 51820**.
3. Connect to your instance via SSH and run:
   ```bash
   sudo apt update && sudo apt install wireguard -y
rea
