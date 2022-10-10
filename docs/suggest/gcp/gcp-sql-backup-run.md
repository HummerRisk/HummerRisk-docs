# Google Cloud SQL实例检测

### 检查规则说明
!!! info ""
    Google Cloud 检测账号下Cloud SQL 实例的备份是否运行并列出超过 5 天的不成功备份，符合的视为“合规”，否则属于“不合规”
    
  ```YAML
  policies:
  # 检测账号下Cloud SQL 实例的备份是否运行并列出超过 5 天的不成功备份，符合的视为“合规”，否则属于“不合规”
  - name: sql-backup-run
    description: |
      check basic work of Cloud SQL filter on backup runs: lists unsucessful backups older than 5 days
    resource: gcp.sql-backup-run
    filters:
      - type: value
        key: status
        op: not-equal
        value: ${{status}}
      - type: value
        key: endTime
        op: greater-than
        value_type: age
        value: ${{day}}
  ```

    
### 处置方案
!!! info ""
    我们以 GCP 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    