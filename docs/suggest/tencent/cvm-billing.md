# 腾讯云CVM实例关机计费模式检测

!!! info "检查项说明"
    Tencent CVM实例的关机计费模式是否为关机停止收费，是视为“合规”，否则视为“不合规”


!!! info "处置方案"
    前往腾讯云控制台，调整公网IP带宽

!!! info "操作步骤"
    1. 使用腾讯云账号登录控制台
    2. 通过导航菜单进入云服务器控制台。https://console.cloud.tencent.com/cvm/instance
    3. 找到相关的CVM
    4. 如果是"按需实例"，在实例计费模式可以查看当前状态，如果是不收费则显示为"按量计费-停止收费"
    5. 注意只有"按需实例"才支持"关机停止收费"
    6. 如果已经关机，但不是"停止收费"状态，可以重新关机，并勾选关机不收费

![处置方案](../../img/suggest/tencent/cvm-bulling.png){ width="900px" }

!!! info "帮助资源"
    https://cloud.tencent.com/document/product/213/19922
    https://cloud.tencent.com/document/product/213/19918
    