# Dockering Flask Application.

- Launched an Ubuntu Ec2 instance for this project 

![ec2](/Project9/img/1-Created-instance-ubuntu.png)

- SSh into the Instance and updated the package index with
```
sudo apt update
```
- installed docker with
```
sudo apt install docker.io -y
```
![install](/Project9/img/2-ssh-into-instance-and-update.png)

- Started docker with the following commands
```
sudo systemctl start docker
```

- enabled docker with 
```
sudo systemctl enable docker
```

![install](/Project9/img/3-Install-start-enable-docker.png)

- went on to check the staus of docker with
```
sudo systemctl status docker
```

![status](/Project9/img/4-status-docker.png)

- used **ctrl+c** to exit the running docker

- I cloned the docker project first installing git with
```
sudo apt install git -y
```
![gitinstall](/Project9/img/5-ctrl+c-and-install-git.png)

- Cloned the project repository with 
```
git clone https://github.com/TobiOlajumoke/docker-flask
```

- then cd into the **docker-flask** directory

![cd](/Project9/img/6-git-clone-and-cd-into-docker-flask.png)

- viewed the docker file details with
```
cat docker-file
```
![docker](/Project9/img/7-in-docker-folder-cat-docker-file.png)

- built the docker image with
```
docker build -t flask-application:1.0.0
```
![build](/Project9/img/8-docker-build-flask.png)

- Checked the image built with 
```
sudo docker images
```
![images](/Project9/img/9-sudo-docker-images.png)

- Ran the docker container with
```
sudo docker run -d -p 8000:8000 flask-application:1.0.0
```
![dockercont](/Project9/img/10-docker-run-flask-application.png)

- Checked if the container is running with and it was running okay
```
sudo docker ps
```
![docker](/Project9/img/11-sudo-docker-ps.png)

- Tested in the browser and webpage from my Ec2 instance could not be accessed via the public ip

![testfail](/Project9/img/12-unreachable.png)

- went to my security and opened port 8000

![openport](/Project9/img/13-.png)

- Went back to the webpage and I had successfully deployed the dockerized flask app on my ec2 instance

![successpagelive](/Project9/img/14-image-live.png)

- To push the image I created a docker Hub and a repository

![docker](/Project9/img/15-creation-of-docker-and-repository.png)

- using my docker command line I logged in with
```
sudo docker login
```

- Logged in my username and password successfully.

![login](/Project9/img/16-sudo-docker-login-and-password-sucess.png)

- Tagged my docker image with my user and  repository name with.

![tag](/Project9/img/17-sudo-docker-TaG-FLASK.png)

- Next I went on to push the image to my repo with 
```
sudo docker push kennykgr/flask-application:1.0.0
```
![push](/Project9/img/18-sudo-docker-push.png)

- When my push was complete I checked my repository and it was okay

![repo](/Project9/img/19_success.png)

![okay](/Project9/img/20_success.png)

## End of Project