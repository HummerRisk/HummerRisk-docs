# AWS EC2 CPU使用率检测

!!! info "检查规则说明"
    AWS  检测您账号下的EC2是否CPU使用率在x天内低于y，高于y视为“合规”，否则视为“不合规”
    
    ```YAML
    policies:
    # 检测您账号下的EC2是否CPU使用率在x天内低于y，高于y视为“合规”，否则视为“不合规”
    - name: aws-ec2-underutilized
        resource: aws.ec2
        filters:
        - type: metrics
            name: CPUUtilization
            days: ${{day}}
            period: 86400  # 检测周期(86400s为一天)
            statistics: Average
            value: ${{used}}
            op: less-than
    ```    

!!! info "处置方案"
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    