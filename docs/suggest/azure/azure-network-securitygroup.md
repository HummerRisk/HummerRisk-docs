# Azure 网络安全组检测


### 检查规则说明
!!! info ""
    Azure  检测您账号下的网络安全组是否打开了某些端口、关闭了某些端口，符合视为“合规”，否则视为“不合规” 
    
    ```YAML
    policies:
    # 检测您账号下的网络安全组是否打开了某些端口、关闭了某些端口，符合视为“合规”，否则视为“不合规”
    - name: azure-close-egress-except-TCP
        resource: azure.networksecuritygroup
        filters:
        - type: ingress
        ports: ${{allow_port}}
        access: 'Allow'
        - type: ingress
        ports: ${{deny_port}}
        access: 'Deny'
    ```

### 处置方案
!!! info ""
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    