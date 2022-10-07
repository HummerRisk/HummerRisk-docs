# Azure Disk关联虚拟机检测

!!! info "检查规则说明"
    Azure  检测您账号下的Disk是否关联虚拟机，关联视为“合规”，否则视为“不合规”
    
```YAML
policies:
  # 检测您账号下的Disk是否关联虚拟机，关联视为“合规”，否则视为“不合规”
  - name: azure-orphaned-disk
    resource: azure.disk
    filters:
      - type: value
        key: managedBy
        value: ${{value}}
```

    
!!! info "处置方案"
    
    我们以 Azure 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    