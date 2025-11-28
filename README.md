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
[Result is shown here](C:\Users\subin\Downloads\last1.png)



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
