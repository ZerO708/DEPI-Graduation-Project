
# Advanced Usage of Tools for Bug Hunting and Penetration Testing

## Reconnaissance
### 1. **Nmap**
- **Purpose**: Network scanning and enumeration.
- **Usage**:
  ```bash
  # Basic scan
  nmap -v -A <target>

  # Specific port scan
  nmap -p 80,443 <target>

  # Discover hosts in a subnet
  nmap -sn 192.168.1.0/24
  ```
- **Pro Tips**:
  - Use the `-oN` option to save results in a readable format.
  - Combine with `-script` for vulnerability detection, e.g., `nmap --script vuln <target>`.

---

### 2. **Shodan**
- **Purpose**: Finding internet-connected devices and services.
- **Usage**:
  - Use the [Shodan CLI](https://cli.shodan.io/) or web interface.
  ```bash
  # Search for services on a target IP
  shodan host <IP>

  # Find vulnerable services globally
  shodan search "Apache 2.4.7"
  ```
- **Pro Tips**:
  - Create saved searches for recurring audits.
  - Monitor exposed services using Shodan alerts.

---

## Web Application Testing
### 3. **Burp Suite**
- **Purpose**: Intercepting, analyzing, and modifying HTTP traffic.
- **Usage**:
  1. Configure your browser to use Burp as a proxy.
  2. Intercept traffic in the "Proxy" tab.
  3. Test for vulnerabilities:
     - SQL Injection: Use "Intruder" to inject payloads into parameters.
     - XSS: Inject `<script>alert(1)</script>` into inputs and observe results.
- **Pro Tips**:
  - Leverage the "Repeater" to test API endpoints manually.
  - Use the "Scanner" for automated vulnerability detection.

---

### 4. **OWASP ZAP**
- **Purpose**: Automated and manual web app security testing.
- **Usage**:
  - Start a scan:
    ```bash
    zap.sh -quickurl <URL>
    ```
  - Use "Active Scan" to detect vulnerabilities like XSS or CSRF.
- **Pro Tips**:
  - Integrate ZAP into CI/CD pipelines for automated testing.
  - Use scripts to create custom attack vectors.

---

## Vulnerability Scanning
### 5. **Nessus**
- **Purpose**: Comprehensive vulnerability assessment.
- **Usage**:
  - Launch Nessus and add the target.
  - Use a pre-built scan template like "Basic Network Scan."
  - Review the report for CVEs and suggested fixes.
- **Pro Tips**:
  - Always keep Nessus plugins updated for the latest vulnerability checks.
  - Use tags to organize scanned assets.

---

### 6. **Nikto**
- **Purpose**: Web server vulnerability scanning.
- **Usage**:
  ```bash
  nikto -h <target>
  ```
- **Pro Tips**:
  - Run Nikto with Burp Suite or ZAP to correlate findings.
  - Use the `-output` option to save results for reporting.

---

## Exploitation
### 7. **Metasploit Framework**
- **Purpose**: Exploiting vulnerabilities.
- **Usage**:
  1. Launch the framework:
     ```bash
     msfconsole
     ```
  2. Search for an exploit:
     ```bash
     search smb
     ```
  3. Configure and run the exploit:
     ```bash
     use exploit/multi/samba/usermap_script
     set RHOST <target>
     exploit
     ```
- **Pro Tips**:
  - Use Metasploit's `auxiliary` modules for recon and password brute-forcing.
  - Regularly sync the latest exploits using `msfupdate`.

---

### 8. **SQLmap**
- **Purpose**: Automating SQL injection attacks.
- **Usage**:
  ```bash
  # Basic usage
  sqlmap -u "http://example.com/index.php?id=1"

  # Test POST requests
  sqlmap -u "http://example.com/login.php" --data="user=test&pass=test"
  ```
- **Pro Tips**:
  - Use `--dump` to extract database contents.
  - Combine with Burp Suite to extract HTTP requests for testing.

---

## Mobile App Testing
### 9. **MobSF**
- **Purpose**: Static and dynamic analysis of mobile apps.
- **Usage**:
  - Upload an APK or IPA file to MobSF's web interface.
  - Review analysis reports for vulnerabilities like hardcoded credentials.
- **Pro Tips**:
  - Use dynamic analysis to test runtime security.
  - Pair with Frida for advanced runtime modifications.

---

## Network Penetration
### 10. **Wireshark**
- **Purpose**: Capturing and analyzing network packets.
- **Usage**:
  - Start capturing packets on the network interface.
  - Apply filters, e.g., `http.request` to focus on HTTP traffic.
- **Pro Tips**:
  - Use "Follow TCP Stream" to view complete conversations.
  - Save capture files as `.pcap` for further analysis.

---

## Advanced Workflow Examples
1. **Comprehensive Web Application Testing Workflow**:
   - Run Nmap to identify open ports and services.
   - Use Nikto to scan for server-side vulnerabilities.
   - Intercept traffic using Burp Suite for parameter tampering tests.
   - Use SQLmap for identified injection points.
   - Test APIs using Postman and ZAP.

2. **Network Vulnerability Assessment**:
   - Scan the network using Masscan or Nmap.
   - Use Metasploit to target specific services (e.g., SMB or FTP).
   - Analyze traffic using Wireshark to identify unencrypted credentials.

---

### Conclusion
This guide equips you with a practical understanding of bug-hunting tools and their advanced use cases. Feel free to contribute additional tools or workflows to this repository.
