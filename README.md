Documentation for Bulk-api-v2 setup instructions in Linux
-

### Prerequisites

- JDK 
- Apache Tomcat
- PostgreSQL
- Spring Tool Suite 3.9.6
- Maven 3.3.X

Note := To open Terminal press Alt+Ctrl+T in keyboard.
       To enter in to Administrative access give command $ sudo su and give password.


Download JDK for Linux
-

To Download and install JDK in Ubuntu open Terminal and give command below each

```			
$ sudo apt-add-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
```

Verifying jdk installation
-
To verify installation of java, give this
  ```
  $ java -version
  ```

Download and Install Apache Tomact 
-
-  Open the Web browser download Apache Tomcat 8 
- Download the tar.gz file of Apache tomact with this link https://tomcat.apache.org/download-80.cgi#8.0.53 
- Extract Tomcat downloaded file, Open Extracted file, open bin, and locate the bin path of this file in terminal.
```
<<apache installed dir>>/apache-tomcat-8.0.53/bin$ ./startup.sh
```
-  Now Open Chrome and type http://localhost:8080/ to open Tomcat home Page, this verifies Tomcat is running successfully in our machine.
--------------------------------------------------------------------------------------------------------------------------------------

Download And Install PostgreSQL Linux
-
PgSQL is a procedural programming language supported by the PostgreSQL ORDBMS. Installation is shown, give each command in terminal and press enter.
```
$ sudo apt-get install postgresql postgresql-contrib
$ ls /etc/postgresql/10/main
$ service postgresql status
$ sudo su postgres
$ psql
$ bash-4.4# psql -U postgres
postgres=#
```

  To Create Database
  -
  - Give below command to create database in terminal
  ```
  For Bulk Data
  postgres=# CREATE DATABASE bulkdata;
  ```
  To connect to our Database
  -
  ```
  For Bulk Data
  postgres=# \c bulkdata
   ```
  To import Database
  -
  - Give below command to create database in terminal
  ```
  For Bulk Data
  postgres=#psql -U username dbname < bulkdata.pgsql
  ```
--------------------------------------------------------------------------------------------------------------------------------------
Load DSTU2 schema and data
-
- To create database hapi
  ```
  postgres=# CREATE DATABASE hapi;
  ```
- To connect to database hapi
  ```
  postgres=# \c hapi
  ```
To import Database hapi

- DSTU2 database file “hapi-server.backup” is located under root directory. Load schema and sample data using psql command
- First Select Database to import its sql file, then go to plugin in menu bar click PSQL Console and give below command in terminal
- Give below command to create database in terminal
  ```
  postgres=#psql -U username dbname < hapi-server.backup
  ```
Clone FHIR Server repository
-
Clone FHIR Server repository using command
```
$ git clone https://github.com/siteadmin/fhir-tools.git
```

Spring Tool Suite Installation
-

  - Download STS for Linux or Windows from below link https://spring.io/tools3/sts/all 
  - Go to Downloads, then Unzip, spring-tool-suite-3.9.6.RELEASE-e4.9.0-win32-x86_64.zip, and now STS is ready to use
  To Open STS
  - Go to Downloads , then open sts-3.9.6.RELEASE , then double click on STS.exe

  Built Application 
  -
  Run Maven build to build application war file. 
  ```
  $ mvn clean install 
  ```
  This will generate a war file under target/{application-name}.war. Copy this to your tomcat webapp directory for deployment.

  To Add Server in STS
  --

   - In Quick Access Type Server and enter
    - Right Click on blank white space, Then New , and Server
    - If we don't find Tomcat Server then follow below steps
      - Go to Help in menu bar click on Eclipse Market Place
      - Here type Eclipse JST Server Adapter and install, now it asks for Restart click on it
    - Apache, here Tomcat v8.0 Server then Next
    - In next window, browse the Tomcat path and give finish.

  To Import Bulk-api-v2 project from existing location in to sts ide
  --
  -  In STS, Click on File in menu bar, click on import then in Maven Projects, click on Existing Maven Projects. Click on Next. Pop-up 	window appears, Click on browse and search the path of bulk-api-v2 project and finally finish

   To Run Bulk-api-v2 Project
   --

   - Right Click on bulk-api-v2 then Click Run AS and Run on Server, a pop-up window opens
    - Select Pivotal or Apache Tomcat Server then Finish
    - Output is shown in console output with local url http://localhost:8080/bulk-data-api/ 

   Client Registration
   --

   -  Once project is running, we have to do client registration with local url http://localhost:8080/bulk-data-api/view/clients.html  with following details
    - Registring New Client 
	     ```
	      UserName 	   abc123
	      Email    	   abc123@gmail.com
	      Full Name         abcdefg
	      Password 	   abcxyz
	     ```
-  Then click OK, inside this another web page opens, click on Register Backend Client with public der file, check for both system and user.
	```
	Backend Client Registration
		Client App Name       bulk data api
		Organization	      Xyram
		Client Issuer URL     http://localhost:8080/bulk-data-api/
		Public Key            Upload Public Key
		Scope		      Check both system and user	
	```

	- After registration, it generate ClientID and token URL as follows
	```
	Client ID :     bulk data apiVxAHtrAqt1
	Token URL :  http://localhost:8080/bulk-data-api/token
