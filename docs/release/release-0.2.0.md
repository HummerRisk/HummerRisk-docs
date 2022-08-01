## 1 新功能 Features

### 1.1 任务报告

!!! Abstract ""
如下图所示，任务报告: 根据任务编排功能进行检测，并生成相应的报告（包括云端检测、漏洞检测、虚拟机检测、镜像检测、软件包检测）。

> 首先，在任务编排页面选择需要检测的账户类型：云端检测、漏洞检测、虚拟机检测、镜像检测、软件包检测。
> 其次，添加右侧对应的规则类型，选择需要检测的规则并在下方列表中进行编排并保存。

![任务编排](../img/release/0.2.0/task.png){ width="900px" }
![任务列表](../img/release/0.2.0/task1.png){ width="900px" }

> 点击任务列表中任务名称可查看任务详情。

![任务详情](../img/release/0.2.0/task10.png){ width="900px" }

> 点击任务列表中任务状态可查看任务状态，并可跳转至检测类型对应的检测结果页面。

![任务状态](../img/release/0.2.0/task11.png){ width="900px" }

> 任务完成后, 进入任务报告界面，选择需要生成报告的任务。

![任务报告](../img/release/0.2.0/task2.png){ width="900px" }

> 任务报告分为云端检测、漏洞检测、虚拟检测、镜像检测、软件包检测等五部分。


> 云端检测

![任务报告](../img/release/0.2.0/task2.png){ width="900px" }
![任务报告](../img/release/0.2.0/task3.png){ width="900px" }

> 漏洞检测

![任务报告](../img/release/0.2.0/task4.png){ width="900px" }

> 虚机检测

![任务报告](../img/release/0.2.0/task5.png){ width="900px" }

> 镜像检测

![任务报告](../img/release/0.2.0/task6.png){ width="900px" }
![任务报告](../img/release/0.2.0/task7.png){ width="900px" }

> 软件包检测

![任务报告](../img/release/0.2.0/task8.png){ width="900px" }
![任务报告](../img/release/0.2.0/task9.png){ width="900px" }

### 1.2 历史信息

!!! Abstract ""
如下图所示，历史信息: 新增历史检测信息留存，便于分析与比对，查看历史安全评分与检测结果。

![历史信息](../img/release/0.2.0/history.png){ width="900px" }
![历史信息](../img/release/0.2.0/history2.png){ width="900px" }

### 1.3 首页数据分析

!!! Abstract ""
新增首页历史数据分析功能。

![首页](../img/release/0.2.0/dashboard.png){ width="900px" }
![分析](../img/release/0.2.0/dashboard2.png){ width="900px" }

### 1.4 漏洞检测

!!! Abstract ""
如下图所示，漏洞检测: 新增漏洞检测重新检测与整体清除功能。

![漏洞检测](../img/release/0.2.0/vuln.png){ width="900px" }

如下图所示，云端检测: 新增云端检测重新检测与整体清除功能。

![云端检测](../img/release/0.2.0/cloud.png){ width="900px" }

### 1.5 安装包

!!! Abstract ""
如下图所示，安装包: 全新升级安装包，一键安装更便捷更实用。

![安装包](../img/release/0.2.0/install.png){ width="900px" }

![安装包](../img/release/0.2.0/install2.png){ width="900px" }

## 2 性能优化 Optimization

### 2.1 任务编排

!!! Abstract ""
优化任务编排功能；

### 2.2 云端检测

!!! Abstract ""
优化云端检测，检测结果按账号汇总生成安全评分。

![组件样式_背景](../img/view_generation/组件样式_背景.png){ width="900px" }

### 2.3 漏洞检测

!!! Abstract ""
优化漏洞检测，检测结果按漏洞汇总生成安全评分。

### 2.4 镜像检测

!!! Abstract ""
优化镜像检测，检测结果按图表展示。

### 2.5 软件检测

!!! Abstract ""
优化软件检测，检测结果按图表展示。


## 3 Bug修复 Bug Fixes

### 3.1 漏洞检测

!!! Abstract ""
修复漏洞检测结果字段过大报错问题。

### 3.2 历史数据

!!! Abstract ""
修复历史数据展示问题。

### 3.3 任务编排

!!! Abstract ""
修复任务编排检测结果因某些规则报错导致流程堵塞的问题。

### 3.4 JSON翻译

!!! Abstract ""
优化JSON因翻译而未格式化的问题。

### 3.5 漏洞库

!!! Abstract ""
内置漏洞库，优化检测流程。
