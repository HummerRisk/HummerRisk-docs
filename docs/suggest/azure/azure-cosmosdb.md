# Azure Cosmos DB检测

### 检查规则说明
!!! info ""
    Azure  检测所有Cosmos DB帐户没有配置防火墙，或者配置了允许超出预期范围访问的帐户，符合视为“合规”，否则视为“不合规”  
    
  ```YAML
  policies:
  # 检测所有Cosmos DB帐户没有配置防火墙，或者配置了允许超出预期范围访问的帐户，符合视为“合规”，否则视为“不合规”
  - name: azure-cosmos-firewall-enable
    resource: azure.cosmosdb
    filters:
      - or:
        - type: value
          key: properties.ipRangeFilter
          value: empty  # The firewall is disabled

        - not:
          - type: firewall-rules
            only:       # Should *only* allow access within the specified maximums here
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
    