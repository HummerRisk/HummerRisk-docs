# AWS EC2标签规范检测

!!! info "检查规则说明"
    在 AWS 的管理最佳实践下，每个 EC2 实例都应该打上合理的标签，以进行管理。本规则是一个实例，检测您账号下的EC2实例是否打了符合要求的标签。。
    这里我们定义所有的主机应该具备3个必要标签：Owner，CostCenter，Project。本规则检测所有非 autoscaling 实例，是否都已具备这3个标签，如果标签完备视为“合规”，否则视为“不合规”

    ```YAML
    policies:
    # 检测您账号下的EC2实例是否符合标签规范（非ASG），符合视为“合规”，否则视为“不合规”
    - name: aws-ec2-tag
        resource: aws.ec2
        comment: |
        Find all (non-ASG) instances that are not conformant
        to tagging policies.
        filters:
        - "tag:aws:autoscaling:groupName": absent
        - "tag:c7n_status": absent
        - or:
            - "tag:Owner": ${{Owner}}
            - "tag:CostCenter": ${{CostCenter}}
            - "tag:Project": ${{Project}}
    ```

!!! info "处置方案"
    您可以使用 AWS 控制台、AWS Command Line Interface (CLI)、REST API 来执行具体的操作。   
    我们以 AWS 控制台为例，在控制台中为 EC2 实例补全必要标签 。

    *注意：
    关于 AWS 中标签的使用，可以参考最佳实践介绍：https://d1.awsstatic.com/whitepapers/aws-tagging-best-practices.pdf*


!!! info "操作步骤"

    * 1.登录 AWS 管理控制台，通过导航菜单进入 EC2 控制面板。 https://console.aws.amazon.com/ec2/ 
    * 2.在导航窗格中，选择资源类型 (例如，实例 Instances)。
    * 3.在 EC2 实例列表中找到 HummerRisk 检测结果中对应的实例，然后选择标签选项卡。
    * 4.依次选择管理标签、添加标签。输入标签的键和值。完成添加标签后，选择保存。

    
    可以通过标签管理来给一组资源添加标签

    * 1.在导航窗格中，选择 标签。
    * 2.在内容窗格的顶部，选择 管理标签。
    * 3.对于筛选条件，选择资源类型（例如，实例）。
    * 4.在资源列表中，选中每个资源旁边的复选框。
    * 5.在添加标签下，输入标签的键和值，然后选择添加标签。





!!! info "帮助资源"
    
    https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/Using_Tags.html