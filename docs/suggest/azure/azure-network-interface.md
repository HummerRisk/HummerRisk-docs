# Azure 网络接口连接检测


### 检查规则说明
!!! info ""
    Azure  检测您账号下的网络接口是否连接到VM，连接视为“合规”，否则视为“不合规”
    
  ```YAML
  policies:
    # Azure  检测您账号下的网络接口是否连接到VM，连接视为“合规”，否则视为“不合规”
    - name: orphaned-nic
      resource: azure.networkinterface
      filters:
        - type: value
          key: properties.virtualMachine
          value: ${{value}}
  ```

### 处置方案
!!! info ""
    我们以 Azure 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    