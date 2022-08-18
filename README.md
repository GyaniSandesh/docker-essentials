 ## Hello everybody, it is me Sandesh Regmi and today I am so happy that I am able to complete and publish this quick docker essentials. 
 #### Make sure to go through all of these and I will upload this file in my github repository and make it public.

So, the question arises what the hell is docker?
Well, docker is a platform that use your os-virtualization and serve you the packages in the form of container. Well, it is completely different from using virtualmachine in Vmware, virtualbox, KVM or other virtualization platforms. In the case of virtualmachine, the fixed part of memory and storage is allocated to your guest operating system whereas in the case of docker, the docker container is going to use all of the memory and storage in case of necessity and in the case of lack memory in your host operating system, it is going to use very less amount of memory.

Well, I hope you guys are clear with the defination of docker and it's difference from virtualmachine. For gathering more information about the topic, you can go the internet and gain more information if you wish but I hope have this base knowledge is enough and as you go through the course, you will be able to gather more information and understand it by yourself about the topic.

Actually I have seen many people are much confused about the difference between docker image and docker container. So let me make you clear before initiating, with their difference
Docker image is the set of read only files which means you can't modify it but you can create a new docker image with the help of existing docker image or base image. They are used to build the container after using docker run command and it produces the output in the form of docker container. So, you can make a conclusion that the docker container is an instance of the docker image while docker image is the blueprint of the docker container. You can make any number of docker container from the same image. Docker container is the actual place where the live application where the database or any application runs and it can contain any software which can be installed in any regular machine. Every docker image at minimum contains the necessary set of files which are nothing than the small and minimal part of an operating system required to run container as an isolated unit.

Now, the interesting part comes into play, which is the installation part of docker depending upon the platform you are using.

Windows Installation:
In case of windows, if you have its professional version, you are not going to face much trouble while installing. However, you need to have at least windows 10 installed in your system. Just go through this guidelines to install docker in your windows operating system.
https://runnable.com/docker/install-docker-on-windows-10

Mac Installation:
In case of mac, go through this guidelines instead in order to install docker.
https://runnable.com/docker/install-docker-on-macos

Linux Installation:
Depending upon the linux distrubution you are using, you have the parallel installation process. However, you are going to take the help of package manager available in your linux distrubution.
In case of Ubuntu and other debian based distros: 'sudo apt full-upgrade && sudo apt install docker.io'
In case of arch based distrubution: 'sudo pacman -Sy docker'[However, in case of arch, you can even take the help of aur helpers just like yay and paru]
In case of fedora: 'sudo dnf install docker-ce docker-ce-cli containerd.io docker-compose-plugin'[This will install the latest version of docker engine, containerd, and docker compose and in ]
After installing, if you are about to start docker service in your systemd based operating system, use the command 'sudo systemctl start docker' or if you want it to get started once the operating system is booted up, then you can use 'sudo systemctl enable docker' command instead.

Basics commands with docker:
docker help or docker --help :to get the quick overview of docker commands.
docker -v :to see the current version of docker you are currently using.
docker info :to view the information regarding docker
docker network ls :To view the networks available with docker
docker image ls :To view the available images
docker ps -a :Prints all the running and stopped docker containers
docker stop [id] :Stops the running container associated with the particular container id
docker start [id] :Starts the container on the basic of id provided
docker rm [id] :Remove the container id 
docker rmi [IMAGE_ID] : Remove particular image id and image too.
docker export -o archlinux.tar [container id]: Exports docker container as a tar file.
docker save -o archlinux.tar [image id] : Exports docker image to the local computer as saves it as tar file.
docker restart [container name] :Restarts docker container
Well, you might be actually confused by seeing some of these above commands. Hence, to keep this beginner friendly, I had implemented it's use in an order so you will be familier with all of these as you go through this course.

Pullling an image in your local repository using docker:
In order to pull the docker image in your local computer, you can use this command.
'docker pull [container name]'
However, you might not be much familier with the name of the container available with docker. So, head over to the website 
https://hub.docker.com
And there in a search tab, you can search and seek out your favourite image and pull into your local computer.
Initially, the docker hub is going to download the image from it's remove server, due to the reason initially it is going to take a bit time too depending upon the speed of your internet connection and size of your image and then, it is going to pull your request. Docker can give the minimal installation of your iso-images[If you are trying to pull the operating system] and even different application as well.
This is how I had installed archlinux in my docker container:
'docker pull archlinux' [This time docker is pulling the latest image of archlinux and if you want to use another image version, then you can specify the tag as well.]
Then, it will download the image and make your container ready to use.

Docker runs on 2373 port by default when it is not getting encrypted whereas it even runs on 2376 in unencrypted communication over tcp.

Running docker image as a container:
The basic command of running docker container is:
'docker run archlinux'
To publish it in specific port, use the help of '--publish' or '-p' flag just like
'docker run --publish 8080:8080 archlinux'
'docker run -d -p 8080:8080 archlinux' : Runs docker in detached mode with the specification of the port number where first specified port is the port used for host operating system and second one is for the container and for ease, we use same port number.
Well, after running 'docker run [container name or id]' command, it gets activated and you can can boot into it using
'docker container start [container id]'
docker ps -a :Now, you will see the container id, image, command, time of last use, start, used port and name of the container.
In order to stop the running container, firstly you remove it and then finally stop. So, this is how you implement that step:
docker stop [container id or actual name] :Initially stopping the running container and if you wanna again start it then use 'docker start [id]'.
docker rm [id] :Remove the container.
[More about running the container]
'docker run --rm --name archbox -it archlinux /bin/bash' : '--rm' command is used to clean up container and start new session after exiting the container. Let me make you clear what I have done after --name command and before that I hope you are clear with that run command. If not, go above and see what I had written. So, here '--name' flag is used to specify the name of the container for our reference which is archbox and '-it' is written to use the interactive terminal which is bash in our case[Coz I had written /bin/bash]. And after '-it' command, I used 'archlinux' which means I am specifying the name of the image. One question might be ranging in your head regarding the use of bash shell in the above line rather than using zsh or other shell. It is because, I am trying to run a linux operating system using docker and for most of the linux operating system, zsh or other shell don't come installed by default but bash shell comes installed by default due to which we might be thrown an error while running other shell but so won't happen if you are trying to do with bash shell. On the other hand, bash shell is more advanced and have lots of features than other shells.
After running above command, you will have a new shell opened which is of archlinux[in my case but might be different in your case]and you can exit it using 'exit' command.

I hope you got the basics of docker and it's usuage. I you are a software developer, having this base knowledge fine but you need to dive in more so that you can utilize the docker in more efficient way but if you are 

Here is a little tip for you:
You can pull the image of vulnerable web application such as juiceshop, dvwa into docker and run it in specific port and this will not harm your computer. On the other hand, while using such web application[not in docker] you will need to start apache, mysql and other service manually and sometimes you might forget to stop the running service due to which your computer might be harmed. But, there is an alternative for this where you can run such application in your docker and whenever you even directly shut down your computer, your service will be also automatically stopped but you need to make sure that you are not running it over deattach.

I hope after coming to this point, you will familier with the command that I listed above.

Thank you for reading this till the end. I hope you love this and got a chance to learn something new. You can provide me respective feedbacks as well.
