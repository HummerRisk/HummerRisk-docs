# Google Cloud 部署管理器检测

### 检查规则说明
!!! info ""
    Google Cloud 检测账号下已达到到期日期的部署，未到期视为“合规”，否则属于“不合规”
    
  ```YAML
  policies:
    # 检测账号下已达到到期日期的部署，未到期视为“合规”，否则属于“不合规”
    - name: expired-deployments
      description: Finds expired deployments
      resource: gcp.dm-deployment
      filters:
      - type: value
        key: insertTime
        value_type: expiration
        op: gte
        value: ${{day}}
  ```

    
### 处置方案
!!! info ""
    我们以 GCP 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    