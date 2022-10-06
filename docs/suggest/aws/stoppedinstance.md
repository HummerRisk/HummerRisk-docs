# AWS EC2实例关机状态检测

!!! info "检查规则说明"
    检测您账号下的EC2实例是否有处于'关机'状态的，开机视为“合规”，关机视为“不合规” 。
    AWS 的 EC2 实例在关机后仍然会收取部分费用，包括存储，IP等，当 EC2 实例不在使用后，不应该长时间处于关机状态，应当及时的进行回收处理。

!!! info "处置方案"
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，删除关机状态的 EC2 实例 。

    *注意：
    EC2 有防止实例意外终止的功能，可以为实例启用终止保护。DisableApiTermination 属性可控制是否可以使用控制台、CLI 或 API 终止实例。默认情况下，终止保护处于禁用状态。您可以在实例启动、运行或已停止时设置该属性值 (针对由 Amazon EBS 支持的实例)。如果开启了该属性，那么需要先关闭该属性，在进行终止实例操作。*

    *注意2：
    EC2 实例删除时需要注意管理的 EBS 卷，如果 EBS 卷不需要保留，要把管理的卷同时删除掉。*

!!! info "操作步骤"

    * 1.登录 AWS 管理控制台，通过导航菜单进入 EC2 控制面板。 https://console.aws.amazon.com/ec2/ 
    * 2.在左侧菜单中找到实例 。
    * 3.在 EC2 实例列表中找到 HummerRisk 检测结果中对应的实例，确认实例状态是'关机'(stopped)。
    * 4.点击上方的实例状态按钮，选择终止实例。




!!! info "帮助资源"
    https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/terminating-instances.html#Using_ChangingInstanceInitiatedShutdownBehavior
    https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/ebs-deleting-volume.html