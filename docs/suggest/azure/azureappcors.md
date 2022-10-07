# Azure App Services CORS配置检测

!!! info "检查规则说明"
    Azure  检测您的账户下App Services是否所有跨源资源共享（CORS）配置设置为允许所有来源的应用程序服务（Web应用程序和功能），符合视为“合规”，否则视为“不合规”
    
```YAML
policies:
  # 检测您的账户下App Services是否所有跨源资源共享（CORS）配置设置为允许所有来源的应用程序服务（Web应用程序和功能），符合视为“合规”，否则视为“不合规”
  - name: azure-app-service-cors-policy
    resource: azure.webapp
    filters:
      - type: configuration
        key: cors.allowedOrigins
        value: ${{value}}
        op: contains
```

    
!!! info "处置方案"
    
    我们以 Azure 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    