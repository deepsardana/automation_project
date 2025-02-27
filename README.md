# Automation_Project

Upgrad Course Assignment

This Script Should Perform below tasks -

1) Perform an update of the package details and the package list at the start of the script.
sudo apt update -y

2) Install the apache2 package if it is not already installed. (The dpkg and apt commands are used to check the installation of the packages.)
Ensure that the apache2 service is running. 
3) Ensure that the apache2 service is enabled. (The systemctl or service commands are used to check if the services are enabled and running. Enabling apache2 as a service ensures that it runs as soon as our machine reboots. It is a daemon process that runs in the background.)
4) Create a tar archive of apache2 access logs and error logs that are present in the /var/log/apache2/ directory and place the tar into the /tmp/ directory. Create a tar of only the .log files (for example access.log) and not any other file type (For example: .zip and .tar) that are already present in the /var/log/apache2/ directory. The name of tar archive should have following format:  <your _name>-httpd-logs-<timestamp>.tar. For example: Ritik-httpd-logs-01212021-101010.tar                                                             Hint : use timestamp=$(date '+%d%m%Y-%H%M%S') )
5) The script should run the AWS CLI command and copy the archive to the s3 bucket. 
	#Hint : use timestamp=$(date '+%d%m%Y-%H%M%S') ) to name  the  tar
	aws s3 \
	cp /tmp/${myname}-httpd-logs-${timestamp}.tar \
	s3://${s3_bucket}/${myname}-httpd-logs-${timestamp}.tar
 
6) Copying to the S3 bucket will require AWS Command Line Interface (CLI)  to be installed in the system. You can install AWS CLI manually before writing and testing the script. 

  Installing awscli 
  
  sudo apt update
 
  sudo apt install awscli

7) Ensure that your script checks for the presence of the inventory.html file in /var/www/html/; if not found, creates it. This file will essentially serve as a web page to get the metadata of the archived logs. (Hitting ip/inventory.html will show the bookkeeping data)
	At any point in time, the first line in the inventory.html file should be a header that will look like this:

	Log Type Time Created Type Size

	If an inventory file already exists, the content of the file should not be deleted or overwritten. New content should be only appended in a new line.

	When your script runs, it should create a new entry in the inventory.html file about the following:

	A) What log type is archived? 
	B) Date when the logs were archived 
	C) The type of archive 
	D) The size of the archive

8) Your script should create a cron job file in /etc/cron.d/ with the name 'automation' that runs the script /root//automation.sh every day via the root user.
	The script should be placed in the /root// directory. (Example: If your Git repository is named ‘Automation_Project’, the cron job will then run the script present in /root/Automation_Project/automation.sh)

	Your automation script is supposed to check if a cron job is scheduled or not; if not, then it should schedule a cron job by creating a cron file in the /etc/cron.d/ folder.  