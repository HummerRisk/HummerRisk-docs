# UCloud Uhost 实例网络类型检测

### 1.检查项说明
!!! info ""
    UCloud 账号下所有 Uhost 实例已关联到VPC，若您配置阈值，则关联的 VpcId 需存在您列出的阈值中，视为“合规”，否则视为“不合规”

### 2.处置方案
!!! info ""
    1. 前往 UCloud 控制台，调整网络类型；
    2. 私有网络 VPC（Virtual Private Cloud）是属于用户的、逻辑隔离的网络环境。在私有网络中，可以创建指定网段的VPC，在VPC中创建子网并自主管理云资源。创建VPC时，可自主规划网段，灵活为VPC指定网段。目前VPC支持的网段范围如下：
        - 10.0.0.0/8（10.0.0.0-10.255.255.255）掩码范围：最大为 /8 掩码，最小为 /29 掩码。
        - 172.16.0.0/12（172.16.0.0-172.31.255.255）掩码范围：最大为 /12 掩码，最小为 /29 掩码。
        - 192.168.0.0/16（192.168.0.0-192.168.255.255）掩码范围：最大为 /16 掩码，最小为 /29 掩码。    
    3. 查看当前 Uhost 的 VPC 是否和预期一致，如果不一致可进行更换；

### 3.操作步骤
!!! info ""
    1. 使用UCloud账号登录控制台；
    2. 通过导航菜单进入云服务器控制台；https://console.ucloud.cn/uhost/uhost
    3. 选择需要更换 VPC 网络的的 Uhost, 点击实例名称；
        ![处置方案](../../img/suggest/ucloud/uhost-list.png){ width="600px" }
        ![处置方案](../../img/suggest/ucloud/eip-network-type.png){ width="600px" }
    4. 进入磁盘与恢复，对当前系统盘制作镜像；
    5. 用新的镜像创建 Uhost, 创建时选择正确的 vpc。
        ![处置方案](../../img/suggest/ucloud/uhost-clone.png){ width="600px" }
        ![处置方案](../../img/suggest/ucloud/vhost-select-vpc.png){ width="600px" }

### 4.帮助资源
!!! info ""
    - https://docs.ucloud.cn/udisk/userguide/clone
    - https://docs.ucloud.cn/uhost/introduction/network/vpc
