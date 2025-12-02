# crud-dd-task-mean-app

## My explanation

After extracting the source code from the ZIP file, I created Dockerfiles for the frontend and backend applications, along with a docker-compose.yml file, all of which are available in this repository.

I then created an Ubuntu EC2 instance in my AWS account. After launching the instance, I connected to it and installed Docker using the following commands:
```shell
sudo apt update
sudo apt install docker.io -y
sudo usermod -aG docker $USER
sudo chown $USER /var/run/docker.sock
```


install docker-compose
```shell
sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.0/docker-compose-linux-x86_64" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```


Then I cloned my repository using the command
```shell
git clone https://github.com/Anju12345hub/crud-dd-task-mean-app.git
```


Created nginx/reverse-proxy.conf file 
Then I run the container using the command 
```shell
docker-compose up -d
```


[Result is shown here]
<img width="1748" height="483" alt="last1" src="https://github.com/user-attachments/assets/d9bb1d7a-2b8d-4f30-bc78-3e229762e73b" />

Now, we can access our application using: EC2-IP/tutorials and EC2-IP/add.

Initially, due to an error, my backend application was unable to connect to MongoDB. 

I will resolve this issue as soon as possible, and therefore my result was incomplete. 

This problem is now fixed by updating the db.config.js file located in app/config/. 

After making the required changes, the backend application successfully connects to the MongoDB database..[application]<img width="1536" height="864" alt="resultimg" src="https://github.com/user-attachments/assets/4be2c3c4-a128-4be6-ae20-8371f2b7490f" />
Now, the current issue is related to the Nginx reverse proxy.
<img width="1145" height="449" alt="nginx-reverseproxy" src="https://github.com/user-attachments/assets/556428f5-12e0-44fe-ab10-3bac5816d592" />
Finally, I identified the issue in my docker-compose.yml.
The reason was that I had created four containers—MongoDB, Backend, Frontend, and Nginx Reverse Proxy—but the Nginx container did not include my frontend build.

This meant that my Angular build (dist/...) was never copied into the Nginx container.
As a result, Nginx displayed the default “Welcome to nginx!” page.

I have now updated the docker-compose.yml file in my repository, and the issue is resolved.

The final output screenshots are attached here:
<img width="1169" height="467" alt="output1" src="https://github.com/user-attachments/assets/f3744992-ae18-45f5-952f-5d67d9826e6e" />

<img width="1145" height="410" alt="output2" src="https://github.com/user-attachments/assets/232b2546-60f8-436d-8823-4c8e486dd871" />

docker containers : 

<img width="1814" height="350" alt="final result" src="https://github.com/user-attachments/assets/63058b03-1b1a-41aa-a0b5-49b3ed954d1b" />

## For setting up the CI/CD pipeline for this MEAN application, we are using GitHub Actions.

I created a cicd.yml file inside the .github/workflows folder, and it is available in this repository.

With this setup, whenever a new commit is pushed, it automatically triggers the pipeline. A new version of the Docker image is built, and the container is restarted with the updated image.
[pipeline]<img width="1225" height="753" alt="ci" src="https://github.com/user-attachments/assets/b0ea26f1-36ae-44df-8c56-655e2d8ad18d" />


This image is the 1st attempt of my CI/CD pipeline.
## stages of pipeline:


build_and_psuh stage: It includes,  

✅Login to My Dockerhub account  

✅ Build Docker images  

✅ Push images to Docker Hub  


deploy stage:  

✅ SSH into your aws ec2 instance  

✅ Pull latest images  

✅ Restart your containers (Docker Compose)


For running this pipeline, we have to create ### GitHub secrets:  

Go to:
GitHub → Repo → Settings → Secrets → Actions  


I have created :  

✅DOCKERHUB_USERNAME -your Docker Hub username  

✅DOCKERHUB_TOKEN	 - Docker Hub Access Token (Go to your DockerHub account -> Account Setttings -> personal access tokens -> generate new token)  

✅EC2_HOST - Public ip of your ec2  

✅EC2_USER - (root or ubuntu)  

✅EC2_SSH_KEY -	 Your private SSH key content 

### Generating SSH Keys

Run the following command on your local machine:
```shell
ssh-keygen -t rsa -b 4096 -C "github-actions"
```
Copy the public key to your ec2 using 
```shell
vim ~/.ssh/authorized_keys
```

### Docker Compose for CI/CD

For running this GitHub Actions CI/CD workflow, I used the docker-compose.cicd.yml file.

Once a new commit is pushed:

A new image is built

A new container is created

When another commit is pushed, the container restarts automatically with the new updated image

You can see this behavior in the image below. <img width="1800" height="594" alt="restart-container" src="https://github.com/user-attachments/assets/e54c2714-024b-4c53-b3a2-ef365704cb0e" />



<img width="1264" height="612" alt="pipeline1" src="https://github.com/user-attachments/assets/e9581683-0c57-4526-b06d-9482c7747361" />






## Company provided details


In this DevOps task, you need to build and deploy a full-stack CRUD application using the MEAN stack (MongoDB, Express, Angular 15, and Node.js). The backend will be developed with Node.js and Express to provide REST APIs, connecting to a MongoDB database. The frontend will be an Angular application utilizing HTTPClient for communication.  

The application will manage a collection of tutorials, where each tutorial includes an ID, title, description, and published status. Users will be able to create, retrieve, update, and delete tutorials. Additionally, a search box will allow users to find tutorials by title.

## Project setup

### Node.js Server

cd backend

npm install

You can update the MongoDB credentials by modifying the `db.config.js` file located in `app/config/`.

Run `node server.js`

### Angular Client

cd frontend

npm install

Run `ng serve --port 8081`

You can modify the `src/app/services/tutorial.service.ts` file to adjust how the frontend interacts with the backend.

Navigate to `http://localhost:8081/`..
