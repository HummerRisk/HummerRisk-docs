
## 1. 一键安装部署

!!! tip "一键部署"
    1. 部署服务器要求
        - 操作系统要求：任何支持 Docker 的 Linux x64
        - CPU内存要求：最低要求 4C8G，推荐 8C16G
        - 部署目录空间（默认/opt目录）要求： 50G
        - 网络要求：可访问互联网
    2. 执行以下脚本进行一键安装：
    ```bash
        curl -sSL https://github.com/HummerRisk/HummerRisk/releases/latest/download/quick_start.sh -o quick_start.sh
    ```
    3. HummerRisk 是一款 B/S 架构的产品，即浏览器/服务器结构，在服务器安装完成后，客户端通过浏览器访问以下地址，即可开始使用。
        - http://目标服务器 IP 地址：服务运行端口，例如：http: 82.157.130.20:80
        - 使用默认用户名 admin 密码 hummer 进行登录。

## 2. 登录并使用

!!! warning "默认 web 登录账户: admin 密码：hummer"
