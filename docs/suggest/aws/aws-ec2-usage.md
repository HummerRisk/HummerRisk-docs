# AWS EC2 CPU使用率检测

### 检查规则说明
!!! info ""
    AWS  检测您账号下的 EC2 是否 CPU 使用率在 x 天内低于 y，高于 y 视为“合规”，否则视为“不合规”
    
    ```YAML
    policies:
    # 检测您账号下的 EC2 是否 CPU 使用率在 x 天内低于 y，高于 y视为“合规”，否则视为“不合规”
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
    在 EC2 的使用中，如果资源使用率太低，说明资源存在错配。本规则主要帮助用户发现 EC2 中那些CPU使用率过低的实例。   
    本规则中设定了2个变量：   
        - {{day}} ：检测的时间周期，也就是多少天内   
        - {{used}} ：使用率基准   
        在使用规则进行检测的时候，可以对这两个变量进行设置。
### 处置方案
!!! info ""
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。    
    CPU 使用率过低的几种可能情况：    
    * 实例配置过高，建议对实例进行降配   
    * 实例类型和业务类型不匹配，例如选择了 CPU 优化实例，但业务对CPU需求很低。建议变更实力类型。   
    * 负载均衡配置，建议检测负载均衡是否正确分配流量到实例。  
    * 实例中应用是否正常运行。建议登录主机进行检查。  


### 帮助资源
!!! info ""
    https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/EC2_GetStarted.html
    https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/instance-types.html
    https://docs.aws.amazon.com/zh_cn/elasticloadbalancing/latest/userguide/what-is-load-balancing.html