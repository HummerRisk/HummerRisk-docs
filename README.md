本仓库保存了 [hummerrisk 项目]() 的 [官方文档](https://docs.hummerrisk.com)，该文档使用 [MkDocs]() 文档框架下的 [Material for MkDocs]() 主题进行构建。

---
## 一、开发环境准备
### 克隆本仓库
```sh
git clone https://github.com/hummerrisk/hummerrisk-docs.git
```

### 运行方式1. 使用 Docker 运行
本地运行环境
```shell
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs registry.cn-beijing.aliyuncs.com/hummerrisk/mkdocs-material:8.4.2
```
本地构建
```shell
docker run --rm -it -v ${PWD}:/docs registry.cn-beijing.aliyuncs.com/hummerrisk/mkdocs-material:8.4.2 build
```
执行上述命令后，会在 `site` 目录下生成文档站点的静态文件，将目录中的内容复制到任意 HTTP 服务器上即可完成文档的部署。

---
### 运行方式2. 本地手动模式
#### 安装依赖

```sh
cd docs
pip3 install -r requirements/requirements.txt
```

#### 运行调试
```sh
pip3 install mkdocs 
mkdocs --version
pip3 install mkdocs-material
mkdocs serve
```
执行上述命令后，可通过 `http://127.0.0.1:8000` 地址查看生成的文档内容，当修改文档后，页面内容会自动更新。

#### 构建文档

```sh
mkdocs build
```
执行上述命令后，会在 `site` 目录下生成文档站点的静态文件，将目录中的内容复制到任意 HTTP 服务器上即可完成文档的部署。


## 二、修改文档内容

本文档的文档结构定义在 `mkdocs.yml` 文件中，文档的具体内容均在 `docs` 目录中。

```yaml
nav:
  - 产品介绍: index.md
  - 系统架构:
      - 架构升级说明: architecture/upgrade.md
      - 微服务版架构: architecture/architecture2.md
      - 单机版架构: architecture/architecture.md
  - 快速入门: quick/quickstart.md
  - 安装部署:
      - 在 Linux 主机上安装:
          - 环境要求: system/microservice-env-requirements.md
          - 安装部署: system/microservice-setup-by-fast.md
          - 备份升级: system/microservice-upgrade.md
      - 在 K8s 上安装:
          - 安装部署: system/microservice-k8s-setup-by-fast.md
          - 备份升级: system/microservice-k8s-upgrade.md
      - 安装 operator: system/k8s-scan.md
  - 功能手册:
      - 使用流程: user/process.md
      - 首页: user/dashboard.md
      - 混合云安全:
          - 资源态势: user/cloud-situation.md
          - 多云检测: user/account.md
          - 合规报告: user/report.md
          - 操作审计: user/event.md
          - 对象存储: user/oss.md
      - 云原生安全:
          - 资源态势: user/k8s-situation.md
          - 主机检测: user/server.md
          - K8s 检测: user/k8s.md
          - 部署检测: user/config.md
          - 镜像检测: user/image.md
          - 源码检测: user/code.md
          - 文件检测: user/fs.md
          - SBOM 管理: user/sbom.md
      - 检测管理:
          - 检测规则: user/rule.md
          - 检测结果: user/resource.md
      - 系统设置: user/settings.md
  - 教学视频: video/video.md
  - 常见问题:
      - 混合云账号校验失败问题: question/cloud.md
      - 多云检测结果状态不停问题: question/rule.md
      - 漏洞里报错需要更新漏洞库: question/updateDb.md
      - K8s 账号校验失败问题: question/k8s.md
      - K8s Operator 校验失败问题: system/k8s-scan.md
      - 页面报错到哪去查看log: question/log.md
      - 安装 Azure CL 并生成 service principal 文件: question/azure.md
      - 等级保护: question/grade-protection.md
      - 安全基线: question/cis.md
      - 开启企业微信通知: question/weixin-settings.md
      - 开启钉钉消息通知: question/dingtalk-settings.md
  - 开发文档:
      - 开发手册(微服务): develop/dev-manual2.md
      - 开发手册(单机版): develop/dev-manual.md
      - 如何自定义云资源检测规则: develop/rule.md
      - 自定义阿里云监控规则示例: develop/example.md
  - 技术文章:
      - 开源工具系列:
          - 开源工具系列(一) Custodian: related/opensource-tool/custodian.md
          - 开源工具系列(二) Trivy: related/opensource-tool/trivy.md
          - 开源工具系列(三) Prowler: related/opensource-tool/prowler.md
          - 开源工具系列(四) Nuclei: related/opensource-tool/nuclei.md
          - 开源工具系列(五) Xray: related/opensource-tool/xray.md
          - 开源工具系列(六) DependencyCheck: related/opensource-tool/dependency.md
          - 开源工具系列(七) Grype: related/opensource-tool/grype.md
          - 开源工具系列(八) Syft: related/opensource-tool/syft.md
          - 开源工具系列(九) Kube-bench: related/opensource-tool/kube-bench.md
          - 开源工具系列(十) Nacos: related/opensource-tool/nacos.md
          - 开源工具系列(十一) Spring Security: related/opensource-tool/spring-security.md
      - 云原生安全系列:
          - 云原生安全系列 1：零信任安全和软件开发生命周期: related/cloudnativesecurity/cloudnativesec-series1.md
          - 云原生安全系列 2：关于镜像安全必须知道的事儿: related/cloudnativesecurity/cloudnativesec-series2.md
          - 云原生安全系列 3：5个 Kubernetes API 网络安全访问最佳实践: related/cloudnativesecurity/cloudnativesec-series3.md
          - 云原生安全系列 4：6个 Kubernetes 安全最佳实践: related/cloudnativesecurity/cloudnativesec-series4.md
          - 云原生安全系列 5：ETCD 安全加固: related/cloudnativesecurity/cloudnativesec-series5.md
      - 云安全系列:
          - 云安全系列 1：深度解析云安全责任共担模型: related/cloudsecurity/cloudsec-series1.md
          - 云安全系列 2：访问安全和身份管理: related/cloudsecurity/cloudsec-series2.md
          - 云安全系列 3：如何构建云安全策略: related/cloudsecurity/cloudsec-series3.md
          - 云安全系列 4：解析云安全工具集: related/cloudsecurity/cloudsec-series4.md
      - 安全检测场景:
          - 安全检测场景 3：云原生安全检测: related/scenes/cloudnative1.md
  - 优化建议:
      - 阿里云:
          - ACK 删除保护检测:  suggest/aliyun/ack-deletion-protection.md
          - CDN 域名 HTTPS 监听检测:  suggest/aliyun/cdn-https.md
          - Disk 磁盘加密状态检测:  suggest/aliyun/disk-encrypt.md
          - ECS 实例公网 IP 检测:  suggest/aliyun/ecs-public-ip.md
          - ECS 实例网络类型检测:  suggest/aliyun/ecs-net-type.md
          - ECS VPC 检测:  suggest/aliyun/ecs-vpc.md
          - EIP 带宽峰值检测:  suggest/aliyun/eip-bandwidth.md
          - Event 事件跟踪检测:  suggest/aliyun/event-trail.md
          - MongoDB 实例网络类型检测:  suggest/aliyun/mongodb-net-type.md
          - MongoDB 实例公网访问检测:  suggest/aliyun/mongodb-public-ip.md
          - MSE VPC 检测:  suggest/aliyun/mse-vpc.md
          - NAS 带宽峰值检测: suggest/aliyun/nas-bandwidth.md
          - NAS 磁盘加密状态检测: suggest/aliyun/nas-encrypted.md
          - OSS 防盗链检测:  suggest/aliyun/oss-referer.md
          - OSS 公开写入访问权限检测:  suggest/aliyun/oss-public-write.md
          - OSS 对象存储桶冗余存储检测:  suggest/aliyun/oss-data-redundancy-type.md
          - OSS 公开读取访问权限检测:  suggest/aliyun/oss-public-read.md
          - OSS 存储桶加密检测:  suggest/aliyun/oss-encrypt.md
          - Polardb VPC 检测:  suggest/aliyun/polardb-vpc.md
          - PolarDB 实例网络类型检测:  suggest/aliyun/polardb-net-type.md
          - PolarDB 实例公网访问检测:  suggest/aliyun/polardb-public-ip.md
          - RAM 用户 MFA 检测: suggest/aliyun/ram.md
          - RDS 实例网络类型检测:  suggest/aliyun/rds-net-type.md
          - RDS 实例高可用状态检测:  suggest/aliyun/rds-ha.md
          - RDS 实例公网访问检测:  suggest/aliyun/rds-public-ip.md
          - RDS 实例多可用区检测:  suggest/aliyun/rds-available-zones.md
          - RDS VPC 检测:  suggest/aliyun/rds-vpc.md
          - RDS 实例白名单检测:  suggest/aliyun/rds-white-list.md
          - RDS 实例的访问模式检测:  suggest/aliyun/rds-connection-mode.md
          - Redis 实例网络类型检测:  suggest/aliyun/redis-net-type.md
          - Redis 实例公网访问检测:  suggest/aliyun/redis-public-ip.md
          - SecurityGroup 安全组配置检测:  suggest/aliyun/security-group-config.md
          - SecurityGroup 安全组端口访问检测:  suggest/aliyun/security-group-port.md
          - SecurityGroup 高危安全组检测:  suggest/aliyun/security-group-high-risk-port.md
          - SLB 带宽峰值检测:  suggest/aliyun/slb-bandwidth.md
          - SLB VPC 检测:  suggest/aliyun/slb-vpc.md
          - SLB 公网访问检测:  suggest/aliyun/slb-public-ip.md
          - SLB 负载均衡实例关联到 VPC 检测:  suggest/aliyun/slb-bind-vpc.md
          - SLB 负载均衡监听检测:  suggest/aliyun/slb-listener.md
          - SLB 负载均衡 HTTPS 监听检测:  suggest/aliyun/slb-https.md
          - SLB 负载均衡实例公网 IP 检测:  suggest/aliyun/slb-bind-public-ip.md
      - 华为云:
          - DDS 实例公网访问检测: suggest/huawei/dds-public-network.md
          - Disk 磁盘加密状态检测: suggest/huawei/disk-encrypted.md
          - ECS 实例公网 IP 检测: suggest/huawei/ecs-public-ip.md
          - ECS 实例网络类型检测: suggest/huawei/ecs-network-type.md
          - EIP 带宽峰值检测: suggest/huawei/eip-bandwidth.md
          - ELB 负载均衡 HTTPS 监听检测: suggest/huawei/elb-https-listener.md
          - ELB 实例关联云服务器组检测: suggest/huawei/elb-bind-ecs.md
          - ELB 实例绑定公网 IP 检测: suggest/huawei/elb-public-ip.md
          - GaussDB 实例公网访问检测: suggest/huawei/gauss-db-internet-access.md
          - GaussDB 实例计费类型检测: suggest/huawei/gauss-db-cost-type.md
          - GaussDB 实例高可用状态检测: suggest/huawei/gauss-db-ha.md
          - GaussDB 实例磁盘空间检测: suggest/huawei/gauss-db-disk.md
          - GaussDB 实例网络类型检测: suggest/huawei/gauss-db-network-type.md
          - GaussDBForOpenGauss 实例网络类型检测: suggest/huawei/gauss-db-for-open-gauss-network-type.md
          - GaussDBForOpenGauss 实例公网访问检测: suggest/huawei/gauss-db-for-open-gauss-internet-access.md
          - GaussDBForOpenGauss 实例高可用状态检测: suggest/huawei/gauss-db-for-open-gauss-ha.md
          - GaussDBForOpenGauss 实例磁盘空间检测: suggest/huawei/gauss-db-for-open-gauss-disk.md
          - GaussDBForOpenGauss 实例计费类型检测: suggest/huawei/gauss-db-for-open-gauss-cost-type.md
          - GaussDBForNoSQL 实例网络类型检测: suggest/huawei/gauss-db-for-nosql-network-type.md
          - GaussDBForNoSQL 实例计费类型检测: suggest/huawei/gauss-db-for-nosql-cost-type.md
          - GaussDBForNoSQL 实例高可用状态检测: suggest/huawei/gauss-db-for-nosql-ha.md
          - GaussDBForNoSQL 实例公网访问检测: suggest/huawei/gauss-db-for-nosql-public-network.md
          - GaussDBForNoSQL 实例磁盘空间检测: suggest/huawei/gauss-db-for-nosql-disk.md
          - IAM 用户是否登录保护检测: suggest/huawei/iam-login.md
          - OBS 公开读取访问权限检测: suggest/huawei/obs-read.md
          - OBS 公开写入访问权限检测: suggest/huawei/obs-write.md
          - RDS 实例计费类型检测: suggest/huawei/rds-cost-type.md
          - RDS 实例磁盘空间检测: suggest/huawei/rds-disk.md
          - RDS 实例公网访问检测: suggest/huawei/rds-public-network.md
          - RDS 实例网络类型检测: suggest/huawei/rds-network-type.md
          - RDS 实例高可用状态检测: suggest/huawei/rds-ha.md
          - Redis 实例公网访问检测: suggest/huawei/redis-unencrypt.md
          - Redis 实例免密码访问检测: suggest/huawei/redis-internet-access.md
          - SecurityGroup 安全组配置检测: suggest/huawei/security-group-config.md
          - SecurityGroup 高危安全组检测: suggest/huawei/security-group-high-risk-port.md
      - 腾讯云:
          - CVM 实例关机计费模式检测: suggest/tencent/cvm-billing.md
          - CVM 实例公网 IP 检测: suggest/tencent/cvm-public-network-ip.md
          - COS 防盗链检测: suggest/tencent/cos-antileech.md
          - COS 公开写入访问权限检测: suggest/tencent/cos-public-write-access-permission.md
          - COS 公开读取访问权限检测: suggest/tencent/cos-public-read-access-permission.md
          - COS 存储桶加密检测: suggest/tencent/cos-bucket-encryption.md
          - CDB 实例网络类型检测: suggest/tencent/cdb-network-type.md
          - CDB 实例高可用状态检测: suggest/tencent/cdb-ha-status.md
          - CDB 实例公网访问检测: suggest/tencent/cdb-public-network-access.md
          - CDB 实例多可用区检测: suggest/tencent/cdb-multi-zone.md
          - CLB 带宽峰值检测: suggest/tencent/clb-bandwidth.md
          - CLB 公网访问检测: suggest/tencent/clb-public-network-access.md
          - CLB 负载均衡实例 VPC 检测: suggest/tencent/clb-associated-with-vpc.md
          - Disk 磁盘加密检测: suggest/tencent/disk-encryption.md
          - EIP 带宽峰值检测: suggest/tencent/eip-bandwidth.md
          - Redis 实例网络类型检测: suggest/tencent/redis-network-type.md
          - SecurityGroup 配置检测: suggest/tencent/securitygroup-configuration.md
          - SecurityGroup 高危检测: suggest/tencent/securitygroup-highrisk-configuration.md
          - MongoDB 实例网络类型检测: suggest/tencent/mongodb-instance-network-type.md
          - MongoDB 实例公网访问检测: suggest/tencent/mongodb-public-network.md
      - AWS:
          - AWS EC2 实例关机状态检测: suggest/aws/aws-stopped-instance.md
          - AWS EC2 标签规范检测: suggest/aws/aws-ec2-tagged.md
          - AWS EC2 运行时间检测: suggest/aws/aws-ec2-runnningtime.md
          - AWS EC2 CPU 使用率检测: suggest/aws/aws-ec2-usage.md
          - AWS EBS 未使用检测: suggest/aws/aws-ebs-unattached.md
          - AWS EBS 加密检测: suggest/aws/aws-ebs-encrypted.md
          - AWS EIP 未使用检测: suggest/aws/aws-eip-unattached.md
          - AWS ELB SSL 黑名单检测: suggest/aws/aws-elb-sslblacklist.md
          - AWS ELB 实例使用检测: suggest/aws/aws-elb-unattached.md
          - AWS RDS 实例加密检测: suggest/aws/aws-rds-encrypted.md
          - AWS RDS 实例公网访问检测: suggest/aws/aws-rds-public-access.md
          - AWS RDS 实例是否使用检测: suggest/aws/aws-rds-unused.md
          - AWS S3 全局访问检测: suggest/aws/aws-s3-global-grants.md
          - AWS S3 公开读写访问权限检测: suggest/aws/aws-s3-public-access.md
          - AWS SecurityGroup 高危安全组检测: suggest/aws/aws-securitygroup-check.md
      - Azure:
          - Azure App Services CORS配置检测: suggest/azure/azure-app-cors.md
          - Azure Cosmos DB 检测: suggest/azure/azure-cosmosdb.md
          - Azure Disk 关联虚拟机检测: suggest/azure/azure-unused-disk.md
          - Azure LoadBalancer 负载均衡器检测: suggest/azure/azure-loadbalancer-publicip.md
          - Azure SQL 数据库保留策略检测: suggest/azure/azure-sql-database.md
          - Azure SQL Server 使用率检测: suggest/azure/azure-sqlserver-usage.md
          - Azure VM 虚拟机状态检测: suggest/azure/azure-stopped-vm.md
          - Azure VM 虚拟机公网 IP 检测: suggest/azure/azure-vm-publicip.md
          - Azure VM 虚拟机使用率检测: suggest/azure/azure-vm-usage.md
          - Azure 存储账户检测: suggest/azure/azure-storage-allowip.md
          - Azure 存储公网访问检测: suggest/azure/azure-storage-public-access.md
          - Azure 公网 IP 地址 DDoS 攻击检测: suggest/azure/azure-publicip-ddos.md
          - Azure 网络接口连接检测: suggest/azure/azure-network-interface.md
          - Azure 网络安全组检测: suggest/azure/azure-network-securitygroup.md
          - Azure 资源组检测: suggest/azure/azure-rg-empty.md
      - GCP:
          - Google Cloud DNS 区域的资源检测: suggest/gcp/gcp-dns-managed-zones.md
          - Google Cloud DNS 策略日志记录检测: suggest/gcp/gcp-dns-policies-if-logging-disabled.md
          - Google Cloud SSL 证书过期检测: suggest/gcp/gcp-appengine-certificate.md
          - Google Cloud SQL 实例检测: suggest/gcp/gcp-sql-backup-run.md
          - Google Cloud 部署管理器检测: suggest/gcp/gcp-expired-deployments.md
          - Google Cloud 防火墙入口规则配置检测: suggest/gcp/gcp-appengine-firewall-ingress.md
          - Google Cloud 防火墙规则检测: suggest/gcp/gcp-appengine-firewall-rules.md
          - Google Cloud 负载均衡器检测: suggest/gcp/gcp-load-balancing-ssl-policies.md
          - Google Cloud 实例模板检测: suggest/gcp/gcp-instance-template.md
          - Google Cloud 域使用状态检测: suggest/gcp/gcp-appengine-blacklist.md
      - VMware:
          - VMware vSphere Cluster 高可用状态检测: suggest/vsphere/cluster.md
          - VMware vSphere Datacenter 关联资源检测: suggest/vsphere/datacenter.md
          - VMware vSphere Datastore 多主机访问检测: suggest/vsphere/datastore.md
          - VMware vSphere Datastore 可用空间检测: suggest/vsphere/datastore-available.md
          - VMware vSphere Datastore 精简配置检测: suggest/vsphere/datastore-config.md
          - VMware vSphere Host 电源状态检测: suggest/vsphere/host.md
          - VMware vSphere Host 连接状态检测: suggest/vsphere/host-connect-status.md
          - VMware vSphere Network 分布式类型检测: suggest/vsphere/network-status.md
          - VMware vSphere ResourcePool CPU 内存检测: suggest/vsphere/resource-pool.md
          - VMware vSphere VM 状态检测: suggest/vsphere/vm-status.md
      - OpenStack:
          - OpenStack 网络状态检测: suggest/openstack/network-status.md
          - OpenStack 项目成员检测: suggest/openstack/project-member.md
          - OpenStack 实例类型检测: suggest/openstack/server-type.md
          - OpenStack 实例标签检测: suggest/openstack/server-tag.md
          - OpenStack 实例镜像检测: suggest/openstack/server-image.md
          - OpenStack 实例时间检测: suggest/openstack/server-time.md
          - OpenStack 用户项目检测: suggest/openstack/user-project.md
          - OpenStack 用户角色检测: suggest/openstack/user-role.md
          - OpenStack 卷加密检测: suggest/openstack/volume-encrypt.md
          - OpenStack 卷状态检测: suggest/openstack/volume-status.md
          - OpenStack 模板类型检测: suggest/openstack/flavor-type.md
          - OpenStack 路由状态检测: suggest/openstack/router-status.md
          - OpenStack 镜像状态检测: suggest/openstack/image-status.md
          - OpenStack SecurityGroups 安全组配置检测: suggest/openstack/security-groups-config.md
          - OpenStack SecurityGroups 高危安全组检测: suggest/openstack/security-groups-high-risk-port.md
      - 百度云:
          - BBC 实例公网 IP 检测: suggest/baidu/bbc-public-network-ip.md
          - BBC 实例带宽检测: suggest/baidu/bbc-bandwidth.md
          - BCC 实例公网 IP 检测: suggest/baidu/bcc-public-network-ip-monitoring.md
          - BCC 实例网络类型检测: suggest/baidu/bcc-network-type.md
          - BCC VPC 检测: suggest/baidu/bcc-vpc.md
          - CDN 域名 HTTPS 监听检测: suggest/baidu/cdn-domain-https-monitoring.md
          - EIP 带宽峰值检测: suggest/baidu/eip-bandwidth.md
          - SecurityGroup 安全组端口访问: suggest/baidu/securityGroup-port-access.md
          - 磁盘加密状态检测: suggest/baidu/disk-encryption.md
          - 普通型负载公网 IP 绑定检测: suggest/baidu/common-public-network-ip.md
          - 应用型负载公网 IP 绑定检测: suggest/baidu/alb-public-network-ip.md
      - 火山引擎:
          - CDN 域名 HTTPS 监听检测: suggest/volc/cdn-https.md
          - ECS VPC 检测: suggest/volc/ecs-vpc.md
          - ECS 实例网络类型检测: suggest/volc/ecs-net-type.md
          - ECS 实例公网 IP 检测: suggest/volc/ecs-public-ip.md
          - EIP 带宽峰值检测: suggest/volc/eip-bandwidth.md
          - MongoDB 实例公网访问检测: suggest/volc/mongodb-public-ip.md
          - MongoDB 实例网络类型检测: suggest/volc/mongodb-net-type.md
          - SecurityGroup 安全组端口访问检测: suggest/volc/securitygroup-port.md
          - SecurityGroup 高危安全组检测: suggest/volc/securitygroup-high-risk-port.md
      - 青云:
          - ECS 实例公网 IP 检测: suggest/qingcloud/ecs-public-network-ip.md
          - ECS VPC 检测: suggest/qingcloud/ecs-vpc.md
          - ECS 实例网络类型检测: suggest/qingcloud/ecs-network-type.md
          - EIP 带宽峰值检测: suggest/qingcloud/eip-bandwidth.md
          - MongoDB 实例公网访问检测: suggest/qingcloud/mongodb-public-network.md
          - MongoDB 实例网络类型检测: suggest/qingcloud/mongodb-network-type.md
          - MySQL 实例网络类型检测: suggest/qingcloud/mysql-network-type.md
          - MySQL 实例公网访问检测: suggest/qingcloud/mysql-public-network-access.md
          - MySQL 实例高可用状态检测: suggest/qingcloud/mysql-ha.md
      - UCloud:
          - EIP 带宽峰值检测: suggest/ucloud/eip-bandwidth.md
          - UHost 公网 IP 检测: suggest/ucloud/uhost-eip.md
          - UHost VPC 检测: suggest/ucloud/uhost-vpc.md
          - UHost 网络类型检测: suggest/ucloud/uhost-network-type.md
          - UHost 挂载磁盘加密检测: suggest/ucloud/uhost-disk-encryption.md
          - ULB 负载均衡 HTTPS 监听检测: suggest/ucloud/ulb-listener.md
          - ULB VPC 检测: suggest/ucloud/ulb-vpc-type.md
          - ULB 带宽峰值检测: suggest/ucloud/ulb-bandwidth.md
          - ULB 负载均衡监听检测: suggest/ucloud/ulb-listener-type.md
          - SecurityGroup 安全组配置检测: suggest/ucloud/sg-source-cidr-ip.md
          - SecurityGroup 安全组端口访问检测: suggest/ucloud/sg-ports.md
          - SecurityGroup 高危安全组检测: suggest/ucloud/sg-high-risk-port.md
  - 版本迭代:
      - 更新日志: about/changelog.md
      - 更新说明:
          - ReleaseNote 1.0.0: release/release-1.0.0.md
          - ReleaseNote 0.10.0: release/release-0.10.0.md
          - ReleaseNote 0.9.1: release/release-0.9.1.md
          - ReleaseNote 0.9.0: release/release-0.9.0.md
          - ReleaseNote 0.8.0: release/release-0.8.0.md
          - ReleaseNote 0.7.0: release/release-0.7.0.md
          - ReleaseNote 0.6.0: release/release-0.6.0.md
          - ReleaseNote 0.5.2: release/release-0.5.2.md
          - ReleaseNote 0.5.1: release/release-0.5.1.md
          - ReleaseNote 0.5.0: release/release-0.5.0.md
          - ReleaseNote 0.4.1: release/release-0.4.1.md
          - ReleaseNote 0.4.0: release/release-0.4.0.md
          - ReleaseNote 0.3.2: release/release-0.3.2.md
          - ReleaseNote 0.3.1: release/release-0.3.1.md
          - ReleaseNote 0.3.0: release/release-0.3.0.md
          - ReleaseNote 0.2.2: release/release-0.2.2.md
          - ReleaseNote 0.2.1: release/release-0.2.1.md
          - ReleaseNote 0.2.0: release/release-0.2.0.md
  - 关于我们:
      - 联系我们: about/contact.md
  - 资源下载: about/download.md
```

文档内容使用 markdown 语法编写，若要添加新的文档，需要先在 `mkdocs.yml` 文件中的 `nav` 部分增加对应章节导航。


## 三、帮助完善文档

### Fork 文档仓库

点击仓库右上角的 `fork` 按钮，复制本仓库到自己的 github 账号。

### 克隆 fork 后的仓库

```sh
git clone https://github.com/your-github-account/docs.git
```

### 本地修改并调试

### Push 修改内容到 GitHub 仓库

### 提交 Pull Request 到本仓库
