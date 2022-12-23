!!! info "说明"
    全新安装的 Linux(x64)  
    需要连接 互联网  
    使用 root 用户执行

### 1.安装环境要求

!!! info "外置环境要求"
    - 推荐使用外置 数据库, 方便日后扩展升级
系统支持:

| OS          | Version   |
|:------------|:----------|
| CentOS      | > = 7.3   |
| Ubuntu      | > = 20.04 |
| Debian      | > = 10.2  |
| OpenCloudOS | > = 8     |
| EulerOS     | > = 2.0   |

系统配置要求:

| 配置项 | 最低配置         | 推荐配置                    |
|:----|:-------------|-------------------------|
| OS  | Ubuntu 20.04 | >= Ubuntu 20.04         |
| CPU | 4核           | 8核                      |
| 内存  | 8G           | 16G                     |
| 磁盘  | 50GB         | 100GB                   |
| 数据库 | MySQL 5.7    | MySQL 5.7/ MariaDB 10.2 |

!!! info "快速安装预览"
[![asciicast](https://asciinema.org/a/514353.svg)](https://asciinema.org/a/514353)

---

### 2.开始安装

=== "一键部署"
    !!! tip "1.使用快速安装脚本一键安装部署"
        ``` bash linenums="1"
        # 下载最新版本的安装脚本
        curl -sSL https://github.com/HummerRisk/HummerRisk/releases/latest/download/quick_start.sh -o quick_start.sh
        
        # 执行安装命令
        bash quick_start.sh

        # 安装完成后配置文件 /opt/hummerrisk/config/install.conf

        ```
    !!! tip "2.其他命令行功能"
        ``` bash linenums="1"
        # 启动
        hrctl start

        # 停止
        hrctl down

        # 查看状态
        hrctl status

        # 卸载
        hrctl uninstall

        # 备份数据库
        hrctl backup_db
        
        # 还原数据库
        hrctl restore_db /opt/hummerrisk/db_backup/hummerrisk-xx.sql

        # 查看当前版本
        hrctl version

        # 帮助
        hrctl -h
        ```

=== "手动部署"
    !!! tip "1.下载安装包"
        ``` bash linenums="1"
        # 指定需要安装的版本
        export hummerrisk_version=v0.2.0

        # 下载安装包
        wget https://github.com/HummerRisk/HummerRisk/releases/download/${hummerrisk_version}/hummerrisk-installer-${hummerrisk_version}.tar.gz

        # 解压安装包       
        tar -xf hummerrisk-installer-${hummerrisk_version}.tar.gz
        cd hummerrisk-installer-${hummerrisk_version}
        ```

    !!! tip "2.根据需要修改配置文件(纯净系统环境使用默认配置即可)"
        ``` vim linenums="1"
        $ vim install.conf

        # 以下设置如果为空系统会自动生成随机字符串填入
        
        ## 安装配置
        # 镜像仓库地址
        HR_DOCKER_IMAGE_PREFIX=registry.cn-beijing.aliyuncs.com
        # 数据持久化目录
        HR_BASE=/opt/hummerrisk
        HR_DOCKER_DIR=/var/lib/docker
        
        ## Service web端口
        HR_HTTP_PORT=${HR_HTTP_PORT}
        
        # 当前版本
        HR_CURRENT_VERSION=v1.0
        
        ##  MySQL 数据库配置, USE_EXTERNAL_MYSQL=1 表示使用外置数据库, 请输入正确的 MySQL 信息
        HR_USE_EXTERNAL_MYSQL=${HR_USE_EXTERNAL_MYSQL}
        HR_DB_HOST=${HR_DB_HOST}
        HR_DB_PORT=${HR_DB_PORT}
        HR_DB_USER=${HR_DB_USER}
        HR_DB_PASSWORD=${HR_DB_PASSWORD}
        HR_DB_NAME=${HR_DB_NAME}
        
        ## docker 配置
        # docker 网段设置
        HR_DOCKER_SUBNET=172.19.0.0/16
        # docker 网关 IP
        HR_DOCKER_GATEWAY=172.19.0.1
        
        ## Compose 项目设置
        # 项目名称
        COMPOSE_PROJECT_NAME=hr

        # 超时时间
        COMPOSE_HTTP_TIMEOUT=3600

        # docker 客户端超时时间
        DOCKER_CLIENT_TIMEOUT=3600

        # cve 漏洞库版本
        TRIVY_SERVER_PORT=4975
        TRIVY_DB_VERSION=2022122020

        ```
    !!! tip "3.开始安装"
        ``` bash linenums="1"
        # 安装
        bash install.sh

        # 启动
        hrctl start

        # 安装完成后默认配置文件在 /opt/hummerrisk/config/install.conf

        ```

=== "离线部署"

    !!! tip "1.准备离线包"
        ``` bash linenums="1"
        百度网盘下载链接: https://pan.baidu.com/s/1LeDx5hF_RkkpO8HcsYUDAQ 提取码: 4ljt
        网站资源下载链接: https://docs.hummerrisk.com/about/download/

        tar zxf hummerrisk-offline-installer-${hummerrisk_version}.tar.gz
        cd hummerrisk-offline-installer-${hummerrisk_version}
        ```

    !!! tip "2.根据需要修改配置文件 （纯净系统环境使用默认配置即可）"
        ``` vim linenums="1"
        $ vim install.conf

        # 以下设置如果为空系统会自动生成随机字符串填入
        
        ## 安装配置
        # 镜像仓库地址
        HR_DOCKER_IMAGE_PREFIX=registry.cn-beijing.aliyuncs.com
        # 数据持久化目录
        HR_BASE=/opt/hummerrisk
        HR_DOCKER_DIR=/var/lib/docker
        
        ## Service web端口
        HR_HTTP_PORT=${HR_HTTP_PORT}
        
        # 当前版本
        HR_CURRENT_VERSION=v1.0
        
        ##  MySQL 数据库配置, USE_EXTERNAL_MYSQL=1 表示使用外置数据库, 请输入正确的 MySQL 信息
        HR_USE_EXTERNAL_MYSQL=${HR_USE_EXTERNAL_MYSQL}
        HR_DB_HOST=${HR_DB_HOST}
        HR_DB_PORT=${HR_DB_PORT}
        HR_DB_USER=${HR_DB_USER}
        HR_DB_PASSWORD=${HR_DB_PASSWORD}
        HR_DB_NAME=${HR_DB_NAME}
        
        ## docker 配置
        # docker 网段设置
        HR_DOCKER_SUBNET=172.19.0.0/16
        # docker 网关 IP
        HR_DOCKER_GATEWAY=172.19.0.1
        
        ## Compose 项目设置
        # 项目名称
        COMPOSE_PROJECT_NAME=hr
        # 超时时间
        COMPOSE_HTTP_TIMEOUT=3600
        # docker 客户端超时时间
        DOCKER_CLIENT_TIMEOUT=3600
        
        # cve 漏洞库版本
        TRIVY_SERVER_PORT=4975
        TRIVY_DB_VERSION=2022122020
        ```

    !!! tip "3.开始安装"
        ``` bash linenums="1"
        # 安装
        ./install.sh

        # 启动
        hrctl start

        # 安装完成后配置文件 /opt/hummerrisk/conf/install.conf
        ```

=== "常用命令"
    !!! tip "常用命令"
        ``` bash linenums="1"
        # 启动
        hrctl start

        # 停止
        hrctl down

        # 查看状态
        hrctl status

        # 卸载
        hrctl uninstall

        # 备份数据库
        hrctl backup_db

        # 还原数据库
        hrctl restore_db /opt/hummerrisk/db_backup/hummerrisk-xx.sql

        # 查看当前版本
        hrctl version

        # 帮助
        hrctl -h
        ```
!!! warning "默认 web 登录账户: admin 密码：hummer"
