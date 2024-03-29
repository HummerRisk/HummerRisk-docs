# Aliyun Disk磁盘加密状态检测

### 1.检查项说明
!!! info ""
    Aliyun 账号下所有的磁盘均已加密；若您配置阈值，则磁盘加密的Id需存在您列出的阈值中，视为“合规”，否则视为“不合规”

### 2.处置方案
!!! info ""
    数据加密适用于数据安全或法规合规等场景，帮助您加密保护存储在阿里云ECS上的数据，您可以选择对系统盘、数据盘或者镜像进行加密，然后基于加密后的云盘和镜像去创建ECS实例，以保护数据的隐私性和安全性。本文主要为您介绍加密云盘、快照和镜像的一些限制条件和相关操作。

### 3.前提条件
!!! info ""
    您已开通当前地域的密钥管理服务KMS（Key Management Service）。具体操作，请参见开通密钥管理服务。

### 3.背景信息
!!! info ""
    加密功能默认使用服务密钥（Default Service CMK）为用户数据进行加密，也支持使用自定义密钥BYOK（Bring Your Own Key）为用户的数据进行加密。云盘的加密机制中，每一块云盘会有相对应的用户主密钥CMK（Customer Master Key）和数据密钥DK（Data Key），并通过信封加密（Envelope Encryption）机制对用户数据进行加密。更多信息，请参见加密概述。
    使用密钥加密时，请仔细阅读以下注意事项：
    
|    限制项    |                                                                                            说明                                                                                             | 
|:---------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|   服务密钥    |                                                                     每个地域每个用户的服务密钥（Default Service CMK）唯一，不支持删除和禁用操作。                                                                      |
| 自定义密钥BYOK |                                 在ECS控制台上首次选择自定义密钥（BYOK）加密云盘时，需单击去授权，根据页面引导为ECS授权AliyunECSDiskEncryptDefaultRole角色，允许ECS访问您的KMS资源。关于角色的更多信息，请参见访问控制RAM介绍。 <br/>在KMS控制台创建密钥时，需选择Aliyun_AES_256或Aliyun_SM4密钥类型，ECS创建加密云盘时暂不支持其他密钥类型。 <br/>用户删除、禁用BYOK密钥前，需要确认卸载或更换该密钥关联的云盘，避免出现云盘数据丢失、实例启动失败等问题。查询密钥关联的云盘信息，请参见API DescribeDisks。 因BYOK密钥一旦删除将无法恢复，使用该密钥加密的内容及产生的数据密钥也将无法解密。在密钥失效前，推荐您使用禁用密钥功能，或者自行排查该密钥是否存在关联使用的云资源，避免密钥丢失后数据不可恢复。                                |
  
### 4.加密系统盘
!!! info ""
    您可以通过ECS控制台、API等方式在创建ECS实例或者复制自定义镜像时，选择是否对系统盘进行加密。系统盘加密后，系统盘上的数据都会被加密。加密密钥可以是系统自建的密钥（CMK），也可以是您导入的密钥（BYOK）。

### 5.加密数据盘
!!! info ""
    1. 已加密的自定义镜像中包含的数据盘，创建ECS实例时对应的数据盘会加密。具体操作，请参见加密系统盘。
    2. 创建ECS实例，添加数据盘时，选中加密并选择密钥。具体操作，请参见创建实例时加密数据盘。
    3. 单独创建云盘时，选中加密并选择密钥。具体操作，请参见创建云盘时加密数据盘。
