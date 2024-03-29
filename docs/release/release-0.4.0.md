## 1 新功能 Features

### 1.1 云资源态势

!!! abstract "云资源态势"
    如下图所示，新增云资源态势功能，根据云账号同步云资源，进行资源汇总。

![云资源态势](../img/release/0.4.0/cloud1.png){ width="95%" }
![云资源态势](../img/release/0.4.0/cloud2.png){ width="95%" }

### 1.2 云资源态势

!!! abstract "云资源态势"
    如下图所示，新增云资源拓扑图功能，根据同步云资源汇总信息，形成拓扑图。

![云资源态势](../img/release/0.4.0/cloud3.png){ width="95%" }
![云资源态势](../img/release/0.4.0/cloud4.png){ width="95%" }

### 1.3 云检测规则组

!!! abstract "云检测规则组"
    如下图所示，新增阿里云最佳实践规则组，新增规则组直接快速检测功能。

![云检测规则组](../img/release/0.4.0/group.png){ width="95%" }
![云检测规则组](../img/release/0.4.0/group2.png){ width="95%" }

### 1.4 云检测规则

!!! abstract "云检测规则"
    如下图所示，新增 UCloud 、 Aliyun 云检测规则。

![云检测规则](../img/release/0.4.0/rule.png){ width="95%" }

### 1.5 云检测结果

!!! abstract "云检测结果"
    如下图所示，新增云资源检测优化建议功能，根据检测规则跳转优化建议页面。

![云检测结果](../img/release/0.4.0/resource.png){ width="95%" }

### 1.6 操作审计

!!! abstract "操作审计"
    如下图所示，新增操作审计概览、云事件聚合功能。

![操作审计](../img/release/0.4.0/event.png){ width="95%" }
![操作审计](../img/release/0.4.0/event2.png){ width="95%" }

### 1.7 源码检测

!!! abstract "源码检测"
    如下图所示，新增源码概览、源码检测历史记录、历史检测数据对比、下载检测报告功能。

![源码检测](../img/release/0.4.0/code.png){ width="95%" }
![源码检测](../img/release/0.4.0/code2.png){ width="95%" }
![源码检测](../img/release/0.4.0/code3.png){ width="95%" }
![源码检测](../img/release/0.4.0/code4.png){ width="95%" }

### 1.8 部署检测

!!! abstract "部署检测"
    如下图所示，新增部署概览、部署检测历史记录、历史检测数据对比、下载检测报告功能。

![部署检测](../img/release/0.4.0/config.png){ width="95%" }
![部署检测](../img/release/0.4.0/config2.png){ width="95%" }
![部署检测](../img/release/0.4.0/config3.png){ width="95%" }
![部署检测](../img/release/0.4.0/config4.png){ width="95%" }
![部署检测](../img/release/0.4.0/config5.png){ width="95%" }

### 1.9 镜像检测

!!! abstract "镜像检测"
    如下图所示，新增镜像概览、镜像检测历史记录、历史检测数据对比、下载检测报告功能。

![镜像检测](../img/release/0.4.0/image.png){ width="95%" }
![镜像检测](../img/release/0.4.0/image2.png){ width="95%" }
![镜像检测](../img/release/0.4.0/image3.png){ width="95%" }
![镜像检测](../img/release/0.4.0/image4.png){ width="95%" }

### 1.10 主机检测

!!! abstract "主机检测"
    如下图所示，新增主机概览、主机检测历史记录、历史检测数据对比功能。

![主机检测](../img/release/0.4.0/server.png){ width="95%" }
![主机检测](../img/release/0.4.0/server2.png){ width="95%" }
![主机检测](../img/release/0.4.0/server3.png){ width="95%" }

### 1.11 K8s 检测

!!! abstract "K8s 检测"
    如下图所示，新增 K8s 概览、K8s 检测历史记录、历史检测数据对比、下载检测报告功能。

![K8s 检测](../img/release/0.4.0/k8s.png){ width="95%" }
![K8s 检测](../img/release/0.4.0/k8s2.png){ width="95%" }
![K8s 检测](../img/release/0.4.0/k8s3.png){ width="95%" }

### 1.12 K8s 资源态势

!!! abstract "K8s 资源态势"
    如下图所示，新增 K8s 资源拓扑图功能，根据同步 K8s 资源汇总信息，形成拓扑图。

![K8s 资源态势](../img/release/0.4.0/k8sto.png){ width="95%" }

### 1.13 HummerRisk 安装

!!! abstract "HummerRisk 安装"
    如下图所示，新增 K8s 安装部署 HummerRisk。

![HummerRisk 安装](../img/release/0.4.0/install.png){ width="95%" }

## 2 性能优化 Optimization

### 2.1 多云检测

!!! abstract "多云检测"
    优化云账号一键检测，提升检测效率与检测速度。

### 2.2 版本升级

!!! abstract "版本升级"
    升级 pom 依赖包版本，升级 spring-boot 和 jdk 等版本。

### 2.3 检测规则组

!!! abstract "检测规则组"
    优化规则组展示顺序与样式。

### 2.4 主机检测

!!! abstract "主机检测"
    优化主机检测规则，维护有状态检测结果。

### 2.5 站内消息

!!! abstract "站内消息"
    站内消息通知，添加k8s、镜像、源码检测等类型。

### 2.6 树结构

!!! abstract "树结构"
    优化所有页面树结构展示样式与数据结构。

### 2.7 i18n

!!! abstract "i18n"
    优化前后端数据翻译展示。

## 3 Bug修复 Bug Fixes

### 3.1 主机检测

!!! abstract "主机检测"
    修复主机检测只有密码时报错不了的问题。

### 3.2 主机检测

!!! abstract "主机检测"
    解决 server 主机凭证数据没有及时刷新，选择不到的问题。

### 3.3 源码检测

!!! abstract "源码检测"
    解决源码检测，连接 github 仓库时，无法自己修改分支名称。

### 3.4 sbom 分析

!!! abstract "sbom 分析"
    解决 sbom 分析里，镜像检测结果详情显示字段不正确的问题。

### 3.5 sbom 分析

!!! abstract "sbom 分析"
    修复 sbom 列表字段展示问题。

### 3.6 云资源检测

!!! abstract "云资源检测"
    解决分组检测重复检测的问题。

### 3.7 漏洞检测

!!! abstract "漏洞检测"
    修改国家信息安全漏洞库网址(旧址换新址)。

### 3.8 漏洞检测

!!! abstract "漏洞检测"
    修复漏洞检测概览数据显示不正确的问题，解决漏洞检测报错的问题。
