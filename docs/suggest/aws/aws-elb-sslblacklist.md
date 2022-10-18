# AWS ELB SSL 黑名单检测

### 检查规则说明
!!! info ""
    测您账号下ELB SSL policy 黑名单检测，在白名单视为“合规”，黑名单视为“不合规”

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
    用户是用 ELB 并设置了 SSL 时，我们要确定对应的 SSL policy进行了正确的配置，如果用户自己定义了 SSL policy 内容，就要保证其中的协议没有被加入黑名单。   
    在实际使用中可以根据需要，调整检测放入黑名单的协议。
### 处置方案
!!! info ""
    建议是提前在 ELB 中定义好需要的 SSL policy ，在使用时直接使用即可。如果发现协议存在问题，可以根据操作步骤进行更新。
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中处理问题 。


### 操作步骤
!!! info ""
    * 通过以下网址打开 Amazon EC2 控制台：https://console.aws.amazon.com/ec2/。  
    * 在导航窗格上的 Load Balancing（负载均衡）下，选择 Load Balancers（负载均衡器）。  
    * 选择您的负载均衡器。  
    * 在 Listeners 选项卡上，对于 Cipher，选择 Change。  
    * 在 Select a Cipher 页面上，使用以下选项之一选择安全策略：  
      * （建议）选择预定义的安全策略，保留默认策略 ELBSecurityPolicy-2016-08，然后选择保存。  
      * 选择 Predefined Security Policy，选择默认值之外的预定义策略，然后选择 Save。  
      * 选择 Custom Security Policy，然后至少启用一项协议和一个密码，如下所示：  
        * 对于 SSL Protocols，选择要启用的一个或多个协议。  
        * 对于 SSL 选项，选择服务器顺序首选项，以便对 SSL 协商使用预定义 SSL 安全策略中列出的顺序。  
        * 对于 SSL Ciphers，选择要启用的一个或多个密码。如果您已有一个 SSL 证书，则必须启用用于创建该证书的密码，因为 DSA 和 RSA 密码特定于签名算法。  
        * 选择保存。  



### 帮助资源
!!! info ""
    https://docs.aws.amazon.com/zh_cn/elasticloadbalancing/latest/classic/ssl-config-update.html#ssl-config-update-console
    