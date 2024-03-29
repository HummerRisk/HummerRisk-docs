# Aliyun ACK 删除保护检测

### 1.检查项说明
!!! info ""
    Aliyun ACK 集群开启删除保护，符合视为“合规”，否则视为“不合规”。

### 2.处置方案
!!! info ""
    1. 前往阿里云云控制台，调整 ACK 集群。
    2. 阿里云容器服务Kubernetes版（Alibaba Cloud Container Service for Kubernetes，简称容器服务ACK）是全球首批通过Kubernetes一致性认证的服务平台，提供高性能的容器应用管理服务，支持企业级Kubernetes容器化应用的生命周期管理，让您轻松高效地在云端运行Kubernetes容器化应用。
        * 集群
            * 集群指容器运行所需要的云资源组合，关联了若干服务器节点、负载均衡、专有网络等云资源。
            * ACK支持的集群类型如下表1。
        * 节点
            * 一台服务器（可以是虚拟机实例或者物理服务器）已经安装了Docker Engine，可以用于部署和管理容器。容器服务ACK的Agent程序会被安装到节点上并注册到一个集群上。集群中的节点数量可以伸缩。
        * 节点池
            * 节点池是集群中全都具有相同配置的一组节点，节点池可以包含一个或多个节点。
            * ACK节点池类型分为节点池和托管节点池。
        * 专有网络VPC
            * 专有网络VPC是您自己独有的云上私有网络。您可以完全掌控自己的专有网络，例如选择IP地址范围、配置路由表和网关等，您可以在自己定义的专有网络中使用阿里云资源如云服务器、云数据库RDS版和负载均衡等。
        * 安全组
            * 安全组是一种虚拟防火墙，具备状态检测和数据包过滤能力，用于在云端划分安全域。安全组是一个逻辑上的分组，由同一地域内具有相同安全保护需求并相互信任的实例组成。
        * 应用目录
            * 应用目录功能集成了Helm，提供了Helm的相关功能，并进行了相关功能扩展，例如提供图形化界面。
        * 编排模板
            * 编排模板是一种保存Kubernetes YAML格式编排文件的方式。
        * Knative
            * Knative是基于Kubernetes的Serverless框架。其目标是制定云原生、跨平台的Serverless编排标准。
        * Kubernetes
            * Kubernetes是一个开源平台，具有可移植性和可扩展性，用于管理容器化的工作负载和服务，简化了声明式配置和自动化。
        * 容器（Container）
            * 打包应用及其运行依赖环境的技术，一个节点可运行多个容器。
        * 镜像（Image）
            * 容器镜像是容器应用打包的标准格式，封装了应用程序及其所有软件依赖的二进制数据。在部署容器化应用时可以指定镜像，镜像可以来自于Docker Hub，阿里云镜像服务，或者用户的私有镜像仓库。镜像ID可以由镜像所在仓库URI和镜像Tag（默认为latest）唯一确认。
        * 镜像仓库（Image Registry）
            * 容器镜像仓库是一种存储库，用于存储Kubernetes和基于容器应用开发的容器镜像。
        * 管理节点（Master Node）
            * 管理节点是Kubernetes集群的管理者，运行着的服务包括kube-apiserver、kube-scheduler、kube-controller-manager、etcd组件，和容器网络相关的组件。
        * 工作节点（Worker Node）
            * 工作节点是Kubernetes集群中承担工作负载的节点，可以是虚拟机也可以是物理机。工作节点承担实际的Pod调度以及与管理节点的通信等。一个工作节点上的服务包括Docker运行时环境、kubelet、Kube-Proxy以及其它一些可选的组件。
        * 命名空间（Namespace）
            * 命名空间为Kubernetes集群提供虚拟的隔离作用。Kubernetes集群初始有3个命名空间，分别是默认命名空间default、系统命名空间kube-system和kube-public，除此以外，管理员可以创建新的命名空间以满足需求。
        * 容器组（Pod）
            * Pod是Kubernetes部署应用或服务的最小的基本单位。一个Pod封装多个应用容器（也可以只有一个容器）、存储资源、一个独立的网络IP以及管理控制容器运行方式的策略选项。
        * 副本控制器（Replication Controller，RC）
            * RC确保任何时候Kubernetes集群中有指定数量的Pod副本在运行。通过监控运行中的Pod来保证集群中运行指定数目的Pod副本。指定的数目可以是多个也可以是1个；少于指定数目，RC就会启动运行新的Pod副本；多于指定数目，RC就会终止多余的Pod副本。
        * 副本集（ReplicaSet，RS）
            * ReplicaSet（RS）是RC的升级版本，唯一区别是对选择器的支持，RS能支持更多种类的匹配模式。副本集对象一般不单独使用，而是作为Deployment的理想状态参数使用。
        * 标签（Label）
            * Labels的实质是附着在资源对象上的一系列Key/Value键值对，用于指定对用户有意义的对象的属性，标签对内核系统是没有直接意义的。标签可以在创建一个对象的时候直接赋予，也可以在后期随时修改，每一个对象可以拥有多个标签，但key值必须唯一。
        * 服务（Service）
            * Service是Kubernetes的基本操作单元，是真实应用服务的抽象，每一个服务后面都有很多对应的容器来提供支持，通过Kube-Proxy的ports和服务selector决定服务请求传递给后端的容器，对外表现为一个单一访问接口。
        * 路由（Ingress）
            * Ingress是授权入站连接到达集群服务的规则集合。您可以通过Ingress配置提供外部可访问的URL、负载均衡、SSL、基于名称的虚拟主机等。通过POST Ingress资源到API Server的方式来请求Ingress。Ingress Controller负责实现Ingress，通常使用负载均衡器，它还可以配置边界路由和其他前端，这有助于以高可用的方式处理流量。
        * 配置项（ConfigMap）
            * 配置项可用于存储细粒度信息如单个属性，或粗粒度信息如整个配置文件或JSON对象。您可以使用配置项保存不需要加密的配置信息和配置文件。
        * 保密字典（Secret）
            * 保密字典用于存储在Kubernetes集群中使用一些敏感的配置，例如密码、证书等信息。
        * 卷（Volume）
            * 和Docker的存储卷有些类似，Docker的存储卷作用范围为一个容器，而Kubernetes的存储卷的生命周期和作用范围是一个Pod。每个Pod中声明的存储卷由Pod中的所有容器共享。
        * 存储卷（Persistent Volume，PV）
            * PV是集群内的存储资源，类似节点是集群资源一样。PV独立于Pod的生命周期，可根据不同的StorageClass类型创建不同类型的PV。
        * 存储卷声明（Persistent Volume Claim，PVC）
            * PVC是资源的使用者。类似Pod消耗节点资源一样，而PVC消耗PV资源。
        * 存储类（StorageClass）
            * 存储类可以实现动态供应存储卷。通过动态存储卷，Kubernetes将能够按照用户的需要，自动创建其所需的存储。
        * 弹性伸缩（Autoscaling）
            * 弹性伸缩是根据业务需求和策略，经济地自动调整弹性计算资源的管理服务。典型的场景包含在线业务弹性、大规模计算训练、深度学习GPU或共享GPU的训练与推理、定时周期性负载变化等。
        * 可观测性（Observability）
            * Kubernetes可观测性体系包含监控和日志两部分，监控可以帮助开发者查看系统的运行状态，而日志可以协助问题的排查和诊断。
        * Helm
            * Helm是Kubernetes包管理平台。Helm将一个应用的相关资源组织成为Charts，然后通过Charts管理程序包。
        * 节点亲和性（nodeAffinity）
            * 节点亲和性指通过Worker节点的Label标签控制Pod部署在特定的节点上。
        * 污点（Taints）
            * 污点和节点亲和性相反，它使节点能够排斥一类特定的Pod。
        * 容忍（Tolerations）
            * 应用于Pod上，允许（但并不要求）Pod调度到带有与之匹配的污点的节点上。
        * 应用亲和性（podAffinity）
            * 应用亲和性决定应用Pod可以和特定Pod部署在同一拓扑域。例如，对于相互通信的服务，可通过应用亲和性调度，将其部署到同一拓扑域（例如同一个主机）中，以减少它们之间的网络延迟。
        * 应用反亲和性（podAntiAffinity）
            * 应用反亲和性决定应用Pod不与特性Pod部署在同一拓扑域。例如，将一个服务的Pod分散部署到不同的拓扑域（例如不同主机）中，以提高服务本身的稳定性。
        * 服务网格（Istio）
            * Istio是一个提供连接、保护、控制以及观测服务的开放平台。阿里云服务网格提供一个全托管式的服务网格平台，兼容社区Istio开源服务网格，用于简化服务的治理，包括服务调用之间的流量路由与拆分管理、服务间通信的认证安全以及网格可观测性能力。

|   集群类型    |   描述    | 
|:-------------:|:-------:|
|    Pro托管集群    |   ACK Pro托管集群是在ACK标准托管版基础上针对企业大规模生产环境进一步增强了可靠性、安全性，并且提供可赔付的SLA的Kubernetes集群。   |
|    标准托管集群    |   只需创建节点，控制面板由容器服务创建并托管。具备简单、低成本、高可用、无需运维管理Kubernetes集群控制面板的特点。   |
|    专有集群    |   需要创建3个Master（高可用）节点及若干Worker节点，可对集群基础设施进行更细粒度的控制，需要自行规划、维护、升级服务器集群。   |
|    异构计算集群    |   ACK异构计算集群，是阿里云推出的支持英伟达GPU，含光NPU等异构节点，并且可以与传统CPU节点混合部署的集群，无需关心驱动的安装和管理，支持主流的AI计算框架，并且支持GPU和NPU的多容器共享和隔离。   |
|    安全沙箱集群    |   创建一个以弹性裸金属（神龙）实例为工作节点的集群，神龙服务器为您提供超高性能容器实例，适合高负载、高带宽需求的业务场景。   |
|    加密计算集群    |   创建一个基于Intel SGX加密计算的托管集群，可以保护您的敏感代码和数据，适合隐私数据保护、区块链、密钥、知识产权、生信基因计算等场景。   |
|    边缘集群    |   边缘托管版是针对边缘计算场景推出的云边一体化协同托管方案。边缘托管集群采用非侵入方式增强，提供边缘自治、边缘单元、边缘流量管理、原生运维API支持等能力，以原生方式支持边缘计算场景下的应用统一生命周期管理和统一资源调度。   |
|    ASK集群    |   无需创建和管理Master节点及Worker节点的Serverless集群，即可通过控制台或者命令配置容器实例的资源、指明应用容器镜像以及对外服务的方式，直接启动应用程序。   |
|    注册集群    |   注册集群是用于将本地数据中心Kubernetes集群或其他云厂商Kubernetes集群接入ACK服务平台统一管理的集群形态。   |


### 3.操作步骤
!!! info ""
   1. 使用阿里云账号登录控制台。
   2. 通过导航菜单进入服务控制台。https://cs.console.aliyun.com/。
   3. 找到相关的资源，进入管理菜单进行设置。

### 4.帮助资源
!!! info ""
    - https://help.aliyun.com/document_detail/128160.html
