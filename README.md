Network Traffic Analysis with tcpdump

Project Overview

This project focuses on using tcpdump for network packet analysis on Kali Linux. It involves setting up permissions, capturing network packets, and filtering traffic based on different criteria.

Setup and Permissions

Initially, running tcpdump -i any resulted in a permission error because capturing network packets requires elevated privileges.

Verified that tcpdump was installed using which tcpdump, which returned the path /usr/bin/tcpdump.

To allow the user to run tcpdump without root privileges, the user was added to the netdev group using sudo usermod -aG netdev $USER.

Further, capabilities were granted using sudo setcap cap_net_raw,cap_net_admin=eip $(which tcpdump), enabling packet capture without needing sudo.

Running tcpdump

After setting up permissions, tcpdump -i any was executed. It displayed a warning that the "any" device does not support promiscuous mode, but packet capture worked.

Network packets were successfully captured, including details like source and destination IP addresses, protocol types, flags (SYN, ACK, etc.), and port numbers.

Filtering Traffic

To analyze specific types of network traffic, different filters were used:

Capturing all packets using tcpdump -i any.

Capturing traffic to and from a specific IP using tcpdump -i any host 192.168.1.100. No packets were captured, indicating no communication with this IP.

Capturing only TCP traffic using tcpdump -i any tcp.

Capturing only UDP traffic using tcpdump -i any udp.

Capturing only DNS traffic by filtering port 53 using tcpdump -i any port 53.

Observations

The captured packets showed details such as source and destination IP addresses, protocols (TCP, UDP, DNS), port numbers (e.g., 80 for HTTP, 443 for HTTPS), and specific request data.

No packets were captured for the specific IP 192.168.1.100, meaning no active communication was detected.

Various types of network traffic, including HTTPS, DNS queries, and other requests, were successfully recorded and analyzed.

Conclusion

This project successfully demonstrates how to set up and use tcpdump for network traffic analysis on Kali Linux. By configuring permissions and applying filters, effective packet capture and analysis were performed. This approach can be used for network monitoring, security auditing, and troubleshooting connectivity issues.
