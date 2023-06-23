# claranet-ansible
This repository contains two playbooks that will configure the needed environment on EC2 Instances.
- claranet-ansible-playbook-application
- claranet-ansible-playbook-database

## claranet-ansible-playbook-application

### Role Variables
--------------
The following variables are the main one used to configure the environment to be able to deploy the application. There are described non explicit variables, to see all of them please refer to `playbooks/config/application_vars.yaml`.

| Variables | Default Values | Descriptions | 
| --------- | -------------- | ------------ | 
| application_service_destination | /lib/systemd/system/cloud-phoenix-kata.service | Directory where to deploy the application service.
| application_start_script | {{ application_code_destination }}start.sh | The directory where to find the start.sh file to start up the application.
| application_code_destination | /opt/app/ | Directory where to clone the application code.


### Roles
This playbook has two main roles 
- install_application : retrieve the code from GIT, deploy the start.sh script on the EC2 instance.
- configure_application : create the service of the application and starts it.

## claranet-ansible-playbook-database

### Role Variables
--------------
The following variables are the main one used to configure the environment to be able to deploy the dattabase. There are described non explicit variables, to see all of them please refer to `playbooks/config/database_vars.yaml`.

| Variables | Default Values | Descriptions | 
| --------- | -------------- | ------------ | 
| mongodb_repository_information_file_destination | /etc/yum.repos.d | Directory where to add the mongodb-org.repo file

### Roles
- install_database : install necessary dependencis, install the MongoDB database and starts up the database.
- configure_database : create a database, create a user for this database and create a cron job for database backup.

