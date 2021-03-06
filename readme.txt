						*****	README	*****

Assignment 2
------------

The objective of this assignment is to find the correlation between servers and network elements. Server metrics such as CPU usage, Requests per sec, 
Bytes per sec and Bytes per request are retrieved from web GUI of apache server(server-status). The bitrate of network elements are retrieved using SNMP 
and stored in RRDs.   
The results are presented through a web dashboard.

This document describes the information about the various files in this folder, modules/software needed and steps to run this assignment.

This folder consists of 6 files in total:
-----------------------------------------

1. backend.pl
2. index.php
3. result.php
3. db.php
4. datapath.pl
5. readme.txt

Software Requirements:
----------------------

1. Operating System: Ubuntu 14.04 LTS.

2. You need to install Apache server, MySQL and PHP.

3. Modules which are needed to be installed from CPAN are:
   Data::Dumper
   DBD::Mysql
   DBI
   Cwd
   LWP::Simple
   Net::SNMP
   RRD::Simple

4. Install packages from terminal (sudo apt-get install ____)
   snmp && snmpd
   rrdtool	 
   librrds-perl		
   php5-rrd
 
Steps to run this assignment:
-----------------------------
1. Once the database and DEVICES table are setup , modify the db.conf file in the root directory accordingly. The backend script will access the 
   database mentioned in db.conf use the device credentials mentioned in the table (IP, PORT and COMMUNITY) to obtain bitrate for network elements
   and server metrics for the servers. 

2. Go to the terminal cd into the directory where this folder is present
   (It is assumed that the working directory configured in the apache server is /var/www/html/, change the path accordingly) 

3. Now, open a web browser and type the following URL:
   http://localhost/et2536-ropo15/assignment2/
   It will open index.php and show the dashboard containing DEVICES table along with tables myserver and mydevice. The required devices and servers are to be inserted into the 
   tables and then the backend must be executed.

4. Run the shell script "backend" in the terminal with the command "perl backend".
   The backend will retrieve device credentials from the table, conduct snmp get request to get interfaces of each device, retrieve bitrate for the interfaces.
   RRDs are used to store inOctets and outOctets. Also, server metrics are retrieved by taking the values from "/server-status?auto" of each server. Seperate RRDs
   are used for each device and server.  

5. Choose the desired options to view the server and device metrics.

NOTE:
-----
Make sure to create the "myserver" table & "mydevice" table in the MySQL database prior to running the backend script in the terminal. 
They are automatically created by accessing the index page of the frontend.

The user can insert or delete devices through web GUI by simply removing them from myserver and mydevice tables.
