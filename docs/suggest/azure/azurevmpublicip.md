# Azure VM虚拟机公网IP检测

!!! info "检查规则说明"
    Azure  检测您账号下的VM是否开放公网IP，不开放视为“合规”，否则视为“不合规”
    
```YAML
policies:
# 检测您账号下的VM是否开放公网IP，不开放视为“合规”，否则视为“不合规”
- name: azure-vms-with-public-ip
    resource: azure.vm
    filters:
    - type: network-interface
    key: 'properties.ipConfigurations[].properties.publicIPAddress.id'
    value: ${{value}}
```

    
!!! info "处置方案"
    
    我们以 Azure 控制台为例，在控制台中处理问题 。



!!! info "操作步骤"





!!! info "帮助资源"
    