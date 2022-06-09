
### 漏洞扫描(Nuclei 规则)

> Github 项目地址：https://github.com/hummerrisk/nuclei
 
> Github 模板项目地址：https://github.com/projectdiscovery/nuclei-templates

> 文档地址：https://nuclei.projectdiscovery.io

> 博客地址：https://blog.projectdiscovery.io/

#### 一、Nuclei 是什么

Nuclei 是一种新型扫描器，它摆脱了漏洞扫描器的传统模型，允许通过非常简单且易于使用的 YAML 模板语法。
    
Nuclei 是一个扫描器——它发送 HTTP/DNS 请求并检查一些响应以发现目标中的异常。

用户可以轻松定义匹配器，它检查各种类型的模式（例如单词或正则表达式）的响应，提取器使用正则表达式从响应中提取一些内容。除了强大的匹配和提取功能外，用户还可以完全自定义发送的请求，从而完全控制请求/响应过程的每个部分。

#### 二、Nuclei 有什么不同？

Nuclei 方法不是将扫描器与漏洞检查捆绑在一起，而是专注于核心引擎，将创建漏洞检查的任务留给最终用户。

内核从一开始就被设计为非常可扩展，允许用户根据需要自定义一切。以下是 Nuclei 项目的核心目标：

- 简单性： Nuclei 模板以非常易于阅读的yaml格式定义，这使非开发人员也可以轻松创建模板，而无需编写冗长的代码并对其进行调试以使其正常工作。
- 灵活性： 可以根据用户的喜好自定义模板。很少有事情是模板本身无法完成的。请求的每个部分都可以根据需要进行定制，并且可以完美运行。
- 可移植性： 核心目标之一是允许用户相互共享模板。每个模板都是一个文件，可以独立运行，无需任何先决条件。您所需要的只是一个核安装。通过这种方式，核概念增加了社区共享。

#### 三、Nuclei 模板

nuclei-templates 是该 nuclei 项目的主要重点。它是一个社区构建的可用于核扫描仪的模板集合。这些模板由 nuclei 用户提供，并经过精心策划，以清除长期以来一直是扫描仪问题的误报、恶意代码等。

Nuclei 集成了对下载和管理 nuclei-templates 存储库的本地副本的支持。用户只需运行 nuclei -update-templates 即可在本地下载存储库。如果发布了更新，用户会收到通知，并且只需再次运行相同的命令即可更新其副本。

#### 四、Nuclei 使用

> 工具使用: nuclei -h

上述命令将显示该工具的帮助信息，下面给出的是该工具的常用选项：

| 选项标签 | 描述信息 | 使用样例 |
| :----: | :----: | :----: |
| -c | 并发请求数（默认为10 | nuclei -c 100 |
| -l | 要运行模板的URL列表 | nuclei -l urls.txt |
| -t | 需跨主机检测的模板输入文件 | nuclei -t git-core.yaml |
| -t | 需跨主机检测的模板输入文件 | nuclei -t “path/*.yaml” |
| -nC | 输出中不使用高亮颜色 | nuclei -nC |
| -o | 保存输出结果文件（可选）| nuclei -o output.txt |
| -silent | 在输出中仅显示找到的结果 | nuclei -silent |
| -retries | 重试失败请求的次数（默认值1） | nuclei -retries 1 |
| -timeout | 超时前等待的秒数（默认为5） | nuclei -timeout 5 |
| -v | 显示详细输出 | nuclei -v |
| -version | 显示Nuclei版本 | nuclei -version |
| -proxy-url | 代理URL | nuclei -proxy-url http://user:pass@this.is.a.proxy:8080 |
| -proxy-socks-url | 代理Socks URL | nuclei -proxy-socks-url socks5://user:pass@this.is.a.proxy.socks:9050 |

#### 五、Nuclei 工具安装

代码安装

该工具的安装其实非常简单，大家可以在该项目 GitHub 库中的 Releases 页面中根据自己的平台选择预编译好的源代码，然后使用 tar 命令进行代码提取，将提取出的代码移动到自己的 $PATH 路径下。所使用的命令如下：

> tar -xzvf nuclei-linux-amd64.tar> mv nuclei-linux-amd64 /usr/bin/nuclei> nuclei -h

源安装

Nuclei 要求目标设备成功配置好 Go v1.13+ 环境，然后运行下列命令获取项目代码：

> GO111MODULE=on go get -u -v github.com/projectdiscovery/nuclei/cmd/nuclei

如需更新 Nuclei，可以使用 -u 选项和 go get 命令。

#### 六、Nuclei 运行

使用单一模板运行 Nuclei。

下列命令将会对 urls.txt 文件中列出的主机进行扫描，并返回匹配的结果：

> nuclei -l urls.txt -t git-core.yaml -o results.txt

你还能够以标准输入（STDIN）的方式传递目标主机列表，下列命令同样可以对 urls.txt 文件中列出的主机进行扫描，并返回匹配的结果：

> cat urls.txt | nuclei -t git-core.yaml -o results.txt

使用多个模板运行 Nuclei。

下列命令将能够使用 path-to-templates 目录中所有模板来对 urls.txt 文件中列出的主机进行扫描，并返回匹配的结果：

> nuclei -l urls.txt -t "path-to-templates/*.yaml" -o results.txt

使用子扫描器和其他类似工具自动化运行 Nuclei。

> subfinder -d hackerone.com -silent | httprobe | nuclei -t "path-to-templates/*.yaml" -o results.txt

#### 七、Nuclei 自定义模板

Nuclei支持通过.yaml文件来自动传递和执行多个模板任务，如需开发自定义模板，请参考 Github 模板项目地址：https://github.com/projectdiscovery/nuclei-templates

##### 工具截图

![img.png](../img/question/nuclei1.png)
