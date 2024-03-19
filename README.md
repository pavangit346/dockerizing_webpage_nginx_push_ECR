# dockerizing_webpage_nginx_push_ECR

Graded Assignment on Dockerizing a Plain HTML Page with Nginx

The objective of this assignment is to familiarize yourself with Docker and containerization by Dockerizing a simple HTML page using Nginx as the web server.

Requirements:


1. Basic HTML Page:
   - Create a plain HTML page named `index.html` with some content (e.g., "Hello, Docker!").
2. Nginx Configuration:
   - Create an Nginx configuration file named `nginx.conf` that serves the `index.html` page.
   - Configure Nginx to listen on port 80.
3. Dockerfile:
   - Create a `Dockerfile` to define the Docker image.
   - Use an official Nginx base image.
   - Copy the `index.html` and `nginx.conf` files into the appropriate location in the container.
   - Ensure that the Nginx server is started when the container is run.
4. Building the Docker Image:
   - Build the Docker image using the `Dockerfile`.
5. Push the image on ECR
  - Make the public repository and push them on the ECR


6. Documentation:
   - Provide a brief documentation (in a README.md file) explaining the purpose of each file (index.html, nginx.conf, Dockerfile) and the steps to build and run the Docker container.


7. Submission:
   - Push all artifacts including the link of the public repository on the README.md file and docker file into the GitHub repository and submit the repository.


My Steps of Execution --

#A. Created index.html file 
"Hello, Docker!!"
Welcome to the World of Docker and Containers.

#B. Created nginx.conf file 
(my_nginx_html.conf)
created custom nginx.conf file by replacing original.
The new conf file be serve the index.html page.

server {
    listen       80;
    listen  [::]:80;
    server_name  _;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    error_page   500 502 503    /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

}

#C. Created the docker image.

At Docker image , pulled the latest NGINX server
also deleted all default conf  and html default page.
copied the index.html from local directory.
EXPOSE PORT 80 for web server
Also givn commands to start nginx


FROM nginx:latest

RUN rm -rf /usr/share/nginx/html/*

RUN rm -rf /etc/nginx/conf.d/*

COPY index.html /usr/share/nginx/html/index.html

COPY my_nginx_html.conf /etc/nginx/conf.d/my_nginx_html.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

added the tags and have run the container successfully.

#D Pushed the Image to Docker Hub.

#E Pushed the Docker image to ECR as well.

Added all pictures required to justify the above steps.




