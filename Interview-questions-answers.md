# Docker Interview Questions & Answers

- Difference between Virtual machine Vs Docker

  Docker and virtual machines (VMs) are both technologies used for virtualization, but they operate at different levels and serve different purposes. Here's a comparison between Docker and virtual machines:

### Docker:

1. **Containerization:**
   - Docker uses containerization technology to encapsulate applications and their dependencies into isolated containers.
   - Containers share the host OS kernel but run in isolated user spaces.

2. **Resource Efficiency:**
   - Containers are lightweight and share the host OS resources efficiently.
   - They have lower overhead compared to virtual machines.

3. **Isolation:**
   - Containers provide process-level isolation, meaning processes inside a container are isolated from the host and other containers.

4. **Speed:**
   - Containers can start and stop quickly, making them suitable for microservices architectures and dynamic scaling.

5. **Portability:**
   - Docker containers are highly portable, and the application and its dependencies are bundled together, ensuring consistent behavior across different environments.

6. **Use Case:**
   - Docker is often used for packaging and distributing applications with all their dependencies, making them easy to deploy and manage.

### Virtual Machines:

1. **Virtualization:**
   - VMs use hypervisors to create virtual instances of an entire operating system, including the kernel, on top of a physical host.

2. **Resource Overhead:**
   - VMs have more overhead compared to containers because each VM requires a full operating system.

3. **Isolation:**
   - VMs provide stronger isolation since each VM has its own full OS, which reduces the risk of security vulnerabilities.

4. **Speed:**
   - VMs typically have a longer start-up time compared to containers.

5. **Portability:**
   - VMs are less portable than containers because they encapsulate an entire operating system, making them larger and potentially more complex to manage.

6. **Use Case:**
   - VMs are often used for running multiple applications with different operating systems on a single physical host, consolidating resources and providing strong isolation.

### Choosing Between Docker and Virtual Machines:

- **Resource Efficiency vs. Isolation:**
  - Choose Docker if you prioritize resource efficiency and want lightweight, easily scalable containers.
  - Choose VMs if you need strong isolation with full OS virtualization.

- **Application Packaging and Deployment:**
  - Docker is excellent for packaging applications and their dependencies, ensuring consistency across different environments.
  - VMs are more suitable when you need to run multiple applications with different operating systems on the same host.

- **Speed and Agility:**
  - Docker is generally faster to start and stop, making it suitable for dynamic environments.
  - VMs may be preferable for more static environments with less frequent changes.

In practice, both Docker and VMs are often used together in a complementary way. Docker containers can run within VMs, providing an additional layer of abstraction and flexibility. The choice between Docker and VMs depends on the specific requirements and characteristics of the applications and infrastructure you are working with.

- **What is Docker engine?**

  Docker engine is a application to build, package and run containarized application with having all the code and dependencies and libraries needed to run the application in a isolated environment.

  Components of Docker engine.

    * **Docker d (docker daemon)** : It is a background process which manages the containers on high level and it manages the docker objects like images, volumes, container, network using container d on low level(code level: like executing the code in reference to manging the containers)
    
    * **Docker CLI** : It is a command line interface which allow user to interact with docker daemon and issue commands to manage image, container etc.
    
    * **Container d** : It manages the execution of container on low level, It handles the comlete lifecycle of creation, execution and destruction of containers. It manages the distribution of container images. This involves pulling container images from container registries (such as Docker Hub) and storing them locally.  

- **How to install docker in Ubuntu?

      sudo apt install docker.io

<img width="596" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/424ae731-f868-4b19-9526-e577253a378d">

- **How to make & run mysql container in docker?**

      docker pull mysql:latest

  <img width="579" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/dc1effee-ed8d-4b1e-842e-07b66b0434f6">

This will pull the mysql:latest image from dockerhub.

  * Run the image to make container and set environment variable for mysql

        docker run -d -e MYSQL_ROOT_PASSWORD=test@123 mysql:latest

<img width="778" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/bc4567aa-fd35-48d4-9663-18a2ba63d66c">

  -e refers to environment variable

  <img width="849" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/81b60593-993d-4f0d-ae4c-078c6bad4304">

  * Go inside the container

        docker exec -it 0b9127049bcf sh

 <img width="531" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/200d217e-66e8-414a-89c7-e0fd472ed280">

   -it refers to interactive terminal

- **Basics of Dockerfile by building a image and container of java app**

      vim Hello.java

  <img width="450" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/2da73fb0-7230-47c5-a79c-f36705361eb6">

    Code of application inside the Hello.java file

    - Creating Dockerfile for builing image of java-app

             # Getting base image
              FROM openjdk:11
          
              # Creating Working directory where all the code will be kept
              WORKDIR /app
              
              # Copying the code to the current directory of the container
              COPY Hello.java .
              
              # Compiling the code
              RUN javac Hello.java
              
              #Run the compiled code
              CMD ["java","Hello"]

   <img width="467" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/3204d5c7-7358-4d9b-b613-9b5b53a383d4">

   - Building image from Dockerfile
 
         docker build . -t java-app

     <img width="602" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/c33178e9-26b8-4d44-bd5d-685309cc208d">

      -t refers to tag

     Image has been made from Dockerfile

     <img width="510" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/ec102b66-ea6c-4c53-bdd5-31ff05644b15">

    - Run the image to make container
 
          docker run -d java-app
 
      <img width="470" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/0c00caa0-00d5-459a-b8ba-16ed8708a105">

      -d refers to detach mode/background

- **RUN VS CMD in Dockerfile**

     In a Dockerfile, both `RUN` and `CMD` are instructions, but they serve different purposes:

1. **`RUN` Instruction:**
   - Used to execute commands during the build process.
   - Any command that needs to be executed during the creation of the image should be specified with `RUN`.
   - Examples include installing dependencies, setting up the environment, and other commands that contribute to building the image.

   ```Dockerfile
   FROM ubuntu:latest

   RUN apt-get update \
       && apt-get install -y python3 \
       && apt-get clean \
       && rm -rf /var/lib/apt/lists/*
   ```

   In this example, the `RUN` instruction is used to update the package list, install Python 3, clean up, and remove unnecessary files.

2. **`CMD` Instruction:**
   - Used to provide a default command for an executing container.
   - It specifies the command and its parameters to run when the container starts.
   - There can only be one `CMD` instruction in a Dockerfile.
   - If the Dockerfile has multiple `CMD` instructions, only the last one is effective.

   ```Dockerfile
   FROM python:3.9

   WORKDIR /app

   COPY . .

   CMD ["python", "app.py"]
   ```

   In this example, the `CMD` instruction specifies that when a container is started from the image, it should run the Python script `app.py`.

In summary, `RUN` is used for executing commands during the build phase to set up the environment, while `CMD` is used to specify the default command to run when a container is started from the image. It's common to use `RUN` for setting up the environment, installing dependencies, etc., and `CMD` for specifying the default command that starts your application.

- **What is the use of publish?**

  - Dockerfile for flaskapp

        # Getting base image
        FROM python:3.9
        
        # Creating a working directory
        WORKDIR /app
        
        # copying the code to working directory
        COPY app.py .
        
        # installing the required libraries
        RUN pip install flask
        
        # run the application
        CMD ["python","app.py"]

    - Running the image with publishing the host port with container port

          docker run -d -p 5000:5000 flask-app:latest

   -p refers to publish, used to bind host port to the container port.

   <img width="682" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/7a783e62-3bb3-46b4-9fec-b108d7b5cee0">

   - After binding the port don't forget to edit inbound rules in security group and add rule port number on custom tcp to allow traffic on port number specified. 

    <img width="368" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/a2d83c5b-28ff-483a-a2ee-b6d196d145c3">

  
- **What are the scenarios in which your container is accessable or not accessable?** (IMPORTANT)

   - No PORT Exposed : In this scenario. there isn't any port exposed in the Dockerfile and no port exposed in the docker run command, so no port are accessable in the container and port are attached to host.

   - EXPOSE 8000 : In this scenario, the container is exposing the port and other conatainer can connect to that port but not the host port. 

   - -p 5000:5000 : In this scenario, 5000(container port):5000 (host port), container port is exposed and mapped to host port.
 
-**Use case of publish port**

  Dockerfile of nodejs-app

              FROM node:12.2.0-alpine
              WORKDIR app
              COPY . .
              RUN npm install
              RUN npm run test
              EXPOSE 8000
              CMD ["node","app.js"]

  - Build the image from Dockerfile

        docker build . -t nodjs-app

  <img width="678" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/858c8c71-4cb0-41b4-b4f1-21ed0c64fbc8">

  - Run the image to make container and publish the container port and map to host port.

        docker run -d -p 8000:8000 nodejs-app
  
      <img width="833" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/17e6da22-48b6-4f43-8dc2-63b5bc249588">

    After that open the traffic to port 8000, by add inbound rule in security group.

    <img width="381" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/dc6dafaa-418d-4793-8d80-379dea1f3352">



- **Difference between ADD & COPY?**

    - COPY: It is used to copy local file to the container.

    - ADD: It is also use to copy file from local to the container. It can automatically extract tarballs (files with extensions like .tar, .tar.gz, .tar.bz2, etc.) during the copy 
      process. It can copy files from a URL.

    In general, if you are only copying local files and want to ensure clarity and simplicity, it's recommended to use COPY. If you need to handle more complex scenarios like extracting 
    tar  balls or copying from URLs, you might choose ADD. However, be aware that using ADD for simple copying can lead to unexpected behavior, and it's generally considered good practice 
    to use COPY for clarity and transparency in your Dockerfiles.

- ** How to create custom nginx Docker image and deploy a static web page**

    - Create custom index.html
 
                <!DOCTYPE html>
          <html>
          <head>
                  <title> Week16 LUIT Project </title>
          </head>
          <body>
                  <body style=text-align:center;background-color:red;font-weight:900;font-size:20px;font-family:Helvetica,Arial,sans-serif>
                  <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png">
                  <h1> Welcome to my custom nginx webpage hosted in a Docker container </h1>
                  <p> This container was deployed: <div id="date"></div></p>
          <script>
                  var date = new Date();
                  document.getElementById("date").innerHTML=date.toLocaleString();
          </script>
          </body>
          </html>

      - Create Dockerfile
     
            #Getting image
            FROM nginx
            
            # Copying the index.html local file to container
            COPY index.html /usr/share/nginx/html
            
            # Exposing port
            EXPOSE 8080

        - Build image and make container
       
          <img width="852" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/6b8a890a-d57f-486d-b1b5-4cc392a1bf59">

        - Add Inbound rule 8080 and Custom static web page has been deployed
       
          <img width="1094" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/e1e3a0cd-f255-458c-8a2e-f95599e7e38a">
 
- **What is Docker compose**

   DOcker compose is used to buikd and deploy the services at once.
  Docker compose file for two-tier application.

       services:
      
        backend:
          build:
            context: .
          ports:
            - "5000:5000"
          environment:
            MYSQL_HOST: mysql
            MYSQL_USER: admin
            MYSQL_PASSWORD: admin
            MYSQL_DB: myDb
          depends_on:
            - mysql
      
        mysql:
          image: mysql:5.7
          environment:
            MYSQL_ROOT_PASSWORD: root
            MYSQL_DATABASE: myDb
            MYSQL_USER: admin
            MYSQL_PASSWORD: admin
          volumes:
            - ./message.sql:/docker-entrypoint-initdb.d/message.sql   # Mount sql script into container's /docker-entrypoint-initdb.d directory to get table automatically created
            - mysql-data:/var/lib/mysql  # Mount the volume for MySQL data storage
      
      volumes:
        mysql-data:

  depemds_on refers to backend service will build after mysql

      docker-compose up -d 

 This will build and deploy the services mentioned in docker compose file.


     docker-compose down

  This will stop all the services of docker compose file.

-**How to reduce size of image?**

   - Using multi stage docker

     First make docker file of flask app

          FROM python:3.9
          WORKDIR /app
          COPY . .
          RUN pip install flask
          CMD ["python","app.py"]

     Build the image and check the size.

     <img width="539" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/52dd0402-5bd9-496c-a32d-69cb9cdfd8fb">

  - Create stages in docke file

          #Stage 1
          FROM python:3.9 AS big-stage
          WORKDIR /app
          COPY . .
          #stage 2
          FROM python:3.9-slim-bullseye
          
          #copying the data in /app in working directory to /app in current directory
          COPY --from=big-stage /app /app
          RUN pip install flask
          CMD ["python","app.py"]

    - Build and check image size
   
       <img width="613" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/71f87d94-e809-4ace-9653-b432f5c99dcf">

-** How to ppush imaages to DockerHub?**

   - First login

         docker login 

  <img width="603" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/9f3e797f-7533-4f83-8b90-ed7f97f441f8">

  - Tag the image

        docker image tag multi-stage-flask-app mnmanish/multistage-flask-app

     <img width="611" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/0191707e-7350-41d1-ac84-26d737caa711">


  - Push to DockerHub

         docker push mnmanish/multistage-flask-app

    <img width="596" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/82f0a47b-2d49-4894-926c-1d5232ae5312">

  -IMage has been pushed tp dockerHUb

  <img width="599" alt="image" src="https://github.com/ManishNegi963/Docker-Inteerview-Questions-Ansers/assets/124788172/d79cfba6-a27c-447e-baca-a4211f631f8a">
