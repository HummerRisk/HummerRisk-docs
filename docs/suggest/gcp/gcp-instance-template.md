# Google Cloud 实例模板检测

### 检查规则说明
!!! info ""
    Google Cloud 检测账号下不符合要求的实例模板，符合的视为“合规”，否则属于“不合规”
    
  ```YAML
  vars:
    disallowed-machine-types: &disallowed-machine-types
      - ${{value1}}
      - ${{value2}}
      - ${{value3}}
      - ${{value4}}
      - ${{value5}}

  policies:
    - name: gcp-instance-template-disallowed-machine-types
      resource: gcp.instance-template
      filters:
        - type: value
          key: properties.machineType
          op: in
          value: *disallowed-machine-types
  ```

    
### 处置方案
!!! info ""
    我们以 GCP 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
https://cloud.google.com/compute/docs/machine-types
    