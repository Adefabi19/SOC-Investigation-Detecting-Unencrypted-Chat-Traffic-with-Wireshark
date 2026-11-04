# Wireshark SOC Lab 5: Follow TCP Stream, Part 2

| | |
|---|---|
| **Platform** | Networkwalks |
| **Tool** | Wireshark |
| **Result** | 100/100 |

---

## Overview

In this lab I used Wireshark to investigate HTTP traffic and uncover a message hidden in an internal company webpage. It tested how well I could reconstruct web conversations from raw packets and read the application-layer content inside them.

## Scenario

A staff member visited five pages on the company intranet. An administrator suspected that one of them contained a hidden message.

As the SOC analyst, I had to inspect the HTTP traffic, find the page, and recover the hidden information.

## Methodology

### 1. Reviewing the capture

The capture contained **282 packets**, so I needed to narrow it down to the relevant web traffic.

### 2. Filtering for HTTP

I applied this display filter and reviewed the requests to see which pages the staff member visited:

```
http
```

### 3. Identifying the suspicious page

Of the five pages, `/staff.html` was the one containing the hidden message.

### 4. Reconstructing the conversation

I right-clicked a packet from the `/staff.html` exchange and selected:

```
Follow > TCP Stream
```

The conversation was **TCP stream 7**, which let me read the full request and response in one view.

### 5. Finding the hidden message

The message was inside an HTML comment, for example:

```html
<!-- Hidden information -->
```

Browsers don't render comments, so the content was invisible on the page. It was still sent in the server's response, so it was fully readable in the packet data.

### 6. Confirming the direction

The hidden note appeared in server-to-client traffic, meaning the server delivered it as part of the page response.

### 7. Identifying the download

The stream also showed a downloaded text file named `report.txt`.

## Key Findings

| Item | Result |
|---|---|
| Suspicious page | `/staff.html` |
| TCP stream | 7 |
| Hidden content location | HTML comment |
| Traffic direction | Server to client |
| Downloaded file | `report.txt` |
| Report prepared by | Nadia |

## Skills Practiced

- Packet capture analysis in Wireshark
- Display filtering and HTTP request inspection
- TCP stream reconstruction
- HTML source inspection
- Finding hidden or sensitive data in web traffic

## Key Takeaway

My background in HTML and web development helped me here. Because I knew how HTML comments work, I understood why a comment is invisible in the browser but still exposed on the wire.

Anything a server sends can be read by anyone who can capture the traffic, so sensitive information should never be left in page source, comments included.

This lab showed me how useful web development knowledge is for security investigation.

## Reference

- [Networkwalks: Wireshark Lab 5](https://networkwalks.com/wireshark-lab5/)
