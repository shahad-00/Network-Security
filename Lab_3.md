# Lab 3: Network Scanning Using Nmap

## Objectives

- Learn how to scan a network.
- Identify open ports and services.
- Understand basic security risks.

## Tools

- Nmap
- Windows Command Prompt
- ipconfig

## Practical Tasks

### 1. Scan Your Local Host

    nmap 127.0.0.1

<img width="655" height="366" alt="Picture1" src="https://github.com/user-attachments/assets/6e37f91d-2898-48fb-b9aa-eb0ca54dbcd2" />


**Explanation:** This command scans the local computer through its loopback address.

The scan reports five open TCP ports:

| Port | State | Service Label |
| --- | --- | --- |
| 135 | Open | msrpc |
| 445 | Open | microsoft-ds |
| 4343 | Open | unicall |
| 4449 | Open | privatewire |
| 8000 | Open | http-alt |

The remaining 995 scanned TCP ports are reported as closed.

**Clarification:** Without service-version detection, these service labels are based primarily on port-number mappings. They do not independently confirm which applications are listening.

### 2. Identify the Network Configuration

    ipconfig

<img width="338" height="323" alt="Picture2" src="https://github.com/user-attachments/assets/3b43500b-8646-46c9-8c25-52d62a0ec029" />


**Image explanation:** The command lists the computer’s network adapters and their IP configurations. One adapter has the address 192.168.56.1 and no default gateway.

<img width="391" height="253" alt="Picture3" src="https://github.com/user-attachments/assets/dbfd0775-7a74-4266-bfbe-4fdf9d207d15" />


**Image explanation:** The Wi-Fi adapter displays:

- IPv4 address: 192.168.1.10
- Subnet mask: 255.255.255.0
- Default gateway: 192.168.1.1

The default gateway address was used as the target for the next scans.

### 3. Scan Another Device

    nmap -Pn 192.168.1.1

<img width="633" height="322" alt="Picture4" src="https://github.com/user-attachments/assets/958fb4f9-f8bd-4d3f-96ea-03e68b85b92a" />


**Explanation:** This command scans the gateway while skipping host discovery.

| Port | State | Service Label |
| --- | --- | --- |
| 22 | Filtered | ssh |
| 23 | Filtered | telnet |
| 53 | Open | domain |
| 80 | Open | http |
| 443 | Open | https |
| 8022 | Filtered | oa-system |

An open port accepted the scan’s connection probe. A filtered port could not be classified as open or closed because filtering prevented a conclusive response.

### 4. Perform an Advanced Scan

    nmap -sS -sV -O -Pn 192.168.1.1

<img width="797" height="587" alt="Screenshot 2026-10-21 014642" src="https://github.com/user-attachments/assets/6e1f03d8-9e7c-469e-85f0-59945db19d85" />



**Image explanation:** The advanced scan combines TCP SYN scanning, service-version detection, and operating-system detection while skipping host discovery.

- -sS: Performs a TCP SYN scan.
- -sV: Probes open ports to identify services and versions.
- -O: Attempts to identify the operating system.
- -Pn: Skips host discovery.

The output identifies port 80 as running lighttpd. Some other service responses are not conclusively identified.

<img width="801" height="583" alt="image" src="https://github.com/user-attachments/assets/91097726-b64c-4442-a8a1-bbf806273a1a" />


**Image explanation:** The output continues with service-response fingerprints and reports that no exact operating-system match was found.

<img width="502" height="204" alt="Picture7" src="https://github.com/user-attachments/assets/d01e9b93-f30c-46f0-b203-3616448ca899" />


**Image explanation:** The final output reports a network distance of one hop and completion of the scan.

**Clarification:** The scan attempted OS detection, but did not conclusively identify the operating system. Fingerprint text is diagnostic output, not a confirmed OS name.

### 5. Scan the Entire Local Subnet

    nmap -Pn 192.168.1.0/24

<img width="358" height="356" alt="Picture8" src="https://github.com/user-attachments/assets/fed5bc53-896f-47d0-9a52-8dfe0355005c" />


**Image explanation:** The scan covers the local /24 subnet. The displayed results include the gateway at 192.168.1.1 and devices at 192.168.1.61 and 192.168.1.63.

The devices at 192.168.1.61 and 192.168.1.63 each show open TCP ports 49152 and 62078.

<img width="440" height="208" alt="Picture9" src="https://github.com/user-attachments/assets/2db884e0-b994-4674-8257-52e15369a33b" />


**Image explanation:** The final portion displays results for the computer at 192.168.1.10.

Its open ports include 135, 139, 445, 4343, 4449, and 8000. The scan summary reports 256 IP addresses scanned and four hosts up.

## Questions and Answers

### A. What is the purpose of Nmap?

A tool used to scan networks, find devices, detect open ports, and identify services and operating systems to help discover security issues.

### B. What is a port?

A port is a virtual endpoint used to identify and transfer data for specific applications or services, represented by numbers like 80 or 443.

### C. What does an open port mean?

It means there is an application or service running on this port that receives connections.

### D. Why do we use -Pn?

It tells Nmap to skip Ping and scan the target directly, even if it doesn’t respond, which is useful when a firewall blocks ICMP but ports are open.

**Explanation:** More precisely, -Pn skips Nmap’s host-discovery stage, which can involve probes beyond ICMP ping.

### E. What does -sV do?

This scan is used to identify the type and version of the service running on a port. It does not only check if the port is open, but also determines the exact software, such as a web server and its version.

**Clarification:** Service identification is an attempt, not a guaranteed result. Some services may remain unidentified.

### F. What service runs on port 80?

HTTP service is used for browsing unencrypted websites.

### G. Why are open ports risky?

Because it can be used by attackers to access the system or exploit vulnerabilities.

**Explanation:** The risk depends on the exposed service, its configuration, and any vulnerabilities. An open port is not automatically a vulnerability.

### H. What does OS detection (-O) do?

It tries to identify the operating system of the target device.

### I. What happens if ping is blocked?

Nmap may think the device is offline unless we use the -Pn option.

**Explanation:** Nmap may still discover a host through other probes. Blocking ICMP ping alone does not always prevent host discovery.

### J. Suggest two ways to secure a system.

- Close unnecessary ports
- Use a firewall

## Conclusion

The goal of this lab was to practice local-host, gateway, and subnet scanning using Nmap, interpret port states, examine service-detection results, and understand the capabilities and limitations of operating-system detection.
