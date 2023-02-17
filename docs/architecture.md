---
layout: page
title: Architecture
permalink: /architecture/
---

## Technologies
AMP 3.5 is deployed using [Apache Tomcat 8.5](https://tomcat.apache.org/download-80.cgi#8.5.85), an open-source Web Server that implements several Java EE specifications. AMP is based on [Java 8](https://www.oracle.com/java/technologies/). The open-source [Nginx HTTP Server](https://www.nginx.com/) is used to deliver the application content to the country-specific domain, with the right pointers to the Public Portal and AMP itself. AMP benefits from its security, traffic control efficiency and its compliance with current HTTP standards. AMP developer setup additionally uses some tools like [Maven 3.8.1](https://maven.apache.org) and [GitHub](https://github.com/devgateway/amp). The AMP Public Portal is deployed as a separate application and can even run on a different server if necessary. The Public Portal uses WordPress.

DG leverages Open Source technologies both as part of the end-product applications as well as its supporting tools in the Software Development process. Our Aid Management Platform relies upon Jenkins for continuous integration. DG uses GitHub extensively in its development process, and our developers are active participants in the Open Source community, with experience in all common Open Source practices.

### PostgreSQL
AMP system relies on an open-source [PostgreSQL](https://www.postgresql.org) Database. It is well known for its high performance, and reliability and, unlike some other open-source RDBMS, it provides a [PostGIS extension](http://postgis.net) that we use for the GIS module. PostgreSQL fulfilled AMP system needs and proved stable over an extensive period of usage in different environments with different resources. We have defined a set of configurations to tune PostgreSQL for AMP needs to gain the best performance for each country setup.
Document Management is handled by the open-source content repository for the Java platform, [Apache Jackrabbit](http://jackrabbit.apache.org/jcr/index.html). 


