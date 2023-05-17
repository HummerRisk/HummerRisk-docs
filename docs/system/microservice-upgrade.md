# 升级文档
!!! warning "更新前请一定要做好数据库备份工作！HummerRisk v1.0 开始采用 springcloud 微服务架构，微服务架构更加易于扩展、易于容错、灵活部署，但是需要注意的是 HummerRisk v0.x 版本无法直接升级到 v1.0，如需使用 HummerRisk 请手动安装最新版本"

### 1.备份
!!! tip "备份"
    ``` bash linenums="1"
    # 该命令会自动备份数据库到 /opt/hummerrisk/db_backup/ 目录
    $ hrctl backup_db
    [SUCCESS]  'Backup succeeded! The backup file has been saved to': /opt/hummerrisk/db_backup/hummerrisk-xxx.sql
    ```

### 2.升级步骤
=== "在线升级"
    !!! warning "📢 注意：如果 upgrade 命令不指定版本号则会升级到当前最新版本，建议去 Github 查看版本号，指定版本升级"
        https://github.com/HummerRisk/HummerRisk/releases

    !!! tip "1.快捷升级"
        ``` bash linenums="1"
        # 例如：升级到指定版本 v1.0.0
        hrctl upgrade v1.0.0
        ```

    !!! question "如果服务器网络环境不佳，可尝试手动在线升级"
        - 中国大陆
        ``` bash linenums="1"
        cd /tmp
        # 指定需要升级的目标版本号
        version=v1.0.0
        wget https://download.hummerrisk.com/HummerRisk/installer/releases/download/${version}/hummerrisk-installer-${version}.tar.gz
        tar -xf hummerrisk-installer-${version}}.tar.gz
        cd hummerrisk-installer-${version}}
        # 执行升级命令，等待升级完成
        hrctl upgrade
        ```
        - 全球：
        ``` bash linenums="1"
        cd /tmp
        # 指定需要升级的目标版本号
        version=v1.0.0
        wget https://github.com/HummerRisk/installer/releases/download/${version}/hummerrisk-installer-${version}.tar.gz
        tar -xf hummerrisk-installer-${version}}.tar.gz
        cd hummerrisk-installer-${version}}
        # 执行升级命令，等待升级完成
        hrctl upgrade
        ```

    !!! tip "2.升级完成后查看当前状态，验证是否升级成功,正常所有容器应该是 healthy"
        ``` bash linenums="1"
        [root@hummerrisk tmp]# hrctl version
        v1.0.0
        [root@hummerrisk tmp]# hrctl status
        NAME                IMAGE                            COMMAND                  SERVICE             CREATED             STATUS                        PORTS
        hmr-auth            hummerrisk/hmr-auth:v1.0.0       "/deployments/run-ja…"   auth                2 minutes ago       Up 2 minutes (healthy)        9200/tcp
        hmr-cloud           hummerrisk/hmr-cloud:v1.0.0      "/deployments/run-ja…"   cloud               2 minutes ago       Up About a minute (healthy)   8778/tcp, 9400/tcp, 9779/tcp
        hmr-flyway          hummerrisk/hmr-flyway:v1.0.0     "/deployments/run-ja…"   flyway              2 minutes ago       Up 2 minutes (healthy)        9000/tcp
        hmr-gateway         hummerrisk/hmr-gateway:v1.0.0    "/deployments/run-ja…"   gateway             2 minutes ago       Up About a minute (healthy)   8080/tcp
        hmr-job             hummerrisk/hmr-job:v1.0.0        "sh -c 'java -jar $J…"   jobs                2 minutes ago       Up About a minute (healthy)
        hmr-k8s             hummerrisk/hmr-k8s:v1.0.0        "/deployments/run-ja…"   k8s                 2 minutes ago       Up About a minute (healthy)   9500/tcp
        hmr-mysql           hummerrisk/mysql:8.0.32          "docker-entrypoint.s…"   mysql               2 minutes ago       Up 2 minutes (healthy)        3306/tcp, 33060/tcp
        hmr-nacos           hummerrisk/nacos-server:v2.2.0   "bin/docker-startup.…"   nacos               2 minutes ago       Up 2 minutes (healthy)        8848/tcp
        hmr-redis           hummerrisk/redis:6.2.10-alpine   "docker-entrypoint.s…"   redis               2 minutes ago       Up 2 minutes (healthy)        6379/tcp
        hmr-system          hummerrisk/hmr-system:v1.0.0     "/deployments/run-ja…"   system              2 minutes ago       Up About a minute (healthy)   9300/tcp
        hmr-ui              hummerrisk/hmr-ui:v1.0.0         "/docker-entrypoint.…"   ui                  2 minutes ago       Up About a minute (healthy)   0.0.0.0:8111->80/tcp, :::8111->80/tcp
        ```

=== "离线升级"
    [离线包下载](https://docs.hummerrisk.com/about/download/)

    !!! tip "1.下载解压离线安装包，进入安装包执行升级命令"
        ``` bash linenums="1"
        cd /tmp
        tar zxf hummerrisk-offline-installer-${hummerrisk_version}.tar.gz
        cd hummerrisk-offline-installer-${hummerrisk_version}
        hrctl upgrade
        ```

    !!! tip "2.升级完成后查看当前状态，验证是否升级成功,正常所有容器应该是 healthy"
        ``` bash linenums="1"
        [root@hummerrisk tmp]# hrctl version
        v1.0.0
        [root@hummerrisk tmp]# hrctl status
        NAME                IMAGE                            COMMAND                  SERVICE             CREATED             STATUS                        PORTS
        hmr-auth            hummerrisk/hmr-auth:v1.0.0       "/deployments/run-ja…"   auth                2 minutes ago       Up 2 minutes (healthy)        9200/tcp
        hmr-cloud           hummerrisk/hmr-cloud:v1.0.0      "/deployments/run-ja…"   cloud               2 minutes ago       Up About a minute (healthy)   8778/tcp, 9400/tcp, 9779/tcp
        hmr-flyway          hummerrisk/hmr-flyway:v1.0.0     "/deployments/run-ja…"   flyway              2 minutes ago       Up 2 minutes (healthy)        9000/tcp
        hmr-gateway         hummerrisk/hmr-gateway:v1.0.0    "/deployments/run-ja…"   gateway             2 minutes ago       Up About a minute (healthy)   8080/tcp
        hmr-job             hummerrisk/hmr-job:v1.0.0        "sh -c 'java -jar $J…"   jobs                2 minutes ago       Up About a minute (healthy)
        hmr-k8s             hummerrisk/hmr-k8s:v1.0.0        "/deployments/run-ja…"   k8s                 2 minutes ago       Up About a minute (healthy)   9500/tcp
        hmr-mysql           hummerrisk/mysql:8.0.32          "docker-entrypoint.s…"   mysql               2 minutes ago       Up 2 minutes (healthy)        3306/tcp, 33060/tcp
        hmr-nacos           hummerrisk/nacos-server:v2.2.0   "bin/docker-startup.…"   nacos               2 minutes ago       Up 2 minutes (healthy)        8848/tcp
        hmr-redis           hummerrisk/redis:6.2.10-alpine   "docker-entrypoint.s…"   redis               2 minutes ago       Up 2 minutes (healthy)        6379/tcp
        hmr-system          hummerrisk/hmr-system:v1.0.0     "/deployments/run-ja…"   system              2 minutes ago       Up About a minute (healthy)   9300/tcp
        hmr-ui              hummerrisk/hmr-ui:v1.0.0         "/docker-entrypoint.…"   ui                  2 minutes ago       Up About a minute (healthy)   0.0.0.0:8111->80/tcp, :::8111->80/tcp
        ```

!!! warning "默认 web 登录账户: admin 密码：hummer"
