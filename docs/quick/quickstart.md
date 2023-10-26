
## 1 一键部署
<script async id="asciicast-gGGWL035bwglpe3vmZ9F63pji" src="https://asciinema.org/a/gGGWL035bwglpe3vmZ9F63pji.js"></script>

!!! tip "3分钟快速一键部署"
    1. 部署服务器要求
        - 操作系统要求：任何支持 Docker 的 Linux x64
        - CPU内存要求：最低要求 4C8G，推荐 8C16G
        - 部署目录空间（默认/opt目录）要求： 50G
        - 网络要求：可访问互联网（如遇内网环境，理论上除公有云安全检测、Github源码检测外，其他功能可照常使用）
    2. 执行以下脚本进行一键安装：
        全球:
        ``` bash linenums="1"
        # 下载安装包
        wget https://github.com/HummerRisk/HummerRisk/releases/download/${hummerrisk_version}/hummerrisk-installer-${hummerrisk_version}.tar.gz
        ```

        中国大陆:
        ``` bash linenums="1"
        wget https://download.hummerrisk.com/HummerRisk/HummerRisk/releases/download/${hummerrisk_version}/hummerrisk-installer-${hummerrisk_version}.tar.gz
        ```

        解压安装包
        ``` bash linenums="1"
        tar -xf hummerrisk-installer-${hummerrisk_version}.tar.gz
        cd hummerrisk-installer-${hummerrisk_version}
        ```

        ``` bash linenums="1"
        # 安装
        bash install.sh
        
        # 启动
        hrctl start
        
        # 安装完成后默认配置文件在 /opt/hummerrisk/config/install.conf
        ```
    3. HummerRisk 是一款 B/S 架构的产品，即浏览器/服务器结构，在服务器安装完成后，客户端通过浏览器访问以下地址，即可开始使用。
        - http://目标服务器 IP 地址：服务运行端口，例如：http: 82.157.130.20:80（默认端口为80，用户可在安装时自定义）
        - 使用默认用户名 admin 密码 hummer 进行登录。

## 2 模块介绍

!!! abstract "进入 HummerRisk 主界面后可以看到界面左侧导航栏，有【首页】【混合云安全】【云原生安全】【检测管理】【系统设置】五大模块"
![模块介绍](../img/quickstart/HummerRisk-module.png){ width="75%" }

<!-- !!! abstract "【首页】【混合云安全】【云原生安全】【检测管理】【系统设置】五大模块的主要功能与作用"

!!! tip "1. 首页"
    - 包含面板、总览、分析、活动记录。
    - 主要作用是快速进入场景、集中展示和分析检测数据、记录操作的日志。
![首页](../img/quickstart/task1.png){ width="95%" }

!!! tip "2. 混合云安全"
    - 包含资源态势、多云检测、漏洞检测、合规报告、操作审计等功能。
    - 主要作用是持续检测和记录评估、审计和评价您的云资源配置，帮助用户快速完成合规性审计、安全性分析、变更管理和操作故障排除。
![混合云安全](../img/quickstart/img_5.png){ width="95%" }

!!! tip "3. 云原生安全"
    - 包含资源态势、主机检测、K8s 检测、部署检测、镜像检测、源码检测、文件检测、SBOM 管理等功能。
    - 主要作用是在整个开发生命周期提供云原生安全和合规性检测服务，深入探究漏洞详情，简单便捷的进行安全性分析，修正漏洞并形成最佳实践。
![云原生安全](../img/quickstart/sbom_analyze.png){ width="95%" }

!!! tip "4. 检测管理"
    - 包含检测规则和检测结果功能。
    - 主要作用是统一汇总所有模块的检测规则和执行检测后获取的检测结果，使用户可以快速便捷的在统一入口查看和操作。
![检测管理](../img/quickstart/img_3.png){ width="95%" }

!!! tip "5. 系统设置"
    包含系统设置（用户设置、参数设置、消息通知、代理设置、站内消息、系统参数、关于等）、个人设置等功能。
![系统设置](../img/quickstart/img_4.png){ width="95%" } -->

## 3 快速上手

### 3.1 场景一：混合云安全
[![快速入门1](../img/vedio/quickstart1.png){ width="380"}](https://www.bilibili.com/video/BV1g84y1b79N/?vd_source=40cffdce443e3b05aff80ddde424f0c3)
#### 3.1.1 绑定账号

!!! abstract "添加/编辑云账号"
    - 进入云账号设置页面，首先需要绑定多云的账号信息（Access Key ID / Access Key Secret）。
    - 点击左上角「创建云账号」按钮，可以添加云账号。
    - 通过对应的云平台，获取账号信息（一般为AK/SK），填写信息并绑定，自动获取区域和认证等信息。
    - 需要注意在云平台赋予相应资源的 IAM 策略信息。
    - 更详细的账号配置操作请参考 [多云检测](../user/account.md)
![云账号](../img/quickstart/img_7.png){ width="95%" }

!!! abstract ""
    - 绑定完成后系统会自动校验账号的状态，状态显示为『有效』时即为绑定成功。
    - 点击账号列表中操作按钮的第三个「编辑」，对已绑定的账号进行编辑。
![云账号](../img/quickstart/img_6.png){ width="95%" }

!!! abstract "云账号调参"
    - 因为检测规则的参数可以灵活配置，不同的云账号可以有不同的安全合规标准，所以在此页面用户可以根据自身需求自定义规则的参数与任意区域。
        - 通过账号列表第二个调参按钮，打开云账号调参页面。
        - 保存参数后，执行检测将优先执行当前调参内容，而且在调参页面可以快速执行某一规则的某些区域快速检测。
        - *注：不设置调参内容不影响检测，检测内容为内置默认参数和所有待检测区域*
![云账号](../img/quickstart/img_9.png){ width="95%" }

#### 3.1.2 执行检测

!!! abstract "基于规则组进行检测"
    - 多云检测基于规则组进行场景检测的，例如检测 Aliyun ECS 最佳安全实践，将检测此规则组下一系列规则，达到覆盖场景的目的。    
    - 有两种方式可以快速开始检测：
        - 通过云账号列表第一个「一键检测」按钮选取多个规则组执行一键检测。
        - 在规则组页面，选择希望执行的规则，选取某个云账号执行快速检测。
![云账号](../img/quickstart/img_49.png){ width="95%" }
![云账号](../img/quickstart/img_10.png){ width="95%" }

!!! abstract "云资源检测结果"
    - 在点击上述一键检测后，将自动跳转云资源检测结果页面，检测结果将会显示正在执行。
    - 等待检测执行完毕后获得检测结果的安全合规信息与优化建议。
![云账号](../img/quickstart/img_11.png){ width="95%" }

#### 3.1.3 查看报告

!!! abstract "云资源合规报告"
    - 待云资源检测完毕后，根据检测结果生成合规报告，用户可查看和下载合规报告。   
    - 详细的合规报告相关操作，请参考 [合规报告](../user/report.md)
![云账号](../img/quickstart/img_13.png){ width="95%" }


#### 3.1.4 分析和审计

!!! abstract "操作审计"
    - 云操作审计，帮助您监控并记录多云账号的活动，包括通过云控制台、OpenAPI、开发者工具对云上产品和服务的访问和使用行为。
    - 用户可以查看这些行为事件，然后进行行为分析、安全分析、资源变更行为追踪和行为合规性审计等操作。
![云账号](../img/quickstart/img_15.png){ width="95%" }

!!! abstract "资源态势"
    - 根据绑定混合云账号信息，即可同步获取云资源汇总信息。
    - 执行检测后，可以自动关联云资源态势信息，可以查看到具体哪些资源具有安全合规风险。
![云账号](../img/quickstart/img_16.png){ width="95%" }


### 3.2 场景二：云原生安全
[![快速入门2](../img/vedio/quickstart2.png){ width="380"}](https://www.bilibili.com/video/BV1yA411D7kc/)
#### 3.2.1 前置 K8s 配置

!!! warning "K8s 检测前置条件"

!!! info "使用云原生 K8s 安全检测任务前需在 k8s 集群上安装 tirvy-operator"
    ```shell
    # 1.添加 chart 仓库
    helm repo add hummer https://registry.hummercloud.com/repository/charts

    # 2.更新仓库源
    helm repo update
    
    # 3.开始安装, 可以自定义应用名称和NameSpace
    helm install trivy-operator hummer/trivy-operator \
    --namespace trivy-system \
    --set image.registry="registry.cn-beijing.aliyuncs.com" \
    --set image.repository="hummerrisk/trivy-operator" \
    --set trivy.image.registry="registry.cn-beijing.aliyuncs.com" \
    --set trivy.image.repository="hummerrisk/trivy" \
    --set trivy.dbRepository="reg.hummercloud.com" \
    --set trivy.dbRepository="trivy/trivy-db" \
    --set trivy.javaDbRegistry="reg.hummercloud.com" \
    --set trivy.javaDbRepository="trivy/trivy-java-db" \
    --set nodeCollector.registry="reg.hummercloud.com" \
    --set nodeCollector.repository="hummerrisk/node-collector" \
    --set trivy.dbRepositoryInsecure="true" \
    --set trivy.ignoreUnfixed=true \
    --set trivy.offlineScan=true \
    --create-namespace
    
    # 4.检测operator是否启动成功
    kubectl get pod -A|grep trivy-operator
    trivy-system   trivy-operator-69f99f79c4-lvzvs           1/1     Running            0          118s
    ```

!!! question "K8s 账号添加校验"
    1. 确定部署 hummerrisk 的主机可以访问该 k8s 集群的 6443 端口，需要网络可达、端口可以通，如果不通可以检查防火墙;
    2. 确定提供的 k8s Token 有足够的权限，hummerrisk 会通过该 Token 调用 k8s apiserver 的 api
    3. k8s token 权限可以参考如下
    
    创建 ServiceAccount
    ```yaml
    cat <<EOF > hummer-sa.yaml
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: hummer
      namespace: kube-system
    EOF
    ```
    创建 clusterrolebinding
    ```yaml
    cat <<EOF > hummer-clusterrolebinding.yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: hummer-user
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: cluster-admin
    subjects:
      - kind: ServiceAccount
      name: hummer
      namespace: kube-system
    EOF
    ```
    创建资源
    ```bash
    kubectl create -f ./hummer-sa.yaml
    kubectl create -f ./hummer-clusterrolebinding.yaml
    ```

!!! question "获取 token"
    ```bash
    # 获取 token
    kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep hummer | awk '{print $1}') | grep token: | awk '{print $2}'
    ```

#### 3.2.2 检测 K8s 风险

!!! abstract "Kuberbetes 配置"      
    - K8s 配置与云原生 K8s 环境安全检测功能，绑定 K8s Url 与 Token 信息即可进行安全检测，并生成安全漏洞结果。
    - K8s 平台环境有四种：分别是 Kubernetes、Rancher、OpenShift、KubeSphere。
![K8s 检测](../img/quickstart/img_42.png){ width="95%" }
![K8s 检测](../img/quickstart/img_43.png){ width="95%" }

!!! abstract "K8s 检测结果"      
    - K8s 检测结果，主要展示 K8s 环境的漏洞安全信息和配置审计风险信息。
![K8s 检测](../img/quickstart/img_44.png){ width="95%" }
![K8s 检测](../img/quickstart/img_45.png){ width="95%" }
![K8s 检测](../img/quickstart/img_46.png){ width="95%" }

!!! abstract "K8s 资源态势"
    - 资源态势功能，绑定 K8s 环境信息，即可获取 K8s 的 Namespace、Pod、Node、Deployment、Service 等20余种资源信息。
    - 绑定完 K8s 账号是可以自动获取资源态势信息的。
    - 同时，也可以在同步日志页面手动获取资源态势信息。
    - 手动创建同步任务，即可查看同步资源数与同步状态。
![K8s 检测](../img/quickstart/img_47.png){ width="95%" }


#### 3.2.3 检测部署文件

!!! abstract "K8s 部署配置"
    - K8s 部署检测功能，输入 K8s 部署配置 YAML 文件，即可进行部署检测，输出部署配置检测结果。
![部署检测](../img/quickstart/img_25.png){ width="95%" }

!!! abstract "部署检测结果"
    - 针对部署文件（YAML），一键执行检测后展示结果。
    - 用户可以根据检测结果的提示，修改对应的 YAML 文件内容，达到最佳要求。
![部署检测](../img/quickstart/img_26.png){ width="95%" }
![部署检测](../img/quickstart/img_27.png){ width="95%" }
![部署检测](../img/quickstart/img_28.png){ width="95%" }

#### 3.2.4 检测镜像风险

!!! abstract "镜像仓库"      
    - 用户可以绑定镜像仓库，之后检测的镜像可以从绑定的镜像仓库中查找和获取。
    - 镜像仓库类型：目前支持四种类型 harbor、dockerhub、nexus 和 other。如果选择 other 不会同步镜像，只做登录验证。
    - 镜像仓库中同步的镜像列表，可以直接执行检测，直接跳转到检测结果页面。（这个过程也会默认在镜像管理中新建一条数据）
![镜像检测](../img/quickstart/img_29.png){ width="95%" }
![镜像检测](../img/quickstart/img_30.png){ width="95%" }

!!! abstract "镜像管理"      
    - 在镜像管理页面，我们可以对具体需要检测的镜像进行管理。
    - 镜像列表中会显示出已经创建成功的待检测镜像，列表会显示出镜像的名称、状态、地址等信息。   
    - 通过校验的镜像，镜像状态会显示为 [有效]，可以对其执行检测。
    - 镜像可以是公有镜像，也可以是私有镜像。可以手动填写镜像地址，上传镜像tar包，也可以从镜像仓库中选择同步的镜像。
    - 在镜像列表中，选择希望执行检测的镜像，点击列表后的[检测]按钮，确认后系统就会对该镜像进行检测。
![镜像检测](../img/quickstart/img_31.png){ width="95%" }
![镜像检测](../img/quickstart/img_32.png){ width="95%" }

!!! abstract "镜像检测结果"      
    - 镜像检测结果列表，展示镜像的漏洞信息。
![镜像检测](../img/quickstart/img_33.png){ width="95%" }
![镜像检测](../img/quickstart/img_34.png){ width="95%" }


#### 3.2.5 检测主机风险

!!! abstract "添加统一凭据"      
    - 用户可以在统一凭据页面将常用的或重复的主机认证进行保存，这样在创建主机的过程中可以直接绑定，方便操作防止重复拷贝。
    - 新建、修改主机信息时，可灵活绑定凭据，统一凭据有三种类型，密码、密钥字符串、密钥文件。
![主机检测](../img/quickstart/img_20.png){ width="95%" }

!!! abstract "添加主机 & 执行检测"      
    - 主机管理列表页面提供了对主机分组、主机的创建、删除、编辑、查找、校验、检测等操作。
    - 创建主机时，可以为多个主机批量添加统一凭据，也可以分别为主机添加凭据。
    - 目前可针对 Linux/Windows 操作系统类型的主机。

![主机检测](../img/quickstart/img_22.png){ width="95%" }
![主机检测](../img/quickstart/img_21.png){ width="95%" }

!!! abstract "主机检测结果"      
    - 在主机管理界面，选中待检测主机，一键执行后将自动跳转到主机检测结果页面。
    - 主检测结果页面将只会保留最新的一次检测结果，历史检测结果请到主机检测历史记录中查看。
    - 点击检测状态按钮，可以查看检测结果日志详情。
![主机检测](../img/quickstart/img_23.png){ width="95%" }
![主机检测](../img/quickstart/img_24.png){ width="95%" }


#### 3.2.6 检测项目风险

!!! abstract "项目源码配置"      
    - 在源码检测部分，通过对源码依赖的扫描，发现项目中存在的漏洞。
    - 目前绑定仓库支持两种类型：GitHub 和 GitLab 。
    - Token 的获取：首先私有仓库需要填入Token，公有仓库无需填写Token。
![源码检测](../img/quickstart/img_35.png){ width="95%" }
![源码检测](../img/quickstart/img_36.png){ width="95%" }

!!! abstract "源码检测结果"      
    - 源码检测，可以针对 branch 分支、可以针对 tag 标签、可以针对 commit 某次提交。
    - 源码检测结果列表，展示源码项目依赖的漏洞信息。
![源码检测](../img/quickstart/img_37.png){ width="95%" }
![源码检测](../img/quickstart/img_38.png){ width="95%" }

!!! abstract "依赖文件管理"      
    - 对于源码检测的补充，如果只想检测源码项目的依赖文件检测，可以上传对应的文件进行检测。
    - 依赖文件可以是单个文件，也可以是文件夹的压缩文件。
    - 依赖文件的格式，例如 java 的 pom.xml，vue 的 package.json 或 yarn.lock 等。
![文件检测](../img/quickstart/img_39.png){ width="95%" }
![文件检测](../img/quickstart/img_48.png){ width="95%" }

!!! abstract "依赖文件检测结果"      
    - 依赖文件检测结果列表，展示项目依赖的漏洞信息。
![文件检测](../img/quickstart/img_40.png){ width="95%" }
![文件检测](../img/quickstart/img_41.png){ width="95%" }

## 4 常用信息

!!! info ""
    - [教学视频](../video/video.md)
    - [常见问题](../question/cloud.md)
    - [功能手册](../user/process.md)
    - [开发文档](../develop/dev-manual.md)

!!! warning "默认 web 登录账户: admin 密码：hummer"
