# Docker

Docker is not virtual machines. There's only a single operating system running. That operating system is just carved up into isolated little spaces. A container is a self contained sealed unit of software. It has everything in it that is needed to run your code. Operating system included, it has all of the code, all of the configs, contains all the processes within that container, it has all of the networking to allow these containers to talk to the other containers they're supposed to be able to talk to, and nothing else. It has all the dependencies that your system needs, bundled up in that container. And it even includes just enough of the operating system to run your code. It takes all the services that make up a Linux server. Networking, storage, code, interprocess communication, the whole works, and it makes a copy of that in the Linux Kernel for each container.

You might have one container on a system running Red Hat Linux, serving a database, through a virtual network to another container running Ubuntu Linux, running a web server that talks to that database, and that web server might also be talking to a caching server that runs in a SUSE Linux based container. The important part to understand is it doesn't matter which Linux each container is running on, it just has to be a Linux. And Docker is the program which manages all of this. Sets it up, monitors

Images to Containers
- An image is every file that makes up just enough of the operating system to do what you need to do.
- Traditionally you'd install a whole operating system with everything for each application you do. With Docker you pair it way down so that you have a little container with just enough of the operating system to do what you need to do, and you can have lots and lots of these efficiently on a computer.

- The Docker run command takes an image and turns it into a living running container with a process in it that's doing something, hopefully something useful, but at least something. So let's take a look at

-TI stands for terminal interactive. It just causes it to have a full terminal within the image so that you can run the shell and get things like tab completion and formatting to work correctly. When you're running commands by typing on

Managing Containers
- Can limit memory (docker run --memory maximum-allowed-memory image-name commmand
- can limit CPU (docker run --cpu-shares) relative to other containers
-Dont let containers fetch dependencies when they start
