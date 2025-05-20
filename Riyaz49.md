Here are the structured notes for the provided AWS RDS lecture:

---

### **AWS RDS (Relational Database Service) Overview**  
- **Full Form**: Relational Database Service  
- **Purpose**: Managed database service in AWS for creating, maintaining, and scaling relational databases.  
- **Managed by AWS**: No SSH/RDP access; AWS handles server management.  

---

### **Key Features**  
1. **Supported Engines (6 Types)**:  
   - MySQL  
   - PostgreSQL  
   - Oracle  
   - Microsoft SQL Server (MSSQL)  
   - MariaDB  
   - **Aurora** (AWS proprietary, compatible with MySQL/PostgreSQL).  

2. **Terminology**:  
   - **DB Instance**: Equivalent to an EC2 instance but for databases.  
   - **Endpoint**: Hostname to connect to the DB (replaces traditional IP).  

3. **Connection Requirements**:  
   - Endpoint  
   - Username/Password  
   - Port (engine-specific, e.g., PostgreSQL: 5432, MSSQL: 1433).  

---

### **Read Replicas**  
- **Purpose**: Improve performance for read-heavy applications (e.g., reporting tools like PowerBI).  
- **Key Points**:  
  - **Max Replicas**: 5 per primary instance (15 for Aurora).  
  - **Replication**: Asynchronous (not real-time).  
  - **Endpoints**: Each replica has its own endpoint.  
  - **Usage**: Redirect read queries to replicas to reduce load on the primary DB.  
  - **Regions/AZs**: Can be in different AZs or cross-region (e.g., primary in Mumbai, replica in US).  
  - **Promotion**: Can promote a replica to a standalone DB (replication stops).  

---

### **Multi-AZ Deployment**  
- **Purpose**: High availability (failover support).  
- **How It Works**:  
  - AWS creates a standby replica in another AZ (synchronous replication).  
  - **Failover**: Automatic if primary fails; endpoint remains the same.  
  - **Cost**: Double (pay for primary + standby).  
- **Limitations**:  
  - Failover only for infrastructure issues (not for DB-level errors like corrupted tables).  
  - Supports read replicas (multi-AZ + read replicas possible).  

---

### **Backups & Snapshots**  
- **Automated Backups**:  
  - **Retention**: Default 7 days (max 35 days).  
  - Scheduled during non-peak hours.  
- **Manual Snapshots**:  
  - No retention limit; stored in S3.  
  - Can be copied/shared across regions/accounts.  
- **Restoration**:  
  - Snapshots restore the entire DB instance (not individual databases).  

---

### **Scaling & Maintenance**  
- **Vertical Scaling (Scale-Up)**:  
  - Change instance type (e.g., T2.small → T2.large).  
  - Requires downtime (instance restart).  
- **Storage Auto-Scaling**:  
  - Define max storage (e.g., 100 GB → 1000 GB); expands automatically.  
- **Patching/Upgrades**: Managed by AWS.  

---

### **Security & Advanced Features**  
1. **Encryption**:  
   - Uses AWS KMS (default key: `aws/rds`).  
2. **Parameter Groups**:  
   - Configure engine-level settings (e.g., global variables for developers).  
3. **Subnet Groups**:  
   - Restrict DB access to specific subnets.  
4. **Performance Insights**:  
   - Dashboard for monitoring queries/connections.  

---

### **Aurora**  
- **AWS Proprietary**: 3–5x faster than MySQL/PostgreSQL.  
- **Features**:  
  - Supports 15 read replicas (uses load balancer for distribution).  
  - Built-in high availability (failover in seconds).  
  - Costlier but optimized for performance.  

---

### **RDS Proxy**  
- **Purpose**: Reduce DB load by pooling/consolidating connections.  
- **Serverless**: Fully managed by AWS.  
- **Supported Engines**: MySQL, PostgreSQL, MariaDB, MSSQL (not Oracle).  
- **Access**: Always private (must be within VPC).  

---

### **Secret Manager**  
- **Use Case**: Securely store DB credentials (usernames/passwords, API keys).  
- **Integration**: Use instead of hardcoding credentials in apps.  

---

### **Key Differences**  
| **Feature**       | **Read Replica**               | **Multi-AZ**                     |  
|-------------------|--------------------------------|----------------------------------|  
| **Purpose**       | Performance (read scaling)     | High availability (failover)     |  
| **Replication**   | Asynchronous                  | Synchronous                     |  
| **Cost**          | Pay per replica               | Double (primary + standby)      |  
| **Endpoint**      | Unique per replica            | Same endpoint after failover    |  

---

### **Best Practices**  
- Use **read replicas** for read-heavy workloads.  
- Enable **multi-AZ** for critical production DBs (despite cost).  
- Schedule backups during **low-traffic periods**.  
- For credentials, use **Secret Manager** over plaintext.  

--- 

**Next Steps**: Practical demo (console setup, snapshots, replication).  

Let me know if you'd like additional details or diagrams!
