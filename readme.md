Setup of Jenkins 

Installation

Build the Jenkins BlueOcean Docker Image 

docker build -t myjenkins-blueocean:2.414.2.

docker pull devopsjourney1/jenkins-blueocean:2.332.3-1 && docker tag devopsjourney1/jenkins-blueocean:2.332.3-1 myjenkins-blueocean:2.332.3-1

Create the network 'jenkins'

docker network create jenkins


Run the Container

docker run --name jenkins-blueocean --restart=on-failure --detach `

  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  
  --volume jenkins-data:/var/jenkins_home `
  
  --volume jenkins-docker-certs:/certs/client:ro `
  
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.414.2

Get the Password

docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword

Connect to the Jenkins

https://localhost:8080/

Setting up the github repository

In Jenkins we will now add this repository link

While configuring we will check the Poll SCM

Then inside the Schedule box " * * * * * " paste this . 

This indicaes for every 1 min it will check the version control to build automatically if new commit has occurred.

Refer the doc for better understanding.
