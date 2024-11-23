1. Sensitive Data Exposure
Description: Sensitive data exposure through unrestricted access to the /ftp directory. The directory was listed in the robots.txt file but was accessible without authentication.
Impact: Exposes configuration files, logs, and sensitive resources.
Mitigation:
Restrict access to /ftp via authentication.
Disable directory listing.
Remove sensitive files from the directory.
2. Parameter Tampering
Description: Parameter tampering vulnerabilities allow attackers to manipulate request parameters, such as product quantities or order IDs, to perform unauthorized actions (e.g., setting a negative price).
Impact: Leads to financial loss, inventory manipulation, or system abuse.
Mitigation:
Validate parameters on the server side.
Restrict input to acceptable ranges.
Reject invalid inputs with error handling.
3. Cross-Site Scripting (XSS)
Reflected XSS: Injects malicious JavaScript via search bars or other inputs.
Stored XSS: Malicious scripts are stored in the database and executed when a user accesses the content.
Impact:
Data theft.
Unauthorized access.
Phishing attacks.
Mitigation:
Sanitize and encode user inputs.
Implement contextual escaping.
4. SQL Injection
Description: Exploitation of poorly handled inputs in SQL queries, enabling attackers to bypass authentication or access sensitive data.
Impact:
Unauthorized access to databases.
Data theft, modification, or deletion.
Mitigation:
Use parameterized queries.
Validate and sanitize user inputs.
Escape special characters in queries.
5. Unauthorized Access to Admin Privileges
Description: Exploitation of weak authorization mechanisms allowed attackers to escalate privileges to an admin account.
Impact:
Access to sensitive data.
System compromise.
Mitigation:
Implement robust role-based access control (RBAC).
Validate all authorization tokens server-side.
6. HTML Injection
Description: Injecting HTML code into inputs, which is reflected in the output. Exploitable for phishing or content manipulation.
Impact:
Content alteration.
Phishing attacks.
Mitigation:
Sanitize all user inputs.
Use output encoding techniques.
7. Information Disclosure via SQL Errors
Description: Detailed SQL error messages expose database structure and other internal information.
Impact:
Aids attackers in crafting SQL injection payloads.
Mitigation:
Use generic error messages.
Log detailed errors server-side.
8. Cross-Origin Resource Sharing (CORS) Misconfiguration
Description: A permissive Access-Control-Allow-Origin header (*) allowed any domain to access resources.
Impact:
Unauthorized API access.
Exposure of sensitive data.
Mitigation:
Restrict CORS headers to trusted domains.
9. Improper Authorization (Referer Header Manipulation)
Description: Authorization based on the Referer header allowed unauthorized access by manipulating the header value.
Impact:
Unauthorized access to administrative endpoints.
Mitigation:
Avoid relying on headers for authorization.
Use secure tokens or session-based validation.
10. Remote Code Execution (RCE) via Samba
Description: Exploitation of a Samba vulnerability (CVE-2007-2447) enabled attackers to execute arbitrary commands.
Impact:
Full system compromise.
Mitigation:
Update to a patched Samba version.
Limit SMB service access to trusted networks.
11. Weak Credentials in Apache Tomcat
Description: Default credentials (tomcat/tomcat) were used for the Tomcat Manager interface, leading to admin access.
Impact:
Remote code execution via deployed WAR files.
Mitigation:
Change default credentials.
Restrict access to the Tomcat Manager interface.
12. Telnet Misconfiguration
Description: Open Telnet service on port 23 allowed unauthenticated access.
Impact:
Full system compromise.
Mitigation:
Disable Telnet.
Use SSH instead.
13. MySQL Misconfiguration
Description: MySQL was configured with root access without a password.
Impact:
Unauthorized access to sensitive database data.
Mitigation:
Set strong passwords for all accounts.
Restrict access to the database by IP.
14. WebDAV Misconfiguration
Description: Misconfigured WebDAV service allowed arbitrary file uploads and reverse shell execution.
Impact:
Server compromise and data exposure.
Mitigation:
Restrict access to WebDAV.
Limit file uploads to safe file types.
15. SSH Enumeration and Exploitation
Description: Weak SSH configurations allowed brute-force attacks to succeed.
Impact:
Unauthorized server access.
Mitigation:
Enable account lockout policies.
Use strong passwords and SSH keys.
