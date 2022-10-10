# Azure 存储账户检测


### 检查规则说明
!!! info ""
    Azure  检测所有防火墙都配置为仅允许从数据中心（或IP空间的任何块）中的IP地址进行访问，符合视为“合规”，否则视为“不合规”
    
  ```YAML
  policies:
    # 检测所有防火墙都配置为仅允许从数据中心（或IP空间的任何块）中的IP地址进行访问，符合视为“合规”，否则视为“不合规”
    - name: azure-storage-only-allow-datacenter-ips
      resource: azure.storage
      filters:
        - or:
          - type: value
            key: properties.networkAcls.defaultAction
            value: 'Allow'

          - not:
            - type: firewall-rules
              only:
                - ${{value1}}
                - ${{value2}}
                - ${{value3}}
  ```

    
    
### 处置方案
!!! info ""
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    