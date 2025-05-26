https://github.com/yeshwanthlm/YouTube/blob/main/aws-rds-masterclass.md
https://www.youtube.com/watch?v=QwXXvFK68cs&t=82s

# RDS

AWS Relational Database Service RDS Masterclass |


**Overview of Databases**


Database - System that store and manage data

Broadly divided in to - Relational (SQL) and Non-Relational (NoSQL)

**Relational (SQL)** - Structured Query Language Relationship between tables
    **Schema** - Structure in and between tables of data

**NoSQL** - Not One Single Thing!
Anything that does not fit into SQL

![image](https://github.com/user-attachments/assets/1e2b43dd-4db8-4743-96f9-4229b790cdef)




**Composite Key in Amazon RDS**
**A composite key in Amazon RDS (Relational Database Service)** is a database concept where two or more columns are combined to form a unique identifier for rows in a table. This is similar to composite keys in any relational database system, as RDS supports standard SQL databases like MySQL, PostgreSQL, Oracle, and SQL Server.

Key Characteristics of Composite Keys in RDS:
  Multiple Columns: A composite key consists of two or more columns that together uniquely identify a row.

Uniqueness Constraint: The combination of values in these columns must be unique across the table, though individual columns may contain duplicate values


![image](https://github.com/user-attachments/assets/21ef0214-0c10-4790-b1aa-a50dd14df36e)
webserver,Application,database this is called three tiere architecture
you  need to think about the costs with data transfer while hosting multilple AZ


***Why should you run DBs on EC2?***

Access to the DB instance OS.
Advanced DB Option tuning (DBROOT).
Vendor demands.
DB or DB version that AWS doesn't provide.
You might need a specific version of an OS and DB that AWS doesn't provide.



**Why shouldn't you run DBs on EC2?**

Admin overhead.

Backup and DR.

EC2 is running in a single AZ.

Will miss out on features from AWS DB products.

Skills and setup time to monitor.

Performance will be slower than AWS options.

***Relational Database Service (RDS)***


Database-as-a-service (DBaaS) - not really true. It is more of Database Server-as-a-service.

Managed Database Instance for one or more databases

Databases - MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL

Amazon Aurora - This is so different from normal RDS, it is a separate product.





**Relational Database Service (RDS)**
Database-as-a-service (DBaaS) - not really true. It is more of Database Server-as-a-service.
**Managed Database Instance** for one or more databases
Databases - MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL
**Amazon Aurora** - This is so different from normal RDS, it is a separate product.


**RDS Database Instance**
Database connects with a CNAME. RDS uses standard database engines.
The database can be optimized for:db.m5 general, db.r5 memory, db.t3 burst.
When you provision an instance, you provision storage that is dedicated to that instance. This is EBS storage located in the same AZ. RDS is vulnerable to failures in that AZ.
The storage can be allocated with SSD or magnetic.
Billing is per instance and hourly rate for that compute. You are billed for storage allocated.
BY default 40 DB instancs


To Create Databse
RDS--?Standard create-->Mariadb
select version -->Templates:Production-->DB instance identifier:demo-rds-database
Credentials Settings-->give user name and  password
Instance configuration->select Db instance class
standard class ,memory optimized,burstable

select storage class
select :stoarge type, Allocated storage
General Purpose SSD (gp2)
Baseline performance determined by volume s
Provisioned IOPS SSD (0)
Floxitility in provuaning
magnetic


Enable storage autoscaling
Enabling tas fatin will allow the storage tokocreate after the soerified theesheld in

Availability & durability
Multi-AZ deployment Into

Connectivity
Don't connect to an EC2 compute resource

Network type
  IPV4, Dual Stack mode(Your resources can communte over IPV4,IPV6 or  both)

  select VPC
  DB Subnet group(Choose the DB subnet group. The DB subnet group defines which subnets and IP ranges the DB instance can use in the VPC that you selected.)(These can be created with the left menu option in RDS)
  Public access:NO

  VPC security group (firewall)- you should make sure you enable port 
 Certificate authority - optional

Using a server certificate provides an extra layer of security by validating that the connection is being made to an Amazon database. It does so by checking the server certificate that is automatically installed on all databases that you provision.

Additional configuration -->you can create a DB from here, Als you can setup backup(snapshot) and retention,Log exports

Maintenance window
Select the period you want pending modifications or maintenance applied to the database by Amazon RDS.
Choose a window
No preference
Enable deletion protection(Protects the database from being deleted accidentally. While this option is enabled, you can’t delete the database.)


every DB instance will have endpoint.Apps connect through endpoint only,it will notchange


Database Instance vs. Database
Database Instance: This refers to the set of memory structures and background processes that manage database files. It handles tasks like query processing, memory management, and transaction control. An instance provides the environment in which databases operate.
This vs. That

Database: This is the organized collection of data stored on disk. It encompasses the actual data files, schemas, tables, indexes, and other objects that store and organize information.


What is a DB Instance Endpoint?
A DB instance endpoint is a unique DNS address assigned to your database instance. It typically includes:
AWS Documentation
Repost

Host: The DNS address of the DB instance.
AWS Documentation

Port: The port number on which the database listens for connections (e.g., 3306 for MySQL, 5432 for PostgreSQL).

When configuring your database client or application, you use this endpoint to establish a connection to the database instance. For example, in a connection string, you'd specify the endpoint as the host and include the appropriate port number. 
A


Step 1: Get the dump of your existing DB on EC2
Step 2: Connect to your RDS DB Instance.
Step 3: Migrate the DB Dump that you have taken in Step 1 to RDS.
Step 4: Verify if the data is available.




https://www.youtube.com/watch?v=PA0MPTzsieM&t=63s
###################




![image](https://github.com/user-attachments/assets/4a7e15f5-a99c-42d4-a82b-dc5393f5e61a)

Aurora Global Database employs asynchronous replication between the primary AWS Region and up to five secondary Regions. This means that write operations to the primary cluster do not wait for the secondary clusters to receive and process the changes. Data is replicated using storage-based, block-level replication with typical latencies under one second, facilitating low-latency global reads and disaster recovery capabilities

If you are reading it from Read replica there will be some lag .you can do this if you are using any reporting environemnt for that some kind of lag is fine
Read replica can be in same region or other region.CRR can help in DR
if US-EAST DB goes down then you can promote the US-WEST Databse as prmary
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.Autoscaling.html
when drastic increase manual storage sclaihg



