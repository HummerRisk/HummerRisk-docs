# Azure 资源组检测


### 检查规则说明
!!! info ""
    Azure  检测您的账户下资源组是否是空的，非空视为“合规”，否则视为“不合规”
    
    ```YAML
    policies:
        # 检测您的账户下资源组是否是空的，非空视为“合规”，否则视为“不合规”
        - name: azure-rg-empty
        resource: azure.resourcegroup
        filters:
            - type: empty-group
    ```

    
### 处置方案
!!! info ""
    我们以 Azure 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    