# HTX_Assignment
In this assignment, we will be building a docker image using the ***interactive method***

We will build an Ubundu docker container image using an ubuntu base image from the dockerhub public repository, embed a message inside the container and save this as a new image. 

## Building the Container
**Image base: ubuntu:22.04**
This is the latest image released on 5 November 2021. We will use the 22.04 tag instead of latest because new tags might be released later. By tagging to a specific version, we will ensure that the exact same container is built every time the code is run.

`docker run --name my_ubuntu -it ubuntu:22.04 /bin/bash`

The following flags are included:
1. `--name my_ubuntu` to give the container a name, else a random string is generated
2. `-it` to open the container's STDIN (command's inpput stream) and allocate a pseudo -TTY to run the interactive commands
3. `/bin/bash` is used to open a shell interface with the container

![Picture 1](https://user-images.githubusercontent.com/77711274/141234915-53d0534c-6487-456c-b4ab-f6437169a684.jpg)

![Picture 2](https://user-images.githubusercontent.com/77711274/141234919-22edd0b5-373a-4375-a2fe-70e95044ade8.jpg)

Now we have built a container named my_ubuntu by using ubuntu v22.04 as the base image. 

## Adding a message to the Container
We can now make changes to the container we have created. Here, we will add the message "hello world" and then exit the container. Following that, we will urn a check to verify that the container my_ubuntu still exists

`echo 'hello world' > /message`

`exit`

`docker ps -all`

![Picture 3](https://user-images.githubusercontent.com/77711274/141234920-0c292b86-4b4a-4ccc-8383-c1a7b238e260.jpg)

## Saving the Container as a New Image

We will now save the container as a new image called hello_world

`docker commit my_ubuntu hello_world`

`docker image ls`

![Picture 4](https://user-images.githubusercontent.com/77711274/141234922-cc052ec4-39ea-4a56-9bce-48a5a54026f4.jpg)

Now, we can see that there are two images, ubuntu (tag 22.04) which is the base image that we have used and hello_world, which is the new image we have created containing the message “hello world”. 

To verify that our new image hello_world has the message inside, we will run a container based on this image to display the message.

`docker run hello_world cat /message`

![Picture 5](https://user-images.githubusercontent.com/77711274/141234924-f5531df9-c1ef-4d0f-8458-9437894d72b8.jpg)

We can see above that the correct message "hello world" is printed.

## Hosting the New Image on Docker Hub

We first log into docker.

`docker login`

![Picture 7](https://user-images.githubusercontent.com/77711274/141234930-d65edb6c-641f-4257-91ee-7fd82d040223.jpg)

Next, we tag the image to our repository and push the image to docker hub.

`docker tag hello_world:latest suniljit1991/hello_world`

`docker images`

`docker push suniljit1991/hello_world`

![Picture 8](https://user-images.githubusercontent.com/77711274/141234933-9cd727d5-5d96-411d-b959-c5d238def9d1.jpg)

We can now see that the hello_world image has been pushed to the suniljit1991 repository. We can also verify this by checking docker hub. 

![Picture 9](https://user-images.githubusercontent.com/77711274/141234936-112873fa-734d-43e0-b5a4-38ae0e916ca6.jpg)

Public view below with the docker pull command. 

![Picture 10](https://user-images.githubusercontent.com/77711274/141234938-27c48624-6620-4ea6-8ea7-2fac50aecf44.jpg)

Link to dockerhub repository: https://hub.docker.com/repository/docker/suniljit1991/hello_world

We can also test that the hosted image on docker hub can be downloaded. 

`docker pull suniljit1991/hello_world`

![Picture 11](https://user-images.githubusercontent.com/77711274/141234942-e67ad459-4e41-4d9e-a055-8bfa8375f10c.jpg)

As we already have the latest image in our harddisk, terminal shows that the image is up to date instead of downloading. However, this verifies that the correct image has been successfully hosted in dockerhub. 








