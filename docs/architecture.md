---
layout: page
title: Architecture
permalink: /architecture/
---

## Technologies
AMP 3.5 is deployed using [Apache Tomcat 8.5](https://tomcat.apache.org/download-80.cgi#8.5.85), an open-source Web Server that implements several Java EE specifications. AMP is based on [Java 8](https://www.oracle.com/java/technologies/). The open-source [Nginx HTTP Server](https://www.nginx.com/) is used to deliver the application content to the country-specific domain, with the right pointers to the Public Portal and AMP itself. AMP benefits from its security, traffic control efficiency and its compliance with current HTTP standards. AMP developer setup additionally uses some tools like [Maven 3.8.1](https://maven.apache.org) and [GitHub](https://github.com/devgateway/amp). The AMP Public Portal is deployed as a separate application and can even run on a different machine if necessary. The Public Portal uses Drupal 7, which runs with PHP7 and has its own DB instance for its settings and storage. 