# 升级文档
!!! warning "更新前请一定要做好数据库备份工作"

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
        - 海外：
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
        v0.7.0
        [root@hummerrisk tmp]# hrctl status
            Name                  Command                  State                         Ports
        ---------------------------------------------------------------------------------------------------------
        hummer_mysql   docker-entrypoint.sh --def ...   Up (healthy)   3306/tcp, 33060/tcp
        hummer_risk    /deployments/run-java.sh         Up (healthy)   0.0.0.0:80->8088/tcp, 8778/tcp, 9779/tcp
        trivy_server   trivy server --skip-update ...   Up (healthy)   0.0.0.0:4975->4975/tcp, 8778/tcp, 9779/tcp
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
        NAME                IMAGE                                                             COMMAND                  SERVICE             CREATED             STATUS                   PORTS
        hmr-auth            registry.cn-beijing.aliyuncs.com/hummerrisk/hmr-auth:v1.0.0       "/deployments/run-ja…"   auth                7 minutes ago       Up 6 minutes (healthy)   0.0.0.0:9200->9200/tcp, :::9200->9200/tcp
        hmr-cloud           registry.cn-beijing.aliyuncs.com/hummerrisk/hmr-cloud:v1.0.0      "/deployments/run-ja…"   cloud               7 minutes ago       Up 6 minutes (healthy)   8778/tcp, 9779/tcp, 0.0.0.0:9400->9400/tcp, :::9400->9400/tcp
        hmr-flyway          registry.cn-beijing.aliyuncs.com/hummerrisk/hmr-flyway:v1.0.0     "/deployments/run-ja…"   flyway              7 minutes ago       Up 6 minutes (healthy)   0.0.0.0:9000->9000/tcp, :::9000->9000/tcp
        hmr-gateway         registry.cn-beijing.aliyuncs.com/hummerrisk/hmr-gateway:v1.0.0    "/deployments/run-ja…"   gateway             2 minutes ago       Up 2 minutes (healthy)   0.0.0.0:8088->8080/tcp, :::8088->8080/tcp
        hmr-job             registry.cn-beijing.aliyuncs.com/hummerrisk/hmr-job:dev           "sh -c 'java -jar $J…"   jobs                7 minutes ago       Up 6 minutes (healthy)
        hmr-k8s             registry.cn-beijing.aliyuncs.com/hummerrisk/hmr-k8s:v1.0.0        "/deployments/run-ja…"   k8s                 7 minutes ago       Up 6 minutes (healthy)   0.0.0.0:9500->9500/tcp, :::9500->9500/tcp
        hmr-mysql           registry.cn-beijing.aliyuncs.com/hummerrisk/mysql:8.0.32          "docker-entrypoint.s…"   mysql               7 minutes ago       Up 7 minutes (healthy)   3306/tcp, 33060/tcp
        hmr-nacos           registry.cn-beijing.aliyuncs.com/hummerrisk/nacos-server:v2.2.0   "bin/docker-startup.…"   nacos               7 minutes ago       Up 6 minutes (healthy)   0.0.0.0:8848->8848/tcp, :::8848->8848/tcp, 0.0.0.0:9848->9848/tcp, :::9848->9848/tcp
        hmr-redis           registry.cn-beijing.aliyuncs.com/hummerrisk/redis:6.2.10-alpine   "docker-entrypoint.s…"   redis               7 minutes ago       Up 7 minutes (healthy)   6379/tcp
        hmr-system          registry.cn-beijing.aliyuncs.com/hummerrisk/hmr-system:v1.0.0     "/deployments/run-ja…"   system              7 minutes ago       Up 6 minutes (healthy)   0.0.0.0:8001->8001/tcp, :::8001->8001/tcp, 0.0.0.0:9300-9301->9300-9301/tcp, :::9300-9301->9300-9301/tcp
        hmr-ui              registry.cn-beijing.aliyuncs.com/hummerrisk/hmr-ui:v1.0.0         "/docker-entrypoint.…"   ui                  7 minutes ago       Up 6 minutes (healthy)   0.0.0.0:8111->80/tcp, :::8111->80/tcp
        ```

!!! warning "默认 web 登录账户: admin 密码：hummer"
