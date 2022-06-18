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
        # 安装完成后配置文件 /opt/hummerrisk/config/config.txt
        ```
        ```sh
        cd /opt/hummerrisk-installer-{{ hummerrisk.version }}

        # 启动
        ./hrctl.sh start

        # 停止
        ./hrctl.sh down

        # 卸载
        ./hrctl.sh uninstall

        # 帮助
        ./hrctl.sh -h
        ```

=== "手动部署"
    !!! tip ""
        ```sh
        cd /opt
        wget https://github.com/HummerRisk/installer/releases/download/{{ hummerrisk.version }}/hummerrisk-installer-{{ hummerrisk.version }}.tar.gz
        tar -xf hummerrisk-installer-{{ hummerrisk.version }}.tar.gz
        cd hummerrisk-installer-{{ hummerrisk.version }}
        cat config-example.txt
        ```
        ```vim
        # 以下设置如果为空系统会自动生成随机字符串填入

        ## 安装配置
        DOCKER_IMAGE_PREFIX=registry.cn-qingdao.aliyuncs.com
        VOLUME_DIR=/opt/hummerrisk
        DOCKER_DIR=/var/lib/docker

        ## Compose 项目设置
        COMPOSE_PROJECT_NAME=hr
        COMPOSE_HTTP_TIMEOUT=3600
        DOCKER_CLIENT_TIMEOUT=3600

        ##  MySQL 配置, USE_EXTERNAL_MYSQL=1 表示使用外置数据库, 请输入正确的 MySQL 信息
        USE_EXTERNAL_MYSQL=0
        DB_HOST=mysql
        DB_PORT=3306
        DB_USER=root
        DB_PASSWORD=
        DB_NAME=hummerrisk

        ## Service 端口
        HTTP_PORT=80

        # 额外的配置
        CURRENT_VERSION=
        ```
        ```sh
        # 安装
        ./hrctl.sh install

        # 启动
        ./hrctl.sh start
        ```

    !!! tip ""
        ```sh
        # 安装完成后配置文件 /opt/hummerrisk/config/config.txt
        ```
        ```sh
        cd /opt/hummerrisk-installer-{{ hummerrisk.version }}

        # 启动
        ./hrctl.sh start

        # 停止
        ./hrctl.sh down

        # 卸载
        ./hrctl.sh uninstall

        # 帮助
        ./hrctl.sh -h
        ```

=== "离线部署"

    !!! tip ""
        ```sh
        百度网盘下载链接: https://pan.baidu.com/s/1LeDx5hF_RkkpO8HcsYUDAQ 提取码: 4ljt
        cd /opt
        unzip hummerrisk-offline-installer-{{ hummerrisk.version }}.zip
        cd hummerrisk-offline-installer-{{ hummerrisk.version }}
        ```
        ```sh
        # 根据需要修改配置文件模板, 如果不清楚用途可以跳过修改
        cat config-example.txt
        ```
        ```vim
        # 以下设置如果为空系统会自动生成随机字符串填入

        ## 安装配置
        DOCKER_IMAGE_PREFIX=registry.cn-qingdao.aliyuncs.com
        VOLUME_DIR=/opt/hummerrisk
        DOCKER_DIR=/var/lib/docker

        ## Compose 项目设置
        COMPOSE_PROJECT_NAME=hr
        COMPOSE_HTTP_TIMEOUT=3600
        DOCKER_CLIENT_TIMEOUT=3600

        ##  MySQL 配置, USE_EXTERNAL_MYSQL=1 表示使用外置数据库, 请输入正确的 MySQL 信息
        USE_EXTERNAL_MYSQL=0
        DB_HOST=mysql
        DB_PORT=3306
        DB_USER=root
        DB_PASSWORD=
        DB_NAME=hummerrisk

        ## Service 端口
        HTTP_PORT=80

        # 额外的配置
        CURRENT_VERSION=
        ```
        ```sh
        # 安装
        ./hrctl.sh install

        # 启动
        ./hrctl.sh start
        ```

    !!! tip ""
        ```sh
        # 安装完成后配置文件 /opt/hummerrisk/config/config.txt
        ```
        ```sh
        cd /opt/hummerrisk-installer-{{ hummerrisk.version }}

        # 启动
        ./hrctl.sh start

        # 停止
        ./hrctl.sh down

        # 卸载
        ./hrctl.sh uninstall

        # 帮助
        ./hrctl.sh -h
        ```

!!! warning "默认 web 登录账户: admin 密码：hummer"
