# boring-stuff


check out [the free online book](https://automatetheboringstuff.com)

## Setting up Docker

If you do not have Docker installed on your system, that is fine. I will provide you some links that will walk you through this. Installing docker is not difficult and should only take a few minutes to do. However, you will need adequate privileges to install it. If you already have docker installed on your system you can skip this section. Below are links to the official install instructions on Docker.com. **Docker for Desktop will require a license for use by organizations with more than 250 employees or more than $10 Million in revenue starting January 1, 2022.** You may also choose to use [Podman](https://podman.io/) as an alternative to Docker if you are using Linux.

* [Install Docker on Windows](https://docs.docker.com/desktop/windows/install/)
* [Install Docker on MacOS](https://docs.docker.com/desktop/mac/install/)
* [Install Docker on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
* [Install Docker on CentOS](https://docs.docker.com/engine/install/centos/)
* [General Docker Install Information](https://docs.docker.com/engine/install/)

## Cloning Repo and Building the Container

**NOTE:** All instruction will be given in the command line. You can use a gui for some of the things I will talk about below, but the instuction will vary from GUI application to GUI appliacation so it is easier for me to present this information in the command line format.

:warning:&nbsp; **Before you start!** It is assumed that you have ```git``` on your computer. If you are unsure if it is installed on your computer, then run the following in the command line:
```git --version```
If you you receive an error then ```git``` is probably not installed. If you need to install ```git``` then please visit this [page](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and follow the instructions there.

1. Create a directory for this repo and then clone it do that directory.

    ```bash
    mkdir boring-stuff
    git clone https://github.com/barweiss45/boring-stuff.git
    ```

2. Change the directory to to the cloned repo of boring-stuff.

    ```bash
    cd boring-stuff
    ```

3. Ensure that you have your container environment ready. If not see [Setting up Docker](#setting-up-docker). If you are using Docker you can verify this by running the following command. If you don't get the expected output when you check for the version then Docker is probably not installed.

    ```bash
    docker --version
    ```

4. As mentioned before I have created a ```Dockerfile``` so that you can run this demo out of my prebuilt and tested environment. To build the Docker container, you can run the following commands. In order for this command to work you need to be in the boring-stuff folder. See step 2 if you are unsure.

   :warning:&nbsp; Be aware that the initial build of this container may take upwards to 5 to 10 minutes depending on your internet connection and local machine.

    ```bash
    docker build -t boring-stuff:latest  .
    ```

5. After you have built the container then verify that the image is now in your local container repository.

    ```bash
    docker images
    ```

6. Your output should look something like this. Once you are at this point you are ready to start the container and begin the demo. Please move on to the next section [Accessing The Lab](#accessing-the-lab) below.

## Accessing The Lab

Access the lab once the container is very straightfoward. After the container is built you will need to first run it. The way that I demonstrate has you open a second ```bash``` session to log it. This way if you exit out of the container you don't stop the container. If you do stop the container then you just simply need to restart the contaier by running the command ```docker start ansible-demo```.

1. First you will need to run the container to get it going.

    ```bash
    docker run -dit --rm --name ansible-demo boring-stuff:latest
    ```

2. If the command is successful you will see a container ID (is a hash) returned in the next line. You can also verify with the following command.

    ```bash
    docker ps -a
    ```

3. Once you have verified that the container is running they log into it by running the following command.

    ```bash
    docker exec -it ansible-demo bash
    ```

4. When you are in the container you will see see a prompt that will look similar to this, ```root@c91ff98ffdec:~#```. The container ID will likely be different than what you see in the example. Verify the file structure, you should be in the home directory of root on the container. It should like what you see below.

    ```bash
    root@c91ff98ffdec:~# ls -al
    total 36
    drwx------ 1 root root 4096 Nov 15 21:10 .
    drwxr-xr-x 1 root root 4096 Nov 15 21:10 ..
    drwx------ 4 root root 4096 Nov 15 21:11 .ansible
    -rw-r--r-- 1 root root 3106 Dec  5  2019 .bashrc
    drwx------ 1 root root 4096 Nov 14 04:31 .cache
    -rw-r--r-- 1 root root  161 Dec  5  2019 .profile
    drwxr-xr-x 1 root root 4096 Nov 14 04:31 .pyenv
    drwxr-xr-x 1 root root 4096 Nov 14 04:32 boring-stuff
    -rw-rw-r-- 1 root root  613 Nov 11 21:58 requirements.txt
    root@c91ff98ffdec:~# 
    ```

5. Change to the ```boring-stuff``` directory in the container.

    ```bash
    cd boring-stuff
    ```

6. Once you are in the ```boring-stuff``` directory you are ready to start the lab.

    ```bash
    # To verify that you are in the right directory use the 'pwd' command 
    # and you should have the following output:
    root@c91ff98ffdec:~/boring-stuff# pwd
    /root/boring-stuff
    ```

7. When you are done with the lab you can simply type ```exit```. If you would like to stop the container then running the following command after you have exited it.

    ```bash
    docker stop ansible-demo
    ```

8. If you want to restart the container you can then run the following command.

    ```bash
    docker start ansible-demo
    ```

    Once your container is back up and running you can just start from step 3 in this section.
