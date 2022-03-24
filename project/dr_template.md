# Infrastructure

## AWS Zones
us-east-2a, us-east-2b, us-east-2c
us-west-1a, us-west-1b

## Servers and Clusters
1 VM 

### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Asset name | Brief description | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| Web Server | Runs business web application | t3.micro | 3 instances per region | Deployed in 2 regions | 
| Web Cluster | HA configuration for web app | t3.medium instances | 2 node clusters | clusters are created in 2 regions |
| Virtual IP | Allows for directing traffic to multiple zones | n/a | VIP in each availability zone | VIPs for clusters in each region |
| Load balancer | Directs traffic in each region | n/a | One load balancer in each region | configuration needs to be duplicated for failover |
| SQL Cluster | Provides out of region resiliency for SQL | t3.micro | SQL runs as primary in region and read only in other regions |
| SQL Data | Data stored in the database | db.t3.micro | 4 db instances | Data replicated to secondary region in near real time |

### Descriptions
The application infrastructure consists of a two node web server cluster with cluster nodes in 2 regions and virtual machine instances in mutiple availability zones.  
Virtual IP address exist in each availabilty zone and a load balancer is configured in each region to route traffic.
SQL is deployed using a two node cluster in two availability zones.  A HA primary read/write copy runs in one region with replicated data going to a read only cluster in the other region. 


## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.
1.  Configure the web server cluster in Terraform in zone 1.  Duplicate the configuration into a zone2 directory and update the appropriate availability zones.
2.  Configure the SQL server primary and secondary instances in terraform zone1 directory.
3.  Run terraform apply from each zone folder to build the infrastructure in both regions


## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region