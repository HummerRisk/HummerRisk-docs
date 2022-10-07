# AWS ELB实例使用检测

!!! info "检查规则说明"
    检测您账号下弹性负载均衡器是否使用，使用视为“合规”，否则视为“不合规”

    ```YAML
    policies:
    # 检测您账号下弹性负载均衡器是否使用，使用视为“合规”，否则视为“不合规”
    - name: aws-elb-unused
      resource: aws.elb
      filters:
        - "tag:maid_status": absent
        - Instances: []
    ```

!!! info "处置方案"
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    