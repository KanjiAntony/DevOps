# Import sql file residing in local machine to a mysql docker container

# Requirements
* Docker installed

# Configuration file
To download our mysql image and run a container, we will use docker compose yaml file.
Below is a sample file

![sample_docker_compose_image]

# 1. Start our docker container
From the compose file, we will pull an image from the public repository to our local machine

Command to run our compose file :

<code>docker-compose -f sample_docker_compose.yaml up</code>

![start_our_docker_containers_image]

# 2. Check our networks, volumes and view sql file inside our mysql container
If we were to containerize our application that will have access to our mysql container, then we must ensure they are on the same network and we can define in our compose file.
Volume on the other hand will provide persistence of our data. It is more like a backup area on our local machine or remote servers.
Volumes will help us maintain our data even after restarting a container.

* Command to check the networks:

    <code>docker network ls</code>

* Command to check the volumes:
    
    <code>docker volume ls</code>
    
* Command to check the running containers:
    
    <code>docker ps</code>
    
* Command to access our container's interactive shell:

    <code>docker exec -it ABCDE /bin/bash</code> or <code>docker exec -it ABCDE /bin/sh</code> where <code>ABCDE</code> is the container ID

![check_network_volume_image]

Once we are the container's interactive shell, we can navigate to our volume location which we specified in our compose file
i.e <code>cd /home</code> and the you can see the sql file which was backed up from our local machine.

# 3. Create our database and import our sql file using two methods

# a.) Method 1

After creating our database, we can use the database and import tables using the command <code>SOURCE /home/backup.sql</code>

![mysql_login_and_import_style_1_image]

Method 1 Tables

![show_tables_imported_image]

# b.) Method 2

Having our known database e.g sql_compose_another, inside the container's interactive shell, we can run the command below to import sql tables to that database

<code>mysql -u root -pPassword sql_compose_another < /home/backup.sql</code>

![mysql_login_and_import_style_2_image]

Method 2 Tables

![mysql_style_2_tables_image]

[sample_docker_compose_image]: images/sample_docker_compose_img.png "Sample docker compose yaml file"
[start_our_docker_containers_image]: images/start_our_docker_containers.png "Start docker container"
[check_network_volume_image]: images/check_network_volume.png "Check our networks and volumes"
[mysql_login_and_import_style_1_image]: images/mysql_login_and_import_style_1.png "First method of importing our sql file"
[show_tables_imported_image]: images/show_tables_imported.png "Tables imported using first method"
[mysql_login_and_import_style_2_image]: images/mysql_login_and_import_style_2.png "Second method of importing our sql file"
[mysql_style_2_tables_image]: images/mysql_style_2_tables.png "Tables imported using second method"