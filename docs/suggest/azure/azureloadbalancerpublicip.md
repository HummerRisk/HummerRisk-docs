# Azure LoadBalancer负载均衡器检测

!!! info "检查规则说明"
    Azure  检测您账号下的负载均衡器是否开放了公网IP，未开放视为“合规”，否则视为“不合规”
    
```YAML
policies:
   # 检测您账号下的负载均衡器是否开放了公网IP，未开放视为“合规”，否则视为“不合规”
   - name: azure-loadbalancer-with-ipv6-frontend
     resource: azure.loadbalancer
     filters:
        - type: frontend-public-ip
          key: properties.publicIPAddressVersion
          op: in
          value_type: normalize
          value: "ipv6"
```

    
!!! info "处置方案"
    
    我们以 Azure 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    