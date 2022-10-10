# AWS ELB SSL 黑名单检测

### 检查规则说明
!!! info ""
    测您账号下ELB SSL 黑名单检测，在白名单视为“合规”，黑名单视为“不合规”

    ```YAML
    policies:
    # 测您账号下ELB SSL 黑名单检测，在白名单视为“合规”，黑名单视为“不合规”
    - name: aws-elb-ssl-whitelist
      resource: aws.elb
      filters:
        - type: ssl-policy
          blacklist:
            - Protocol-TLSv1
            - Protocol-TLSv1.1
            - Protocol-TLSv1.2
    ```

### 处置方案
!!! info ""
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    