### Creating a RDS PostgreSQL Database on the AWS Free Tier
Reference: https://www.youtube.com/watch?v=I_fTQTsz2nQ

#### Initial Setup Instructions
- In search bar, search for RDS, and select the button to Create a Database.
- Choose standard create option. Select Postgresql engine type.
- Select Free Tier under Templates section.

Settings Section
- Update DB instance name: media-backlog-api
- Update master username: postgres
- Set master password: to-be-determined

Instance Configuration
- Utilize: db.t3.micro

Storage
- General Purpose SSD (gp2)
- Allocated Storage: 20 GB
- Disable Storage Autoscaling

Connectivity
- Default VPC, and Subnet Groups: Default
- Public Access: Yes
- Security Group
  - Choose Existing VPC
  - Maintain "default" security group
  - No preference necessary for Availability Zone (AZ)
  - Database port: 5432

Database Authentication: Password authentication

Initial Database Name: media-backlog-api
- Disable automated backups
- Enable encryption
- Performance Insights: Enabled

Monitoring: Disable
Maintenance and Others: Default

### Working with Postgresql
[Reference #1]([url](https://www.codementor.io/@engineerapart/getting-started-with-postgresql-on-mac-osx-are8jcopb))
[Reference #2](https://www.commandprompt.com/education/different-methods-to-create-a-table-in-postgresql/)

Network ACL
- Establishes rules for network traffic. Attached at subnet level.
Security group. Attached at level of EC2 instance
- All things that I want to accept. 

To Do:
1. Update security groups with new port range and source
2. GET/UUID to get one record back, POST, DELETE
3. Make web application able to run on server.
4. Run on server with database.
