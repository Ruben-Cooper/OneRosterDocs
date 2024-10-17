# Moodle Docker Install Guide

This installation guide is provided for any person that wishes to host a Moodle 3.11 Server using docker. Docker is supported on Linux, MacOS an Windows, however this guide will be specifically showing the Windows installation, although other operating systems will be very similiar. 


**Purpose**: A installation guide showing how to successfully install a complete contanerised moodle server. This guide can be used by anyone was specifically made to assist open-soure contributors to setup a environment ready for plug-in development. 

## Prerequisites
- WSL 2 with Linux Installation (for windows users only) 
- Docker (Latest Version)

## Installation Steps
1. **Setting up the Docker Compose files**
- Step 1: Download the following zip: https://github.com/Ruben-Cooper/T075-IFB399-Docs/blob/master/assets/docker-capstone.zip
- Step 2: Download Moodle 3.10.11: https://download.moodle.org/releases/legacy/
- Step 3: Place the Moodle download into /sites/
- Step 4: Copy the `./config.php` into `./sites/moodle/config.php`

2. **Install docker containers via docker compose**
- Step 1: Open a WSL terminal 
- Step 2: Change directory to the file path of the docker-capstone directory: 
  This can be done by going through the /mnt/ directory for example:
  ```cd /mnt/c/Users/{username}/Desktop/docker-capstone```<br>
  Note: While its easier to develop Moodle plugins using the mnt directory this can cause Moodle to be very slow due to slow R/W speeds (due to filesystem conversion) consider using the native WSL directory if you run into anny errors, see Troubleshooting for more information.<br><br>
- Step 3: In the terminal run ```docker compose up -d```

1. **Install Moodle**
- Step 1: Visit https://moodle.localhost and follow the installation steps until you get to the database setup screen.
- Step 2: Select PostgreSQL and fill in the relevant fields seen here:
   ![pgsql](/img/pgsql.png)
- Step 3: Continue to follow the installation steps.
<br>
  Moodle will now be fully installed and ready to use and develop, look at the next section for programming best practices. 


## Troubleshooting
