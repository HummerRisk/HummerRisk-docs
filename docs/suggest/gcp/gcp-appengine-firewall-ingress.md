# Google Cloud 防火墙入口规则配置检测

!!! info "检查规则说明"
    Google Cloud 检测账号下防火墙规则是否只有一个规则允许所有连接，符合视为“合规”，否则属于“不合规”
    
  ```YAML
  policies:
    # 检测账号下防火墙规则是否只有一个规则允许所有连接，符合视为“合规”，否则属于“不合规”
    - name: gcp-app-engine-firewall-ingress-rule-if-default-unrestricted-access
      resource: gcp.app-engine-firewall-ingress-rule
      filters:
        - and:
          - type: value
            value_type: resource_count
            op: eq
            value: ${{value}}
          - type: value
            key: sourceRange
            value: '*'
          - type: value
            key: action
            value: ALLOW
  ```

    
!!! info "处置方案"
    
    我们以 GCP 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    