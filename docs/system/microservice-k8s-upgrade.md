!!! warning "更新前请一定要做好数据库备份工作"

### 1.更新 hummerrisk
!!! info ""
    ``` bash
    # 更新某个配置项，例如修改 Service 类型为 NodePort
    helm upgrade hummerrisk hummerrisk/hummerrisk --set hummerrisk.serviceType=NodePort -ndev
    
    # 更新 hummerrisk
    helm upgrade --install -n hummer hummerrisk hummerrisk/hummerrisk [--version 0.3.3 ] [-f values.yaml]
    ```

### 2.常用可配置项
!!! info ""
    ```yaml linenums="1"
    全局配置:
        --set global.imageRegistry=""           # 设置镜像仓库地址
        --set global.imagePullPolicy="Always"   # 设置镜像拉取策略
        --set global.storageClass="nfs"         # 设置存储类
        --set hummerrisk.serviceType="NodePort" # 设置 service 类型，例如：CLusterIP/NodePort
        --set hummerrisk.replicas=2             # 设置 hummerrisk 副本数量
        --set hummerrisk.image.tag="v0.4.0"     # 设置 hummerrisk 版本
    trivy Server部分:
        --set trivyServer.trivyDBVersion="2022122008"  # 漏洞库版本
        --set trivyServer.servicePort=4975             # service 端口号
        --set trivyServer.serviceType=ClusterIP        # service 类型
    内部数据库部分:
        --set mysql.enabled=true                # 开启内部数据库，会在k8s集群启动一个MySQL
        --set mysql.rootPassword="password"     # 设置数据库密码
        --set mysql.persistence.enable=true     # 开启持久化存储
    外部数据库部分:
        --set externalMySQL.enabled=true        # 开启外部部数据库，会在k8s集群启动一个MySQL
        --set externalMySQL.host="192.168.10.100"     # 设置数据库地址，IP或者域名
        --set externalMySQL.port=true           # 设置数据库端口，默认 3306
        --set externalMySQL.username="root"     # 设置数据库用户名，默认 root
        --set externalMySQL.password="pass"     # 设置数据库密码
        --set externalMySQL.databases="hummerrisk"    # 设置数据库名称
    持久化存储配置:
        --set storage.logSize="20Gi"            # 设置hummerrisk日志存储卷大小
        --set storage.imageSize="30Gi"          # 设置hummerrisk镜像存储卷大小
        --set storage.fileSize="30Gi"           # 设置hummerrisk文件存储卷大小
        --set storage.dbSize="50Gi"             # 设置hummerrisk数据库存储卷大小，如果使用内部数据需要设置
    ingress配置:
        --set ingress.enabled=false             # ture 启用ingress，false 不启用 ingress
        --set ingress.hosts.host="hr.example.local" # 设置访问域名
    ```
