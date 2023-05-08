# YOLO Application Containerization
This document will take you through the steps I followed to containerize yolo application.
Yolo is divided into three parts: [client](./client/){:target="_blank"} , [backend](./backend/){:target="_blank"} and a mongodb database.

## 1. Docker file for client microservice

Here's a link to the [Dockerfile](./client/Dockerfile){:target="_blank"}.
Here are some key steps I  followed to create the dockerfile:

 1. Used node:16-alpine3.17 base image
 2. Created a working directory and copied package.json file
 3. Run npm install and copied rest of the files to the working directory to set up project environment
 4. Exposed port 3000 and then run npm start

I also used .dockerignore to ignore some files and directories when building image

## 2. Docker file for backend microservice

Here's a link to the [Dockerfile](./backend/Dockerfile){:target="_blank"}.
Here are some key steps I  followed to create the dockerfile:

 1. Used node:16-alpine3.17 base image
 2. Created a working directory and copied package.json file
 3. Run npm install and copied rest of the files to the working directory to set up project environment
 4. Defined an environment for mongodb database
 5. Exposed port 5000 and then run npm start

 I also used .dockerignore to ignore some files and directories when building image

## 3. Creating the docker compose file

 Here's a [link](./docker-compose.yml) to the file.

 Here are the steps I followed:

 1. Defined three services (database, backend, client), a network and a volume.

 ### Services

 #### 1. Database service
  1. Used mongo:4.4 base image.
  2. Attached a volume (yolo-volume) to it to persist data.
  3. Specified ports correctly.
  4. Connected it to the network (yolo-network) that I defined.

 #### 2. Backend service
  1. Used dedanwamalwa/yolo-backend:v1.0.0 image I built and pushed to dockerhub. Here's a [link](https://hub.docker.com/repository/docker/dedanwamalwa/yolo-backend/general){:target="_blank"} to the image.
  2. Specified mongodb environment as specified in the backend dockerfile.
  3. Published correct ports (5000:5000).
  4. Specified that this service depends on the database service.
  5. Connected it to the user-defined network (yolo-network).

 #### 3. Client service
  1. Used dedanwamalwa/yolo-client:v1.0.0 image I built and pushed to dockerhub. Here's a [link](https://hub.docker.com/repository/docker/dedanwamalwa/yolo-client/general){:target="_blank"} to the image.
  2. Published correct ports (3000:3000).
  3. Specified that this service depends on the backend service.
  4. Connected it to the user-defined network (yolo-network).

  NB: I made a change to package.json file to correct an error that prevented this image from running. I downgraded react-scripts dependancy from v3.4.1 to v3.4.0. Here's a [link](https://stackoverflow.com/questions/60790440/docker-container-exiting-immediately-after-starting-when-using-npm-init-react-ap){:target="_blank"} to the issue on stack overflow.

 ### Network

  1. Defined a network called yolo-network using bridge driver.

 ### Volume

  1. Defined a volume called yolo-volume to persist our data.




