https://github.com/yeshwanthlm/YouTube/blob/main/aws-rds-masterclass.md
# RDS

AWS Relational Database Service RDS Masterclass |

AWS RDS Full Course |

RDS Zero to Hero |

AWS Demo

K

**Overview of Databases**

A MO

Database - System that store and manage data

Broadly divided in to - Relational (SQL) and Non-Relational (NoSQL)

Relational (SQL) - Structured Query Language

Relationship between tables

Schema - Structure in and between tables of data

NoSQL - Not One Single Thing!


relation -sql(strucured query language)
NoSQL

![image](https://github.com/user-attachments/assets/1e2b43dd-4db8-4743-96f9-4229b790cdef)


Anything that does not fit into SQL

Composite Key in Amazon RDS
A composite key in Amazon RDS (Relational Database Service) is a database concept where two or more columns are combined to form a unique identifier for rows in a table. This is similar to composite keys in any relational database system, as RDS supports standard SQL databases like MySQL, PostgreSQL, Oracle, and SQL Server.

Key Characteristics of Composite Keys in RDS:
Multiple Columns: A composite key consists of two or more columns that together uniquely identify a row.

Uniqueness Constraint: The combination of values in these columns must be unique across the table, though individual columns may contain duplicate values


![image](https://github.com/user-attachments/assets/21ef0214-0c10-4790-b1aa-a50dd14df36e)
webserver,Application,dataase this is called three tiere architecture
you  need to think about the costs with data transfer while hosting multilple AZ
K

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


K

***Relational Database Service (RDS)***


Database-as-a-service (DBaaS) - not really true. It is more of Database Server-as-a-service.

Managed Database Instance for one or more databases

Databases - MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL

Amazon Aurora - This is so different from normal RDS, it is a separate product.





Relational Database Service (RDS)
Database-as-a-service (DBaaS) - not really true. It is more of Database Server-as-a-service.
Managed Database Instance for one or more databases
Databases - MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL
Amazon Aurora - This is so different from normal RDS, it is a separate product.


RDS Database Instance
Database connects with a CNAME. RDS uses standard database engines.
The database can be optimized for:db.m5 general, db.r5 memory, db.t3 burst.
When you provision an instance, you provision storage that is dedicated to that instance. This is EBS storage located in the same AZ. RDS is vulnerable to failures in that AZ.
The storage can be allocated with SSD or magnetic.
Billing is per instance and hourly rate for that compute. You are billed for storage allocated.


BY default 40 DB instancs

