# Create docker image
docker build . -t ssi_jenkins_local

# Create a docker volume - this will setup the container to be stateful 
docker volume create DOCKER_VOLUME

# run / build the docker container using the latest version of jenkins
docker container run -d \
    -p 8080:8080 \
    -v //var/run/docker.sock:/var/run/docker.sock \
    -v DOCKER_VOLUME:/var/jenkins_home \
    --name ssi-jenkins-local \
    ssi_jenkins_local

# install docker insdie
curl https://get.docker.com/ > dockerinstall && chmod 777 dockerinstall && ./dockerinstall

apt-get install maven
