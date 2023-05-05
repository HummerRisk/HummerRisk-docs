### 常见安装问题

#### Q. 安装过程中，Docker 检测失败
![docker](../img/question/install/start-docker.png){ width="65%" }

!!! question ""
    A. 默认情况下，使用 HummerRisk 安装脚本安装时会检测您 Linux 主机上是否安装 Docker 以及 docker-compose ，如果都已安装，则会跳过安装步骤，此时你应该保证您的 Docker 和 docker-compose 是可以正常使用的，通过命令`docker ps` 和 `docker-compose -v`可以进行自检。如果您依旧解决不了此问题，建议使用纯净的Linux系统重新安装，HummerRisk 安装脚本会自动安装所有依赖软件，包括 docker 和 docker-compose。

#### Q. 安装过程出现的 Docker network 错误
出现的错误日志可能是： `failed to create network hummer_net: Error response from daemon: Pool overlaps with other one on this address space`
!!! question ""
    A. 出现该问题的原因通常是因为 docker network 的网段冲突，此时您可以修改 HummerRisk 的 install.conf 的配置文件中的 HMR_DOCKER_SUBNET 字段来修复网段冲突问题

#### Q. 安装过程出现端口被占用
出现的错误日志可能是： `0.0.0.0:80 bind: address already in use`
!!! question ""
    A. 将端口修改为未被占用的端口即可，通过命令`netstat -ntpl` 可以查看当前系统的端口占用情况，修改 install.conf 的配置文件中的 HMR_HTTP_PORT 来更改监听端口，之后使用 `hrctl restart` 重新启动