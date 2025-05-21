RDS is regional
templates 
Production
dev/test
free tier


Prodcution: primary db and two read intances with each DB nstance in different AZ

DB instance calass
--
stnadard class (m class)
Memory optimized class (r & x)
Burstableclasses (t )

io1 minimum 100gb we have to give
iops we can give 1000 to 80k

storage autoscalnng
---
minimum and maximum we can give

when we select RDS proxy it automatically
 creates IMA and secret manager secret for the RDS proxy

postgres port:5432


monitoring 
---
performance insights
- how many machines are connects
query tim


devops guru detects performance issues


db instance name ie engine name
now we are give DB name
DB parametre group?

we can giv backup window
backp retention period

we can check rds logs in cloudwatch logs

mainteance
enable minir version upgrade


delete protection is enabled .it protects from being deleted accidently.you cannot delete it

cost optimization
---
remove multi az
move io1 to gp2
redice iops if ur using io1
scale down the instance type
reserver db instance



elastic cache(redis em cached ,80 times faster)
RDS Proxy

after creatinf db status backing up-->avaialble

what is setup ec2 instance,lamba function

aurora is compatible with postgres and mysql
how many querys


rds proxy doesnt support oracle


A Subnet Group in Amazon RDS (Relational Database Service) is a collection of subnets that you designate for your RDS DB instances in a Virtual Private Cloud (VPC). These subnet groups serve several important purposes:
