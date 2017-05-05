# Docker Containers to develop (micro)services with MuleSoft

A set of Dockerfiles to set up a environment for development and testing purposes.

## Containers

### 1.  MuleSoft Anypoint API Gateway Docker image (using temporary license for development)

1.1. Getting a Docker image from Docker Hub:
```bash
$ docker pull chilcano/mule-api-gw
```

1.2. Building and tagging the Docker base image (if the Docker Hub is not used), make sure `Dockerfile` is under `docker-mulesoft-dev/mule-api-gw/`:
```bash
$ git clone https://github.com/chilcano/docker-mulesoft-dev

$ docker build --rm -t chilcano/mule-api-gw docker-mulesoft-dev/mule-api-gw/.
```

1.3. Creating/starting a container in detached mode:
```bash
$ docker run -dt --name muleapigw01 chilcano/mule-api-gw
```

1.4. Creating/starting a container in interactive mode:
```bash
$ docker run -it --name muleapigw02 chilcano/mule-api-gw
```

1.5. Creating/starting a container in detached mode with volumes and accessible ports:
```bash
$ docker run -dt --name muleapigw03 \
-p 17777:7777 -p 18082:8082 \
-v ~/3docker/muleapigw01/logs:/opt/muleapigw/logs \
-v ~/3docker/muleapigw01/conf:/opt/muleapigw/conf \
-v ~/3docker/muleapigw01/apps:/opt/muleapigw/apps \
chilcano/mule-api-gw
```

1.6. Getting Shell access in interactive mode:
```bash
$ docker exec -it muleapigw01 bash
```

1.7. Destroying the containers and base image:
```bash
$ docker rm muleapigw01 muleapigw03 muleapigw03
$ docker rmi -f chilcano/mule-api-gw
```

1.8. Listing containers and images:
```bash
$ docker ps -a
$ docker images
```

__Considerations:__
* MuleSoft Anypoint API Gateway can be downloaded from here: https://www.mulesoft.com/ty/dl/api-gateway
* This Docker image only provides a 30 day license of MuleSoft Anypoint API Gateway. To deploy a new license, remove/destroy the Docker image or create a new one, download a new version of MuleSoft API Gateway if deeded and place the license file into the `conf` directory, previously to map `conf` to your host.
* Setup MuleSoft Anypoint Studio account. It will be need for the license. After that go to the settings page and get your `client_id` and `client_secret`. Next update the `wrapper.conf` file to include the below two lines:
```
wrapper.java.additional.<n>=-Danypoint.platform.client_id=<your-client-id>
wrapper.java.additional.<n>=-Danypoint.platform.client_secret=<your-client-secret>
```
* To deploy your APIs and Applications created with MuleSoft Studio you have to mount the `apps` directory and place the zip there.

### 2.  MuleSoft Runtime Docker image (using temporary license for development)

TBC

### 3.  MuleSoft Management Console Docker image (using temporary license for development)

TBC
