# Google Cloud 负载均衡器检测

!!! info "检查规则说明"
    Google Cloud 检测账号下负载均衡器是否有 TLS 1.2 版的 SSL 策略，符合的视为“合规”，否则属于“不合规”
    
    ```YAML
    policies:
        # 检测账号下DNS 策略中的日志记录状态，未禁用视为“合规”，否则属于“不合规”
        - name: gcp-dns-policies-if-logging-disabled
        resource: gcp.dns-policy
        filters:
            - type: value
            key: enableLogging
            value: ${{value}}
    ```

    
!!! info "处置方案"
    
    我们以 GCP 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    