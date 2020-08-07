# Docker

Docker is not virtual machines. There's only a single operating system running. That operating system is just carved up into isolated little spaces. A container is a self contained sealed unit of software. It has everything in it that is needed to run your code. Operating system included, it has all of the code, all of the configs, contains all the processes within that container, it has all of the networking to allow these containers to talk to the other containers they're supposed to be able to talk to, and nothing else. It has all the dependencies that your system needs, bundled up in that container. And it even includes just enough of the operating system to run your code. It takes all the services that make up a Linux server. Networking, storage, code, interprocess communication, the whole works, and it makes a copy of that in the Linux Kernel for each container.

You might have one container on a system running Red Hat Linux, serving a database, through a virtual network to another container running Ubuntu Linux, running a web server that talks to that database, and that web server might also be talking to a caching server that runs in a SUSE Linux based container. The important part to understand is it doesn't matter which Linux each container is running on, it just has to be a Linux. And Docker is the program which manages all of this. Sets it up, monitors

Images to Containers
- An image is every file that makes up just enough of the operating system to do what you need to do.
- Traditionally you'd install a whole operating system with everything for each application you do. With Docker you pair it way down so that you have a little container with just enough of the operating system to do what you need to do, and you can have lots and lots of these efficiently on a computer.

- The Docker run command takes an image and turns it into a living running container with a process in it that's doing something, hopefully something useful, but at least something. So let's take a look at

-TI stands for terminal interactive. It just causes it to have a full terminal within the image so that you can run the shell and get things like tab completion and formatting to work correctly. When you're running commands by typing on

Containers Management
- Can limit memory (docker run --memory maximum-allowed-memory image-name commmand
- can limit CPU (docker run --cpu-shares) relative to other containers
- Dont let containers fetch dependencies when they start. (e.g. If you're using things like Node.js some day, somebody's gonna remove some library out from the node repos, and all of a sudden, all your containers just stop throughout your whole system. Fetch make your containers include their dependencies inside the container)
- Fetch make your containers include their dependencies inside the container themselves.
- Don't leave important things in unnamed stopped containers. 

Container Networking
- Docker is almost universally used to run network services such as web and database servers. Programs in containers are isolated from the internet by default.
- docker run --rm -ti(terminal interactive) -p(publish) 45678:45678(publish port 45678 and connect it to port 45678) -p 45679:45679 --name echo-server(explicit name) ubuntu: 14.04 bash
- docker desktop for windows nc (use IP address) port number 
- Exposing ports dynamially. Ports inside a container are fixed. Using multiple ports (12) Docker has that solved. You can leave off the host side of the port definition and Docker will fill it in from one of the available ports. This allows many containers running the same programs to share the same host. This is often used with some sort of an orchestration or discovery service like Kubernetes or something like that. 

Docker Commands
- docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
- --publish asks Docker to forward traffic incoming on the host’s port 8000 to the container’s port 8080. Containers have their own private set of ports, so if you want to reach one from the network, you have to forward traffic to it in this way. Otherwise, firewall rules will prevent all network traffic from reaching your container, as a default security posture.
- --detach(asks Docker to run this container in the background.)
- name specifies a name with which you can refer to your container in subsequent commands, in this case bb
docker rm --force bb
- force option stops a running container, so it can be removed. If you stop the container running with docker stop bb first, then you do not need to use --force to remove it.
- docker run [OPTIONS] IMAGE(The conatainer image to run. By default, these are pulled from DockerHub)[:TAG](A specific image tag. Usually used to pull a specific version ) [COMMAND](command to run im the container) [ARGS...](Arguments to pass when running the command)
(e.g. docker run busybox-IMAGE[TAG] echo[COMMAND] hello world![ARGUMENT])
- -d :Run a container in detached mode. The docker run command will exit immediately and the container will run in the background.
- --name ngnix:A container is assigned a random name by default, but you can give it a more descriptive name with this flag.


Storage Driver
Provides a pluggable framework for managing the temporary,internal storage of a container's writable layer.If you have software inside container thats writing files to the disk and not using mounted volume or external storage. It will write to the containers internal storage. The way it gets managed depends on the storage driver 
Docker offer storage driver framework. supports a variety of storage drivers. The best storage driver to use depends on the enviroment and storage needs.

overlay2 file-based storage. Default for Ubuntu and CentOS 8.
devicemapper: Block storage, more efficent for doing lots of writes. Default for Centos 7 and earlier

https://docs.docker.com/storage/storagedriver/select-storage-driver/

in storage drivers how do we save and quit when in changes mode

Logging Drivers
-- pluggable framework for accessing log data from servies and containers in Docker. DOcker supports a variety of logging drivers.
--Configuring logging drivers isnt neccessary they already come configured

Namespaces: they are a aLinux technology that allows processes to be isolated in terms of the resources that they see. They can be used to prevent different processes from interfereing or interacting with one another. Docker user namespaces to isolate containers. THis technology allows containers to operate independently and securely.
-pid(process isolation): DOcker is only able to see the process inside the container only
-net(network intefaces): manages network resources within the container(e.g. if theres net in different containers it wont see them)
-ipc(inter-process communication):
-mnt(Filesystem mounts):
-uts(Kernel and version identifiers):
-user namespaces: Require special configuration. REquires you to coordinate your enviromet. Allows container processes to run as root inside the container while mapping that user to an unprivileged user on host.
Allows you to run as root in the container while running as an unprivilged user outside the container.

cgroups-limit resource uses. Used by docker to enforce rules on resources 

