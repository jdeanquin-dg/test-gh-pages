---
layout: page
title: Install
permalink: /install/
---

# Installation instructions


### Hosting requirements:
Operating System: GNU Linux/Unix
CPU: 4 cores, 64 bit
RAM Memory: 16 GB
Storage: 350 GB
Network: Public IP address, Domain name, port 443

### Prerequisites:
Open JDK 8
Apache Tomact 8.5
PostgreSQL 14 with PostGIS 3.2.3 extension


### Deliverables:
Main application: amp-v3.5.war


### Email

Configure SMTP server to serve on localhost port 25 without any authentication, if you are enabling the server to send emails. 

### PostgreSQL

Application connects to the database via 5432 port.

Make sure that postgres user exists and PostgreSQL is configured to trust all local ip v4 connections.

In /etc/postgresql/14/main/pg_hba.conf you must have the following lines:

```
IPv4 local connections:
host	all         	all         	127.0.0.1/32        	trust
```


### Application Settings:




###  Installation steps:


### Nginx

Web requests to the applications are dispatched by Nginx 1.14 webserver, running on Debian GNU/Linux Stable (Buster) AMD64.

The webserver is configured to redirect any plain text (HTTP) requests to their TLS-encrypted (HTTPS) counterparts. Additionally, it is enforcing Strict Transport Security by pinning the necessary headers. TLS certificate is provided by LetsEncrypt service. The server is configured to only allow secure modern encryption protocols (TLS v1.2 and v1.3) as well as only strong cipher suites.

The server requests compliant robots not to index the website by serving a restrictive robots.txt file.

