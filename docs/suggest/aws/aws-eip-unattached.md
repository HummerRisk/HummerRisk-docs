# AWS EIP未使用检测

### 检查规则说明
!!! info ""
    检测您账号下的弹性IP实例是否都已使用，是视为“合规”，否则视为“不合规”

    ```YAML
    policies:
    # 检测您账号下的弹性IP实例是否已连接，是视为“合规”，否则视为“不合规”
    - name: aws-unused-network-addr
        resource: aws.network-addr
        filters:
        - NetworkInterfaceId: absent
        - AssociationId: absent
    ```
    什么是 EIP ？  
    弹性 IP 地址 是专为动态云计算设计的静态 IPv4 地址。弹性 IP 地址会分配给您的 AWS 账户，并且在您释放它之前一直属于您。使用弹性 IP 地址，您可以快速将地址重新映射到您的账户中的另一个实例，从而屏蔽实例故障。或者，您可以在域的 DNS 记录中指定弹性 IP 地址，以使域指向您的实例。
    
    
### 处置方案
!!! info ""
    释放未使用的 EIP   
    如果一个 EIP 没有管理的网络，也没有管理的实例，那么这个 EIP 就没有被使用，应当及时回收。  
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""

    * 通过以下网址打开 Amazon EC2 控制台：https://console.aws.amazon.com/ec2/。   

    * 在导航窗格中，选择 Elastic IPs。   

    * 选择要释放的弹性 IP 地址，然后依次选择 Actions (操作)、Release Elastic IP addresses (释放弹性 IP 地址)。   

    * 选择 Release (释放)。   



### 帮助资源
!!! info ""

    https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html   
    https://docs.aws.amazon.com/cli/latest/reference/ec2/release-address.html
