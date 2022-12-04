### 查看 log 日志

#### 1.log日志

!!! info "命令"
    ``` bash
    # 查看日志在宿主机位置
    cd /opt/hummerrisk/logs/hummerrisk/

    # 可以看到5个文件
    -rw-r--r-- 1 root root      0 10月 24 07:57 debug.log
    -rw-r--r-- 1 root root 365879 10月 25 20:34 error.log
    drwxr-xr-x 2 root root   4096 10月 27 00:58 history
    -rw-r--r-- 1 root root   2127 10月 27 06:58 info.log
    -rw-r--r-- 1 root root      0 10月 24 07:57 warn.log

    # 实时打印最新日志
    tail -1000f error.log

    # 旧日志会定期存储在当前目录下的 history 文件夹下，默认30天
    ```


