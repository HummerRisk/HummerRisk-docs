# AWS RDS实例公网访问检测

### 检查规则说明
!!! info ""
    检测您账号下RDS实例不允许任意来源公网访问，不允许视为“合规”，否则视为“不合规”

    ```YAML
    policies:
    # 检测您账号下RDS实例不允许任意来源公网访问，视为“合规”，否则视为“不合规”。
    - name: aws-rds-publicly-accessible
      resource: aws.rds
      filters:
        - PubliclyAccessible: ${{value}}
    ```

### 处置方案
!!! info ""
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    