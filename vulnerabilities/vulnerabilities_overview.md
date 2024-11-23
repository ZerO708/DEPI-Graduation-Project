
# Vulnerabilities Overview

## 1. **Sensitive Data Exposure via Unrestricted Access to `/ftp`**
### **Exploit**
- **Steps**:
  1. Check the `robots.txt` file for disallowed paths.
  2. Directly access `/ftp` via a browser or a tool like `wget` or `curl`.
  3. If directory listing is enabled, view the listed files.
  4. If disabled, guess or brute-force file names to access them.
- **Tools**: Browser, Burp Suite, curl, wget.

### **Mitigation**
1. Implement authentication and authorization for sensitive directories.
2. Remove or relocate sensitive files from public directories.
3. Disable directory listing on the web server.
4. Use server-side restrictions (e.g., `.htaccess` rules).

---

## 2. **Parameter Tampering Vulnerability (Quantity Manipulation)**
### **Exploit**
- **Steps**:
  1. Add an item to the cart.
  2. Intercept the request with tools like Burp Suite.
  3. Modify the `quantity` parameter to a negative value (e.g., `-5`).
  4. Observe the price calculation resulting in a negative value.
- **Tools**: Burp Suite, OWASP ZAP.

### **Mitigation**
1. Validate inputs on both client and server sides.
2. Restrict `quantity` values to positive integers.
3. Implement logical boundaries for quantities and enforce constraints.
4. Use error handling to reject invalid inputs.

---

## 3. **Parameter Tampering Vulnerability (Order ID Manipulation)**
### **Exploit**
- **Steps**:
  1. Add an item to the cart and proceed to checkout.
  2. Intercept the request and locate the `order_id` parameter.
  3. Modify the `order_id` value to another user's valid order ID.
  4. Forward the request and observe unauthorized access to another order.
- **Tools**: Burp Suite, OWASP ZAP.

### **Mitigation**
1. Validate order ownership server-side to ensure `order_id` is tied to the user session.
2. Use token-based authentication and restrict sensitive operations to authenticated users.
3. Replace numeric `order_id` with a UUID to make guessing difficult.

---

## 4. **Cross-Site Scripting (Reflected XSS)**
### **Exploit**
- **Steps**:
  1. Locate an input field (e.g., search bar).
  2. Inject a malicious payload like `<script>alert('XSS')</script>`.
  3. Submit the input and observe the payload executing in the browser.
- **Tools**: Burp Suite, browser developer tools.

### **Mitigation**
1. Validate and sanitize all user inputs.
2. Use output encoding before rendering user input on the page.
3. Employ Content Security Policy (CSP) headers to restrict script execution.

---

## 5. **Cross-Site Scripting (Stored XSS)**
### **Exploit**
- **Steps**:
  1. Locate a field that stores user input (e.g., comments or profiles).
  2. Inject a payload like `<script>alert('Stored XSS')</script>`.
  3. Trigger the malicious script when a user views the stored data.
- **Tools**: Burp Suite, browser developer tools.

### **Mitigation**
1. Sanitize and encode user input before storing it.
2. Use contextual escaping based on output locations (HTML, JavaScript).
3. Regularly review and patch stored input vulnerabilities.

---

## 6. **SQL Injection**
### **Exploit**
- **Steps**:
  1. Locate an input field (e.g., login form).
  2. Inject SQL payloads like `' OR 1=1--` into the input field.
  3. Observe unauthorized data access or bypass login authentication.
- **Tools**: SQLmap, Burp Suite.

### **Mitigation**
1. Use parameterized queries or prepared statements.
2. Validate and sanitize user inputs.
3. Implement strict database permissions to limit data exposure.

---

## 7. **Unauthorized Access to Admin Privileges**
### **Exploit**
- **Steps**:
  1. Attempt to access admin functionalities with a non-admin account.
  2. Observe the response granting admin privileges due to a flaw in access control.
- **Tools**: Burp Suite, browser developer tools.

### **Mitigation**
1. Implement robust Role-Based Access Control (RBAC).
2. Perform authorization checks on every sensitive operation.
3. Regularly audit and patch access control mechanisms.

---

## 8. **HTML Injection**
### **Exploit**
- **Steps**:
  1. Enter an HTML payload like `<a href="http://malicious.com">Click Here</a>` into a search field.
  2. Submit the form and observe the injected HTML being rendered.
- **Tools**: Burp Suite, browser developer tools.

### **Mitigation**
1. Sanitize and encode user inputs before displaying them.
2. Use output encoding for HTML content.
3. Validate inputs to allow only safe HTML if necessary.

---

## 9. **Information Disclosure via SQL Error**
### **Exploit**
- **Steps**:
  1. Submit invalid input to trigger a SQL error (e.g., duplicate data).
  2. Observe detailed error messages revealing internal database structures.
- **Tools**: Burp Suite, SQLmap.

### **Mitigation**
1. Return generic error messages to users.
2. Log detailed error information server-side.
3. Validate and sanitize user inputs to prevent SQL errors.

---

## 10. **CORS Misconfiguration**
### **Exploit**
- **Steps**:
  1. Send a cross-origin request to the application.
  2. Observe the `Access-Control-Allow-Origin: *` header in the response.
  3. Leverage the misconfiguration to access sensitive data.
- **Tools**: curl, Postman.

### **Mitigation**
1. Restrict `Access-Control-Allow-Origin` to specific trusted domains.
2. Avoid enabling credentials for untrusted origins.
3. Evaluate and limit CORS access to necessary endpoints.

---

## 11. **Improper Authorization via Referer Header Manipulation**
### **Exploit**
- **Steps**:
  1. Intercept a request with a valid `Referer` header.
  2. Modify the `Referer` header to an untrusted domain.
  3. Observe the server processing the request despite the altered header.
- **Tools**: Burp Suite, OWASP ZAP.

### **Mitigation**
1. Avoid relying on headers like `Referer` for authorization.
2. Implement token-based or session-based authentication.
3. Enforce role-based access controls for sensitive endpoints.

---
