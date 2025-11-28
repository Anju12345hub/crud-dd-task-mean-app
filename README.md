#crud-dd-task-mean-app

## My explanation

After getting the source code from the zip file, I created Dockerfile for Frontend, beckend application ,and docker-compose.yml ,which is available in this repository.


Created an ubuntu ec2 instance on my AWS account.
Go to that ec2 -->connect to the instance and install docker using following commands
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

Now, We can access our application uisng <ec2-ip>/tutorals, <ec2-ip/add>  

But, Due to some error my backend app refused to connect to the mongodb.  
I will try to solve the error immediately.hence my result is incomplete.[application]<img width="1536" height="864" alt="resultimg" src="https://github.com/user-attachments/assets/4be2c3c4-a128-4be6-ae20-8371f2b7490f" />


For setting CI/CD pipeline for this MEAN-APP ,Here we are using Github Ations.  

For that I creted CI/CD.yml inside .github/worflows folder.Its availble inthis repo.  

So, when a new commit generated, it trigger the pipeline and new version of image will create and new container is created.



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

Navigate to `http://localhost:8081/`
