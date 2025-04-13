
# 🕵️‍♂️ Network Traffic Analysis with tcpdump

## Project Overview

This project focuses on using **tcpdump** for **network packet analysis** on Kali Linux. It involves setting up permissions, capturing network packets, and filtering traffic based on various criteria to observe different types of network traffic.

---

## 🛠 Setup and Permissions

### Initial Setup
Initially, running the command:
```bash
tcpdump -i any
```
resulted in a **permission error** because capturing network packets requires elevated privileges.

### Installation Check
Verified that tcpdump was installed by checking its path:
```bash
which tcpdump
```
Output:
```bash
/usr/bin/tcpdump
```

### Granting Necessary Permissions
To run tcpdump without root privileges:
1. Added the user to the `netdev` group:
    ```bash
    sudo usermod -aG netdev $USER
    ```

2. Set the necessary capabilities to allow tcpdump packet capture without requiring `sudo`:
    ```bash
    sudo setcap cap_net_raw,cap_net_admin=eip $(which tcpdump)
    ```

---

## 🚀 Running tcpdump

After setting up the permissions, we ran:
```bash
tcpdump -i any
```

- A warning appeared stating that the "any" device does not support promiscuous mode, but **packet capture worked successfully**.

### Captured Information
The following packet details were captured:
- **Source and Destination IP addresses**
- **Protocol types** (TCP, UDP, DNS)
- **Flags** (SYN, ACK, etc.)
- **Port numbers** (e.g., 80 for HTTP, 443 for HTTPS)

---

## 🔎 Filtering Traffic

We used various filters to capture specific types of network traffic:

1. **Capture all network traffic**:
    ```bash
    tcpdump -i any
    ```

2. **Capture traffic to/from a specific IP**:
    ```bash
    tcpdump -i any host 192.168.1.100
    ```
    - No packets were captured for this IP, indicating no active communication.

3. **Capture only TCP traffic**:
    ```bash
    tcpdump -i any tcp
    ```

4. **Capture only UDP traffic**:
    ```bash
    tcpdump -i any udp
    ```

5. **Capture DNS traffic** (filtering port 53):
    ```bash
    tcpdump -i any port 53
    ```

---

## 🧐 Observations

- **Captured Packets**: The captured packets showed details like source/destination IPs, protocols (TCP, UDP, DNS), port numbers (e.g., 80 for HTTP, 443 for HTTPS), and specific request data.
- **No Communication with Specific IP**: No packets were captured for IP `192.168.1.100`, meaning there was no communication detected with this host.
- **Diverse Traffic**: Various network traffic types, including **HTTPS**, **DNS queries**, and other requests, were successfully captured and analyzed.

---

## 🏁 Conclusion

This project successfully demonstrates how to set up and use **tcpdump** for **network traffic analysis** on **Kali Linux**. By configuring the necessary permissions and applying filters, effective packet capture and analysis were performed. This approach can be applied for:
- **Network monitoring**
- **Security auditing**
- **Troubleshooting connectivity issues**

This tool is a valuable resource for understanding and analyzing network traffic in real-time.
