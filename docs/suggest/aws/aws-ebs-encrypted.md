# AWS EBS加密检测

### 检查规则说明
!!! info ""
    检测您账号下的EBS是否加密，加密视为“合规”，否则视为“不合规”

    ```YAML
    policies:
    # 检测您账号下的EBS是否加密，加密视为“合规”，否则视为“不合规”
    - name: aws-unencrypted-ebs
        resource: aws.ebs
        filters:
        - Encrypted: ${{value}}
    ```
    使用 Amazon EBS 加密 作为与 EC2 实例关联的 EBS 资源的直接加密解决方案。借助 EBS 加密，无需构建、维护和保护自己的密钥管理基础设施。创建加密卷和快照时， EBS 加密使用 AWS KMS keys。
    加密操作在托管 EC2 实例的服务器上进行，用于确保静态数据安全性以及在实例和其附加的 EBS 存储之间传输的数据的安全性。
    从安全的角度，我们应当确保所有使用中的 EBS 都已经是加密的。
### 处置方案
!!! info ""
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。    
    分两种情况   
    1. 开启默认加密：  
    您可以配置 AWS 账户对您创建的新 EBS 卷和快照副本进行加密。例如，Amazon EBS 加密当您启动实例时创建的 EBS 卷以及您从未加密的快照复制的快照。
    默认情况下，加密对现有 EBS 卷或快照没有影响。
    2. 从未加密转换为加密 EBS:   
    您无法直接加密现有未加密卷或快照。但是，您可以从未加密的卷或快照创建加密卷或快照。如果已开启默认加密，Amazon EBS 将使用 EBS 加密的默认设置 KMS 密钥自动加密新卷和快照。否则，您可以在创建单个卷或快照时启用加密。  



### 操作步骤
!!! info ""
    *通过以下网址打开 Amazon EC2 控制台：https://console.aws.amazon.com/ec2/。
    *从导航栏中选择区域。  
    *从导航窗格中，选择 EC2 控制面板。  
    *在页面的右上角，选择账户属性，然后选择 EBS 加密。  
    *选择管理。  
    *选择 Enable (启用)。您可以将系统代表您创建的 AWS 托管式密钥（别名为 alias/aws/ebs）保留为默认加密密钥，或者选择对称客户管理加密密钥。   
    *选择更新 EBS 加密。  



### 帮助资源
!!! info ""
    https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/EBSEncryption.html
    https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/EBSEncryption.html#encrypt-unencrypted