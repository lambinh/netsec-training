
##  Basic Nmap commands

Nmap, or Network Mapper, is a powerful open-source tool for network scanning and security auditing. With Nmap, you can detect devices on a network, discover open ports, identify the operating system and services running, and detect vulnerabilities. This training guide will provide you with the essentials of using Nmap for IPv4, IPv6, and vulnerability scanning.

Remember: Always use Nmap responsibly, and only scan networks where you have explicit permission to do so. Unauthorized scanning can be considered illegal and unethical.

### 1. Target Selection

Specify the targets of your Nmap scan using these commands:

Scan a range of IPs:

-   IPv4: `nmap 192.168.1.10-200`
-   IPv6: `nmap 2001:db8::1-200`

Scan a subnet:

-   IPv4: `nmap 192.168.1.0/24`
-   IPv6: `nmap 2001:db8::/64`
-   Scan targets from a text file: `nmap -iL hosts.txt`

### 2. Port Selection

Choose specific ports to scan with these commands:

Scan a range of ports:

-   IPv4: `nmap -p 1-100 192.168.1.11`
-   IPv6: `nmap -p 1-100 2001:db8::11`

Scan 100 most common ports:

-   IPv4: `nmap -F 192.168.1.11`
-   IPv6: `nmap -F 2001:db8::11`

Scan all ports:

-   IPv4: `nmap -p- 192.168.1.11`
-   IPv6: `nmap -p- 2001:db8::11`

Specify UDP or TCP scan:

-   IPv4: `nmap -p U:137,T:139 192.168.1.11`
-   IPv6: `nmap -p U:137,T:139 2001:db8::11`

### 3. Scan Types

Choose the type of scan you wish to perform:

Scan using TCP SYN scan:

-   IPv4: `nmap -sS 192.168.1.11`
-   IPv6: `nmap -6 -sS 2001:db8::11`

Scan UDP ports:

-   IPv4: `nmap -sU -p 123,161,162 192.168.1.11`
-   IPv6: `nmap -6 -sU -p 123,161,162 2001:db8::11`

Scan selected ports (Ignore Discovery):

-   IPv4: `nmap -Pn -F 192.168.1.11`
-   IPv6: `nmap -6 -Pn -F 2001:db8::11`

### 4. Service and OS Detection

Detect operating systems and services:

Detect OS and Services:

-   IPv4: `nmap -A 192.168.1.11`
-   IPv6: `nmap -6 -A 2001:db8::11`

Standard service detection:

-   IPv4: `nmap -sV 192.168.1.11`
-   IPv6: `nmap -6 -sV 2001:db8::11`

Aggressive service detection:

-   IPv4: `nmap -sV --version-intensity 5 192.168.1.11`
-   IPv6: `nmap -6 -sV --version-intensity 5 2001:db8::11`

### 5. Output Formats

Choose how to save your scan results:

Save default output to a file:

-   IPv4: `nmap -oN result.txt 192.168.1.11`
-   IPv6: `nmap -oN result.txt 2001:db8::11`

Save results as XML:

-   IPv4: `nmap -oX result.xml 192.168.1.11`
-   IPv6: `nmap -oX result.xml 2001:db8::11`

Save results in Grepable format:

-   IPv4: `nmap -oG result.gnmap 192.168.1.11`
-   IPv6: `nmap -oG result.gnmap 2001:db8::11`

Save in all formats:

-   IPv4: `nmap -oA allformats 192.168.1.11`
-   IPv6: `nmap -oA allformats 2001:db8::11`

### 6. Vulnerability Scanning

Nmap can also be used to perform vulnerability scanning, thanks to the Nmap Scripting Engine (NSE). Use these commands to identify vulnerabilities:

Scan using the `vulscan` script:

-   IPv4: `nmap --script vulscan/vulscan.nse 192.168.1.11`
-   IPv6: `nmap -6 --script vulscan/vulscan.nse 2001:db8::11`

Scan using the `vuln` category scripts:

-   IPv4: `nmap --script vuln 192.168.1.11`
-   IPv6: `nmap -6 --script vuln 2001:db8::11`

Running a vulnerability scan requires administrative privileges, and the effectiveness of the scan largely depends on the quality and breadth of the scripts used. Use them as part of a larger security evaluation process.

Warning: Running a vulnerability scan can be seen as aggressive and potentially illegal on networks where you do not have explicit permission to do so. Always obtain proper authorization before conducting any vulnerability scanning.

### 7. Advanced Scanning Techniques

Nmap can be used to perform advanced scanning techniques, which may help in identifying potential vulnerabilities or misconfigurations.

Several ports are often targeted in DDoS attacks due to the services that commonly run on them. They include:

-   Port 19 (Chargen Protocol): The chargen protocol can be used as a reflector in DDoS attacks.
-   Port 53 (DNS): Open DNS resolvers can be used to launch amplified reflection DDoS attacks.
-   Port 123 (NTP): Certain older versions of NTP (Network Time Protocol) are vulnerable to being used in amplified reflection DDoS attacks.
-   Port 161/162 (SNMP): Simple Network Management Protocol (SNMP) can be used in amplified reflection DDoS attacks.
-   Port 389 (LDAP): The Lightweight Directory Access Protocol (LDAP) service on this port can be used for DDoS attacks if it is incorrectly configured.
-   Port 1900 (SSDP): The Simple Service Discovery Protocol (SSDP) can be used in DDoS attacks, especially if the service is publicly accessible from the internet.
-   Port 3478 and 3479 (STUN/TURN): These are used in VoIP services and can be exploited for DDoS attacks.
-   Port 11211 (Memcached): Memcached on UDP port 11211 is used for caching data but can be repurposed to launch powerful DDoS attacks.

For a comprehensive scan for potential DDoS reflectors across these commonly targeted ports, the command would be:

-   IPv4: 
```
nmap -sU -A -PN -n -pU:19,53,123,161,162,1900,389,3478,3479,11211 --script=ntp-monlist,dns-recursion,snmp-sysdescr 192.168.1.0/24
```

This command uses Nmap’s scripting engine to check for services with potential for UDP-based Distributed Denial of Service (DDoS) attacks. The `-sU` switch is used for UDP scan. The `-A` switch enables OS detection, version detection, script scanning, and traceroute. `-PN` treats all hosts as online (skips host discovery). `-n` disables DNS resolution.

Please note that this kind of scan may be intrusive and could cause issues on the network. Always obtain proper authorization and understand the impact before conducting this kind of scanning.

### 8. One line command to find live hosts:

Find live ipv4 hosts from the network, and save to live_hosts.txt

```bash
nmap -sP -n -oX  out.xml 192.168.1.0/24 | grep "Nmap" | cut -d " " -f 5 >live_hosts.txt
```

**Please remember to always perform these scans responsibly and with the appropriate permissions.**