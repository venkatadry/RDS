https://github.com/yeshwanthlm/YouTube/blob/main/aws-rds-masterclass.md
https://www.youtube.com/watch?v=QwXXvFK68cs&t=82s

# RDS

**Amazon Aurora** is a cloud-native relational database service offered by AWS, compatible with MySQL and PostgreSQL. By default, Aurora operates within a single AWS Region, providing high availability and scalability within that region.

However, with the Aurora Global Database feature, you can extend an Aurora database across multiple AWS Regions. This setup allows for low-latency global reads and provides disaster recovery capabilities in case of regional outages. The global database consists of one primary region where write operations occur and up to 10 read-only secondary regions that asynchronously replicate data from the primary region

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

**TO Create DB**

https://medium.com/@brian639/a-guide-to-setting-up-and-connecting-to-mysql-database-on-amazon-rds-1d6e50848119
https://medium.com/@achelengwanelson/how-to-setup-a-database-on-aws-rds-a2dc17fc38ec

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


Database Instance vs. Database
**Database Instance:** This refers to the set of memory structures and background processes that manage database files. It handles tasks like query processing, memory management, and transaction control. An instance provides the environment in which databases operate.


**Database:** This is the organized collection of data stored on disk. It encompasses the actual data files, schemas, tables, indexes, and other objects that store and organize information.




A **DB instance endpoint** is a unique DNS address assigned to your Amazon RDS (Relational Database Service) database instance. It serves as the network address that applications and clients use to connect to the database. Each endpoint includes a host (DNS address) and a port number, which together direct traffic to the specific database instance.
 For example, in a connection string, you'd specify the endpoint as the host and include the appropriate port number. 

### 🔹 Components of a DB Instance Endpoint

* **Host (DNS Address)**: This is the unique DNS name of your DB instance. For example: `mydb.123456789012.us-east-1.rds.amazonaws.com`.

* **Port**: The port number on which the database engine listens for connections. Common default ports include

  * MySQL/MariaDB: `3306`
  * PostgreSQL: `5432`
  * Oracle: `1521`
  * Microsoft SQL Server: `1433`
  * Db2: `50000`([AWS Documentation][2])

When configuring your database client or application, you'll use the endpoint as the host and specify the appropriate port number to establish a connection to the DB instance.

### 🔹 Stability and Behavior of Endpoints

* **Consistency**: The endpoint remains consistent for the lifetime of the DB instance. If you delete and then recreate a DB instance with the same identifier, the endpoint remains the same. 

* **Renaming Instances**: If you rename your DB instance, the endpoint changes to reflect the new name, but the underlying identifier remains the same. ([AWS Documentation][4])



```bash
aws rds describe-db-instances \
    --db-instance-identifier your-db-instance-identifier \
    --query 'DBInstances[].Endpoint'
```


############

Step 1: Get the dump of your existing DB on EC2
Step 2: Connect to your RDS DB Instance.
Step 3: Migrate the DB Dump that you have taken in Step 1 to RDS.
Step 4: Verify if the data is available.




https://www.youtube.com/watch?v=PA0MPTzsieM&t=63s
###################




![image](https://github.com/user-attachments/assets/4a7e15f5-a99c-42d4-a82b-dc5393f5e61a)

Aurora Global Database employs asynchronous replication between the primary AWS Region and up to five secondary Regions. This means that write operations to the primary cluster do not wait for the secondary clusters to receive and process the changes. Data is replicated using storage-based, block-level replication with typical latencies under one second, facilitating low-latency global reads and disaster recovery capabilities

Up to 5 Read Replicas
Within AZ, Cross AZ or Cross Region
Replication is ASYNC, so reads are eventually consistent
Replicas can be promoted to their own DB
Applications must update the connection string to leverage read replicas

Both your source DB cluster and your cross-Region read replica DB cluster can have up to 15 Aurora Replicas, along with the primary instance for the DB cluster.


If you are reading it from Read replica there will be some lag .you can do this if you are using any reporting environemnt for that some kind of lag is fine
Read replica can be in same region or other region.CRR can help in DR

if US-EAST DB goes down then you can promote the US-WEST Databse as prmary

https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.Autoscaling.html

when drastic increase manual storage sclaihg




![image](https://github.com/user-attachments/assets/a7bc68fa-64fa-41fb-8522-3d83ab4066d1)


![image](https://github.com/user-attachments/assets/8853c90f-a064-4b3e-8615-f077e4036cb0)



![image](https://github.com/user-attachments/assets/32472ad9-ce46-4932-b363-710da4789450)

![image](https://github.com/user-attachments/assets/1df742c6-bec2-47ac-8c8e-7eae255b33bf)

**RDS Security - Encryption**
**At rest encryption**
Possibility to encrypt the master & read replicas with AWS KMS - AES-256 encryption
Encryption has to be defined at launch time
If the master is not encrypted, the read replicas cannot be encrypted
Transparent Data Encryption (TDE) available for Oracle and SQL Server

**In-flight encryption**
SSL certificates to encrypt data to RDS in flight
Provide SSL options with trust certificate when connecting to database
To enforce SSL:
PostgreSQL: rds.force_ssl= I in the AWS RDS Console (Parameter Groups)
MySQL: Within the DB:
GRANT USAGE ON *.* TO 'mysqluser'@'%' REQUIRE SSL;








