############
Architecture
############

**************
Infrastructure
**************

SaaS platform. You can create a login on the IQNOMY website.

Servers are located in the Dutch datacenter EvoSwitch which is ISO 27001 certified.

The IQNOMY platform architecture is specialized in Big Data. The platform exists of several microservices that are combined to create the platform. All servers are redundant and server hardware is specialized for the applications it is serving.

Main language is J2EE and API's are available in JSON. We are using: Linux Debian OS, Glassfish cluster Applicatieserver, Cassandra (NoSQL), MySQL, Apache, HAProxy.

Incoming requests are loadbalanced over multiple webservers, data collection is stored in a cassandra cluster existing of multiple nodes and configuration in MySQL Master - Slaves setup. Images and files are available on NTFS.

* Availability: 99.98%
* HTTP / HTTPS
* CDN for fast serving



**********
Monitoring
**********

We monitor 24 * 7 and system administrators are 24 * 7 available.

* uptime of IQNOMY
* response time
* connected
* requests done
