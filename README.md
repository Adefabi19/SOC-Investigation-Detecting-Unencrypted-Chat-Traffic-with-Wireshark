# Wireshark Network Traffic Analysis

## Project Overview

This project demonstrates practical network traffic analysis using Wireshark. The objective was to investigate captured network traffic, identify non-web TCP communication, and analyze a plain-text office chat application.

## Objectives

- Identify and filter TCP traffic.
- Exclude HTTP (port 80) and HTTPS (port 443) traffic.
- Identify an unencrypted office chat application.
- Determine the TCP port used by the chat application.
- Identify the computer that initiated the TCP connection.
- Analyze the conversation using Follow TCP Stream.

## Tools Used

- Wireshark
- PCAP network capture
- TCP display filters

## Investigation and Findings

### 1. Filtering TCP Traffic

Display filter:

```wireshark
tcp.port != 80 && tcp.port != 443 && tcp.len > 0
```

This filter excludes HTTP and HTTPS traffic and displays TCP packets containing payload data.

### 2. Identifying the Office Chat Application

The investigation identified TCP port **5000** as the port used by the plain-text office chat application.

Display filter:

```wireshark
tcp.port == 5000
```

### 3. Identifying the Connection Initiator

Display filter:

```wireshark
tcp.port == 5000 && tcp.flags.syn == 1 && tcp.flags.ack == 0
```

The source IP address of the initial SYN packet identifies the computer that initiated the TCP connection.

**Source IP:** [Insert discovered IP address]

### 4. Analyzing the TCP Conversation

Using:

Right-click packet → Follow → TCP Stream

The conversation was inspected to identify readable, unencrypted chat messages.

**Total conversation size:** [Insert byte count from Wireshark]

## Key Learning Outcomes

- Understanding TCP display filters.
- Identifying non-standard TCP ports.
- Understanding TCP three-way handshake initiation.
- Identifying source and destination IP addresses.
- Analyzing unencrypted application-layer communication.
- Following TCP streams to reconstruct conversations.

## Conclusion

This investigation demonstrated how Wireshark can be used to identify non-web network traffic, determine connection initiators, and inspect plain-text application communication.

The exercise highlights the importance of encryption in protecting sensitive information transmitted over networks.

---

**Disclaimer:** This analysis was performed on an authorized network capture for educational purposes. Any packet captures shared publicly should be sanitized to remove sensitive information.
