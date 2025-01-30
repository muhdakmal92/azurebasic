1) Click Create a resource.
2) Select Database > SQL Database > Create
3) Fill out the SQL Database form with the following information

   Resource group: Select rg_eastus_XXXXX
   Database name: Enter WhizDatabase
   Server: Click on create new
   Server name: Enter a unique name
   Location: Select East US
   Authentication method: Select Use SQL authentication
    Server admin login: Enter WhizAdmin
    Password: Enter a password
    Confirm password: Re-enter the password

4) Server: Select the newly created server
   Want to use SQL elastic pool : Select No
   Compute + Storage : Select Configure database
   Service tier : Select Basic (For less demanding workloads)
   Backup storage redundancy: Select Locally-redundant backup storage

5) Networking and update the connectivity method to public endpoint.
   ##This allow access from Public IP such as our personal PC.

6) Once the server is created, click the hostname and open "Networking"
   Under, Firewall rules, click + Add your client IPv4 address on the toolbar to add your current IP address to a new IP firewall rule. An IP firewall rule can open port 1433 for a single IP address or a range of IP addresses. 
   Scroll down and check the box for Allow Azure services and resources to access this server

7) Go to "Query editor" to edit your dataabase
8) Use this and Run to test

-- Create Person table          
CREATE TABLE person        
(          
personid INT IDENTITY PRIMARY KEY,          
firstname NVARCHAR(128) NOT NULL,          
middelinitial NVARCHAR(10),        
lastname NVARCHAR(128) NOT NULL,            
dateofbirth DATE NOT NULL          
)          
-- Create Student table        
CREATE TABLE student            
(          
studentid INT IDENTITY PRIMARY KEY,        
personid INT REFERENCES person (personid),          
email NVARCHAR(256)        
)          
-- Create Course table          
CREATE TABLE course        
(          
courseid INT IDENTITY PRIMARY KEY,          
NAME NVARCHAR(50) NOT NULL,        
teacher NVARCHAR(256) NOT NULL          
)          
-- Create Credit table          
CREATE TABLE credit        
(          
studentid INT REFERENCES student (studentid),          
courseid INT REFERENCES course (courseid),          
grade DECIMAL(5, 2) CHECK (grade <= 100.00),            
attempt TINYINT,            
CONSTRAINT [UQ_studentgrades] UNIQUE CLUSTERED ( studentid, courseid, grade, attempt )          
)
