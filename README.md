# Docker Picapport installation on ARM

## Install from scratch

Follow those simple steps: 

1. Clone the git repo
    ```bash
    git clone https://github.com/patklaey/docker-picapport
    cd docker-picapport
    ```
1. Modify the ```docker-compose.yml``` file and make sure you have mapped all the folders you need as volumes
    ```bash
    vi docker-compose.yml
    ```
1. Start up the container
    ```bash
    docker-compose up -d
    ```
    
## Install from existing Picapport installation

Only follow these steps if you had the same setup before (location of the pictures, DB version, etc), otherwise the
database might have to be initialized again so you could also start from scratch

1. Clone the git repo
    ```bash
    git clone https://github.com/patklaey/docker-picapport
    cd docker-picapport
    ```
1. Modify the ```docker-compose.yml``` file and make sure you have mapped all the folders you need as volumes
    ```bash
    vi docker-compose.yml
    ```
1. Start and stop the container to let docker create the volumes
    ```bash
    docker-compose up -d
    docker-compose down 
    ```
1. Check the database volume mount point
    ```bash
    docker volume inspect --format '{{ index .Mountpoint }}' docker-picapport_database
    ```
1. Copy the database from your backup to the volume mountpoint
    ```bash
    cp -r /path/to/backup/db_xyz /mountpoint/db_xyz
    cp /path/to/backup/dbconfig.txt /mountpoint/dbconfig.txt
    ```
1. If you have a backup of the cache and/or users, repeat exact same steps for cache. For users just copy the users 
directory to the container once it's up and running
1. Start the docker container again
    ```bash
    docker-compose up -d
    ```
    
# Operations

## Add new pictures

To add new pictures, simply add them to the ```/data/Pictures``` directory in the container. To do that, add a new line 
in the ```docker-compose.yml``` file under ```volumes``` to have your directory on the host shared with the container.
Then simply recreate the container (careful, do NOT add the -v option to docker-compose down to not delete the volumes): 

```bash
docker-compose down
docker-compose up -d
```