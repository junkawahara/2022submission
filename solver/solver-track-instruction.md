## About output (solution) files




## About solver (as a docker container)

- Please submit your solver executable on Ubuntu 20.04 as a docker container archive (tar.gz archive).

### Instruction 
At first, edit Dockerfile as you like (cloning 2022solver is mandatory). 

``` bash
FROM ubuntu:20.04

#------------------------------------------------
# (1) install fundamental commands
#------------------------------------------------
RUN \
    apt update && \
    apt -y upgrade && \
    apt install -y curl git man unzip vim wget sudo

#   Hint: you may want to additionally install the followings. 
#   apt install -y build-essential
#   apt install -y software-properties-common

#------------------------------------------------
# (2) clone the 2022solver directory to /
#------------------------------------------------
RUN git clone https://github.com/core-challenge/2022solver.git
```

Then, build your docker image by the following command. Note that `mysolver` can be any "image name" and `v01` can be any "tag name". 

```bash
docker build -t mysolver:v01 .
```

- It may take minutes. 
- If the command is successfully finished, `[+] Building xxx.xs (y/y) FINISHED` is displayed. 

`$ docker image ls` shows the image you just created. 

```bash
$ docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
mysolver     v01       af8aaca552c0   3 minutes ago   277MB
```

- Next, let's launch your "container" from the image. 

```bash
$ docker run -it --name mysolver-container mysolver:v01 bash
root@13765b36541e:/# 
root@13765b36541e:/# ls 2022solver/
README.md  example  run.sh
```

- `root@13765b36541e:/# ` is the prompt in the running container. 
- Then, let's detach from your container by `ctrl-pq` (keeping `ctrl` on, and type `p` and `q`) which will keep your container alive (do not use `exit` or `ctrl-d` which will stop your container). 
- You get back to the prompt of your local machine. Then, `docker ps` will show your container running. 

```bash
$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS          PORTS     NAMES
13765b36541e   mysolver:v01   "bash"    13 minutes ago   Up 13 minutes             mysolver-container
```

- If you want to copy some file/directory on your local machine into the running container, please use `docker cp` as follows:

```bash
docker cp solver-track-instruction.md mysolver-container:/2022solver/
```

- In this example, a file `solver-track-instruction.md` is copied to `/2022solver/` of `mysolver-container`. 
- To re-enter a running container, use `docker exec` as follows. You can find the file `solver-track-instruction.md` copied from your local machine. 

```bash
$ docker exec -it mysolver-container bash
root@13765b36541e:/# ls 2022solver/
README.md  example  run.sh  solver-track-instruction.md
```

- By using the commands explained above, please install your solver and rewrite `run.sh` so that the command `/2022solver/run.sh /2022solver/example/hc-toyno-01.col /2022solver/example/hc-toyno-01_01.dat` returns appropriate output. 

- After completing your installation, the final task is `docker export`. 
- If you are in the running container, please detach by `ctrl-pq`. 
- Check your container exists `docker ps -a`. 

```bash
$ docker ps -a
CONTAINER ID   IMAGE          COMMAND   CREATED          STATUS          PORTS     NAMES
13765b36541e   mysolver:v01   "bash"    39 minutes ago   Up 39 minutes             mysolver-container
``` 

- Then, execure the following command, which will create your solver archive. 

```bash
$ docker export mysolver-container | gzip -c > mysolver-container.tar.gz
```

- Please add `mysolver-container.tar.gz` to your repository at your submission. 

### Cheet sheet

- `docker build`
- `docker export`
- `docker image ls`
- `docker ps -a`
- `docker cp`
- `docker exec`
- `docker export`
