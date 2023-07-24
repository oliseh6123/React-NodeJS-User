# React-NodeJS-User

First move the pen file to the .ssh folder on local device
mv Downloads/docker-server.pem ~/.ssh/

ls -l .ssh/docker-server.pem 

Second change mode to make it read only chmod 400

cdmod 400 .ssh/docker-server.pem

Thirdly ssh into the EC2 instance

ssh -i ~/.ssh/docker-server.pem ec2-user@ip

Yum update on the instance

sudo yum update

sudo yum install docker

sudo service docker start

Check if docker is running

ps aux | grep docker

Ensure you don’t have to always sudo into user

sudo usermod -aG docker $USER

Loading the creating a docker image of your app and pushing to docker hub

docker build -t <your-dockerhub-username>/<image-name>:<tag> .

docker images

docker tag <image-id> <your-dockerhub-username>/<image-name>:<tag>

docker login

docker push <your-dockerhub-username>/<image-name>:<tag>

Login into docker on ec2 instance 

docker login   (luckily once you login you don’t have to again it creates a hidden file in ls .docker/config.json)

next you pull the images with docker pull repo name and appname:tag

docker pull obiwan6123/demo-test:1.0

Run (docker images) to see the images

Finally run the images in detach mode (-d) with (-p) instance port first:app port declared in the docker file

docker run -d -p 3000:80 obiwan6123/demo-test:1.0

On you Amazon console go to the running instance select the instance, go to security now  we want to add a new Inbound rule for port 3000 so that port can be open for the application. Refresh the instance page, open the site url with  IP:3000
