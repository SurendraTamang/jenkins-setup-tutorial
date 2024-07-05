# jenkins-setup-tutorial
Installing jenkins https://www.jenkins.io/doc/book/installing/docker/
I am following this docs for installing jenkins on docker :)


### Steps
1. Create the bridge network for jenkins
   ```bash
   docker network bridge jenkins
   ```
   This network name **jenkins** will be used.

2. Pull the docker bind image, used for executing Docker commands inside Jenkins nodes
   ```bash
   docker image pull docker:dind
   ```

3. Run below command for for executing the docker commands

 ```bash
   docker run --name jenkins-docker --rm -d --privileged --network jenkins --network-alias docker --env DOCKER_TLS_CERTDIR=/certs --volume jenkins-docker-certs:/certs/client --volume jenkins-data:/var/jenkins_home --publish 2376:2376 docker:dind --storage-driver overlay2
  ```
4. Make sure to have the **Dockerfile** file copied
5. Building the image
```bash
    docker build -t mylocaljenkins-blueocean:0.0.0.1 .
   ```
6. Now time for running the image
   ```bash
  docker run --name jenkins-blueocean --restart=on-failure --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --publish 8080:8080 --publish 50000:50000 --volume jenkins-data:/var/jenkins_home --volume jenkins-docker-certs:/certs/client:ro mylocaljenkins-blueocean:0.0.0.1
   ```
