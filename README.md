# Production Maintenance and Incident Response Runbook

## Overview
This repository documents a comprehensive Site Reliability Engineering (SRE) and Operations drill. The project focuses on maintaining, monitoring, and recovering a production-ready React application served via Nginx on an Ubuntu Linux environment.

## Technology Stack
* Operating System: Ubuntu Linux
* Web Server: Nginx
* Application: React (Single Page Application)
* Networking: IPv4, UFW (Uncomplicated Firewall)
* Process Management: systemd

## Operations Performed

### 1. Network Validation
Verified external and internal network connectivity to ensure the web application is safely exposed.
* Confirmed Nginx is actively listening on port 80 (HTTP) and SSH is secured on port 22.
* Verified UFW status to ensure strict access control.

![Network Connectivity Validation](images/media_1791419519825.png)
![Firewall Status](images/media_1791419495791.png)

### 2. Service Health and Systemd Validation
Executed rigorous health checks on the Nginx web server.
* Validated configuration syntax prior to live reloads.
* Inspected background master and worker processes.

![Nginx Service Health](images/media_1791447525835.png)

### 3. Traffic and Error Log Analysis
Simulated live traffic and analyzed server logs to confirm request handling.
* Audited Nginx access logs to trace digital footprints and user agents.
* Audited Nginx error logs and systemd journalctl to ensure zero unhandled exceptions.

![Access Logs](images/media_1791447912974.png)
![System Journal](images/media_1791449941055.png)

### 4. System Resource Capacity Monitoring
Monitored critical system resources to detect potential capacity bottlenecks.
* Assessed CPU load averages, memory allocation, and disk usage across the /var partition.

![Resource Monitoring](images/media_1791450335828.png)

### 5. Deployment Verification
Conducted file system analysis to verify the integrity of the live application.
* Utilized text processing tools to search the source code and confirm the exact deployment version is active.

![Deployment Verification](images/media_1791451170494.png)

## Incident Response Simulations

### Incident 1: Configuration Syntax Failure
* Simulation: Introduced a critical syntax error into the Nginx configuration file.
* Recovery: Corrected the syntax, validated the configuration, and successfully reloaded the service.

![Configuration Failure](images/media_1791451603062.png)
![Configuration Recovery](images/media_1791451755078.png)

### Incident 2: Web Root Content Deletion
* Simulation: The primary web root directory was unexpectedly emptied, resulting in 500 Internal Server Error responses.
* Recovery: Restored the web root from a secure backup and verified the return of 200 OK HTTP responses.

![Web Root Failure](images/media_1791452459729.png)
![Web Root Recovery](images/media_1791452675493.png)

## Security and Reliability Standards
* Authentication: Enforced SSH key-based authentication over password sharing to prevent brute force attacks.
* Attack Surface Reduction: Restricted open ports exclusively to essential services (HTTP and SSH).
* Automation: Ensured critical services are enabled on boot to minimize downtime during unexpected server outages.
