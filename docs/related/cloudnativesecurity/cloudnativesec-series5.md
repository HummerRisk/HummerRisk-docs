![配图](../../img/related/cloudnativesec-series4-pic4.jpeg){ width="80%" }
### 引言

!!! abstract ""
    etcd是一个强一致性的分布式键值存储，它提供了一种可靠的方式来存储需要被分布式系统或机器集群访问的数据。通过 raft 算法它能在网络分区期间优雅地处理领导者的选举，并能容忍机器故障，甚至在领导者节点上。除此之外， etcd 还是 kubernetes 最为核心的组件之一，存储着 kubernetes 所有的元信息，因此如何保障 etcd 的安全性十分重要。

![配图](../../img/related/cloudnativesec-series5-pic1.png){ width="80%" }

### 小知识
!!! abstract ""
    * Raft 是一种共识算法，设计得很容易理解。它在容错和性能方面与 Paxos 相当。不同的是，它被分解成相对独立的子问题，并干净地解决了实际系统所需的所有主要部分。
    * 而且 Raft 宣称的强一致性则是依靠"共识算法"来实现的。共识是容错分布式系统的一个基本问题，共识涉及多个服务器对数值的同意。一旦他们就某一数值达成了决定，该决定就是最终的。典型的共识算法在其任何大多数服务器可用时都会取得进展；例如，一个由5个服务器组成的集群，即使有2个服务器失败，也能继续运行。如果有更多的服务器失败，他们就会停止取得进展（但永远不会返回一个错误的结果）。
    * 共识通常出现在复制状态机的背景下，这是一种构建容错系统的一般方法。每个服务器都有一个状态机和一个日志。状态机是我们想让其成为容错的组件，比如说哈希表。在客户看来，即使集群中的少数服务器发生故障，他们也是在与一个单一的、可靠的状态机进行交互。每个状态机从其日志中获取命令作为输入。在我们的哈希表例子中，日志将包括像set x to 3这样的命令。一个共识算法被用来同意服务器日志中的命令。共识算法必须确保，如果任何一个状态机将set x to 3作为第n条命令，其他状态机将永远不会应用不同的第n条命令。因此，每个状态机都会处理同一系列的命令，从而产生同一系列的结果，到达同一系列的状态。
    * 有关Raft算法的知识可以参考下方的官方链接：
        - https://raft.github.io/
    * 可视化页面可以帮助你理解 Raft 算法是怎么实现"共识"以及选举"领导者"的
        - http://thesecretlivesofdata.com/raft/

### etcd 的安全模型

!!! abstract ""
    * etcd 支持自动 TLS 以及通过客户端证书对客户端到服务器以及对等（服务器到服务器/集群）通信的身份验证。
    * 要启动并运行，首先要有一个 CA 证书和一个成员的签名密钥对。建议为集群中的每个成员创建并签署新的密钥对。
    * 为方便起见，可以使用 cfssl 工具自动生成证书，详细步骤可参考 cfssl 官方文档： https://github.com/cloudflare/cfssl


### etcd 的基本配置
!!! info "控制平面的安全"
    * etcd 通过命令行标志或环境变量采用几个与证书相关的配置选项：
    * 客户端到服务器的通信：
        - `--cert-file=<path>`：用于etcd 的 SSL/TLS 连接的证书。设置此选项后，advertise-client-urls 可以使用 HTTPS 模式。
        - `--key-file=<path>`：证书的密钥。必须未加密。
        - `--client-cert-auth`：设置后，etcd 将检查所有传入的 HTTPS 请求以获取由受信任的 CA 签名的客户端证书，不提供有效客户端证书的请求将失败。如果启用身份验证，则证书会为 Common Name 字段给出的用户名提供凭据。
        - `--trusted-ca-file=<path>`：受信任的证书颁发机构。
        - `--auto-tls`：为与客户端的 TLS 连接使用自动生成的自签名证书。
    * 对等（服务器到服务器/集群）通信：
        对等选项的工作方式与客户端到服务器选项的工作方式相同：
        - `--peer-cert-file=<path>`：用于对等点之间 SSL/TLS 连接的证书。这将用于侦听对等地址以及向其他对等点发送请求。
        - `--peer-key-file=<path>`：证书的密钥。必须未加密。
        - `--peer-client-cert-auth`：设置后，etcd 将检查来自集群的所有传入对等请求，以获取由提供的 CA 签名的有效客户端证书。
        - `--peer-trusted-ca-file=<path>`：受信任的证书颁发机构。
        - `--peer-auto-tls`：使用自动生成的自签名证书进行对等点之间的 TLS 连接。
    如果提供了客户端到服务器或对等证书，则还必须设置密钥。所有这些配置选项也可通过环境变量、ETCD_CA_FILE等ETCD_PEER_CA_FILE获得。

### 配置示例
!!! abstract ""
    1. 客户端指定CA证书和签名密钥对通过 https 访问 etcd 服务
    ```shell
    etcd --name infra0 --data-dir infra0 \
    --cert-file=/path/to/server.crt --key-file=/path/to/server.key \
    --advertise-client-urls=https://127.0.0.1:2379 --listen-client-urls=https://127.0.0.1:237
    ```
    2. 通过 https 客户端证书验证客户端到etcd服务器的身份
    使用客户端证书来防止对 etcd 的未授权访问,客户端将向服务器提供证书，服务器将检查证书是否由提供的 CA 签名并决定是否为请求提供服务。
    ```shell
    etcd --name infra0 --data-dir infra0 \
    --client-cert-auth --trusted-ca-file=/path/to/ca.crt --cert-file=/path/to/server.crt --key-file=/path/to/server.key \
    --advertise-client-urls https://127.0.0.1:2379 --listen-client-urls https://127.0.0.1:2379
    ```
    3. 配置 etcd 集群成员直接通信的证书
    假设我们有我们ca.crt和两个成员，他们有自己的密钥对（member1.crt& member1.key，member2.crt& member2.key）由这个 CA 签名，我们启动 etcd 如下：
    ```shell
    DISCOVERY_URL=... # from https://discovery.etcd.io/new
    # 成员1
    $ etcd --name infra1 --data-dir infra1 \
      --peer-client-cert-auth --peer-trusted-ca-file=/path/to/ca.crt --peer-cert-file=/path/to/member1.crt --peer-key-file=/path/to/member1.key \
      --initial-advertise-peer-urls=https://10.0.1.10:2380 --listen-peer-urls=https://10.0.1.10:2380 \
      --discovery ${DISCOVERY_URL}
    # 成员2
    $ etcd --name infra2 --data-dir infra2 \
      --peer-client-cert-auth --peer-trusted-ca-file=/path/to/ca.crt --peer-cert-file=/path/to/member2.crt --peer-key-file=/path/to/member2.key \
      --initial-advertise-peer-urls=https://10.0.1.11:2380 --listen-peer-urls=https://10.0.1.11:2380 \
      --discovery ${DISCOVERY_URL}
    ```
    4. 使用自动签名进行安全传输
    对于需要通信加密而非身份验证的情况，etcd 支持使用自动生成的自签名证书加密其消息。这简化了部署，因为不需要在 etcd 之外管理证书和密钥。
    配置 etcd 以将自签名证书用于带有标志的客户端和对等--auto-tls连接--peer-auto-tls：
    ```shell
    DISCOVERY_URL=... # from https://discovery.etcd.io/new
    # member1
    $ etcd --name infra1 --data-dir infra1 \
      --auto-tls --peer-auto-tls \
      --initial-advertise-peer-urls=https://172.16.10.10:2380 --listen-peer-urls=https://172.16.10.10:2380 \
      --discovery ${DISCOVERY_URL}
    # member2
    $ etcd --name infra2 --data-dir infra2 \
      --auto-tls --peer-auto-tls \
      --initial-advertise-peer-urls=https://172.16.10.11:2380 --listen-peer-urls=https://172.16.10.11:2380 \
      --discovery ${DISCOVERY_URL}
    ```
    * 关于更多 etcd 安全配置，可以参考 etcd 官方文档：
        - https://etcd.io/docs/v3.2/op-guide/security/#example-1-client-to-server-transport-security-with-https