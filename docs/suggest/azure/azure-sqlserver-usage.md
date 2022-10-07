# Azure SQL Server使用率检测

!!! info "检查规则说明"
    Azure  检测您账号下的SQL Server是否x小时内平均DTU消耗少于y％，多于y％视为“合规”，否则视为“不合规”
    
  ```YAML
  policies:
    # 检测您账号下的SQL Server是否x小时内平均DTU消耗少于y％，多于y％视为“合规”，否则视为“不合规”
    - name: azure-dtu-consumption
      resource: azure.sqlserver
      filters:
        - type: metric
          metric: dtu_consumption_percent
          aggregation: average
          op: lt
          threshold: ${{threshold}}
          timeframe: ${{timeframe}}
          filter:  "DatabaseResourceId eq '*'"
  ```

    
!!! info "处置方案"
    
    我们以 Azure 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    