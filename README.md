Test answer updated

How to use:
specify AWS details in **roles/ec2_instance/defaults/main.yml**

run playbok as
    ansible-playbook aws.yml

Notes:
It was required to use lightweight image and Alpine was used
https://hub.docker.com/_/alpine/

Using local key ~/.ssh/id_rsa.pub it should be changed if you have other one

The ansible script consists of 4 roles:

**ec2-instance** - created EC2 instance

AWS connection and key details in roles/ec2_instance/defaults/main.yml

**docker** - installing docker on EC2 created instance

**ssl** - generate self signed cert for haufe.test domain name

**nginx** - building image with nginx and started container

**site** folder contains:
* Dockerfile - for image/container
* index.html - "Hello world" page
* nginx.conf - nginx configuration
* htpasswd - basic nginx authentication ( user / haufe)


My example:

[root@ip-172-31-32-121 ec2-user]# docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
    84be0be5eac4        nginx-test          "nginx -g 'daemon of…"   2 minutes ago       Up 2 minutes        0.0.0.0:443->443/tcp   nginx-test

    ansible-playbook aws.yml
    PLAY RECAP ************************************************************************************************
    XX.197.46.164              : ok=14   changed=13   unreachable=0    failed=0   
    localhost                  : ok=7    changed=4    unreachable=0    failed=0   

    curl -u user:haufe -k https://18.197.46.164
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
