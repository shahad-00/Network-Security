# Lab 4: Password Recovery and Firewall Configuration

## Objectives

- Explore password recovery using iSunshare.
- Understand dictionary attacks and password salting.
- Test access to a web server from a virtual machine and its host.
- Distinguish web-server access errors from firewall blocking.

## Tools

- iSunshare RAR Password Genius
- VirtualBox
- Web Browser
- Internet Information Services (IIS)
- IPinfo

## Practical Lab 4 part1:
### Using isunshare software to crack the password

### Practical Result

<img width="553" height="453" alt="Picture1" src="https://github.com/user-attachments/assets/d0898e7c-0875-446a-a6f1-290fa185e93d" />


**Explanation:** iSunshare RAR Password Genius was used to recover the password of the test archive test.txt.rar. The result window reports successful recovery and an elapsed time of 4 minutes and 28 seconds.

**Clarification:** The background displays brute-force character-range settings. The screenshot does not establish that dictionary mode was used.

### 1- What is the main purpose of a dictionary attack?

The main purpose of a dictionary attack is to try a list of common passwords to find the correct password quickly.

### 2- What does salting a password do?

It adds random data to make the password harder to crack.

**Explanation:** A salt is stored with a password hash and makes identical passwords produce different hashes when different salts are used. It reduces the usefulness of precomputed hash tables but does not prevent password guessing.

## Practical Lab 4 part 2:
### Configuring Firewall

- VM machine will be our Web Server
- The host OS (your real computer) will be the client
- Make sure they are all in the same network

### Access Test Inside the Virtual Machine

<img width="510" height="370" alt="Picture2" src="https://github.com/user-attachments/assets/8956e96e-548a-45cf-b61b-0211a25f4025" />


**Explanation:** The browser inside the Windows 7 virtual machine accesses the web server at 172.20.10.2:4444. IIS returns HTTP Error 401.3 — Unauthorized, indicating that access is denied because of resource permissions or access-control settings.

The response demonstrates that the request reached IIS. It does not show a firewall blocking the connection.

### Access Test from the Host Computer

<img width="570" height="93" alt="Picture3" src="https://github.com/user-attachments/assets/c6b56ba1-eb12-4d3c-bff9-7519c3b79af4" />


**Explanation:** The host browser accesses the same server address and receives a 401 Unauthorized response stating that access is denied due to invalid credentials.

This shows that the server responded to the host’s request, but access was not authorized.

### IP Address Inspection

<img width="603" height="319" alt="Picture4" src="https://github.com/user-attachments/assets/ab2ca20a-6832-4929-9385-3ec43e2c6d46" />


**Explanation:** IPinfo identifies 172.20.10.2 as a private or reserved address. It falls within the private IPv4 range 172.16.0.0/12.

This lookup provides address information; it does not test connectivity or verify firewall rules.

### 1- Why must the host and VM be on the same network?

Because they need to communicate and access each other

**Explanation:** In this lab setup, the host needs a reachable network path to the VM’s web server. Devices can also communicate across different networks when routing and access rules permit it.

### 2- What is the main function of a firewall?

To monitor and control network traffic and block unauthorized access.

### Result Clarification

The screenshots document server responses from both browsers. They do not display firewall rules or a before-and-after blocking test, so successful firewall configuration cannot be independently verified from these images.

## Conclusion

The goal of this lab was to explore password recovery, understand dictionary attacks and password salting, and practice testing access between a host and a virtual web server while distinguishing server authorization errors from firewall restrictions.
