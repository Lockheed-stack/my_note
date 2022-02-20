# Docker

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

