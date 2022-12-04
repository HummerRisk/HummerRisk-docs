
### Cloud Custodian

!!! info "项目地址"
    * Github 项目地址：https://github.com/hummerrisk/cloud-custodian/tree/hummerrisk
    * Cloud Custodian 官方文档：https://cloudcustodian.io/docs/index.html

#### 一、Cloud Custodian 是什么

!!! abstract "Cloud Custodian 是什么"
    * Cloud Custodian 是用于管理公有云帐户和资源的规则引擎。规则策略用简单的 YAML 格式，使用户能够指定资源类型（EC2、ASG、Redshift、CosmosDB、PubSub 主题）的策略，并由过滤器和操作的词汇表构建。
    * 官方的 Cloud Custodian 可用于管理 AWS、Azure 和 GCP 环境，我们在此基础上新增了阿里云、华为云、腾讯云、火山云、金山云、百度云、青云、七牛云、UCloud、OpenStack、VMware vSphere等。

#### 二、Cloud Custodian 项目结构

```
.
├── c7n                                           # c7n基础 aws
├── docker                                        # docker
├── docs
├── tests
├── tools                                         # 其他平台
│   ├── c7n_aliyun                                # 阿里云
│   ├── c7n_azure                                 # Azure          
│   ├── c7n_gcp                                   # Google Cloud
│   ├── c7n_huawei                                # 华为云
│   ├── c7n_kube                                  # k8s
│   ├── c7n_openstack                             # OpenStack
│   ├── c7n_tencent                               # 腾讯云
│   └── c7n_vsphere                               # VMware vSphere
├── pyproject.toml
├── poetry.lock
├── requirements.txt
└── setup.py                                       
```

!!! abstract "Custodian 特征"
    * 对公共云服务和资源的全面支持，具有丰富的操作和过滤器库，可用于构建策略。
    * 支持对具有嵌套布尔条件的资源进行任意过滤。
    * 试运行任何政策，看看它会做什么。
    * 自动配置无服务器函数和事件源（AWS CloudWatchEvents、AWS Config Rules、Azure EventGrid、GCP AuditLog 和 Pub/Sub 等）
    * 与策略匹配的资源上的云提供商本机指标输出
    * 将结构化输出到云原生对象存储中，其资源与策略相匹配。
    * 智能缓存使用以最小化 api 调用。
    * 支持多账户/订阅/项目使用。
    * 经过实战测试 - 在一些非常大的云环境中进行生产。

#### 三、Cloud Custodian 快速安装

!!! tip "快速安装"
        ```bash
        $ python3 -m venv custodian
        $ source custodian/bin/activate
        (custodian) $ pip install c7n
        (custodian) $ pip install -e tools/c7n_aliyun
        ```

#### 四、Cloud Custodian 用法

使用 Cloud Custodian 的第一步是编写包含您要运行的策略的 YAML 文件。每个策略指定策略将运行的资源类型，一组控制资源将受此策略影响的过滤器，策略对匹配资源采取的操作，以及控制策略执行方式的模式。

最好的入门指南是云提供商特定的教程。

!!! tip "作为快速浏览，下面是 AWS 资源的一些示例策略"
    1. 将强制所有 S3 存储桶都没有启用跨账户访问。
    2. 将终止任何新启动的没有加密 EBS 卷的 EC2 实例。
    3. 将在四天内停止任何没有跟随标签“Environment”、“AppId”和“OwnerContact”或“DeptID”的 EC2 实例。
    ```bash
    policies:
      - name: s3-cross-account
        description: |
          Checks S3 for buckets with cross-account access and
          removes the cross-account access.
        resource: aws.s3
        region: us-east-1
        filters:
          - type: cross-account
        actions:
          - type: remove-statements
            statement_ids: matched

      - name: ec2-require-non-public-and-encrypted-volumes
        resource: aws.ec2
        description: |
          Provision a lambda and cloud watch event target
          that looks at all new instances and terminates those with
          unencrypted volumes.
        mode:
          type: cloudtrail
          role: CloudCustodian-QuickStart
          events:
          - RunInstances
        filters:
          - type: ebs
            key: Encrypted
            value: false
        actions:
          - terminate

      - name: tag-compliance
        resource: aws.ec2
        description: |
          Schedule a resource that does not meet tag compliance policies to be stopped in four days. Note a separate policy using the`marked-for-op` filter is required to actually stop the instances after four days.
        filters:
          - State.Name: running
          - "tag:Environment": absent
          - "tag:AppId": absent
          - or:
            - "tag:OwnerContact": absent
            - "tag:DeptID": absent
        actions:
          - type: mark-for-op
            op: stop
            days: 4
    ```

!!! tip "您可以使用以下命令使用示例策略验证、测试和运行 Cloud Custodian"
    ```bash
    # Validate the configuration (note this happens by default on run)
    $ custodian validate policy.yml
    
    # Dryrun on the policies (no actions executed) to see what resources
    # match each policy.
    $ custodian run --dryrun -s out policy.yml
    
    # Run the policy
    $ custodian run -s out policy.yml
    ```

!!! tip "您也可以通过 Docker 运行 Cloud Custodian"
    ```bash
    # Download the image
    $ docker pull cloudcustodian/c7n
    $ mkdir output
    
    # Run the policy
    #
    # This will run the policy using only the environment variables for authentication
    $ docker run -it \
    -v $(pwd)/output:/home/custodian/output \
    -v $(pwd)/policy.yml:/home/custodian/policy.yml \
    --env-file <(env | grep "^AWS\|^AZURE\|^GOOGLE") \
    cloudcustodian/c7n run -v -s /home/custodian/output /home/custodian/policy.yml
    
    # Run the policy (using AWS's generated credentials from STS)
    #
    # NOTE: We mount the ``.aws/credentials`` and ``.aws/config`` directories to
    # the docker container to support authentication to AWS using the same credentials
    # credentials that are available to the local user if authenticating with STS.
    
    $ docker run -it \
    -v $(pwd)/output:/home/custodian/output \
    -v $(pwd)/policy.yml:/home/custodian/policy.yml \
    -v $(cd ~ && pwd)/.aws/credentials:/home/custodian/.aws/credentials \
    -v $(cd ~ && pwd)/.aws/config:/home/custodian/.aws/config \
    --env-file <(env | grep "^AWS") \
    cloudcustodian/c7n run -v -s /home/custodian/output /home/custodian/policy.yml
    ```

!!! warning "目前 HummerRisk 所使用的 Cloud Custodian 为二开项目，暂未开源，有需要者请联系管理员"
    邮箱：support@hummercloud.com
