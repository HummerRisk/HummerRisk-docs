# Azure VM虚拟机状态检测


### 检查规则说明
!!! info ""
    Azure  检测您账号下的VM是否停止运行，运行视为“合规”，否则视为“不合规”
    
  ```YAML
  policies:
    #  检测您账号下的VM是否停止运行，运行视为“合规”，否则视为“不合规”
    - name: azure-stopped-vm
      resource: azure.vm
      filters:
      - type: instance-view
        key: statuses[].code
        op: not-in
        value_type: swap
        value: ${{value}}
  ```

    
### 处置方案
!!! info ""
    我们以 Azure 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    