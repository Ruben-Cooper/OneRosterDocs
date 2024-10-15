# RosterHub Installation Guide

This installation guide is provided for our OneRoster plug-in project to be used as a backend RESTAPI server (compatiable with the OneRoster v1.1 spec) and is strictly used for testing purposes. 

The main reason for the use of rosterhub is due to its ability to convert CSV data directly into its RESTAPI, allowing for a greater understanding of the OneRoster spec and for testing. 

**Github**: https://github.com/lepo-project/roster-hub

**Purpose**: A quickstart guide showing how to successfully install a contanerised rosterhub server instance to be used as a backend RestAPI server for the oneroster plugin.

## Prerequisites

- Docker
- Moodle (< 3.11)
- OneRoster Moodle Plugin

## Installation Steps

1. **Adding the RosterHub docker container**
  Create a new Dockerfile with the following contents:
```Dockerfile
FROM ubuntu:22.04

ENV TZ="Australia/Brisbane"

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    ruby-dev \
    build-essential \
    git \
    libmysqlclient-dev \
    libyaml-dev \
    tzdata

RUN git clone https://github.com/lepo-project/roster-hub.git /opt/roster-hub
RUN gem install bundler
WORKDIR /opt/roster-hub
RUN bundle install
RUN EDITOR="vi" bin/rails credentials:edit
RUN rails db:migrate
CMD ["bin/rails", "server", "-b", "0.0.0.0"]

```
Note: Place this under /sites/rosterhub if using the provided docker files.

2. **Update the docker compose file**
   Update the docker-compose.yaml file to recognise the additional docker container:
   ```yaml
   services:
    rosterhub:
      ports:
        - "3000:3000"
    restart: always
    build:
      context: ./sites/rosterhub/
      dockerfile: Dockerfile
   ``` 
   Note: Remember to run docker compose again in order for the RosterHub installation and container initalisation to take place.
   <br>
3. **Create oauth application**
   Create a new oauth application using doorkeeper by running the following commands within the rosterhub container:
- Step 1: Enter the rails console by running: ```rails console```
- Step 2: Create a new doorkeeper app by running:
  ```
  app = Doorkeeper::Application.new
    name: 'rosterhub',
    redirect_uri: 'http://moodle.localhost/admin/oauth2callback.php'
    uid: 'admin'
    secret: 'F9RYtkHLyjK4mW4K5Rl5uzTZo0G3XfqW' 
  ```
  Note: Replace secret with your choice of a secret key
- Step 3: Save the new app: ```app.save```
4. **Request a bearer token**
   - In order to test if the installation has worked successfully run the following code on the moodle container:
   ``` 
   curl -i http://rosterhub:3000/oauth/token -F grant_type="client_credentials" -F client_id="admin" -F client_secret="F9RYtkHLyjK4mW4K5Rl5uzTZo0G3XfqW"
   ```
   - This command should output a bearer token like so:<br>
     ![bearer](/img/tokenoutput.png)
  Note: If an error occurs due to a blocked host, consult the troubleshooting section at the end of this guide.
<br>

5. **Connect RosterHub to the OneRoster PlugIn on Moodle**
   - Navigate to the settings of OneRoster and make a connection to the new RosterHub server.
   - An Example Configuration is as follows:<br>
     ![connection](/img//connection.png)

6. **Import CSV Files**
   - Step 1: Import the OneRoster CSV files this can be completed by placing a zip file named ```oneroster.zip``` containing the OneRoster CSV Files into /opt/roster-hub/storage/csv on the RosterHub docker container.
   - Step 2: Execute the CSVImport bash script, this will import the CSV files into RosterHub's SQL Database:<br>
    ![bash](/img/Bashscript.png)

7. **Run OneRoster full_sync**
   - Wait for the next full_sync job or run manually, this will complete the import process and retrieve data from the RosterHub API.
  



## Troubleshooting

If you encounter issues with Blocked Hosts as seen here:<br>
![blockedhost](/img/blocked.png)

Follow these steps to resolve:
1. On the RosterHub container open the config/environments/development.rb file.

Note: this file might be different depending on the configured environment this can be found by running:<br>
![env](/img/env.png)

2. Add the rosterhub:3000 to the whitelist by adding the following line to the file:
   ```
   Rails.application.config.hosts << "rosterhub:3000"
   ```
3. Restart the rails server by running: ```rails restart```

Troubleshooting Suggestions
If further troubleshooting is required test the API with curl alternatively test with API Platforms such as Postman or Insomnia on your localmachine. Otherwise consult the RosterHub Github Repo.

Example 1:
An example of testing the API using Postman from the local machine can be seen here:<br>
![postman](/img/postman.png)

Example 2:
Testing the API on the Moodle Container by running: 
```
curl -i http://rosterhub:3000/oauth/token -F grant_type="client_credentials" -F client_id="admin" -F client_secret="F9RYtkHLyjK4mW4K5Rl5uzTZo0G3XfqW"
```

This outputs:<br>
![apioutput](/img/output.png)