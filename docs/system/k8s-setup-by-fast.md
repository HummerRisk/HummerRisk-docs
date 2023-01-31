### Hummerrisk helm-chart
!!! warning "环境要求"
    - Kubernetes 1.20 +
    - Helm 3.0

### 1.快速安装

!!! info "1. 添加 helm 仓库源"
    ```bash
    helm repo add hummerrisk https://hummerrisk.github.io/helm-repo
    ```

!!! info "2. 更新 helm 仓库"
    ``` bash
    helm repo list
    helm repo update
    ```

!!! info "3. 安装 hummerrisk"
    ``` bash
    # 查询 hummerrisk 安装包
    helm search repo hummerrisk

    # 安装
    helm install hummerrisk hummerrisk/hummerrisk -n hummer --create-namespace \
    --set hummerrisk.serviceType="NodePort" \
    --set trivyServer.serviceType="NodePort" \
    --set trivyServer.servicePort=4975 \
    --set global.storageClass="<StorageClass Name>"
    ```

!!! info "4. 使用外部的 MySQL 安装 hummerrisk"
    ``` bash
    # 查询 hummerrisk 安装包
    helm search repo hummerrisk

    # 使用 --set 设置外部数据库配置信息，存储信息
    helm install hummerrisk hummerrisk/hummerrisk -n hummer --create-namespace  \
    --set hummerrisk.serviceType="NodePort" \
    --set trivyServer.serviceType="NodePort" \
    --set trivyServer.servicePort=4975 \
    --set global.storageClass="cfs"  \                # 你的存储类名称
    --set storage.accessModes={"ReadWriteOnce"}  \    # 存储类的访问模式，ReadWriteOnce、ReadWriteMany等
    --set mysql.enabled=false   \                     # 关闭创建 MySQL 实例
    --set externalMySQL.enabled=true  \               # 开启使用外部 MySQL 数据库
    --set externalMySQL.host="172.21.0.7"   \
    --set externalMySQL.username="root"   \
    --set externalMySQL.port=3306   \
    --set externalMySQL.password="Your password"  \
    --set externalMySQL.databases="hummerrisk"
    ```
 
### 2.自定义配置参数说明
通过修改 vales.yaml 文件或者 helm --set 可以修改 HummerRisk 安装参数，例如：端口、存储信息等，以下为默认配置项，可根据实际环境修改。

!!! info "通过 --set 配置参数"
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
    --set mysql.enabled=true                # 开启后会在 k8s 集群启动一个 MySQL
    --set mysql.rootPassword="password"     # 设置数据库密码
    --set mysql.persistence.enable=true     # 开启持久化存储
    外部数据库部分:
    --set externalMySQL.enabled=true        # 开启后直接连接外部数据库
    --set externalMySQL.host="192.168.10.100"     # 设置数据库地址，IP 或者域名
    --set externalMySQL.port=3306           # 设置数据库端口，默认 3306
    --set externalMySQL.username="root"     # 设置数据库用户名，默认 root
    --set externalMySQL.password="pass"     # 设置数据库密码
    --set externalMySQL.databases="hummerrisk"    # 设置数据库名称
    持久化存储配置:
    --set storage.logSize="20Gi"            # 设置 hummerrisk 日志存储卷大小
    --set storage.imageSize="30Gi"          # 设置 hummerrisk 镜像存储卷大小
    --set storage.fileSize="30Gi"           # 设置 hummerrisk 文件存储卷大小
    --set storage.dbSize="50Gi"             # 设置 hummerrisk 数据库存储卷大小，如果使用内部数据需要设置
    ingress配置:
    --set ingress.enabled=false             # ture 启用 ingress，false 不启用 ingress
    --set ingress.hosts.host="hr.example.local" # 设置访问域名
    ```

!!! info "通过 value.yaml 配置参数"
    ```yaml linenums="1"
    # 全局配置
    global:
      imageRegistry: "registry.cn-beijing.aliyuncs.com"
      ## E.g.
      ## imagePullSecrets:
      ##   - myRegistryKeySecretName
      ##
      imageTag: v0.3.1
      imagePullSecrets: []
      imagePullPolicy: Always
      ## 指定存储类
      storageClass: "nfs"
    
    # hummerrisk 配置项
    hummerrisk:
      image:
        repository: nginx
        pullPolicy: IfNotPresent
        # Overrides the image tag whose default is the chart appVersion.
        tag: v0.4.0
      replicas: 1
      # servicePort is the HTTP listener port for the webserver
      servicePort: 80
      serviceType: ClusterIP
      sessionAffinity: ClientIP
    
    # 外部数据库信息
    externalMySQL:
      enabled: false
      host: mysql.local
      port: 3306
      username: root
      password: ""
      database: ""

    #  trivy Server 配置
    trivyServer:
      trivyDBVersion: "2022122008"
      servicePort: 4975
      serviceType: ClusterIP

    # 存储卷配置
    storage:
      logSize: 20Gi
      imageSize: 30Gi
      fileSize: 10Gi
      dbSize: 50Gi
      accessModes:
        - ReadWriteMany
    ```
