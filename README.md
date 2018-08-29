Test answer updated

How to use:
specify AWS details in **roles/ec2_instance/defaults/main.yml**

run playbok as
    ansible-playbook aws.yml

Notes:
It was required to use lightweight image and Alpine was used
https://hub.docker.com/_/alpine/

Using local key ~/.ssh/id_rsa.pub it should be changed if you have other one

The ansible script consists of 3 roles:

**ec2-instance** - created EC2 instance

AWS connection and key details in roles/ec2_instance/defaults/main.yml

**docker** - installing docker on EC2 created instance

**nginx** - building image with nginx and started container

**site** folder contains:
* Dockerfile - for image/container
* index.html - "Hello world" page
* nginx.conf - nginx configuration
* htpasswd - basic nginx authentication ( user / haufe)


My example:

    [root@ip-172-31-38-170 nginx]# docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
    aad0770785df        nginx-test          "nginx -g 'daemon of…"   24 minutes ago      Up 24 minutes       0.0.0.0:80->80/tcp   nginx-test
    [root@ip-172-31-38-170 nginx]# curl -u user:haufe http://127.0.0.1/
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="utf-8">
        <title>test review</title>
      </head>
      <body>
        <h1>Hello World</h1>
      </body>
    </html>

