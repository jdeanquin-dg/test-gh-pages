---
layout: page
title: Install
permalink: /install/
---

# Installation instructions


### Hosting requirements:
Operating System: GNU Linux/Unix
CPU: 4 cores, 64 bit
RAM Memory: 16 GB
Storage: 350 GB
Network: Public IP address, Domain name, port 443

### Prerequisites:
Open JDK 8
Apache Tomact 8.5
PostgreSQL 14 with PostGIS 3.2.3 extension


### Deliverables:
Main application: amp-v3.5.war


### Email

Configure SMTP server to serve on localhost port 25 without any authentication, if you are enabling the server to send emails. 

### PostgreSQL

Application connects to the database via 5432 port.

Make sure that postgres user exists and PostgreSQL is configured to trust all local ip v4 connections.

In /etc/postgresql/14/main/pg_hba.conf you must have the following lines:

```
IPv4 local connections:
host	all         	all         	127.0.0.1/32        	trust
```


### Application Settings

### Installation steps

#### **Here are the steps to install the application on a Linux server**

- Create a database backup (you can skip this step if it's a fresh first installation):

  - If it doesn't exist already, create  `~/bin/amp_pg_backup.sh` `(touch ~/bin/amp_pg_backup.sh)`
  - Run the following command to create a backup of the database:

    ```bash
    chmod +x ~/bin/amp_pg_backup.sh
    ```

  - insert with your favourite text editor the following lines (replacing `<server_name>` and `<version>`):

    ```bash
    DBNAME="amp_<server_name>_<version>
    cdate=$(date +%Y_%m_%d-%H.%M)
    pg_dump -vFc -Z 0 -h localhost -U postgres -w $DBNAME | 7za a -si "$DB_NAME_$cdate_pre_upgrade.sql.7z"
    ```

    e.g

    ```bash
    DBNAME="amp_moldova_211"
    cdate=$(date +%Y_%m_%d-%H.%M)
    pg_dump -vFc -Z 0 -h localhost -U postgres -w $amp_moldova_211 | 7za a -si "$amp_moldova_02_11_2015_pre_upgrade.sql.7z"
    ```

    - Check the username and pass for creating the database backup on the corresponding country installation page, if this doesn't work.
  
  - Execute the script: `~/bin/amp_pg_backup.sh`
  - (optional, but highly recommended) Validate the database backup (download it to your local machine, unpack it, and restore to a new database). If it managed to restore properly, which can be checked with a ```select count(*) from amp_activity_version``` returning some number, the backup is OK.

- Clone the repository from Github
  
- Build the application with Maven
  
    ```bash
    mvn clean package -Dapidocs=true -DserverName=local -Djdbc.db=<amp_dbname_version> -Djdbc.user=<db_user> -Djdbc.password=<db_password> -Djdbc.port=5432
    ```

- You can put the script in a file and execute it, e.g. `~/bin/amp_build.sh`:

    ```bash
    #!/bin/bash
    mvn clean package -Dapidocs=true -DserverName=local -Djdbc.db=<amp_dbname_version> -Djdbc.user=<db_user> -Djdbc.password=<db_password> -Djdbc.port=5432
    ```

- Verify that the PostgreSQL user and pass (jdbc.user and jdbc.password) are correct by checking the corresponding country installation page.

- Stop the application server (Tomcat)

- Delete the symlink to the application (replace `<version>` with your version of Tomcat)
- Create a new symbolic link in the tomcat webapps folder
  Example:

    ```bash
    ln -s <amp_folder_location> /var/lib/tomcat8/webapps/amp
    ```

- Configure the country you are installing AMP by doing the following:
  - Download from [Download Geonames dump](http://download.geonames.org/export/dump/) the ZIP file corresponding to the country of the installation you're working on.
  - The names of the zip files are based on the 2-letter ISO code for countries [ISO Country Codes](http://userpage.chemie.fu-berlin.de/diverse/doc/ISO_3166.html).
  - Extract the archive it and rename the `<TWO-letter-code-file>.txt` to `gazeteer.csv`. (This file is used on AMP startup to populate a table with the locations for a given country)
  - Copy the file in the `/doc` directory under the AMP installation.
  - Configure the latitude and longitude for the country you are installing AMP:
    - Login as Administrator (the country installation page can help you with getting the credentials, or the AMP online URLs page), go to Global Settings
    - Fill in the latitude and longitude for the country
    - Save the settings

- Start the application server (Tomcat)
- Verify that the application is running:
  - Go to the external address this server is visible at (check the country installation page for that)
  - Attempt to use AMP a bit: log in, see that tabs are loading, run a report, create an activity, add a document, open GIS, open dashboards.
  - Check Tomcat logs (usually under the tomcat directory / logs): check whether there any patches that failed to apply, or any exceptions having been thrown.
  
#### **Here are the steps to install the application on a Windows server**

- Create a database backup (go to pgadmin 4, right-click on your database->backup)
- Clone the repository from Github
- Stop the tomcat service (from the Administration tools -> Services app)
- Open a console, cd to the folder to which you have exported AMP.
- Build AMP (don't forget to modify `<server_name>`, `<version>`, and check the jdbc password, port and user in the corresponding country installation page)

```bash
mvn clean generate-resources process-resources -Dapidocs=true -DserverName=local -Djdbc.db=amp_<server_name>_<version> -Djdbc.user=amp -Djdbc.password=amp123 -Djdbc.port=5432
```

- Open a console and create a symlink on c:\amp\tomcat\webapps to the AMP version your upgrading to:
  
    ```bash
    mklink /J <path_to_tomcat>\webapps\ROOT <path_to_AMP>
    ```

- Configure the country you are installing AMP by doing the following:
  - Download from [Download Geonames dump](http://download.geonames.org/export/dump/) the ZIP file corresponding to the country of the installation you're working on.
  - The names of the zip files are based on the 2-letter ISO code for countries [ISO Country Codes](http://userpage.chemie.fu-berlin.de/diverse/doc/ISO_3166.html).
  - Extract the archive it and rename the `<TWO-letter-code-file>.txt` to `gazeteer.csv`. (This file is used on AMP startup to populate a table with the locations for a given country)
Make sure you have file extensions being shown ("hide file extensions for known file types" disabled under Folder options)
  - Copy the file in the `/doc` directory under the AMP installation.
  - Configure the latitude and longitude for the country you are installing AMP:
    - Login as Administrator (the country installation page can help you with getting the credentials, or the AMP online URLs page), go to Global Settings
    - Fill in the latitude and longitude for the country
    - Save the settings

- Start the tomcat service (from the Administration tools -> Services app)
- Verify that the application is running:
  - Go to the external address this server is visible at (check the country installation page for that)
  - Attempt to use AMP a bit: log in, see that tabs are loading, run a report, create an activity, add a document, open GIS, open dashboards.
  - Check Tomcat logs (usually under the tomcat directory / logs): check whether there any patches that failed to apply, or any exceptions having been thrown.

### Nginx

Web requests to the applications are dispatched by Nginx 1.14 webserver, running on Debian GNU/Linux Stable (Buster) AMD64.

The webserver is configured to redirect any plain text (HTTP) requests to their TLS-encrypted (HTTPS) counterparts. Additionally, it is enforcing Strict Transport Security by pinning the necessary headers. TLS certificate is provided by LetsEncrypt service. The server is configured to only allow secure modern encryption protocols (TLS v1.2 and v1.3) as well as only strong cipher suites.

The server requests compliant robots not to index the website by serving a restrictive robots.txt file.
