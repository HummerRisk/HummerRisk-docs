# Google Cloud 防火墙规则检测

!!! info "检查规则说明"
    Google Cloud 检测账号下防火墙规则是否符合规则，符合视为“合规”，否则属于“不合规”
    
  ```YAML
  vars:
      min-network-prefix-size: &min-network-prefix-size ${{value2}}
  policies:
      # 检测账号下防火墙规则是否符合规则，符合视为“合规”，否则属于“不合规”
      - name: appengine-firewall-rules
        description: |
          Check if firewall rule network prefix size is long enough
        resource: gcp.app-engine-firewall-ingress-rule
        filters:
          - not:
            - type: value
              key: sourceRange
              op: regex
              # 过滤掉*特殊字符和没有网络前缀长度的IP地址
              value: ${{value1}}
            - type: value
              key: sourceRange
              value_type: cidr_size
              op: ge
              value: *min-network-prefix-size
  ```

    
!!! info "处置方案"
    
    我们以 GCP 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    