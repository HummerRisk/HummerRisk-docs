# Azure VM虚拟机使用率检测

!!! info "检查规则说明"
    Azure  检测您账号下的虚拟机是否x小时内CPU使用率<= y％，使用率> y％视为“合规”，否则视为“不合规”
    
```YAML
policies:
  # 检测您账号下的虚拟机是否x小时内CPU使用率<= y％，使用率> y％视为“合规”，否则视为“不合规”
  - name: azure-unused-vms
    resource: azure.vm
    filters:
      - type: metric
        metric: Percentage CPU
        op: le
        aggregation: average
        threshold: ${{threshold}}
        timeframe: ${{timeframe}}
```

    
!!! info "处置方案"
    
    我们以 Azure 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    