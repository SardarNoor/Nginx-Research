

##  Project Overview

This project demonstrates how NGINX can be configured and used as:

- A static web server  
- A reverse proxy  
- A load balancer  
- An SSL termination point  
- A PHP-FPM handler  
- A rewrite & redirect engine  
- A security gateway  
- A logging and monitoring tool  

The goal was to understand NGINX from scratch and configure it exactly like a production-grade environment.

---

#  Features Implemented 

### **1. NGINX Installation & Setup**
- Installed NGINX on Ubuntu EC2  
- Verified service, firewall, and default web page

### **2. Static Content Hosting**
- Hosted a simple HTML website  
- Used `root` and `index` directives  
- Served content through a dedicated server block

### **3. Reverse Proxy**
- Configured proxy_pass to a Node.js backend  
- Added forwarding headers (`$remote_addr`, `$host`, `$proxy_add_x_forwarded_for`, etc.)

### **4. Load Balancing**
- Implemented upstream block  
- Tested:
  - **round robin**
  - **least_conn**
  - **ip_hash**  
- Added custom header `X-Upstream` to track backend server

### **5. SSL/TLS (Self-Signed Certificate)**
- Generated certificate using OpenSSL  
- Configured HTTPS server block  
- Redirected HTTP → HTTPS  
- Tested using browser + curl

### **6. PHP-FPM Integration**
- Installed PHP-FPM 8.3  
- Added FastCGI configuration  
- Served dynamic PHP pages (`phpinfo.php`)  
- Verified PHP-FPM socket handling

### **7. URL Rewriting & Redirects**
Implemented:

- `/old` → `/new` redirect  
- Pretty URLs (`/user/10` → `/user.php?id=10`)  
- Directory redirect (`/blog`)  
- Trailing slash enforcement rules  
- Query string rewrites

### **8. Security Hardening**
Added common production-grade headers:

- `X-Frame-Options`  
- `X-XSS-Protection`  
- `X-Content-Type-Options`  
- `Referrer-Policy`  
- `Permissions-Policy`

### **9. Basic Authentication**
- Protected `/admin` route  
- Used `.htpasswd` with encrypted credentials

### **10. Custom Error Pages**
- Created:
  - `404.html`
  - `403.html`
  - `500.html`
- Configured `error_page` with alias location

### **11. Multi-Site Hosting**
- Hosted multiple domains:
  - example.com  
  - reverseproxy.com  
  - phpsite.com  
  - ssl-test.com  
- Enabled/enforced separate server blocks

### **12. WebSocket Support**
- Added upgrade headers:
  ```
  proxy_http_version 1.1;
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection "upgrade";
  ```

### **13. Rate Limiting & Connection Limits**
Implemented production traffic control:

```
limit_req_zone $binary_remote_addr zone=one:10m rate=5r/s;
limit_conn_zone $binary_remote_addr zone=addr:10m;
```

Applied:

```
limit_req zone=one burst=10 nodelay;
limit_conn addr 10;
```

### **14. Logging & Monitoring**
- Monitored access logs  
- Monitored error logs  
- Triggered intentionally bad requests to test debugging

### **15. Proxy Caching (Configuration Only)**
Configured complete caching logic including:

- `proxy_cache_path`
- `proxy_cache`
- `proxy_cache_valid`
- `X-Cache-Status` header

---

#  Project Structure

```
NGINX-Research-Project/
│── configs/
│   ├── example.com
│   ├── reverseproxy.com
│   ├── phpsite.com
│   ├── ssl-test.com
│── documentation/
│   ├── NGINX_Research_Detailed.pdf
│── README.md
```

---

# Full Documentation (PDF)
A complete step-by-step guide containing explanations, configurations, and screenshots is included inside:

```
Task2(Nginx Research).pdf
```

This PDF contains detailed logs, rewrite rules, custom errors, rate limiting tests, SSL tests, and more.

---

#  Technologies Used
- **NGINX (1.24+)**
- **Ubuntu Server 22.04**
- **PHP 8.3 + PHP-FPM**
- **OpenSSL**
- **Node.js (for reverse proxy backend)**
- **AWS EC2 (Hosting environment)**

---

#  What I Learned
Through this project I gained hands-on experience with:

- How NGINX handles requests internally  
- TCP/HTTP lifecycle  
- Reverse proxy & backend communication  
- SSL/TLS encryption  
- PHP-FPM processing  
- Request rewriting & routing  
- Performance optimization  
- Error handling and debugging  
- Web server security  




