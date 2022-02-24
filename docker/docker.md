Docker

### 1.概述

虚拟机技术缺点：1.资源占用多。

​							   2.冗余步骤多。

​							   3.启动慢。

<img src="https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210923161538494.png" alt="image-20210923161538494" style="zoom:80%;" />



容器化技术：不是模拟一个完整的操作系统。

<img src="https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210923161626449.png" alt="image-20210923161626449" style="zoom:80%;" />



**docker和虚拟机技术的不同**

* 传统虚拟机，虚拟出一套硬件，运行一个完整的操作系统，在这个系统上安装和运行软件。
* 容器内的应用直接运行在宿主机的内容，容器是没有子集的内核，也没有虚拟出硬件，所以轻巧。
* 每个容器互相隔离，每个容器都有一个属于子集的文件系统，互不影响。



> Devops(开发，运维)

**应用更快的交付和部署**

传统：一堆文档，安装程序。

Docker：打包镜像发布测试，一键运行。

**更会计的升级和扩缩容**

部署应用如搭积木一般，项目打包为一个镜像，扩展服务器A、B

**更简单的系统运维**

开发、测试环境都是高度一致。

**更高效的计算资源的利用**

Docker是内核级别的虚拟化，可以在一个物理机上运行很多容器实例。

----



### 2.docker基本组成

![image-20210924154311561](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210924154311561.png)

> **镜像（image）：**docker镜像类似模板，可以通过这个模板来创建容器服务。通过这个镜像可以创建多个容器（最终服务运行或者项目运行是在容器中的）。
>
> **容器（container）：**独立运行一个或者一组应用，通过镜像来创建的。
>
> 启动、停止、删除、基本命令；
>
> **仓库（repository）：**仓库就是存放镜像的地方，分为私有仓库、公有仓库。

-----



### 3.运行hello world镜像的流程

![image-20210924153824117](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210924153824117.png)

*run 的运行流程*

----

### 4.底层原理

**docker怎么工作的**

docker是一个CS结构的系统，docker的守护进程（或者称为服务）运行在主机上，通过socket从客户端访问。

DockerServer接收到DockerClient的指令，就执行这个命令。

![image-20210924161252373](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210924161252373.png)



**docker为什么比VM快**

1. docker有着比虚拟机更少的抽象层。
2. docker利用的是宿主机的内核，vm需要是Guest OS

![image-20210924162116699](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210924162116699.png)

*hypervisor：物理层和OS之间的中间件，允许多个操作系统和应用共享硬件。*



### 5.常用命令

#### 帮助命令

``` shell
docker version # 显示版本信息
docker info # 显示docker的系统信息，包括镜像和容器的数量。
docker 命令 --help #查看有关命令的帮助信息。
```

#### 镜像命令

* 查看所有本地主机上的镜像

````shell
docker images [OPTIONS] [REPOSITORY[:TAG]] 
````

**Options**

| Name, shorthand   | Default | Description                                         |
| ----------------- | ------- | --------------------------------------------------- |
| `--all` , `-a`    |         | Show all images (default hides intermediate images) |
| `--digests`       |         | Show digests                                        |
| `--filter` , `-f` |         | Filter output based on conditions provided          |
| `--format`        |         | Pretty-print images using a Go template             |
| `--no-trunc`      |         | Don't truncate output                               |
| `--quiet` , `-q`  |         | Only show image IDs                                 |

----

* 搜索镜像

````shell
docker search [OPTIONS] TERM 
````

**Options**

| Name, shorthand   | Default | Description                                |
| ----------------- | ------- | ------------------------------------------ |
| `--filter` , `-f` |         | Filter output based on conditions provided |
| `--format`        |         | Pretty-print search using a Go template    |
| `--limit`         | `25`    | Max number of search results               |
| `--no-trunc`      |         | Don't truncate output                      |

`This example displays images with a name containing ‘busybox’, at least 3 stars and the description isn’t truncated in the output:`

````shell
docker search --filter=stars=3 --no-trunc busybox
````

----

* 下载镜像

````shell
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
````

**Options**

| Name, shorthand           | Default | Description                                                  |
| ------------------------- | ------- | ------------------------------------------------------------ |
| `--all-tags` , `-a`       |         | Download all tagged images in the repository                 |
| `--disable-content-trust` | `true`  | Skip image verification                                      |
| `--platform`              |         | [**API 1.32+**](https://docs.docker.com/engine/api/v1.32/) Set platform if server is multi-platform capable |
| `--quiet` , `-q`          |         | Suppress verbose output                                      |



*example*

To download a particular image, or set of images (i.e., a repository), use `docker pull`. If no tag is provided, Docker Engine uses the `:latest` tag as a default. This command pulls the `debian:latest` image:

![image-20210924202718970](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210924202718970.png)

*（默认下载 latest 版本，digest为签名信息）*

Docker images can consist of multiple layers. In the example above, the image consists of two layers; `fdd5d7827f33` and `a3ed95caeb02`.

Layers can be reused by images. For example, the `debian:jessie` image shares both layers with `debian:latest`. Pulling the `debian:jessie` image therefore only pulls its metadata, but not its layers, because all layers are already present locally:

![image-20210924203111272](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210924203111272.png)

**相同的镜像层（layer）可以重复利用，节省内存**

----

* 删除镜像

````shell
docker rmi [OPTIONS] IMAGE [IMAGE...]

Name, shorthand	Default	Description
--force , -f		Force removal of the image
--no-prune		Do not delete untagged parents
````

You can remove an image using its short or long ID, its tag, or its digest.

-----

#### 容器命令

*有了镜像才可以创建容器*

* 新建容器并启动

````shell
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

# 参数说明（部分）
--name="NAME"	容器名字 tomcat01、tomcat02...容器跑起来后，用来区分容器
-d				后台方式运行
-it				使用交互式运行，进入容器查看内容
-p				指定容器的端口，如 -p 8080:8080
	-p 主机端口:容器端口(常用)
	-p ip:主机端口:容器端口
	-p 容器端口
	容器端口
-P				随机指定端口
````

**Options**

| Name, shorthand           | Default   | Description                                                  |
| ------------------------- | --------- | ------------------------------------------------------------ |
| `--add-host`              |           | Add a custom host-to-IP mapping (host:ip)                    |
| `--attach` , `-a`         |           | Attach to STDIN, STDOUT or STDERR                            |
| `--blkio-weight`          |           | Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0) |
| `--blkio-weight-device`   |           | Block IO weight (relative device weight)                     |
| `--cap-add`               |           | Add Linux capabilities                                       |
| `--cap-drop`              |           | Drop Linux capabilities                                      |
| `--cgroup-parent`         |           | Optional parent cgroup for the container                     |
| `--cgroupns`              |           | [**API 1.41+**](https://docs.docker.com/engine/api/v1.41/) Cgroup namespace to use (host\|private) 'host': Run the container in the Docker host's cgroup namespace 'private': Run the container in its own private cgroup namespace '': Use the cgroup namespace as configured by the default-cgroupns-mode option on the daemon (default) |
| `--cidfile`               |           | Write the container ID to the file                           |
| `--cpu-count`             |           | CPU count (Windows only)                                     |
| `--cpu-percent`           |           | CPU percent (Windows only)                                   |
| `--cpu-period`            |           | Limit CPU CFS (Completely Fair Scheduler) period             |
| `--cpu-quota`             |           | Limit CPU CFS (Completely Fair Scheduler) quota              |
| `--cpu-rt-period`         |           | [**API 1.25+**](https://docs.docker.com/engine/api/v1.25/) Limit CPU real-time period in microseconds |
| `--cpu-rt-runtime`        |           | [**API 1.25+**](https://docs.docker.com/engine/api/v1.25/) Limit CPU real-time runtime in microseconds |
| `--cpu-shares` , `-c`     |           | CPU shares (relative weight)                                 |
| `--cpus`                  |           | [**API 1.25+**](https://docs.docker.com/engine/api/v1.25/) Number of CPUs |
| `--cpuset-cpus`           |           | CPUs in which to allow execution (0-3, 0,1)                  |
| `--cpuset-mems`           |           | MEMs in which to allow execution (0-3, 0,1)                  |
| `--detach` , `-d`         |           | Run container in background and print container ID           |
| `--detach-keys`           |           | Override the key sequence for detaching a container          |
| `--device`                |           | Add a host device to the container                           |
| `--device-cgroup-rule`    |           | Add a rule to the cgroup allowed devices list                |
| `--device-read-bps`       |           | Limit read rate (bytes per second) from a device             |
| `--device-read-iops`      |           | Limit read rate (IO per second) from a device                |
| `--device-write-bps`      |           | Limit write rate (bytes per second) to a device              |
| `--device-write-iops`     |           | Limit write rate (IO per second) to a device                 |
| `--disable-content-trust` | `true`    | Skip image verification                                      |
| `--dns`                   |           | Set custom DNS servers                                       |
| `--dns-opt`               |           | Set DNS options                                              |
| `--dns-option`            |           | Set DNS options                                              |
| `--dns-search`            |           | Set custom DNS search domains                                |
| `--domainname`            |           | Container NIS domain name                                    |
| `--entrypoint`            |           | Overwrite the default ENTRYPOINT of the image                |
| `--env` , `-e`            |           | Set environment variables                                    |
| `--env-file`              |           | Read in a file of environment variables                      |
| `--expose`                |           | Expose a port or a range of ports                            |
| `--gpus`                  |           | [**API 1.40+**](https://docs.docker.com/engine/api/v1.40/) GPU devices to add to the container ('all' to pass all GPUs) |
| `--group-add`             |           | Add additional groups to join                                |
| `--health-cmd`            |           | Command to run to check health                               |
| `--health-interval`       |           | Time between running the check (ms\|s\|m\|h) (default 0s)    |
| `--health-retries`        |           | Consecutive failures needed to report unhealthy              |
| `--health-start-period`   |           | [**API 1.29+**](https://docs.docker.com/engine/api/v1.29/) Start period for the container to initialize before starting health-retries countdown (ms\|s\|m\|h) (default 0s) |
| `--health-timeout`        |           | Maximum time to allow one check to run (ms\|s\|m\|h) (default 0s) |
| `--help`                  |           | Print usage                                                  |
| `--hostname` , `-h`       |           | Container host name                                          |
| `--init`                  |           | [**API 1.25+**](https://docs.docker.com/engine/api/v1.25/) Run an init inside the container that forwards signals and reaps processes |
| `--interactive` , `-i`    |           | Keep STDIN open even if not attached                         |
| `--io-maxbandwidth`       |           | Maximum IO bandwidth limit for the system drive (Windows only) |
| `--io-maxiops`            |           | Maximum IOps limit for the system drive (Windows only)       |
| `--ip`                    |           | IPv4 address (e.g., 172.30.100.104)                          |
| `--ip6`                   |           | IPv6 address (e.g., 2001:db8::33)                            |
| `--ipc`                   |           | IPC mode to use                                              |
| `--isolation`             |           | Container isolation technology                               |
| `--kernel-memory`         |           | Kernel memory limit                                          |
| `--label` , `-l`          |           | Set meta data on a container                                 |
| `--label-file`            |           | Read in a line delimited file of labels                      |
| `--link`                  |           | Add link to another container                                |
| `--link-local-ip`         |           | Container IPv4/IPv6 link-local addresses                     |
| `--log-driver`            |           | Logging driver for the container                             |
| `--log-opt`               |           | Log driver options                                           |
| `--mac-address`           |           | Container MAC address (e.g., 92:d0:c6:0a:29:33)              |
| `--memory` , `-m`         |           | Memory limit                                                 |
| `--memory-reservation`    |           | Memory soft limit                                            |
| `--memory-swap`           |           | Swap limit equal to memory plus swap: '-1' to enable unlimited swap |
| `--memory-swappiness`     | `-1`      | Tune container memory swappiness (0 to 100)                  |
| `--mount`                 |           | Attach a filesystem mount to the container                   |
| `--name`                  |           | Assign a name to the container                               |
| `--net`                   |           | Connect a container to a network                             |
| `--net-alias`             |           | Add network-scoped alias for the container                   |
| `--network`               |           | Connect a container to a network                             |
| `--network-alias`         |           | Add network-scoped alias for the container                   |
| `--no-healthcheck`        |           | Disable any container-specified HEALTHCHECK                  |
| `--oom-kill-disable`      |           | Disable OOM Killer                                           |
| `--oom-score-adj`         |           | Tune host's OOM preferences (-1000 to 1000)                  |
| `--pid`                   |           | PID namespace to use                                         |
| `--pids-limit`            |           | Tune container pids limit (set -1 for unlimited)             |
| `--platform`              |           | [**API 1.32+**](https://docs.docker.com/engine/api/v1.32/) Set platform if server is multi-platform capable |
| `--privileged`            |           | Give extended privileges to this container                   |
| `--publish` , `-p`        |           | Publish a container's port(s) to the host                    |
| `--publish-all` , `-P`    |           | Publish all exposed ports to random ports                    |
| `--pull`                  | `missing` | Pull image before running ("always"\|"missing"\|"never")     |
| `--read-only`             |           | Mount the container's root filesystem as read only           |
| `--restart`               | `no`      | Restart policy to apply when a container exits               |
| `--rm`                    |           | Automatically remove the container when it exits             |
| `--runtime`               |           | Runtime to use for this container                            |
| `--security-opt`          |           | Security Options                                             |
| `--shm-size`              |           | Size of /dev/shm                                             |
| `--sig-proxy`             | `true`    | Proxy received signals to the process                        |
| `--stop-signal`           | `SIGTERM` | Signal to stop a container                                   |
| `--stop-timeout`          |           | [**API 1.25+**](https://docs.docker.com/engine/api/v1.25/) Timeout (in seconds) to stop a container |
| `--storage-opt`           |           | Storage driver options for the container                     |
| `--sysctl`                |           | Sysctl options                                               |
| `--tmpfs`                 |           | Mount a tmpfs directory                                      |
| `--tty` , `-t`            |           | Allocate a pseudo-TTY                                        |
| `--ulimit`                |           | Ulimit options                                               |
| `--user` , `-u`           |           | Username or UID (format: <name\|uid>[:<group\|gid>])         |
| `--userns`                |           | User namespace to use                                        |
| `--uts`                   |           | UTS namespace to use                                         |
| `--volume` , `-v`         |           | Bind mount a volume                                          |
| `--volume-driver`         |           | Optional volume driver for the container                     |
| `--volumes-from`          |           | Mount volumes from the specified container(s)                |
| `--workdir` , `-w`        |           | Working directory inside the container                       |

*example*

This example runs a container named `test` using the `debian:latest` image. The `-it` instructs Docker to allocate a pseudo-TTY connected to the container’s stdin; creating an interactive `bash` shell in the container. In the example, the `bash` shell is quit by entering `exit 13`.

![image-20210924220930747](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20210924220930747.png)



* 列出所有运行的容器

  ```shell
  docker ps [OPTIONS]
  #常用
  -a	#列出当前正在运行的容器和历史运行过的容器
  -n=?	#显示最近创建的容器
  -q	#只显示容器的编号
  ```
  
  **Options**
  
  | Name, shorthand   | Default | Description                                             |
  | ----------------- | ------- | ------------------------------------------------------- |
  | `--all` , `-a`    |         | Show all containers (default shows just running)        |
  | `--filter` , `-f` |         | Filter output based on conditions provided              |
  | `--format`        |         | Pretty-print containers using a Go template             |
  | `--last` , `-n`   | `-1`    | Show n last created containers (includes all states)    |
  | `--latest` , `-l` |         | Show the latest created container (includes all states) |
  | `--no-trunc`      |         | Don't truncate output                                   |
  | `--quiet` , `-q`  |         | Only display container IDs                              |
  | `--size` , `-s`   |         | Display total file sizes                                |
  
  
  
* 退出容器

  ```shell
  exit	#直接退出容器并停止
  Ctrl+p+q	#容器退出但不停止
  ```

  

* 删除容器

  ```shell
  docker rm 容器id #删除指定的容器
  docker rm -f $(docker ps -aq)	#删除所有容器
  docker ps -aq |xargs docker rm	#删除所有容器
  ```

  

* 启动和停止容器的操作

  ```shell
  docker start 容器id	#启动容器
  docker restart 容器id	#重启容器
  docker stop 容器id	#停止当前正在运行的容器
  docker kill 容器id	#强制停止当前容器
  ```




-----

#### 其他常用命令

* 后台启动容器

  ```shell
  #命令 docker run -d 镜像名
  docker run -d centos
  ```
  
  出现问题：使用docker ps，发现 centos停止了。
  
  原因：docker容器使用后台运行，必须要有一个前台进程。docker没有发现前台应用，就会自动停止。
  
  
  
* 查看日志

  ```shell
  docker logs [OPTIONS] CONTAINER
  ```
  
  **Options**
  
  | Name,shorthand    | Default | Description                                                  |
  | ----------------- | ------- | ------------------------------------------------------------ |
  | --details         |         | Show extra details provided to logs                          |
  | --follow , -f     |         | Follow log output                                            |
  | --since           |         | Show logs since timestamp (e.g. 2013-01-02T13:23:37Z) or relative (e.g. 42m for 42 minutes) |
  | --tail , -n       | all     | Number of lines to show from the end of the logs             |
  | --timestamps , -t |         | Show timestamps                                              |
  | --until           |         | API 1.35+<br/>Show logs before a timestamp (e.g. 2013-01-02T13:23:37Z) or relative (e.g. 42m for 42 minutes) |
  
  
  
  *example*
  
  Retrieve logs until a specific point in time.
  
  In order to retrieve logs before a specific point in time, run:
  
  ![image-20211006213955750](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211006213955750.png)
  
  
  
* 查看容器中的进程信息

  ```shell
  docker top CONTAINER [ps OPTIONS]
  ```

* 查看镜像的元数据
  `Return low-level information on Docker objects`

  ```shell
  docker inspect [OPTIONS] NAME|ID [NAME|ID...]
  ```

**Options**

  | Name, shorthand   | Default | Description                                       |
  | ----------------- | ------- | ------------------------------------------------- |
  | `--format` , `-f` |         | Format the output using the given Go template     |
  | `--size` , `-s`   |         | Display total file sizes if the type is container |
  | `--type`          |         | Return JSON for specified type                    |



* 进入当前正在运行的容器
  
  `一般是进入后台运行的容器`
  
  *方式一：*
  
  ```shell
  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
  ```
  
  **Options**
  
  | Name, shorthand        | Default | Description                                                  |
  | ---------------------- | ------- | ------------------------------------------------------------ |
  | `--detach` , `-d`      |         | Detached mode: run command in the background                 |
  | `--detach-keys`        |         | Override the key sequence for detaching a container          |
  | `--env` , `-e`         |         | [**API 1.25+**](https://docs.docker.com/engine/api/v1.25/) Set environment variables |
  | `--env-file`           |         | [**API 1.25+**](https://docs.docker.com/engine/api/v1.25/) Read in a file of environment variables |
  | `--interactive` , `-i` |         | Keep STDIN open even if not attached                         |
  | `--privileged`         |         | Give extended privileges to the command                      |
  | `--tty` , `-t`         |         | Allocate a pseudo-TTY                                        |
  | `--user` , `-u`        |         | Username or UID (format: <name\|uid>[:<group\|gid>])         |
  | `--workdir` , `-w`     |         | [**API 1.35+**](https://docs.docker.com/engine/api/v1.35/) Working directory inside the container |



*方式二：*

```she
docker attach [OPTIONS] CONTAINER

#Use docker attach to attach your terminal’s standard input, output, and error (or any combination of the three) to a running container using the container’s ID or name. This allows you to view its ongoing output or to control it interactively, as though the commands were running directly in your terminal.
```

**Options**

| Name, shorthand | Default | Description                                         |
| --------------- | ------- | --------------------------------------------------- |
| `--detach-keys` |         | Override the key sequence for detaching a container |
| `--no-stdin`    |         | Do not attach STDIN                                 |
| `--sig-proxy`   | `true`  | Proxy all received signals to the process           |

*example*

Attach to and detach from a running container

```shell
$ docker run -d --name topdemo ubuntu /usr/bin/top -b
$ docker attach topdemo
```



* 从容器内拷贝文件到主机

```shell
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
```

**Options**

| Name, shorthand        | Default | Description                                 |
| ---------------------- | ------- | ------------------------------------------- |
| `--archive` , `-a`     |         | Archive mode (copy all uid/gid information) |
| `--follow-link` , `-L` |         | Always follow symbol link in SRC_PATH       |

#### 小结

![image-20220220210704987](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220220210704987.png)

--------------------

### 练习

#### 1.安装nginx

> 1. 搜索镜像（去docker官网上搜）
>
> 2. 下载镜像 pull
>
> 3. 运行
> 	 ```bash
>    docker run -d --name nginx01 -p 3344:80 nginx
>    ```
>    
> 4. 本机测试
>
>     ```bash
>     curl localhost:3344
>     ```
>
>     测试结果：通过,，得到如下内容
>
>     ```html
>     <!DOCTYPE html>
>     <html>
>     <head>
>     <title>Welcome to nginx!</title>
>     <style>
>     html { color-scheme: light dark; }
>     body { width: 35em; margin: 0 auto;
>     font-family: Tahoma, Verdana, Arial, sans-serif; }
>     </style>
>     </head>
>     <body>
>     <h1>Welcome to nginx!</h1>
>     <p>If you see this page, the nginx web server is successfully installed and
>     working. Further configuration is required.</p>
>                             
>     <p>For online documentation and support please refer to
>     <a href="http://nginx.org/">nginx.org</a>.<br/>
>     Commercial support is available at
>     <a href="http://nginx.com/">nginx.com</a>.</p>
>                             
>     <p><em>Thank you for using nginx.</em></p>
>     </body>
>     </html>
>     ```
>
>     
>
> 5. 进入容器查看，切换到/etc/nginx目录下
>
>     ```bash
>     docker exec -it nginx01 /bin/bash
>     ```
>
>     ![image-20220220212838124](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220220212838124.png)
>
> 6. 问题：每次改动nginx配置文件，都需要进入容器内部修改。是否可以在容器外部提供一个映射路径，使得在容器外修改文件，容器内即可自动修改？` 答：数据卷技术volumn，后面讲`。
>
> 

#### 2.安装tomcat

>1. 官方提供的方法：
>
>   ```bash
>   docker run -it --rm tomcat:9.0
>   ```
>
>   该方法用来测试，用完即删，用`docker ps -a`无法查看到容器。
>
>   
>
>2. 下载
>
>   ```bash
>   docker pull tomcat
>   ```
>
>   
>
>3. 后台运行
>
>   ```bash
>   docker run -d -p 3345:8080 --name tomcat01 tomcat
>   ```
>
>   
>
>4. 测试，可以访问，显示404
>
>5. 进入容器
>
>   ```bash
>   docker exec -it tomcat01 /bin/bash
>   ```
>
>   
>
>6. 出现以下问题：
>
>   + linux命令少了
>   + webapps中没有东西
>
>   **答：镜像的原因，默认是最小镜像，所有不必要的部分都会删除，保证最小可运行环境。可将webapps.dist复制到webapps中。**
>
>   
>
>

#### 3.可视化界面

> docker图形化管理界面
>
> ```
> docker run -d -p 9000:9000 \
> --restar=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
> ```
>
> 



# 稍微深入

### 镜像是什么

> 镜像是一种轻量级、可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置文件
>
> 如何得到镜像：
>
> * 从远程仓库下载
> * 从别人处拷贝
> * 自己制作一个镜像DockerFile



### Docker镜像加载原理

**UnionFS联合文件系统**

> docker容器是建立在Aufs基础上的，Aufs是一种UnionFS，Unionfs是一种分层、轻量级并且高性能的文件系统，它支持队文件系统的修改，作为一次提交来一层层叠加，同时可以将不同目录挂载到同一个虚拟文件系统下。*下载镜像的时候可以看到*。
>
> UnionFS时docker镜像的基础，镜像可以通过分层来进行继承，基于基础镜像（即没有父镜像），可以制作各种具体的应用镜像。
>
> **特性：**一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合文件系统会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录。

**Docker镜像的加载**

> > bootfs
> >
> > bootfs(boot file system)主要包含bootloader和kernel，bootloader主要是引导加载kernel，Linux刚启动时会加载bootfs，在Docker镜像的最底层是bootfs。当boot加载完成后整个内核就在内存中，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。
>
> > rootfs
> >
> > rootfs(root file system)，在bootfs之上，包含的就是典型Linux系统中的/dev，/proc，/bin，/etc等标准目录和文件，rootfs就是各种不同的操作系统发行版，比如Ubuntu、centos等。
>
> ![img](https://www.erlo.vip/joke?src=https://images2018.cnblogs.com/blog/1011251/201806/1011251-20180610104201926-841982810.png)
>
> ----------
>
> 传统的Linux加载bootfs时会先将rootfs设为read-only，然后在系统自检之后将rootfs从read-only改为read-write，然后我们就可以在rootfs上进行写和读的操作了。
>
> 但Docker的镜像却不是这样，它在bootfs自检完毕之后并不会把rootfs的read-only改为read-write。而是利用union mount（UnionFS的一种挂载机制）将一个或多个read-only的rootfs加载到之前的read-only的rootfs层之上。在加载了这么多层的rootfs之后，仍然让它看起来只像是一个文件系统，在Docker的体系里把union mount的这些read-only的rootfs叫做Docker的镜像。
>
> 但是，此时的每一层rootfs都是read-only的，我们此时还不能对其进行操作。当我们创建一个容器，也就是将Docker镜像进行实例化，系统会在一层或是多层read-only的rootfs之上分配一层空的read-write的rootfs。
>
> ![img](https://www.erlo.vip/joke?src=https://images2018.cnblogs.com/blog/1011251/201806/1011251-20180610105404291-1224869556.png)
>
> ------------
>
> 得益于AUFS的特性，每一个对readonly层文件/目录的修改都只会存在于上层的writeable层中。这样由于不存在竞争，多个container可以共享readonly的FS层。
>
> 所以Docker将readonly的FS层称作"image" - 对于container而言整个rootfs都是read-write的，但事实上所有的修改都写入最上层的writeable层中，image不保存用户状态，只用于模版、新建和复制使用。
>
> ![img](https://www.erlo.vip/joke?src=https://images2018.cnblogs.com/blog/1011251/201806/1011251-20180610105837781-1145664389.png)
>
> ![img](http://dockone.io/uploads/article/20190626/a20b70e3e4ca61faa2c3436e1bb2d93a.png)
>
> 举个例子验证上面所说的：
>
> ```bash
> docker run ubuntu touch happiness.txt
> ```
>
> 即使这个ubuntu容器不再运行，我们依旧能够在主机的文件系统上找到这个新文件。
>
> ![image-20220221195259840](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220221195259840.png)
>
> *注：在Docker version 20.10.12中，没有aufs这个目录了，取而代之的是overlay2目录。*
>
> --------
>
> 上层的image依赖下层的image称作base image。因此想要从一个image启动一个container,Docker会先加载这个image和依赖的父images以及base image,用户的进程运行在writeable的layer中。所有parent image中的数据信息以及ID、网络和lxc管理的资源限制等具体container的配置，构成一个Dokcer概念上的container。
>
> ![img](https://www.erlo.vip/joke?src=https://images2018.cnblogs.com/blog/1011251/201806/1011251-20180610110218450-1804104016.png)

### commit镜像

>```bash
>docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
>```
>
>**Options**
>
>| Name, shorthand    | Default | Description                                                |
>| ------------------ | ------- | ---------------------------------------------------------- |
>| `--author` , `-a`  |         | Author (e.g., "John Hannibal Smith <hannibal@a-team.com>") |
>| `--change` , `-c`  |         | Apply Dockerfile instruction to the created image          |
>| `--message` , `-m` |         | Commit message                                             |
>| `--pause` , `-p`   | `true`  | Pause container during commit                              |
>
>将容器的可读写层转换为一个只读层，这样就把一个容器转换为不可变的镜像。
>
>![img](http://dockone.io/uploads/article/20190626/28059b3a499faba896263c0ff077fe3a.png)
>
>
>
>**测试**
>
>* 启动一个默认的tomcat
>* 发现没有这个没有webapps应用
>* 我自己拷贝了一些文件放入webapps
>* 将操作过的容器通过commit提交，产生一个新镜像
>* ![image-20220221211924675](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220221211924675.png)通过命令，发现多了一个“tomcat02”的镜像。
>
>

### 容器数据卷

**什么是容器数据卷**

> 如果数据都在容器中，当容器删除，数据就会丢失。**需求：数据持久化**
>
> 容器之间可以有一个数据共享的技术，docker容器中产生的数据，同步到本地（宿主机）
>
> ![image-20220221213738074](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220221213738074.png)
>
> **总结：容器的持久化和同步操作**

**使用方法**

*方式一：直接使用命令挂载  -v*

> ```bash
> docker run -it -v 主机目录:容器内目录
> ```
>
> 测试：
>
> * 新运行一个容器Ubuntu02，映射关系为/home/lee/docker_volume_sync : /home，并在Ubuntu02中/home目录下创建创建一个文件![image-20220221215012650](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220221215012650.png)
> * 回到主机中查看，确认同步成功。![image-20220221215213851](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220221215213851.png)
> * 反之，在主机中创建一个文件，容器Ubuntu02中也出现了，确认同步成功。![image-20220221215643290](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220221215643290.png)

#### 练习：安装MySQL

> 1. 获取镜像
>
>    ```bash
>    docker pull mysql
>    ```
>
> 2. 运行镜像，设置挂载、mysql密码
>
>    ```bash
>    docker run -d -p 3310:3306 -v /home/lee/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=lilin001 --name mysql01 mysql
>    ```
>
>    
>
> 3. 测试连接（我是用vscode连接，OK）
>
> 4. 查看映射路径，OK

#### 具名挂载、匿名挂载

> **匿名挂载**
>
> `-v 容器内路径`，没有容器外的路径
>
> example
>
> ```bash
> docker run -d -P --name nginx02 -v /etc/nginx nginx
> ```
>
> 使用命令`docker volume ls`查看：
>
> ![image-20220222201820556](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220222201820556.png)
>
> 卷名volume name是一串随机生成的字符串
>
> 
>
> **具名挂载**
>
> `-v 卷名：容器内路径`
>
> example
>
> ```bash
> docker run -d -P --name nginx03 -v volume_nginx:/etc/nginx nginx
> ```
>
> 通过命令查看，发现多了一个“volume_nginx”的卷。
>
> ![image-20220222202641077](H:\school_materal_temp\硕士\MK笔记\docker\docker.assets\image-20220222202641077.png)
>
> 再具体点，使用命令`docker volume inspect`查看，可以看到具体挂载的地方。
>
> ![image-20220222203048458](H:\school_materal_temp\硕士\MK笔记\docker\docker.assets\image-20220222203048458.png)
>
> 其实都是放在`/var/lib/docker/volume`当中。
>
> **小结**
>
> ```shell
> -v 容器内路径	#匿名挂载
> -v 卷名：容器内路径		#具名挂载
> -v 宿主机路径：容器内路径		#指定路径挂载
> #拓展
> -v 容器内路径：ro|rw		#改变文件读写权限
> ro为readonly，只能通过宿主机来修改
> rw为readwrite，是默认方式
> 
> ```
>
> 

*方式二：使用dockerfile*

#### 初识dockerfile

> dockerfile是用来构建docker镜像的构建文件，即命令脚本。通过这个脚本可以生成镜像，每个命令，都是镜像的一层。
>
> **过程：**
>
> 1. 编写dockerfile
>
>    ```dockerfile
>    FROM ubuntu
>    VOLUME ["volume01","volume02"]
>    CMD echo "---completed-----"
>    CMD /bin/bash
>    ```
>
>    
>
> 2. 执行命令`docker build -f dockerfile1 -t buildtest:1.0.0 ./`，输出以下结果：![image-20220222212225672](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220222212225672.png)
>    不难看出，是一层层构建的。通过命令可以看到自己新建的镜像：![image-20220222212955426](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220222212955426.png)
>
> 3. 运行并进入容器，可以看到有volume1和volume2![image-20220222213813386](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220222213813386.png)这两个卷肯定和外部有关联。由于是匿名挂载，所以是一串随机字符串。
>
> 4. 用`docker inspect`查看容器，可看到挂载的地方![image-20220222215055138](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220222215055138.png)

#### 数据卷容器

> 应用场景举例：多个MySQL同步数据
>
> ![image-20220223155747431](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220223155747431.png)
>
> 测试：
>
> 1. 用之前dockerfile构建的镜像，运行一个容器`ubuntu_container01`,作为数据卷容器。
>
> 2. 再运行一个容器`ubuntu_container02`，并继承`ubuntu_container01`。
>
>    ```bash
>    docker run -it --name ubuntu_container02 --volumes-from ubuntu_container01 buildtest:1.0.0
>    ```
>
> 3. 在`ubuntucontainer01`中volume01目录下创建一个文件`createBycontainer01`，再进入`ubuntucontainer02`中volume01目录下查看，发现多了一个文件，同步成功。![image-20220223161911982](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220223161911982.png)
>
> 4. 反之在`ubuntu_container02`中的volume01目录下创建文件，也能同步，都可以共享。把``ubuntu_container01`删除后，共享的文件也不会丢失。
>
> 5. **小结：拷贝的概念，是一种双向拷贝。数据卷的生命周期一直持续到没有容器使用为止。**![image-20220223162634992](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220223162634992.png)

### dockerfile

#### 介绍

具体情况前往https://docs.docker.com/engine/reference/builder/，这里做了点摘录

> dockerfile是用来构建docker镜像的文件，是命令参数脚本。dockerfile是面向开发的。
>
> 构建步骤:
>
> 1. 编写一个dockerfile文件。
> 2. docker build构建成为一个镜像。
> 3. docker run 运行镜像。
> 4. 或者docker push发布镜像（dockerhub、xxx镜像仓库）。

**格式**

> Here is the format of the `Dockerfile`:
>
> ```bash
> # Comment
> INSTRUCTION arguments
> ```
>
> The instruction is **not case-sensitive**. However, convention is for them to be UPPERCASE to distinguish them from arguments more easily.
>
> Docker runs instructions in a `Dockerfile` in order. A `Dockerfile` **must begin with a `FROM` instruction**.This may be after [parser directives](https://docs.docker.com/engine/reference/builder/#parser-directives), [comments](https://docs.docker.com/engine/reference/builder/#format), and globally scoped [ARGs](https://docs.docker.com/engine/reference/builder/#arg). The `FROM` instruction specifies the [*Parent Image*](https://docs.docker.com/glossary/#parent-image) from which you are building. `FROM` may only be preceded by one or more `ARG` instructions, which declare arguments that are used in `FROM` lines in the `Dockerfile`.
>
> -------------------
>
> **注释 #**
>
> > Docker treats lines that *begin* with `#` as a comment, unless the line is a valid [parser directive](https://docs.docker.com/engine/reference/builder/#parser-directives). A `#` marker anywhere else in a line is treated as an argument. This allows statements like:
> >
> > ```dockerfile
> > # Comment
> > RUN echo 'we are running some # of cool things'
> > ```
>
> **解释器指令Parser directives**
>
> > Parser directives are optional, and affect the way in which subsequent lines in a `Dockerfile` are handled. Parser directives do not add layers to the build, and will not be shown as a build step. 
> >
> > Parser directives are written as a special type of comment in the form `# directive=value`. A single directive may only be used once.
> >
> > All parser directives must be at the very top of a `Dockerfile`.
> >
> > Parser directives are not case-sensitive. However, convention is for them to be lowercase.
> >
> > 
> >
> > The following parser directives are supported:
> >
> > - `syntax`
> > - `escape`
> >
> > **syntax**
> >
> > The syntax directive defines the location of the Dockerfile syntax that is used to build the Dockerfile.This feature is only available when using the [BuildKit](https://docs.docker.com/engine/reference/builder/#buildkit) backend, and is ignored when using the classic builder backend.
> >
> > ```dockerfile
> > # syntax=[remote image reference]
> > ```
> >
> > For example:
> >
> > ```dockerfile
> > # syntax=docker/dockerfile:1
> > # syntax=docker.io/docker/dockerfile:1
> > # syntax=example.com/user/repo:tag@sha256:abcdef...
> > ```

#### dockerfile的指令

> ![img](https://www.freesion.com/images/301/f7913396947af4dc8fc65b51f4a449a5.png)
>
> ```dockerfile
> FROM	#基础镜像，一切从这里开始构建
> MAINTAINER	#镜像是谁写的
> RUN		#镜像构建的时候需要运行的命令
> ADD		#步骤，添加内容
> WORKDIR		#镜像的工作目录
> VOLUME		#挂载的目录
> EXPOSE		#暴露端口配置
> CMD			#指定这个容器的时候要运行的命令，只有最后一个会生效，可替代
> ENTRYPOINT		#指定这个容器启动的时候要运行的命令，可以追加命令
> ONBUILD		#它后面跟的是其它指令，比如 RUN, COPY 等，而这些指令，在当前镜像构建时并不会被执行。只有以当前镜像为基础镜像，去构建下一级镜像的 时候才会被执行
> COPY		#类似ADD，将我们文件拷贝到镜像中
> ENV			#构建的时候设置环境变量
> ```
>

#### 练习：创建一个centos

docker hub中99%的镜像都是从`scratch`这个基础镜像而来，`FROM scratch`。然后配置所需软件和配置文件进行构建。

> 1. `pull`下载的镜像是高度精简的，没有vim、ifconfig命令，因此自己构建一个包含这两个命令的镜像。
>
> 2. 编写dockerfile，注意使用centos8会报错，因为默认最新的是centos8，但无法找到。
>
> ```dockerfile
>    FROM centos:7
>    MAINTAINER lockheed<myemail@gmail.com>
> 
>    ENV MYPATH /usr/local
>    WORKDIR $MYPATH
> 
>    RUN yum -y install vim
>    RUN yum -y install net-tools
> 
>    EXPOSE 80
>    CMD echo $MYPATH
>    CMD echo "---end---"
>    CMD /bin/bash
> ```
>
> 3. 注意步骤2的问题即可`build`成功，输出内容很长就不截图了。输入`docker images`命令可以发现多了一个镜像，由于没有指定版本，因此默认tag是`lastest`。![image-20220224155314920](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220224155314920.png)
> 4. 进入容器，默认的工作目录已经改为`/usr/local`，`ifconfig`、`vim`等指令都可直接使用。![image-20220224160046052](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220224160046052.png)
> 5. 使用`docker history`查看一下本地进行的变更历史![image-20220224161500204](https://gitee.com/Lockheed_LEE/images/raw/master/img/image-20220224161500204.png)

#### CMD和ENTRYPOINT的区别

**测试CMD**

> 1. dockerfile文件
>
>    ```dockerfile
>    FROM centos:7
>    CMD ["ls","-a"]
>    ```
>
> 2. build后运行，启动容器后就直接运行了`ls -a`命令
>
>    ```shell
>    root@lee:/home/lee/dockerfile_test# docker run -it --name cmd_test1 cmd_test
>    .   .dockerenv         bin  etc   lib    media  opt   root  sbin  sys  usr
>    ..  anaconda-post.log  dev  home  lib64  mnt    proc  run   srv   tmp  var
>    root@lee:/home/lee/dockerfile_test#
>    ```
>
> 3. 换种方式run，报错，因为`-l`替换了`ls -a`，显然没有`-l`这个命令。
>
>    ```bash
>    root@lee:/home/lee/dockerfile_test# docker run -it --name cmd_test2 cmd_test -l
>    docker: Error response from daemon: OCI runtime create failed: container_linux.go:380: starting container process caused: exec: "-l": executable file not found in $PATH: unknown.
>    root@lee:/home/lee/dockerfile_test#
>    ```
>
>    
>
> 4. 再换种方式run，成功，因为`ls -al`替换了`ls -a`，且这个命令存在
>
>    ```bash
>    root@lee:/home/lee/dockerfile_test# docker run -it --name cmd_test3 cmd_test ls -al
>    total 64
>    drwxr-xr-x   1 root root  4096 Feb 24 09:14 .
>    drwxr-xr-x   1 root root  4096 Feb 24 09:14 ..
>    -rwxr-xr-x   1 root root     0 Feb 24 09:14 .dockerenv
>    -rw-r--r--   1 root root 12114 Nov 13  2020 anaconda-post.log
>    lrwxrwxrwx   1 root root     7 Nov 13  2020 bin -> usr/bin
>    drwxr-xr-x   5 root root   360 Feb 24 09:14 dev
>    drwxr-xr-x   1 root root  4096 Feb 24 09:14 etc
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 home
>    lrwxrwxrwx   1 root root     7 Nov 13  2020 lib -> usr/lib
>    lrwxrwxrwx   1 root root     9 Nov 13  2020 lib64 -> usr/lib64
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 media
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 mnt
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 opt
>    dr-xr-xr-x 177 root root     0 Feb 24 09:14 proc
>    dr-xr-x---   2 root root  4096 Nov 13  2020 root
>    drwxr-xr-x  11 root root  4096 Nov 13  2020 run
>    lrwxrwxrwx   1 root root     8 Nov 13  2020 sbin -> usr/sbin
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 srv
>    dr-xr-xr-x  12 root root     0 Feb 24 09:14 sys
>    drwxrwxrwt   7 root root  4096 Nov 13  2020 tmp
>    drwxr-xr-x  13 root root  4096 Nov 13  2020 usr
>    drwxr-xr-x  18 root root  4096 Nov 13  2020 var
>    root@lee:/home/lee/dockerfile_test#
>    ```

**ENTRYPOINT测试**

> 1. 编写dockerfile并build
>
>    ```dockerfile
>    FROM centos:7
>    ENTRYPOINT ["ls","-a"]
>    ```
>
> 2. run一下，正常。尝试用一下之前`CMD`失败的方式，发现可以这样操作。
>
>    ```bash
>    root@lee:/home/lee/dockerfile_test# docker run -it --name entrypoint_test01 entrypoint_test
>    .   .dockerenv         bin  etc   lib    media  opt   root  sbin  sys  usr
>    ..  anaconda-post.log  dev  home  lib64  mnt    proc  run   srv   tmp  var
>    root@lee:/home/lee/dockerfile_test# docker run -it --name entrypoint_test02 entrypoint_test -l
>    total 64
>    drwxr-xr-x   1 root root  4096 Feb 24 09:26 .
>    drwxr-xr-x   1 root root  4096 Feb 24 09:26 ..
>    -rwxr-xr-x   1 root root     0 Feb 24 09:26 .dockerenv
>    -rw-r--r--   1 root root 12114 Nov 13  2020 anaconda-post.log
>    lrwxrwxrwx   1 root root     7 Nov 13  2020 bin -> usr/bin
>    drwxr-xr-x   5 root root   360 Feb 24 09:26 dev
>    drwxr-xr-x   1 root root  4096 Feb 24 09:26 etc
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 home
>    lrwxrwxrwx   1 root root     7 Nov 13  2020 lib -> usr/lib
>    lrwxrwxrwx   1 root root     9 Nov 13  2020 lib64 -> usr/lib64
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 media
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 mnt
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 opt
>    dr-xr-xr-x 179 root root     0 Feb 24 09:26 proc
>    dr-xr-x---   2 root root  4096 Nov 13  2020 root
>    drwxr-xr-x  11 root root  4096 Nov 13  2020 run
>    lrwxrwxrwx   1 root root     8 Nov 13  2020 sbin -> usr/sbin
>    drwxr-xr-x   2 root root  4096 Apr 11  2018 srv
>    dr-xr-xr-x  12 root root     0 Feb 24 09:26 sys
>    drwxrwxrwt   7 root root  4096 Nov 13  2020 tmp
>    drwxr-xr-x  13 root root  4096 Nov 13  2020 usr
>    drwxr-xr-x  18 root root  4096 Nov 13  2020 var
>    root@lee:/home/lee/dockerfile_test#
>    ```

#### 练习：tomcat镜像

> 大致步骤：
> 1. 准备镜像文件 tomcat压缩包、jdk压缩包。
> 2. dockerfile文件的编写。
