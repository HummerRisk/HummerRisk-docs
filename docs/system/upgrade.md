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
        # 例如：升级到指定版本 v0.7.0 
        hrctl upgrade v0.7.0
        ```

    !!! question "如果服务器网络环境不佳，可尝试手动在线升级"
        ``` bash linenums="1"
        cd /tmp
        # 指定需要升级的目标版本号
        version=v0.7.0
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
        v0.7.0
        [root@hummerrisk tmp]# hrctl status
            Name                  Command                  State                         Ports
        ---------------------------------------------------------------------------------------------------------
        hummer_mysql   docker-entrypoint.sh --def ...   Up (healthy)   3306/tcp, 33060/tcp
        hummer_risk    /deployments/run-java.sh         Up (healthy)   0.0.0.0:80->8088/tcp, 8778/tcp, 9779/tcp
        trivy_server   trivy server --skip-update ...   Up (healthy)   0.0.0.0:4975->4975/tcp, 8778/tcp, 9779/tcp
        ```

!!! warning "默认 web 登录账户: admin 密码：hummer"
