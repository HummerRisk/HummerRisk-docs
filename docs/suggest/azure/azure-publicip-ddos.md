# Azure 公网IP地址DDoS攻击检测


### 检查规则说明
!!! info ""
    Azure  检测您账号下的公网IP地址是否受到DDoS攻击，没有受到DDoS攻击视为“合规”，否则视为“不合规”，否则视为“不合规”
    
    ```YAML
    policies:
    # 检测您账号下的公网IP地址是否受到DDoS攻击，没有受到DDoS攻击视为“合规”，否则视为“不合规”
    - name: azure-publicip-dropping-packets
        resource: azure.publicip
        filters:
        - type: metric
            metric: IfUnderDDoSAttack
            op: gt
            aggregation: maximum
            threshold: 0
            timeframe: ${{timeframe}}
    ```

    
    
### 处置方案
!!! info ""
    我们以 Azure 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    