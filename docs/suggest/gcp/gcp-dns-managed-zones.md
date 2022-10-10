# Google Cloud DNS 区域的资源检测

### 检查规则说明
!!! info ""
    Google Cloud 检测账号下DNS 区域的资源中是否禁用了 DNSSEC，未禁用视为“合规”，否则属于“不合规”
    
  ```YAML
  policies:
      # 检测账号下DNS 区域的资源中是否禁用了 DNSSEC，未禁用视为“合规”，否则属于“不合规”
      - name: gcp-dns-managed-zones-if-no-dnssec
        resource: gcp.dns-managed-zone
        filters:
          - type: value
            key: dnssecConfig.state
            # off without quotes is treated as bool False
            value: ${{value}}
  ```

    
### 处置方案
!!! info ""
    我们以 GCP 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    