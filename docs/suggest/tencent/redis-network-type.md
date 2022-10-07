# 腾讯云 Redis VPC 网络检测

### 1.检查项说明
!!! info ""
    Tencent  检测您账号下的Redis实例是否运行在VPC网络环境下，是视为“合规”，否则属于“不合规”

### 2.处置方案
!!! info ""
    前往腾讯云控制台，

### 3.操作步骤
!!! info ""
    1. 使用腾讯云账号登录控制台。
    2. 通过导航菜单进入云数据库-redis控制台。https://console.cloud.tencent.com/redis
    3. 查看当前redis实例的网络类型，如果是非VPC网络，根据实际情况可迁移至VPC网络
    4. 登录 Redis 控制台。
    5. 在右侧实例列表页面上方，选择地域。
    6. 在实例列表中，找到目标实例。
    7. 单击目标实例 ID，进入实例详情页面。
    8. 在实例详情的网络信息区域，可看到当前 Redis 实例所属网络和内网地址，单击所属网络后面的更换网络。
    9. 可从基础网络转换为私有网络或从当前私有网络更换到另一个私有网络。

![处置方案-查看当前网络类型](../../img/suggest/tencent/redis-network-type.png){ width="900px" }
![处置方案-修改redis网络类型](../../img/suggest/tencent/redis-change-network.png){ width="900px" }

### 4.帮助资源
!!! info ""
    - https://cloud.tencent.com/document/product/239/30871
    - https://cloud.tencent.com/document/product/239/30910
    