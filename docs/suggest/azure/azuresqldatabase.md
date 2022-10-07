# Azure SQL数据库保留策略检测

!!! info "检查规则说明"
    Azure  检测您的账户下SQL数据库短期保留至少n天，符合视为“合规”，否则视为“不合规”
    
```YAML
policies:
    # 检测您的账户下SQL数据库短期保留至少n天，符合视为“合规”，否则视为“不合规”
    - name: azure-short-term-backup-retention-policy
      resource: azure.sqldatabase
      filters:
        - type: short-term-backup-retention
          op: lt
          retention-period-days: ${{value}}
```

    
!!! info "处置方案"
    
    我们以 Azure 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    