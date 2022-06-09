
### 阿里云监控规则示例( Cloud Custodian 规则)

> 一、Aliyun CPU使用率扫描(无需安装插件)，扫描7天内cpu平均值小于30，监控采样频率周期为一天（86700秒）

规则示例：
```
policies:
  # ECS主机连续n天内业务高峰阶段CPU平均使用率在不高于x%，符合条件视为”不合规“，否则视为”合规“
  - name: aliyun-ecs-cpu-underutilized
    resource: aliyun.ecs
    filters:
      - type: metrics
        name: CPUUtilization
        days: 7
        period: 86400
        statistics: Average
        value: 30
        op: less-than
```

> 二、Aliyun 虚机处于关机状态，或指定时间范围内内存使用率为0（或无数据）

规则示例：
```
policies:
  # ECS主机处于关机状态，或指定时间范围内内存使用率为0（或无数据）,符合条件视为”不合规“，否则视为”合规“
  - name: aliyun-ecs-memory-metrics
    resource: aliyun.ecs
    filters:
      - or:
        - type: stopped
        - type: metrics
          name: memory_usedutilization
          days: 7
          period: 86700
          statistics: Average
          value: 0
          op: eq
```

> 三、Aliyun 指定时间范围内，CPU平均使用率低于指定值（基于agent监控）

规则示例：
```
policies:
  # ECS主机指定时间范围内，CPU平均使用率低于指定值（基于agent监控）,符合条件视为”不合规“，否则视为”合规“
  - name: aliyun-ecs-cpu-metrics
    resource: aliyun.ecs
    filters:
      - or:
        - type: metrics
          name: cpu_total
          days: 7
          period: 86700 
          statistics: Average
          value: 30
          op: less-than
```

> 四、Aliyun 指定时间范围内，内存平均使用率低于指定值（基于agent监控）

规则示例：
```
policies:
  # ECS主机指定时间范围内，内存平均使用率低于指定值（基于agent监控）,符合条件视为”不合规“，否则视为”合规“
  - name: aliyun-ecs-memory-metrics
    resource: aliyun.ecs
    filters:
      - or:
        - type: metrics
          name: memory_usedutilization
          days: 7
          period: 86700 
          statistics: Average
          value: 30
          op: less-than
```


> 五、Aliyun 磁盘状态为未挂载，或指定时间范围内读写监控值为0（或无数据）

规则示例：
```
policies:
  # Disk磁盘状态为未挂载，或指定时间范围内读写监控值为0（或无数据）,符合条件视为”不合规“，否则视为”合规“
  # 系统盘I/O读写总操作，单位：次/s。IOPSTotal
  # 系统盘读写总带宽，单位：Byte/s。BPSTotal
  - name: aliyun-disk-iopstotal-metrics
    resource: aliyun.disk
    filters:
      - or:
        - type: unused
        - type: metrics
          name: IOPSTotal
          days: 7
          #数据的精度，单位为秒。取值范围：60/600/3600,默认值：60
          period: 3600 
          statistics: Average
          #监控值(单位：bit/s)
          value: 0 
          op: eq
```

> 六、Aliyun 磁盘状态为未挂载，或指定时间范围内读写监控值为0（或无数据）

规则示例：
```
policies:
  # Disk磁盘状态为未挂载，或指定时间范围内读写监控值为0（或无数据）,符合条件视为”不合规“，否则视为”合规“
  # 系统盘I/O读写总操作，单位：次/s。IOPSTotal
  # 系统盘读写总带宽，单位：Byte/s。BPSTotal
  - name: aliyun-disk-iopstotal-metrics
    resource: aliyun.disk
    filters:
      - or:
        - type: unused
        - type: metrics
          name: IOPSTotal
          days: 7
          #数据的精度，单位为秒。取值范围：60/600/3600,默认值：60
          period: 3600 
          statistics: Average
          #监控值(单位：bit/s)
          value: 0 
          op: eq
```

> 七、Aliyun 指定时间范围内，虚拟机公网流量（流出）或 EIP 公网流量（流出）的平均值/总带宽比值低于指定百分比

规则示例：
```
policies:
  # 指定时间范围内，虚拟机公网流量（流出）或 EIP 公网流量（流出）的平均值/总带宽比值低于指定百分比,符合条件视为”不合规“，否则视为”合规“
  - name: aliyun-ecs-rate-metrics
    resource: aliyun.ecs
    filters:
      - type: metrics
        name: InternetOutRate_Percent
        days: 7
        period: 86700
        statistics: Average
        value: 30
        op: less-than
      - type: metrics
        name: VPC_PublicIP_InternetOutRate_Percent
        days: 7
        period: 86700
        statistics: Average
        value: 30
        op: less-than
```

> 八、Aliyun RDS实例在指定时间范围内，CPU和内存平均使用率低于指定值(单位: 使用率%)

规则示例：
```
policies:
  # RDS实例在指定时间范围内，CPU和内存平均使用率低于指定值(单位: 使用率%),符合条件视为”不合规“，否则视为”合规“
  - name: aliyun-rds-metrics
    resource: aliyun.rds
    filters:
      - type: metrics
        name: CpuUsage
        days: 7
        period: 86700
        statistics: Average
        value: 30
        op: less-than
      - type: metrics
        name: MemoryUsage
        days: 7
        period: 86700
        statistics: Average
        value: 30
        op: less-than
```


> 九、Aliyun RDS实例在指定时间范围内 IOPS 监控值低于指定值(单位: 使用率%)

规则示例：
```
policies:
    # RDS实例在指定时间范围内 IOPS 监控值低于指定值(单位: 使用率%),符合条件视为”不合规“，否则视为”合规“
    # IOPS使用率:IOPSUsage
    # 连接数使用率: ConnectionUsage
    # 内存使用率: MemoryUsage
    # CPU使用率: CpuUsage
  - name: aliyun-rds-metrics
    resource: aliyun.rds
    filters:
      - type: metrics
        name: IOPSUsage
        days: 7
        period: 86700
        statistics: Average
        value: 30
        op: less-than
```

> 十、Aliyun SLB在指定时间范围内，流量监控低于某值(单位：bit/s)

规则示例：
```
policies:
  # SLB在指定时间范围内，流量监控低于某值(单位：bit/s),符合条件视为”不合规“，否则视为”合规“
  - name: aliyun-slb-metrics
    resource: aliyun.slb
    filters:
      - type: metrics
        name: InstanceTrafficTX
        days: 7
        period: 86700
        statistics: Average
        value: 30000
        op: less-than
```
