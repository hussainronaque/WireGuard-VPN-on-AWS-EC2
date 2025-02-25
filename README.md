# **WireGuard VPN on AWS EC2**

A complete guide and implementation of a secure Virtual Private Network (VPN) using **WireGuard** on an **AWS EC2** instance. This project explores modern network security practices with a focus on high performance, ease of configuration, and robust encryption.  

**[Read our full research paper here](./Paper/Security-at-Network-Layer-IPSec-and-VPNs.pdf)**

---

## **Overview of the Project**

This project demonstrates how to deploy a WireGuard VPN server on an AWS EC2 instance. The VPN allows secure, encrypted connections over public networks, ensuring data privacy and protection from cyber threats.  

It includes:  
- A server setup on AWS EC2 running **Ubuntu 20.04**  
- End-to-end encrypted connections using **WireGuard**  
- A thorough comparison between **IPSec** and **WireGuard** protocols  
- Automated configuration scripts for easy deployment  

---

## **Why WireGuard?**

WireGuard is a next-generation VPN protocol designed to replace older protocols like IPSec and OpenVPN. Here’s why it stands out:

- **High Performance**: Uses state-of-the-art cryptographic primitives (e.g., ChaCha20 for encryption) that are faster than traditional algorithms used in IPSec.  
- **Robust Security**: Simpler codebase (~4000 lines) reduces the chances of security flaws.  
- **Easy Configuration**: Straightforward setup with minimal configuration needed.  
- **Cross-Platform Support**: Compatible with Linux, macOS, Windows, iOS, and Android.  
- **Seamless Roaming**: Maintains connection across network changes without interruptions.  

---

## **Features of the VPN Setup**

- **Secure tunneling of internet traffic through AWS EC2**  
- **End-to-end encryption with modern cryptographic techniques**  
- **Bypass geographical restrictions**  
- **Minimalistic, efficient configuration**  
- **Easy client setup with pre-configured scripts**  

---

## **How to Set Up**

### **Requirements**

1. An account on a cloud platform that offers a virtual machine (e.g. AWS, Azure, Google Cloud, etc.).
2. Ubuntu 20.04 Server Virtual Machine.
3. A public IP address assigned to your VM.
4. UDP port 51820 open to incoming traffic from all sources (0.0.0.0/0).
5. The region chosen to raise the machine in this tutorial was South America (São Paulo, Brazil) (sa-east-1), but choose your preferred region.

### **Server Setup (AWS EC2)**

1. Launch an EC2 instance with **Ubuntu 20.04**.
2. Allow inbound traffic on **UDP port 51820**.
3. Connect to your instance via SSH and run:
   ```bash
   sudo apt update && sudo apt install wireguard -y
   ```
4. Generate server keys:
   ```bash
   wg genkey | sudo tee /etc/wireguard/privatekey | wg pubkey | sudo tee /etc/wireguard/publickey
   ```
5. Configure WireGuard (/etc/wireguard/wg0.conf):
   ```bash
   [Interface]
   Address = 10.0.0.1/24
   SaveConfig = true
   ListenPort = 51820
   PrivateKey = <your-server-private-key>
   PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
   PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
   ```

6. Start the service:
   ```bash
   sudo systemctl enable wg-quick@wg0
   sudo systemctl start wg-quick@wg0
   ```

### **Client Setup**
1. Install WireGuard:
   ```bash
   sudo apt update && sudo apt install wireguard -y
   ```
2. Generate client keys and configure /etc/wireguard/wg0.conf:
   ```bash
   [Interface]
   PrivateKey = <your-client-private-key>
   Address = 10.0.0.2/24

   [Peer]
   PublicKey = <server-public-key>
   Endpoint = <AWS-EC2-Public-IP>:51820
   AllowedIPs = 0.0.0.0/0`
   ```
3. Connect to the VPN:
   ```bash
   sudo wg-quick up wg0
   ```

### **Testing the Connection**

1. Ping the Server
   From the client, ping the server's virtual IP to test the connection:
   ```bash
   ping 10.0.0.1
   ```
   If the connection is successful, you should see replies from the server.

2. Check Your IP
   Verify that your traffic is routed through the VPN by visiting:
   https://whatismyipaddress.com
   The displayed IP should match the server's public IP, confirming that the VPN is working.


