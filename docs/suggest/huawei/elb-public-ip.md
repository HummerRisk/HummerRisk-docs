# Huawei ELB 实例绑定公网 IP 检测

### 1.检查项说明
!!! info ""
    Huawei 负载均衡实例未直接绑定公网 IP，符合视为“合规”，否则视为“不合规”。该规则仅适用于 IPv4 协议。

### 2.处置方案
!!! info ""
    1. 前往华为云控制台，调整 ELB 实例管理。
    2. 可以根据业务需要为负载均衡实例绑定IP地址，或者将负载均衡实例已经绑定的IP地址进行解绑。
        * 独享型：支持绑定和解绑IPv4公网IP、IPv4私有IP、IPv6地址。
        * 共享型：支持绑定和解绑IPv4公网IP。

!!! warning ""
    * 解绑IPv4公网IP后，对应的弹性负载均衡器将无法进行IPv4公网流量转发；
    * 解绑IPv4私有IP后，对应的弹性负载均衡器将无法基于IPv4私有IP进行私网流量转发；
    * 解绑IPv6地址后，对应的弹性负载均衡器将无法基于IPv6地址进行流量转发，请谨慎操作。

### 3.操作步骤
!!! info ""
    1. 使用华为云账号登录控制台。
    2. 通过导航菜单进入服务控制台。https://console.huaweicloud.com/vpc。
    3. 找到相关的资源，进入管理菜单进行设置。

!!! info "绑定IPv4公网IP"
    1. 登录管理控制台。
    2. 在管理控制台左上角单击图标，选择区域和项目。
    3. 单击页面左上角的，选择“网络 > 弹性负载均衡”。
    4. 在“负载均衡器”界面，待修改的负载均衡器所在行，选择“更多 > 绑定IPv4公网IP”。
    5. 在“绑定IPv4公网IP”对话框中，选择需要绑定的公网IP。
    6. 单击“确定”。

当前仅独享型负载均衡支持此功能。
!!! info "绑定IPv4私有IP"
    1. 登录管理控制台。
    2. 在管理控制台左上角单击图标，选择区域和项目。
    3. 单击页面左上角的，选择“网络 > 弹性负载均衡”。
    4. 在“负载均衡器”界面，待修改的负载均衡器所在行，选择“更多 > 绑定IPv4私有IP”。
    5. 在“绑定IPv4私有IP”对话框中，选择待绑定的IPv4地址所在子网，并设置目标IP地址。
    6. 系统默认自动分配IP地址，如果需要手动指定IP地址，请去勾选“自动分配IPv4地址”，并在参数“IPv4地址”行输入目标IP地址。
    7. 输入的IP地址必须属于所选择的子网且未被使用。
    8. 单击“确定”。

当前仅独享型负载均衡支持此功能。
!!! info "绑定IPv6地址"
    1. 登录管理控制台。
    2. 在管理控制台左上角单击图标，选择区域和项目。
    3. 单击页面左上角的，选择“网络 > 弹性负载均衡”。
    4. 在“负载均衡器”界面，待修改的负载均衡器所在行，选择“更多 > 绑定IPv6地址”。
    5. 在“绑定IPv6地址”对话框中，选择待绑定的IPv6地址所在子网。
    6. 单击“确定”。

解绑IPv4公网IP后，对应弹性负载均衡器将无法进行IPv4公网流量转发，请谨慎操作。
!!! warning "解绑IPv4公网IP"
    1. 登录管理控制台。
    2. 在管理控制台左上角单击图标，选择区域和项目。
    3. 单击页面左上角的，选择“网络 > 弹性负载均衡”。
    4. 在“负载均衡器”界面，待修改的负载均衡器所在行，选择“更多 > 解绑IPv4公网IP”。
    5. 在“解绑IPv4公网IP”对话框中，确认需要释放的IPv4公网IP地址，单击“是”。

当前仅独享型负载均衡支持此功能。
解绑IPv6地址后，对应的弹性负载均衡器将无法基于IPv6地址进行流量转发，请谨慎操作。
!!! warning "解绑IPv6地址"
    1. 登录管理控制台。
    2. 在管理控制台左上角单击图标，选择区域和项目。
    3. 单击页面左上角的，选择“网络 > 弹性负载均衡”。
    4. 在“负载均衡器”页面，待设置的负载均衡器所在行单击“更多 > 解绑IPv6地址”。
    5. 在“解绑IPv6地址”对话框中，确认需要释放的IPv6地址，单击“是”。

### 4.帮助资源
!!! info ""
    - https://support.huaweicloud.com/usermanual-elb/elb_ug_fz_0009.html