
### Cloud Custodian

!!! info "项目地址"
    * Github 项目地址：https://github.com/hummerrisk/cloud-custodian/tree/hummerrisk
    * Cloud Custodian 官方文档：https://cloudcustodian.io/docs/index.html

#### 一、Cloud Custodian 是什么

!!! abstract "DependencyCheck 是什么"
    * Cloud Custodian 是用于管理公有云帐户和资源的规则引擎。规则策略用简单的 YAML 格式，使用户能够指定资源类型（EC2、ASG、Redshift、CosmosDB、PubSub 主题）的策略，并由过滤器和操作的词汇表构建。
    * 官方的 Cloud Custodian 可用于管理 AWS、Azure 和 GCP 环境，我们在此基础上新增了阿里云、华为云、腾讯云、OpenStack、VMware vSphere等。

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
