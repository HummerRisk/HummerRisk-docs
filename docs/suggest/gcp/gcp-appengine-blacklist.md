# Google Cloud 域使用状态检测

### 检查规则说明
!!! info ""
  Google Cloud 检测账号下列入黑名单的域是否仍在使用中，未使用视为“合规”，否则属于“不合规”
    
  ```YAML
  vars:
    blacklisted-domains-in-use: &blacklisted-domains
      - ${{domains1}}
      - ${{domains2}}
      - ${{domains3}}
  policies:
    # 检测账号下列入黑名单的域是否仍在使用中，未使用视为“合规”，否则属于“不合规”
    - name: gcp-app-engine-domain-if-blacklisted-in-use
      resource: gcp.app-engine-domain
      filters:
        - type: value
          key: id
          op: in
          value: *blacklisted-domains
  ```

    
### 处置方案
!!! info ""
    我们以 GCP 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    