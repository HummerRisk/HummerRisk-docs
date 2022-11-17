# 总体介绍

!!! tip "HummerRisk"
    HummerRisk 是开源的云原生安全平台，以非侵入的方式解决云原生环境的安全和治理问题。核心能力包括混合云的安全治理和容器云安全检测。

## 功能架构图

![系统架构图](./img/index/architecturev.png){ width="95%" }

## HummerRisk 能做什么

### 混合云安全治理

!!! info "混合云安全治理"
    * 多云检测： 对主流的公(私)有云资源进行安全合规检测，例如等保2.0预检、CIS 合规检查、各种基线检测，同时可自定义检测规则；
    * 资源态势： 同步云上资源，快速查看混合云的各种资源态势与云资源拓扑图；
    * 漏洞检测： 基于漏洞规则库，通过扫描等手段对指定的网络设备及应用服务的安全脆弱性进行检测；
    * 合规报告： 根据云资源安全检测结果，一键获取合规报告，全面掌控安全态势；
    * 操作审计： 统一监控多云环境上的账号活动，对云上产品和服务的访问和使用行为的操作日志进行审计；
    * 对象存储： 同步云上对象存储桶资源，查看、上传、下载存储对象。根据对象存储安全与合规要求，快速检测并生成报告。
  
![混合云安全合规](./img/index/multi-cloud.png){ width="95%" }

!!! abstract "优势是什么"
    * 支持全面: 支持的几乎所有公有云，包括：阿里云、腾讯云、华为云、火山引擎、百度云、青云、UCloud、Amazon Web Services、Microsoft Azure、Google Cloud，支持的私有云包括：OpenStack、VMware vSphere，并还在不断的扩充支持的范围；
    * 容易上手: 只需绑定云账号，就可以一键执行检测；
    * 灵活便捷: 多种维度查看检测结果，根据需求任务编排；
    * 开箱即用: 内置大量规则，并且不断迭代新增。用户可以按需自定义规则。 


### 容器云安全检测

!!! info "容器云安全检测"
    * 资源态势： 可以关联多个 K8S 集群，统一查看各个关联环境的资源态势；
    * 主机检测： 可以自定义检测内容，发现底层主机、虚机中存在问题；
    * K8s 检测： 根据 K8S 安全基线进行检测，发现存在的配置错误、安全漏洞、危险动作等内容；
    * 部署检测： 检测 K8S 的部署编排文件，在部署前发现其中的配置问题；
    * 镜像检测： 全面检测镜像相关的漏洞，包括操作系统、软件包、应用程序依赖等方面；
    * 源码检测： 检测开发者的源代码，提前发现其中的开源协议、依赖、漏洞、代码等问题；
    * 文件检测： 检测源码项目中特定的语言文件或文件夹，发现应用程序依赖的漏洞风险；
    * SBOM 管理: SBOM 的可视化管理和分析，检测 SBOM 的变更，快速发现和定位软件供应链中的风险和漏洞，给出合理的处理建议。

![k8s](./img/index/k8s.png){ width="95%" }

!!! abstract "优势是什么"
    * 兼容性: 支持多种 K8s 发行版；
    * 独立性: 中立产品，客观检测；
    * 可靠性: 急速响应，快速准确；
    * 无侵入：无侵入式检测。

## 功能列表

!!! warning "说明：功能后带有 "X-Pack" 标识含义为此功能为企业版本所有，其它核心功能均开源开放。"

<table>
	<tr>
		<td bgcolor="#d4944d" align="middle" style="font-weight:bold;color: white;width: 20%">
			功能模块
		</td>
		<td bgcolor="#d4944d" align="middle" style="font-weight:bold;color: white;width: 20%">
			功能名称
		</td>
		<td bgcolor="#d4944d" align="middle" style="font-weight:bold;color: white;width: 60%"> 
			功能描述
		</td>
	</tr>
	<tr>
		<td rowspan="4">
			首页
		</td>
		<td rowspan="1">
			面板
		</td>
		<td>
			登录进入 HummerRisk 的导航，快速进入混合云安全治理与容器云安全检测场景；
		</td>
	</tr>
    <tr>
		<td rowspan="1">
			总览
		</td>
		<td>
			总览页面展示用户数、账号数、规则数、结果数、任务数、安全评分等信息。以及多云检测统计、漏洞检测统计、主机检测统计、K8s 检测统计、部署检测统计、镜像检测统计、源码检测统计、文件检测统计等，通过日历展示任务执行情况；
		</td>
	</tr>
    <tr>
		<td rowspan="1">
			分析
		</td>
		<td>
			通过用户自定义展示样式与颜色，按分析周期、检测人员、检测类型、检测账号等信息进行分析。通过按检测类型筛选、按检测分组筛选、按检测账号筛选、按风险等级筛选、按检测人员筛选、按时间节点筛选数据，获取检测结果；
		</td>
	</tr>
    <tr>
		<td rowspan="1">
			活动记录
		</td>
		<td>
			活动页面记录并显示了所有的用户主要活动信息，包括操作人、操作、操作描述、资源名称、资源类型、操作 IP、时间等；
		</td>
	</tr>
	<tr>
		<td rowspan="33">
			混合云安全
		</td>
		<td rowspan="3">
			资源态势
		</td>
		<td>
			云资源态势功能，绑定混合云账号信息，即可同步获取云资源汇总信息。执行检测后，可以自动关联云资源态势信息，可以查看到具体哪些资源具有安全合规风险；
		</td>
	</tr>
	<tr>
		<td>
			云资源拓扑图功能，根据同步云资源汇总信息，形成资源拓扑图；
		</td>
	</tr>
	<tr>
		<td>
			云资源同步日志，绑定完混合云账号可以自动获取资源态势信息。同时，也可以在同步日志页面手动获取资源态势信息。手动创建同步任务，即可查看同步资源数与同步状态；
		</td>
	</tr>
	<tr>
		<td rowspan="6">
			多云检测
		</td>
		<td>
			云资源概览，云账号概览可以查看云资源安全合规检测情况；
		</td>
	</tr>
	<tr>
		<td>
			云账号设置，提供了对云账号的创建、删除、编辑、查找、校验、检测、调参等操作；
		</td>
	</tr>
	<tr>
		<td>
			云检测规则组，提供了对规则组的创建、删除、编辑、查找、绑定规则、执行检测等操作。；
		</td>
	</tr>
	<tr>
		<td>
			云资源检测规则，定义了需要检测与过滤的基本内容。规则标签、规则组、等保条例、漏洞等从不同维度针对检测规则的统计划分；
		</td>
	</tr>
	<tr>
		<td>
			云账号定时检测，可以创建定时任务，便于定时检测某些云账号或某些规则；
		</td>
	</tr>
	<tr>
		<td>
			云资源检测结果，可以查看所有云账号的检测状态和检测结果；
		</td>
	</tr>
	<tr>
		<td rowspan="4">
			漏洞检测
		</td>
		<td>
			漏洞检测概览，对漏洞进行统计分析，可以直观的看到系统漏洞情况；
		</td>
	</tr>
	<tr>
		<td>
			漏洞检测设置，提供了对漏洞目标地址的创建、删除、编辑、查找、校验、检测、调参等操作；
		</td>
	</tr>
    <tr>
		<td>
			漏洞检测规则，列表页面，可以添加、修改、查看所有漏洞检测规则；
		</td>
	</tr>
    <tr>
		<td>
			漏洞检测结果，可以查看所有漏洞检测结果；
		</td>
	</tr>
	<tr>
		<td rowspan="6">
			合规报告
		</td>
        <td>
            云资源合规报告，展示按规则组与等保条例统计资源合规报告信息。可查看/下载云资源合规详情信息，报告以 Excel 形式展示，不合规的资源列表和风险条例列表；
        </td>
	</tr>
	<tr>
		<td>
			云资源历史记录，记录根据云账号，展示历史检测安全评分；
		</td>
	</tr>
	<tr>
		<td>
			云资源统计分析，根据云账号，展示不同维度的检测结果信息，包括检测规则、规则组别、等保条例、规则标签、检测区域、检测资源等维度展示数据；
		</td>
	</tr>
    <tr>
        <td>
            漏洞检测合规报告，展示漏洞检测目标地址按规则组与等保条例统计资源合规报告信息；
        </td>
    </tr>
	<tr>
		<td>
			漏洞历史记录，根据漏洞检测目标地址，展示历史检测安全评分；
		</td>
	</tr>
	<tr>
		<td>
			漏洞统计分析，根据漏洞检测目标地址，展示不同维度的检测结果信息，包括检测规则、规则组别、等保条例、规则标签、检测资源等维度展示数据；
		</td>
	</tr>
    <tr>
        <td rowspan="4">
            操作审计
        </td>
		<td>
			云事件概览，操作审计云事件数据概览；
        </td>
	</tr>
	<tr>
		<td>
			云事件同步，获取云事件同步日志列表，选择云账号、区域及事件事件范围点击同步按钮可同步云事件；
		</td>
	</tr>
	<tr>
		<td>
			云事件分析，根据云账号、区域、日期范围等条件查询云事件；
		</td>
	</tr>
	<tr>
		<td>
			云事件聚合，根据同步的云事件数据进行深度聚合查询；
		</td>
	</tr>
	<tr>
		<td rowspan="5">
			对象存储
		</td>
		<td>
			对象存储概览，对象存储概览页面展示对象存储信息与数据；
		</td>
	</tr>
	<tr>
		<td>
			对象存储账号，展示对象存储账号信息，提供了对对象存储账号的创建、删除、编辑、查找、校验等操作；
		</td>
	</tr>
	<tr>
		<td>
			存储桶列表，对象存储桶列表页面展示对象存储bucket与object信息，并且可以执行上传、下载、删除等操作。；
		</td>
	</tr>
	<tr>
		<td>
			对象存储风险统计，根据对象存储规则组检测对象存储合规情况；
		</td>
	</tr>
    <tr>
		<td>
			对象存储合规报告，对象存储安全合规检测的报告信息；
		</td>
	</tr>
	<tr>
		<td rowspan="5">
			费用分析
		</td>
		<td>
			费用概览，展示混合云费用统计数据；<span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td>
			账单分析，根据云账号同步账单元数据；<span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
    <tr>
		<td>
			费用分析，根据云账号账单元数据，进行费用聚合和过滤分析；<span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
    <tr>
		<td>
			趋势分析，根据云账号账单元数据，进行费用趋势分析；<span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
    <tr>
		<td>
			成本优化，根据云账号账单元数据，进行成本优化建议；<span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td rowspan="32">
            云原生安全
		</td>
		<td rowspan="3">
			资源态势
		</td>
		<td>
			K8s 资源态势，绑定 K8s 环境信息，即可获取 K8s 的 Namespace、Pod、Node、Deployment、Service 等20余种资源信息；
		</td>
	</tr>
	<tr>
		<td>
			K8s 资源拓扑图，根据同步 K8s 资源汇总信息，形成拓扑图。同时，根据 K8s 资源的镜像与检测得到镜像漏洞风险信息；
		</td>
	</tr>
	<tr>
		<td>
			K8s 资源同步日志，绑定完 K8s 账号是可以自动获取资源态势信息的。同时，也可以在同步日志页面手动获取资源态势信息。手动创建同步任务，即可查看同步资源数与同步状态；
		</td>
	</tr>
	<tr>
		<td rowspan="6">
			主机检测
		</td>
		<td>
			主机数据概览，展示主机风险检测统计数据；
		</td>
	</tr>
	<tr>
		<td>
			统一凭证，主机认证统一凭证，新建、修改主机信息时，可灵活绑定凭证，凭证由密码或密钥组成；
		</td>
	</tr>
	<tr>
		<td>
			主机管理，提供了对主机分组、主机的创建、删除、编辑、查找、校验、检测等操作；
		</td>
	</tr>
	<tr>
		<td>
			主机检测规则，规则列表页面，可以添加、修改、查看所有主机检测规则；
		</td>
	</tr>
	<tr>
		<td>
			主机检测结果，可以查看所有主机安全风险检测结果；
		</td>
	</tr>
	<tr>
		<td>
			主机检测结果历史记录，查看历史检测数据信息；
		</td>
	</tr>
	<tr>
		<td rowspan="4">
			K8s 检测
		</td>
		<td>
			K8s 概览，展示 K8s 风险检测统计数据；
		</td>
	</tr>
	<tr>
		<td>
			K8s 账号配置，绑定 K8s 账号, 执行安全检测；
		</td>
	</tr>
	<tr>
		<td>
			K8s 检测结果，点击"统计按钮"进入详情列表，点击"状态按钮"查看日志与报告；
		</td>
	</tr>
	<tr>
		<td>
			K8s 检测历史记录，查看历史检测数据信息；
		</td>
	</tr>
    <tr>
        <td rowspan="4">
            部署检测
        </td>
        <td>
            部署概览，展示部署风险检测统计数据；
        </td>
    </tr>
    <tr>
        <td>
            部署配置，添加部署文件, 执行安全检测；
        </td>
    </tr>
    <tr>
        <td>
            部署检测结果，点击"统计按钮"进入详情列表，点击"状态按钮"查看日志与报告；
        </td>
    </tr>
	<tr>
		<td>
			部署检测历史记录，查看历史检测数据信息；
		</td>
	</tr>
	<tr>
		<td rowspan="5">
			镜像检测
		</td>
		<td>
			镜像概览，展示镜像风险检测统计数据；
		</td>
	</tr>
	<tr>
		<td>
			镜像仓库，绑定镜像仓库同步私有镜像，集中一键检测；
		</td>
	</tr>
	<tr>
		<td>
			镜像管理，手动添加镜像，执行一键检测；
		</td>
	</tr>
    <tr>
        <td>
            镜像检测结果，点击"统计按钮"进入详情列表，点击"状态按钮"查看日志与报告；
        </td>
    </tr>
    <tr>
        <td>
            镜像检测历史记录，查看历史检测数据信息；
        </td>
    </tr>
	<tr>
		<td rowspan="4">
			源码检测
		</td>
		<td>
			源码概览，展示源码风险检测统计数据；
		</td>
    </tr>
    <tr>
		<td>
			项目源码配置，源代码仓库中的项目绑定，执行一键检测；
		</td>
    </tr>
    <tr>
		<td>
			源码检测结果，点击"统计按钮"进入详情列表，点击"状态按钮"查看日志与报告；
		</td>
	</tr>
	<tr>
		<td>
			源码检测历史记录，查看历史检测数据信息；
		</td>
	</tr>
	<tr>
		<td rowspan="4">
			文件检测
		</td>
		<td>
			依赖文件概览，展示依赖文件风险检测统计数据；
		</td>
	</tr>
	<tr>
		<td>
			依赖文件管理，手动添加依赖文件或压缩文件夹，执行一键检测；
		</td>
	</tr>
	<tr>
		<td>
			依赖文件检测结果，点击"统计按钮"进入详情列表，点击"状态按钮"查看日志与报告；
		</td>
	</tr>
	<tr>
		<td>
			依赖文件检测历史记录，查看历史检测数据信息；
		</td>
	</tr>
	<tr>
		<td rowspan="2">
			SBOM 管理
		</td>
		<td>
			项目管理，项目和项目版本管理，绑定检测镜像、源码或检测文件；
		</td>
    </tr>
    <tr>
		<td>
			SBOM 分析，根据项目绑定的源码、镜像或软件包，生成软件物料清单，并结合漏洞生成 SBOM + CVE；
		</td>
	</tr>
    <tr>
        <td rowspan="3">
            任务编排
        </td>
        <td rowspan="2">
            任务管理
        </td>
        <td>
            任务编排，在任务编排部分可以自由将各个模块中的检测任务进行编排，组合成一个综合检测任务，简化用户进行跨模块、跨资源的检测操作；
        </td>
    </tr>
    <tr>
        <td>
            任务列表，任务编排中创建生成的任务会在列表显示，任务列表页面可以查看任务与日志信息；
        </td>
    </tr>
    <tr>
        <td rowspan="1">
            任务报告
        </td>
        <td>
            任务报告，根据任务编排，执行任务完成后, 可以进入任务报告界面，查看任务生成详细结果报告。最终可导出 H5；<span class="x-pack-span">X-Pack</span>
        </td>
    </tr>
    <tr>
        <td rowspan="2">
            检测管理
        </td>
        <td rowspan="1">
            检测规则
        </td>
        <td>
            检测规则，规则是 HummerRisk 针对各种资源检测进行检测的基础，它定义了需要检测与过滤的基本内容。检测规则模块定义了规则标签、规则组、风险条例以及其他资源的检测规则。规则将不断丰富，已达到用户需求；<span class="x-pack-span">X-Pack</span>
        </td>
    </tr>
    <tr>
        <td rowspan="1">
            检测结果
        </td>
        <td>
            检测结果，展示整体资源检测结果的信息，并根据资源对应的规则展示资源信息、检测日志等信息。检测结果在每个菜单模块有单独显示，此处只是将所有类型检测结果统一展示；
        </td>
    </tr>
    <tr>
		<td rowspan="38">
			系统设置
		</td>
		<td rowspan="4">
			用户管理
		</td>
		<td>
			支持用户的新建、编辑、删除、修改密码、启用、禁用、搜索等；
		</td>
	</tr>
	<tr>
		<td>
			支持批量导入用户； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td>
			支持给用户分配组织； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td>
			支持给用户分配角色； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td rowspan="1">
			角色管理
		</td>
		<td>
			支持角色的新建、编辑、删除、搜索等； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td rowspan="1">
			组织管理
		</td>
		<td>
			支持组织的新建、编辑、删除、搜索、排序、移动等； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td rowspan="3">
			权限管理
		</td>
		<td>
			支持从组织、角色、用户维度（组织架构维度）进行使用、管理、授权等形式的权限控制； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td>
			支持菜单和操作层面的权限控制； <span class="x-pack-span">X-Pack（计划）</span> 
		</td>
	</tr>
	<tr>
		<td>
			支持检测结果权限控制； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
    <tr>
        <td rowspan="4">
            参数设置
        </td>
        <td>
            邮件设置，SMTP主机、SMTP端口、SMTP账户、SMTP密码设置，测试连接；
        </td>
    </tr>
    <tr>
        <td>
            企业微信设置，cropid、agentid、secret设置，测试连接；
        </td>
    </tr>
    <tr>
        <td>
            钉钉设置，AppKey、AgentId、AppSecret设置，测试连接；
        </td>
    </tr>
    <tr>
        <td>
            检测参数设置，数据库更新、安全检测项、风险等级、离线检测等设置，更新漏洞库；
        </td>
    </tr>
    <tr>
		<td rowspan="3">
			消息通知
		</td>
		<td>
			支持邮件通知设置，设置通知事件类型、通知人、接收方式；
		</td>
	</tr>
    <tr>
		<td>
			支持企业微信通知设置，设置通知事件类型、通知人、接收方式；
		</td>
	</tr>
	<tr>
		<td>
			支持钉钉通知设置，设置通知事件类型、通知人、接收方式；
		</td>
	</tr>
    <tr>
		<td rowspan="1">
			代理设置
		</td>
		<td>
			通过代理设置，配置 Proxy 类型、Proxy IP、Proxy 端口、Proxy 用户名、Proxy 密码等信息。提供代理配置供资源检测使用；
		</td>
	</tr>
    <tr>
		<td rowspan="4">
			站内消息
		</td>
		<td>
			支持系统常见消息的通知；
		</td>
	</tr>
    <tr>
		<td>
			支持消息的接收配置；
		</td>
	</tr>
	<tr>
		<td>
			支持消息状态标记；
		</td>
	</tr>
	<tr>
		<td>
			支持已读消息的删除；
		</td>
	</tr>
    <tr>
        <td rowspan="4">
            系统参数
        </td>
        <td>
            支持手动更新部署宿主机的操作系统各项参数；
        </td>
    </tr>
    <tr>
        <td>
            支持设置系统请求超时时间、消息保留时间、风险检测时间间隔；<span class="x-pack-span">X-Pack（计划）</span>
        </td>
    </tr>
    <tr>
        <td>
            支持设置默认登录方式（普通登录、LDAP、OIDC、CAS）；  <span class="x-pack-span">X-Pack（计划）</span>
        </td>
    </tr>
    <tr>
        <td>
            支持设置限制登录失败次数及限制登录失败时间；<span class="x-pack-span">X-Pack（计划）</span>
        </td>
    </tr>
	<tr>
		<td rowspan="1">
			显示设置
		</td>
		<td>
			支持头部系统 Logo 、登录页 Logo 、登录页图片、登录页标题、系统名称、系统图标、帮助文档及首页链接、登录页脚等设置； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td rowspan="3">
			主题设置
		</td>
		<td>
			支持两种默认主题； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td>
			支持自定义主题的新建、编辑、删除等； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td>
			支持对主题进行基础配色、字体配色、边框配色、背景配色等多属性的设置； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
    <tr>
        <td rowspan="3">
            平台对接
        </td>
        <td>
            支持飞书与国际飞书平台接入，可扫码登录、接收消息和定时报告；  <span class="x-pack-span">X-Pack（计划）</span>
        </td>
    </tr>
    <tr>
        <td>
            支持钉钉平台接入，可扫码登录、接收消息和定时报告；  <span class="x-pack-span">X-Pack（计划）</span>
        </td>
    </tr>
    <tr>
        <td>
            支持企业微信平台接入，可扫码登录、接收消息和定时报告；  <span class="x-pack-span">X-Pack（计划）</span>
        </td>
    </tr>
	<tr>
		<td rowspan="3">
			认证设置
		</td>
		<td>
			支持 LDAP 认证对接； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
    </tr>
    <tr>
		<td>
			支持 OIDC 单点登录系统对接； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
    </tr>
    <tr>
		<td>
			支持 CAS 单点登录系统对接； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td rowspan="1">
			集成与扩展
		</td>
		<td>
			提供完善的 API 接口及文档； <span class="x-pack-span">X-Pack（计划）</span>
		</td>
	</tr>
	<tr>
		<td rowspan="1">
			操作日志
		</td>
		<td>
			支持系统操作日志的记录、查看、搜索及导出；
		</td>
	</tr>
    <tr>
        <td rowspan="1">
            插件列表
        </td>
        <td>
            展示混合云检测与云原生检测使用的各项组件，插件类型与检测类型；
        </td>
    </tr>
    <tr>
        <td rowspan="2">
            安装模式
        </td>
        <td rowspan="1">
            在 Linux 主机上安装
        </td>
        <td>
            支持一键主机 All in one 部署，自带 MySQL，也可自行另外配置 MySQL 引擎；
        </td>
    </tr>
    <tr>
        <td rowspan="1">
            在 K8s 上安装
        </td>
        <td>
            支持 K8s 模式部署，自带 MySQL，可另外配置 MySQL 引擎；
        </td>
    </tr>
</table>

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=HummerRisk/HummerRisk&type=Date){ width="95%" }](https://star-history.com/#HummerRisk/HummerRisk&Date)

!!! warning "默认 web 登录账户: admin 密码：hummer"
