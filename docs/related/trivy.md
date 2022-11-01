
### Trivy

!!! info "项目地址"
    Github 项目地址：https://github.com/aquasecurity/trivy
 
#### 一、Trivy 是什么

!!! abstract "Trivy 是什么"
    - Trivy（tri 发音为 trigger，vy 发音为 envy）是一个简单而全面的漏洞/错误配置扫描器，用于容器和其他工件。 
    - 软件漏洞是软件或操作系统中存在的故障、缺陷或弱点。 
    - Trivy 检测操作系统包（Alpine、RHEL、CentOS 等）和特定语言包（Bundler、Composer、npm、yarn 等）的漏洞。 
    - 此外，Trivy 会扫描基础设施即代码 (IaC) 文件，例如 Terraform 和 Kubernetes，以检测使您的部署面临攻击风险的潜在配置问题。 
    - Trivy 易于使用。 只需安装二进制文件，您就可以开始扫描了。 扫描所需要做的就是指定一个目标，例如容器的图像名称。

![Trivy](../img/question/trivy1.png){ width="95%" }

!!! abstract "Trivy 类型"
    1. Trivy 检测两种类型的安全问题 ：
        * 漏洞
        * 配置错误
    2. Trivy 可以扫描三种不同的工件：
        * 容器镜像
        * 文件系统
        * Git存储库
    3. Trivy 可以在两种不同的模式下运行：
        * 独立
        * 客户端服务器
    4. 它旨在用于 CI。在推送到容器注册表或部署应用程序之前，您可以轻松扫描本地容器镜像和其他工件。

#### 二、Trivy 特征

!!! abstract "Trivy 特征"
    * 全面的漏洞检测
    * 操作系统包（Alpine、Red Hat Universal Base Image、Red Hat Enterprise Linux、CentOS、Oracle Linux、Debian、Ubuntu、Amazon Linux、openSUSE Leap、SUSE Enterprise Linux、Photon OS 和 Distroless）
    * 特定于语言的包（Bundler、Composer、Pipenv、Poetry、npm、yarn、Cargo、NuGet、Maven 和 Go）
    * 检测 IaC 错误配置
      * 各种各样的内置策略提供了开箱：
        * Kubernetes
        * 码头工人
        * 地形
        * 更多即将推出
      * 支持自定义策略
    * 简单的
    * 仅指定图像名称、包含 IaC 配置的目录或工件名称
    * 快速地
      * 第一次扫描将在 10 秒内完成（取决于您的网络）。随后的扫描将在几秒钟内完成。
      * 与在第一次运行时需要很长时间才能获取漏洞信息（约 10 分钟）并鼓励您维护持久漏洞数据库的其他扫描程序不同，Trivy 是无状态的，不需要维护或准备。
    * 简易安装
      * apt-get install,yum install并且brew install是可能的
      * 没有先决条件，如安装DB的，图书馆等
    * 高精确度
      * 特别是 Alpine Linux 和 RHEL/CentOS
      * 其他操作系统也高
    * 开发安全运营
      * 适用于Travis CI、CircleCI、Jenkins、GitLab CI 等 CI。
    * 支持多种格式
      * 容器镜像
        * 作为守护进程运行的 Docker Engine 中的本地镜像
        * Podman中暴露套接字的本地图像
        * Docker Registry 中的远程镜像，例如 Docker Hub、ECR、GCR 和 ACR
        * 存储在docker save/podman save格式文件中的 tar 存档
        * 符合OCI 图像格式的图像目录
      * 本地文件系统
      * 远程 git 仓库

#### 三、Trivy 安装

=== "Yum 源方式安装"
    !!! tip "Yum 源方式安装"
        ```bash
        $ sudo vim /etc/yum.repos.d/trivy.repo
        [trivy]
        name=Trivy repository
        baseurl=https://aquasecurity.github.io/trivy-repo/rpm/releases/$releasever/$basearch/
        gpgcheck=0
        enabled=1
        $ sudo yum -y update
        $ sudo yum -y install trivy
        ```

=== "rpm 方式安装"
    !!! tip "rpm 方式安装"
        ```bash
        rpm -ivh https://github.com/aquasecurity/trivy/releases/download/v0.19.2/trivy_0.19.2_Linux-64bit.rpm
        ```

=== "二进制方式安装"
    !!! tip "二进制方式安装"
        ```bash
        mkdir -p $GOPATH/src/github.com/aquasecurity
        cd $GOPATH/src/github.com/aquasecurity
        git clone --depth 1 --branch v0.19.2 https://github.com/aquasecurity/trivy
        cd trivy/cmd/trivy/
        export GO111MODULE=on
        go install
        ```

#### 四、容器镜像漏洞扫描
!!! tip "镜像扫描"
    ```bash
    # trivy image nginx:1.16 
    2021-08-16T19:15:48.528+0800    INFO    Detected OS: debian
    2021-08-16T19:15:48.528+0800    INFO    Detecting Debian vulnerabilities...
    2021-08-16T19:15:48.541+0800    INFO    Number of language-specific files: 1

    nginx:1.16 (debian 10.3)
    ========================
    Total: 207 (UNKNOWN: 0, LOW: 105, MEDIUM: 33, HIGH: 49, CRITICAL: 20)

    +-----------------+---------------------+----------+---------------------------+---------------------------+------------------------------------------------------------+
    |     LIBRARY     |  VULNERABILITY ID   | SEVERITY |     INSTALLED VERSION     |       FIXED VERSION       |                           TITLE                            |
    +-----------------+---------------------+----------+---------------------------+---------------------------+------------------------------------------------------------+
    | apt             | CVE-2020-27350      | MEDIUM   | 1.8.2                     | 1.8.2.2                   | apt: integer overflows and underflows                      |
    |                 |                     |          |                           |                           | while parsing .deb packages                                |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2020-27350                      |
    +                 +---------------------+          +                           +---------------------------+------------------------------------------------------------+
    |                 | CVE-2020-3810       |          |                           | 1.8.2.1                   | Missing input validation in                                |
    |                 |                     |          |                           |                           | the ar/tar implementations of                              |
    |                 |                     |          |                           |                           | APT before version 2.1.2...                                |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2020-3810                       |
    +                 +---------------------+----------+                           +---------------------------+------------------------------------------------------------+
    |                 | CVE-2011-3374       | LOW      |                           |                           | It was found that apt-key in apt,                          |
    |                 |                     |          |                           |                           | all versions, do not correctly...                          |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2011-3374                       |
    +-----------------+---------------------+          +---------------------------+---------------------------+------------------------------------------------------------+
    | bash            | CVE-2019-18276      |          | 5.0-4                     |                           | bash: when effective UID is not                            |
    |                 |                     |          |                           |                           | equal to its real UID the...                               |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2019-18276                      |
    +                 +---------------------+          +                           +---------------------------+------------------------------------------------------------+
    |                 | TEMP-0841856-B18BAF |          |                           |                           | -->security-tracker.debian.org/tracker/TEMP-0841856-B18BAF |
    +-----------------+---------------------+          +---------------------------+---------------------------+------------------------------------------------------------+
    | bsdutils        | CVE-2021-37600      |          | 2.33.1-0.1                |                           | util-linux: integer overflow                               |
    |                 |                     |          |                           |                           | can lead to buffer overflow                                |
    |                 |                     |          |                           |                           | in get_sem_elements() in                                   |
    |                 |                     |          |                           |                           | sys-utils/ipcutils.c...                                    |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2021-37600                      |
    +-----------------+---------------------+          +---------------------------+---------------------------+------------------------------------------------------------+
    | coreutils       | CVE-2016-2781       |          | 8.30-3                    |                           | coreutils: Non-privileged                                  |
    |                 |                     |          |                           |                           | session can escape to the                                  |
    |                 |                     |          |                           |                           | parent session in chroot                                   |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2016-2781                       |
    +                 +---------------------+          +                           +---------------------------+------------------------------------------------------------+
    |                 | CVE-2017-18018      |          |                           |                           | coreutils: race condition                                  |
    |                 |                     |          |                           |                           | vulnerability in chown and chgrp                           |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2017-18018                      |
    +-----------------+---------------------+          +---------------------------+---------------------------+------------------------------------------------------------+
    | fdisk           | CVE-2021-37600      |          | 2.33.1-0.1                |                           | util-linux: integer overflow                               |
    |                 |                     |          |                           |                           | can lead to buffer overflow                                |
    |                 |                     |          |                           |                           | in get_sem_elements() in                                   |
    |                 |                     |          |                           |                           | sys-utils/ipcutils.c...                                    |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2021-37600                      |
    +-----------------+---------------------+----------+---------------------------+---------------------------+------------------------------------------------------------+
    | gcc-8-base      | CVE-2018-12886      | HIGH     | 8.3.0-6                   |                           | gcc: spilling of stack                                     |
    |                 |                     |          |                           |                           | protection address in cfgexpand.c                          |
    |                 |                     |          |                           |                           | and function.c leads to...                                 |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2018-12886                      |
    +                 +---------------------+          +                           +---------------------------+------------------------------------------------------------+
    |                 | CVE-2019-15847      |          |                           |                           | gcc: POWER9 "DARN" RNG intrinsic                           |
    |                 |                     |          |                           |                           | produces repeated output                                   |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2019-15847                      |
    +-----------------+---------------------+----------+---------------------------+---------------------------+------------------------------------------------------------+
    | gpgv            | CVE-2019-14855      | LOW      | 2.2.12-1+deb10u1          |                           | gnupg2: OpenPGP Key Certification                          |
    |                 |                     |          |                           |                           | Forgeries with SHA-1                                       |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2019-14855                      |
    +-----------------+---------------------+----------+---------------------------+---------------------------+------------------------------------------------------------+
    | libapt-pkg5.0   | CVE-2020-27350      | MEDIUM   | 1.8.2                     | 1.8.2.2                   | apt: integer overflows and underflows                      |
    |                 |                     |          |                           |                           | while parsing .deb packages                                |
    |                 |                     |          |                           |                           | -->avd.aquasec.com/nvd/cve-2020-27350                      |
    +                 +---------------------+          +                           +---------------------------+------------------------------------------------------------+
    |                 | CVE-2020-3810       |          |                           | 1.8.2.1                   | Missing input validation in                                |
    |                 |                     |          |                           |                           | the ar/tar implementations of                              |
    |                 |                     |          |                           |                           | APT before version 2.1.2...                                |
    --More--
    ```

!!! info "漏洞等级"
    ```
    漏洞等级：
    * CRITICAL
    * HIGH 
    * MEDIUM 
    * LOW 
    * UNKNOWN
    ```

#### 五、文件系统漏洞扫描

!!! tip "扫描文件系统（例如主机、虚拟机镜像或解压缩的容器镜像文件系统）"
    ```bash
    # trivy fs /application/zookeeper/
    2021-08-16T19:23:19.322+0800    INFO    Number of language-specific files: 35
    2021-08-16T19:23:19.322+0800    INFO    Detecting jar vulnerabilities...
    lib/jetty-server-9.4.39.v20210325.jar (jar)
    ===========================================
    Total: 2 (UNKNOWN: 0, LOW: 1, MEDIUM: 1, HIGH: 0, CRITICAL: 0)
    +--------------------------------+------------------+----------+-------------------+------------------------+---------------------------------------+
    |            LIBRARY             | VULNERABILITY ID | SEVERITY | INSTALLED VERSION |     FIXED VERSION      |                 TITLE                 |
    +--------------------------------+------------------+----------+-------------------+------------------------+---------------------------------------+
    | org.eclipse.jetty:jetty-server | CVE-2019-10247   | MEDIUM   | 9.4.39.v20210325  |                        | jetty: error path                     |
    |                                |                  |          |                   |                        | information disclosure                |
    |                                |                  |          |                   |                        | -->avd.aquasec.com/nvd/cve-2019-10247 |
    +                                +------------------+----------+                   +------------------------+---------------------------------------+
    |                                | CVE-2021-34428   | LOW      |                   | 11.0.3, 10.0.3, 9.4.41 | jetty: SessionListener can            |
    |                                |                  |          |                   |                        | prevent a session from being          |
    |                                |                  |          |                   |                        | invalidated breaking logout           |
    |                                |                  |          |                   |                        | -->avd.aquasec.com/nvd/cve-2021-34428 |
    +--------------------------------+------------------+----------+-------------------+------------------------+---------------------------------------+
    lib/log4j-1.2.17.jar (jar)
    ==========================
    Total: 1 (UNKNOWN: 0, LOW: 0, MEDIUM: 0, HIGH: 0, CRITICAL: 1)
    +-------------+------------------+----------+-------------------+---------------+---------------------------------------+
    |   LIBRARY   | VULNERABILITY ID | SEVERITY | INSTALLED VERSION | FIXED VERSION |                 TITLE                 |
    +-------------+------------------+----------+-------------------+---------------+---------------------------------------+
    | log4j:log4j | CVE-2019-17571   | CRITICAL | 1.2.17            |               | log4j: deserialization of             |
    |             |                  |          |                   |               | untrusted data in SocketServer        |
    |             |                  |          |                   |               | -->avd.aquasec.com/nvd/cve-2019-17571 |
    +-------------+------------------+----------+-------------------+---------------+---------------------------------------+
    ```

#### 六、Git 存储库漏洞扫描

!!! tip "扫描您的远程 git 存储库"
    ```bash
    # trivy repo https://github.com/kubernetes/kubernetes.git
    Enumerating objects: 370096, done.
    Counting objects: 100% (370096/370096), done.
    Compressing objects: 100% (153736/153736), done.
    Total 370096 (delta 246795), reused 313878 (delta 202418), pack-reused 0
    2021-08-16T19:27:54.433+0800    INFO    Number of language-specific files: 31
    2021-08-16T19:27:54.434+0800    INFO    Detecting gomod vulnerabilities...
    cluster/addons/fluentd-elasticsearch/es-image/go.sum (gomod)
    ============================================================
    Total: 4 (UNKNOWN: 0, LOW: 0, MEDIUM: 1, HIGH: 3, CRITICAL: 0)
    +-----------------------------+------------------+----------+-----------------------------------+------------------------------------+---------------------------------------+
    |           LIBRARY           | VULNERABILITY ID | SEVERITY |         INSTALLED VERSION         |           FIXED VERSION            |                 TITLE                 |
    +-----------------------------+------------------+----------+-----------------------------------+------------------------------------+---------------------------------------+
    | github.com/dgrijalva/jwt-go | CVE-2020-26160   | HIGH     | 3.2.0+incompatible                |                                    | jwt-go: access restriction            |
    |                             |                  |          |                                   |                                    | bypass vulnerability                  |
    |                             |                  |          |                                   |                                    | -->avd.aquasec.com/nvd/cve-2020-26160 |
    +-----------------------------+------------------+          +-----------------------------------+------------------------------------+---------------------------------------+
    | github.com/gogo/protobuf    | CVE-2021-3121    |          | 1.3.1                             | v1.3.2                             | gogo/protobuf:                        |
    |                             |                  |          |                                   |                                    | plugin/unmarshal/unmarshal.go         |
    |                             |                  |          |                                   |                                    | lacks certain index validation        |
    |                             |                  |          |                                   |                                    | -->avd.aquasec.com/nvd/cve-2021-3121  |
    +-----------------------------+------------------+          +-----------------------------------+------------------------------------+---------------------------------------+
    | golang.org/x/crypto         | CVE-2020-29652   |          | 0.0.0-20200622213623-75b288015ac9 | v0.0.0-20201216223049-8b5274cf687f | golang: crypto/ssh: crafted           |
    |                             |                  |          |                                   |                                    | authentication request can            |
    |                             |                  |          |                                   |                                    | lead to nil pointer dereference       |
    |                             |                  |          |                                   |                                    | -->avd.aquasec.com/nvd/cve-2020-29652 |
    +-----------------------------+------------------+----------+-----------------------------------+------------------------------------+---------------------------------------+
    | k8s.io/client-go            | CVE-2020-8565    | MEDIUM   | 0.19.2                            | v0.20.0-alpha.2                    | kubernetes: Incomplete fix            |
    |                             |                  |          |                                   |                                    | for CVE-2019-11250 allows for         |
    |                             |                  |          |                                   |                                    | token leak in logs when...            |
    |                             |                  |          |                                   |                                    | -->avd.aquasec.com/nvd/cve-2020-8565  |
    +-----------------------------+------------------+----------+-----------------------------------+------------------------------------+---------------------------------------+
    go.sum (gomod)
    ==============
    Total: 2 (UNKNOWN: 0, LOW: 0, MEDIUM: 1, HIGH: 1, CRITICAL: 0)
    ```

#### 七、Trivy 过滤漏洞

默认情况下， Trivy还会检测未修补/未修复的漏洞。这意味着即使您更新所有软件包，您也无法修复这些漏洞。如果您想忽略它们，请使用该--ignore-unfixed选项。

!!! tip "隐藏未修复得漏洞"
    ```bash
    # trivy image --ignore-unfixed nginx:1.16 
    ```

!!! tip "按严重程度, 使用--severity选项"
    ```bash
    # trivy image --severity HIGH,CRITICAL  nginx:1.16
    ```

!!! tip "按漏洞ID, 使用.trivyignore"
    ```bash
    # cat .trivyignore
    # Accept the risk
    CVE-2018-14618
    
    # No impact in our settings
    CVE-2019-1543
    
    # trivy image  nginx:1.16
    ```

!!! tip "按类型, 使用--vuln-type选项"
    ```bash
    # trivy image --vuln-type os  nginx:1.16
    ```

#### 八、漏洞数据库

!!! tip "跳过漏洞数据库得更新，Trivy开始运行时每 12 小时下载一次漏洞数据库。这通常很快，因为数据库的大小只有 10~30MB。但是，如果您甚至想跳过它，请使用该--skip-db-update选项。"
    ```bash
    # trivy image --skip-db-update nginx:1.16
    ```

!!! tip "只下载漏洞数据库"
    ```bash
    # trivy image --download-db-only
    ```

!!! abstract "轻量级数据库"
    - 轻量级数据库不包含漏洞详细信息，例如描述和参考。因此，DB 的大小更小，下载速度更快。
    - 当您不需要漏洞详细信息并且适用于 CI/CD 时，此选项很有用。要查找其他信息，您可以在 NVD 网站上搜索漏洞详细信息。https://nvd.nist.gov/vuln/search

!!! tip "--light"
    ```bash
    # trivy image --light nginx:1.16
    # --light 选项不会像下面的例子那样显示标题。
    ```

#### 九、Trivy 缓存

!!! tip "使用--clear-cache选项删除缓存。"
    ```bash
    # trivy image --clear-cache
    ```

!!! tip "指定缓存的存储位置--cache-dir"
    ```bash
    $ trivy --cache-dir /tmp/trivy/ image nginx:1.16
    ```

!!! abstract "缓存后端"
    两个选项： - fs - 缓存路径可以通过--cache-dir - redis:// -redis://[HOST]:[PORT]

!!! tip "Trivy 支持本地文件系统和 Redis 作为缓存后端。此选项特别适用于客户端/服务器模式。"
    ```bash
    # trivy server --cache-backend redis://localhost:6379
    ```

#### 十、Trivy 漏洞报告格式

!!! tip "指定输出格式为表格（默认）"
    ```bash
    # trivy image -f table nginx:1.16
    ```

!!! tip "指定输出格式为表格 json"
    ```bash
    trivy image -f json -o results.json nginx:1.16
    ```
