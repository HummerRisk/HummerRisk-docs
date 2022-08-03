# 安装文档

!!! info "说明"
    全新安装的 Linux(x64)  
    需要连接 互联网  
    使用 root 用户执行

## 安装方式

!!! info "外置环境要求"
    - 推荐使用外置 数据库, 方便日后扩展升级

| DB      | Version |
| :------ | :------ |
| MySQL   | >= 5.7  |
| MariaDB | >= 10.2 |


=== "一键部署"

    !!! tip ""
        ```sh
        curl -sSL https://github.com/HummerRisk/HummerRisk/releases/download/{{ hummerrisk.version }}/quick_start.sh | bash
        ```

    !!! tip ""
        ```sh
        # 安装完成后配置文件 /opt/hummerrisk/config/install.conf
        ```
        ```sh
        cd /opt/hummerrisk-installer-{{ hummerrisk.version }}

        # 启动
        hrctl start

        # 停止
        hrctl stop

        # 卸载
        hrctl uninstall

        # 帮助
        hrctl -h
        ```

=== "手动部署"
    !!! tip ""
        ```sh
        cd /opt
        wget https://github.com/HummerRisk/HummerRisk/releases/download/{{ hummerrisk.version }}/hummerrisk-installer-{{ hummerrisk.version }}.tar.gz
        tar -xf hummerrisk-installer-{{ hummerrisk.version }}.tar.gz
        cd hummerrisk-installer-{{ hummerrisk.version }}
        cat install.conf
        ```
        ```vim

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

        ```
        ```sh
        # 安装
        bash install.sh

        # 启动
        hrctl start
        ```

    !!! tip ""
        ```sh
        # 安装完成后配置文件 /opt/hummerrisk/config/install.conf
        ```
        ```sh
        cd /opt/hummerrisk-installer-{{ hummerrisk.version }}

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

=== "离线部署"

    !!! tip ""
        ```sh
        百度网盘下载链接: https://pan.baidu.com/s/1LeDx5hF_RkkpO8HcsYUDAQ 提取码: 4ljt
        网站资源下载链接: https://docs.hummerrisk.com/about/download/

        tar zxf hummerrisk-offline-installer-{{ hummerrisk.version }}.tar.gz
        cd hummerrisk-offline-installer-{{ hummerrisk.version }}
        ```
        ```sh
        # 根据需要修改配置文件模板, 如果不清楚用途可以跳过修改
        cat install.conf
        ```
        ```vim
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
        ```
        ```sh
        # 安装
        hrctl install

        # 启动
        hrctl start
        ```

    !!! tip ""
        ```sh
        # 安装完成后配置文件 /opt/hummerrisk/config/config.txt
        ```
        ```sh

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
