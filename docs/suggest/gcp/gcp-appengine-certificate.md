# Google Cloud SSL 证书过期检测

!!! info "检查规则说明"
    Google Cloud 检测账号下 SSL 证书是否即将到期，未到期视为“合规”，否则属于“不合规”
    
  ```YAML
  policies:
      # 检测账号下 SSL 证书是否即将到期，未到期视为“合规”，否则属于“不合规”
      - name: appengine-certificate-age
        description: |
          Check existing certificate
        resource: gcp.app-engine-certificate
        filters:
        - type: value
          key: expireTime
          op: ${{op}}
          value_type: expiration
          value: ${{day}}
  ```

    
!!! info "处置方案"
    
    我们以 GCP 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    