# Most important Docker operations

**[Docker Cheat Sheet](https://www.geeksforgeeks.org/docker-cheat-sheet/)**

1️⃣ **List all running containers** 
```bash 
docker ps -a
```

2️⃣ **Run a container in interactive mode and provide access to the terminal** 
```bash
docker run -it --name <container_name>
```

3️⃣ **Change the image Installation Directory** 
* [How to move docker data directory to another location on ubuntu](https://www.guguweb.com/2019/02/07/how-to-move-docker-data-directory-to-another-location-on-ubuntu/) &
* [Docker image change installation directory](https://www.baeldung.com/ops/docker-image-change-installation-directory)
```bash 
docker info -f '{{ .DockerRootDir }}'
mkdir -p /tmp/new-docker-root
sudo vi /etc/docker/daemon.json
sudo cat /etc/docker/daemon.json
{ 
   "data-root": "/tmp/new-docker-root"
}
sudo systemctl restart docker
docker info -f '{{ .DockerRootDir}}'
```

4️⃣ **Run an existing container again**
```bash
docker start  `docker ps -q -l` # restart it in the background
docker attach `docker ps -q -l` # reattach the terminal & stdin
```

5️⃣ **Delete all local docker images**
Source: https://stackoverflow.com/questions/44785585/how-can-i-delete-all-local-docker-images

* Delete all containers and volumes
```bash
$ docker rm -vf $(docker ps -aq)
```

* Delete all images
```bash
docker rmi -f $(docker images -aq)
```

6️⃣ **Clean-up complete after deleting all images**
Source: https://stackoverflow.com/questions/64068185/docker-image-taking-up-space-after-deletion
```bash
docker system prune -a
docker volume rm $(docker volume ls -q -f dangling=true)
```

7️⃣ **Open a second terminal for a docker container that is running**
```bash
docker exec -it <container_name> bash
```

-----------------------------------------------
Docker Compose (similar to launch files in ROS)
-----------------------------------------------

1️⃣ **Specify a [docker compose](https://docs.docker.com/compose/) file** 
**IMPORTANT:** The extension has to be .yml e.g. docker-compose.yml

```bash
version: "<version>"   // Prefer to use the latest version found on the docker page.
services:
  <custom_service_name>:   
    image: <image_name>
    ports:
      - <host_port>:<container_port>
    volumes:
      - <custom_volume_name1>:<container_directory_path1>
      - <custom_volume_name2>:<container_directory_path2>
volumes:
    <custom_volume_name1>
    <custom_volume_name2>
    ...
```

2️⃣ **Build an image via docker compose file**
```bash
docker-compose build --no-cache
```

3️⃣ **Execute a docker compose yml file**
```bash
docker-compose -f <yaml_name>.yml
```

4️⃣ **Start the image builded with docker compose**
```bash
docker-compose up
docker-compose up --build # can be combined with build
```

5️⃣ **Run the container with GPU support**

```bash
docker run --name <container_name> -it --rm \
  --net=host \
  --gpus all \
  -e NVIDIA_VISIBLE_DEVICES=all \
  -e NVIDIA_DRIVER_CAPABILITIES=all,graphics,utility,compute \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v /<host-folder-to map>:<docker-folder> \
  -e DISPLAY=$DISPLAY \
  -e LIBGL_ALWAYS_INDIRECT=0 \
  --add-host=host.docker.internal:host-gateway \
  <docker-image-name>
```

--------------
Docker Volumes
--------------
1️⃣ **Different kinds of [mounting volumes](https://www.youtube.com/watch?v=p2PH_YPCsis)**
* Host volume 
```bash
docker run -v <host_directory_path>:<container_directory_path>
```
* Anonymous volume 
```bash
docker run -v <container_directory_path>  # Here the host directory is located in the data directory usually: /var/lib/docker/volumes/random_hash/_data
```
* Named volume 
```bash
docker run -v <custom_name>:<host_directory_path>
```

----------
[Dockerfile](https://docs.docker.com/engine/reference/builder/)
----------
1️⃣ Create a file named Dockerfile (Note: in VS Code the dockerfile gets automatically identified)
