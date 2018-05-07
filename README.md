# Basic PostgreSQL Monitoring & Health Check
This document is trageted towards covering basic PostgreSQL monitoring and health check related system objects like tables, views, etc. This allows simple monitoring of PostgreSQL database via some custom services, which I'll attach at the end of this document, from the ThingWorx Composer itself. I'll also try to cover short detail on all the services that are included with the Thing: PostgreSQLHealthCheck which implements Database ThingTemplate.

# How to enhance

* After forking, import the entity in ThingWorx
* Make Required changes to the Thing / Services, or even adding more entities as needed
* Make sure to add them to the project PostgreSQLHealthCheckExtension & Tag them with Application | PSQLHealthCheck (Project & tag will be created automatically when entities.twx is imported)
* Once done with changes, export the project in binary
* and commit

![Project and Tag](https://support.ptc.com/images/cs/articles/2018/05/1525703909V01M/Project&Tag.jpg)