Documentation for Bulk-api-v2 setup instructions in Linux
-

### Prerequisites

- JDK 
- Apache Tomcat
- postgreSQL
- pgAdmin4
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
To verify installation give this
  ```
  <<java installed dir>>java -version
  ```

Download and Install Apache Tomact 
-
  Open the Web browser say Chrome to download Apache Tomcat 8 with link given below	
- Download the tar.gz file of Apache tomact with this link https://tomcat.apache.org/download-80.cgi#8.0.53 
- Extract Tomcat downloaded file, Open Extracted file, open bin, and locate the bin path of this file in terminal.
```
<<apache installed dir>>/apache-tomcat-8.0.53/bin$ ./startup.sh
```
-  Now Open Chrome and type http://localhost:8080/ to open Tomcat home Page, this verifies Tomcat is running successfully in our machine.
--------------------------------------------------------------------------------------------------------------------------------------

Download And Install PostgresSQL Linux
-
PgSQL is a procedural programming language supported by the PostgreSQL ORDBMS. Installation is shown, give each command in terminal and press enter.
```
$ sudo apt-get install postgresql postgresql-contrib
$ ls /etc/postgresql/10/main
$ service postgresql status
$ sudo su postgres
$ psql
```

Download And Install pgAdmin4 for Linux
-

Give below each commands in terminal 
```
  $ sudo apt-get install python2.7-dev virtualenv python-pip libpq-dev
  $ mkdir -p pgadmin4
  $ cd pgadmin4
  $ virtualenv venv -p /usr/bin/python2.7
  $ source ./venv/bin/activate
  $ wget https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v3.3/pip/pgadmin4-3.3-py2.py3-none-any.whl
  $ sudo pip install pgadmin4-3.3-py2.py3-none-any.whl
  $ cp ./venv/lib/python2.7/site-packages/pgadmin4/config.py ./venv/lib/python2.7/site-packages/pgadmin4/config_local.py
   (If there is no pgadmin4 file, copy and paste from pgadmin4-3.3-py2.py3-none-any.whl to site-packages)
  $ sudo python ./venv/lib/python2.7/site-packages/pgadmin4/pgAdmin4.py
  Starting pgAdmin 4. Please navigate to http://127.0.0.1:5050 in your browser.
  ```

Open pgAdmin4 in Ubuntu
-
  Note: To Connect to localhost, first we have to connect pgsql to localhost(psql -h localhost  -p 5432 -U postgres  in terminal), only then we can create and connect to server in pgAdmin4


  - Open pgAdmin4 in port 5050 with link as http://localhost:5050/browser/ 

  - Set the server, for this, right click on server, create and server a pop-up window will open
     In general give name as pgsql
     In connection give host name as localhost, then username as postgres password as postgres then save   
  To Create Database
  - Right click on Database which is below Server then Create and Database, pop-up window will appear
  - Give Database name as bulkdata and press OK. 

  To connect to our Database
  - click on pgsql which is below the server if server is connected
  - click on bulkdata
  - click on schemas
  - click on public
  - click on tables

To Download pgadmin3
-
  Give the below command in Terminal and enter, it installs the pgadmin3
  ```
  $ sudo apt-get install pgadmin3
  ```
  Next Open pgadmin3 here we have to set Server first
  To Add Server
  -
  - Go to file on top left corner of pgadmin3, then choose Add Server, a pop up window opens, give as below

    In Properties
    Name   			               psql
    Host   			               localhost   or 127.0.0.1
    Port    		            	 5432
    Service
    Maintenance Database		   postgres    
    User Name     		         postgres
    Password      	           postgres
    Store Password   	       	Check
    Give OK,, Again Ok for another window as well


  To import Database
  -
  First Select Database to import its sql file, then go to plugin in menu bar click PSQL Console and give below command in terminal
  ```
  bulkdata=# \i Downloads/export_30-03-2018.sql  
  ```
  ( Here after \i , that is the path of export_30-03-2018.sql file )
  - It imports Database in to project bulkdata.

--------------------------------------------------------------------------------------------------------------------------------------

To Import Database into pgAdmin4
-

Load DSTU2 schema and data
-
Create the database by running the below command in command prompt
```
	$ createdb -h localhost -p 5432 -U postgres hapi
```
DSTU2 database file “hapi-server.backup” is located under root directory. Load schema and sample data using psql command
```
	$ psql -U postgres -d hapi -f hapi-server.backup
```
Clone FHIR Server repository
-
Clone FHIR Server repository using command
```
$ git clone https://github.com/siteadmin/fhir-tools.git
```

Spring Tool Suite Installation
-

  Download STS for Linux or Windows from below link
  - https://spring.io/tools3/sts/all (Download From this)
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

   -  After running above project, we have to do client registration with local url http://localhost:8080/bulk-data-api/view/clients.html  with following details
    - Registring New Client 
	     ```
	      UserName 	   abc123
	      Email    	   abc123@gmail.com
	      Full Name    abcdefg
	      Password 	   abcxyz
	     ```
     Then give OK, inside this another web page opens, click on Register Backend Client with public der file, check for both system and user.
     
		    ```
			    Backend Client Registration
		      Client App Name       bulk data api
		      Organization	    Xyram
		      Client Issuer URL     http://localhost:8080/bulk-data-api/
		      Public Key            Upload Public Key
		      Scope		    Check both system and user	
		    ```

   - After registration it generate ClientID and token URL as follows
   
	    ```
	    Client ID :     bulk data apiVxAHtrAqt1
	    Token URL :  http://localhost:8080/bulk-data-api/token
	    ```
