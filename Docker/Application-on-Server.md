## Task

```
he Nautilus DevOps team is conducting application deployment tests on selected application servers.
They require a nginx container deployment on Application Server 1. Complete the task with the following instructions:


On Application Server 1 create a container named nginx_1 using the nginx image with the alpine tag. Ensure container is in a running state.

```

## Solution

```sh

ssh tony@stapp01 #password

docker --version

sudo docker run -d --name nginx_1 nginx:alpine

docker ps -a

```
