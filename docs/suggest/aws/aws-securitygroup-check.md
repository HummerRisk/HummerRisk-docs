# AWS SecurityGroup高危安全组检测

### 检查规则说明
!!! info ""
    检测安全组是否开启风险端口，未开启视为“合规”，否则属于“不合规”

    ```YAML
    policies:
    #检测开放以下高危端口的安全组：
    #(20,21,22,25,80,773,765,1733,1737,3306,3389,7333,5732,5500)
    - name: aws-security-group
        resource: aws.security-group
        description: |
        Add Filter all security groups, filter ports
        [20,21,22,25,80,773,765,1733,1737,3306,3389,7333,5732,5500]
        on 0.0.0.0/0 or
        [20,21,22,25,80,773,765, 1733,1737,3306,3389,7333,5732,5500]
        on ::/0 (IPv6)
        filters:
            - or:
                - type: ingress
                Ports: ${{ipv4_port}}
                Cidr: "0.0.0.0/0"
                - type: ingress
                Ports: ${{ipv6_port}}
                CidrV6: "::/0"
        
    ```
    
### 处置方案
!!! info ""
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""




### 帮助资源
!!! info ""
    
    