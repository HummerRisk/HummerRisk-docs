# Azure Cosmos DB检测

!!! info "检查规则说明"
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

    
!!! info "处置方案"
    
    我们以 Azure 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    