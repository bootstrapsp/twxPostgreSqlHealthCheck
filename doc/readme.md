# ThingWorx Persistence Provider : Basic PostgreSQL Monitoring & Health Check

## Overview

 This document is trageted towards covering basic PostgreSQL monitoring and health check related system objects like tables, views, etc. This allows simple monitoring of PostgreSQL database via some custom services, which I'll attach at the end of this document, from the ThingWorx Composer itself. I'll also try to cover short detail on all the services that are included with the Thing: PostgreSQLHealthCheck which implements Database ThingTemplate.

## Pre-requisite

 The document assumes that the user already has ThingWorx running with PostgreSQL as a Persistence Provider. 

## How to install

Usage for this is fairly straight forward, import the Thing and the associated DataShapes and that's it. Each Service under the Thing: PostgreSQLHealthCheck has its own DataShape currently reverting full dataset. If you wish to use this as part of any mashup feel free to edit the services accordingly and the corresponding DataShape.

### Note : System objects from PostgreSQL used here are not restricted, thus users can use these services to query non-ThingWorx related database created under PostgreSQL as part of the external JDBC connection.

## Detailing Services from Thing: PostgreSQLHealthCheck

1. DescribeTableStructure

- Takes two inputs **Table Name** and the **Schema Name** in which the ThingWorx database tables exists both inputs have default values that can be modified to match your PostgreSQL schema setup and required table name
- It provides information on a Table's structure, see below

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525686173fFv8/DescribeAnyTable.jpg)

2. GetAllPSQLConfig

- Doesn't take any input
- Provides runtime details on all the configurations done in the postgresql.conf which are in-effect
- For detail on pg_settings see [doc](https://www.postgresql.org/docs/9.4/static/view-pg-settings.html)

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525690325X0Dv/GetAllPSQLConfig.jpg)

3. GetAllPSQLConfigLimited

- Similar to GetAllPSQLConfig, however with limited information

4. GetAllPSQLRoles

- Lists all the database roles/users
- Also lists their access rights permissions together with OID
- Helpful in identifying if the role is active/inactive or carries any limitation on the DB connections

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525691070C1G_/GetAllPSQLRoles.jpg)

5. GetPG_Stat_Activity

- Part of the Statistics Collector subsystem for the PostgreSQL DB
- Shows current state of the schema e.g. connections, queries, etc.
- For more detail on the output refer to the [doc](https://www.postgresql.org/docs/9.4/static/monitoring-stats.html)

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525691603S4Wa/GetPG_STAT_Activity.jpg)

6. GetPSQLDBLocksInformation

- Shows the kind of locks in effect on which database and on which relation (table)
- Particularly useful in identifying the relations and what lock mode is enabled on them

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525691979mEzA/GetPSQLDBLocksInformation.jpg)

7. GetPSQLDBStat

- Shows database wide statistics
- Like Commits, reads, block reads, tupples (rows) fetched, inserted, deadlocks, etc
- For more detail refer to [PostgreSQL Doc](https://www.postgresql.org/docs/9.4/static/monitoring-stats.html)

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525692435zG6z/GetPSQLDBStat.jpg)

8. GetPSQLLogDesitnation

- Checks where the PostgreSQL server logs are directed to
- I.e. stderr, csvlog or syslog
- Default is stderr

9. GetPSQLLogFileName

- Fetches the log PostgreSQL log file name and the filename format, 
- E.g. postgresql-%Y-%m-%d_%H%M%S.log

10. GetPSQLLoggingLocation

- Fetches the location where the logs are stored for PostgreSQL
- e.g. pg_log, which is also the default location
- Desired location for the logs can be done in the postgresql.conf file

11. GetPSQLRelationIndexes

- Gets information on the Indexes
- Information like index size, number of rows, table names on which the index is created

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525693320Quwr/GetPSQLRelationIndexes.jpg)

12. GetPSQLReplicationStat

- Shows information related to the Replication on PostgreSQL DB
- Applicable to the PostgreSQL DBs where replication is enabled

13. GetPSQLTablespaceInfo

- Takes tablespace name as input (String DataType), service defaults to 'thingworx' - modify if needed
- Fetches information like owner oid, tablespace ACL

![Output](https://support.ptc.com/images/cs/articles/2018/05/152569425902Rz/GetPSQLTablespaceInfo.jpg)

14. GetPSQLUserIndexIO

- Fetches index that are created only on the User created DB objects
- Shows relations (table) vs index relations ids (index on table), together with their names
- Also shows additional info like number of disk blocks read from this index & number of buffer hits in this index

![Output](https://support.ptc.com/images/cs/articles/2018/05/15256946445czJ/GetPSQLUserIndexIO.jpg)

15. GetPSQLUserSequencesIOStats

- Fetches informtion on Sequence objects used on user defined relations (tables)
- Number of disk blocks read from this sequence & buffer hits in this sequence

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525694949YbmH/GetPSQLUserSequencesIOStats.jpg)

16. GetPSQLUserTableIOStat

- Fetches disk I/O information on the user created tables

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525695347NWJo/GetPSQLUserTableIOStat.jpg)

17. GetPSQLUserTables

- Fetches all the user created tables, together with their
    - name, OID
    - Disk I/O
    - Last autovacuum
    - Also lists the amount of rows each relation (table) has

![Output](https://support.ptc.com/images/cs/articles/2018/05/1525695752tqdn/GetPSQLUserTables.jpg)


## Finally

The attached Thing PostgreSQLHealthCheck has some additional service not yet covered in this blog, as they are minor services. Therefore for brevity of this blog I've left them out for now, feel free to explore or enhance this. I will continue to look for any additional services and will enhance this document and the entities belong to this.