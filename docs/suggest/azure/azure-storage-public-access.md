# Azure 存储公网访问检测


### 检查规则说明
!!! info ""
    Azure  检测您的账户下存储是否具有指定ip规则的存储帐户的访问(公共访问)，符合视为“合规”，否则视为“不合规”
    
  ```YAML
  policies:
    # 检测您的账户下存储是否具有指定ip规则的存储帐户的访问，符合视为“合规”，否则视为“不合规”
    - name: azure-storage-block-public-access
      resource: azure.storage
      filters:
      - type: value
        key: properties.networkAcls.ipRules
        value_type: size
        op: ne
        value: 0
  ```

    
### 处置方案
!!! info ""
    我们以 Azure 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    