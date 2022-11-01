
### DependencyCheck

!!! info "项目地址"
    * Github 项目地址：https://github.com/jeremylong/DependencyCheck
    * 文档地址：https://jeremylong.github.io/DependencyCheck/

#### 一、DependencyCheck 是什么

!!! abstract "DependencyCheck 是什么"
    * Dependency-Check 是 OWASP（Open Web Application Security Project）的一个实用开源程序，用于识别项目依赖项并检查是否存在任何已知的，公开披露的漏洞。目前，已支持Java、.NET、Ruby、Node.js、Python等语言编写的程序，并为C/C++构建系统（autoconf和cmake）提供了有限的支持。而且该工具还是OWASP Top 10的解决方案的一部分。
    * Dependency-Check 支持面广（支持多种语言）、可集成性强，作为一款开源工具，在多年来的发展中已经支持和许多主流的软件进行集成，比如：命令行、Ant、Maven、Gradle、Jenkins、Sonar等；具备使用方便，落地简单等优势。

#### 二、DependencyCheck 实现原理？

!!! abstract "实现原理"
    1. 依赖性检查可用于扫描应用程序（及其依赖库），执行检查时会将 Common Platform Enumeration (CPE)国家漏洞数据库及NPM Public Advisories库下载到本地，再通过核心引擎中的一系列分析器检查项目依赖性，收集有关依赖项的信息。
    2. 然后根据收集的依赖项信息与本地的CPE&NPM库数据进行对比，如果检查发现扫描的组件存在已知的易受攻击的漏洞则标识，最后生成报告进行展示。

#### 三、DependencyCheck 集成

!!! abstract "集成"
    1. 与maven集成
        * Dependency-check-maven非常易于使用，可以作为独立插件使用，也可以作为maven site的一部分使用。
        * 该插件需要使用Maven 3.1或更高版本，第一次执行时，可能需要20分钟或更长时间，因为它会从NIST托管的国家漏洞数据库下载漏洞数据到本地备份库。
        * 第一次批量下载后，只要插件每七天至少执行一次，本地漏洞库就会自动更新，更新只需几秒钟。
        * 集成很简单，只需要在项目的pom文件中增加maven配置即可。

用法一 在target目录中创建dependency-check-report.html

!!! tip "用法一"
    ```sh
        <plugin>
            <groupId>org.owasp</groupId>
            <artifactId>dependency-check-maven</artifactId>
            <version>4.0.2</version>
            <configuration>
                <autoUpdate>true</autoUpdate>
            </configuration>
            <executions>
                <execution>
                    <goals>
                        <goal>check</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    ```

用法二 在maven site中创建聚合性的报告

!!! tip "用法二"
    ```sh
        <plugin>
            <groupId>org.owasp</groupId>
            <artifactId>dependency-check-maven</artifactId>
            <version>4.0.2</version>
            <reportSets>
                <reportSet>
                    <reports>
                        <report>aggregate</report>
                    </reports>
                </reportSet>
            </reportSets>
        </plugin>
    ```

用法三 设置当风险指数（CVSS）大于等于8时（CVSS分数为0-10）则项目编译失败

!!! tip "用法三"
    ```sh
        <plugin>
            <groupId>org.owasp</groupId>
            <artifactId>dependency-check-maven</artifactId>
            <version>4.0.2</version>
            <configuration>
                <failBuildOnCVSS>8</failBuildOnCVSS>
            </configuration>
            <executions>
                <execution>
                    <goals>
                        <goal>check</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    ```

用法四 仅更新NVD（漏洞库）数据，而不执行检查

!!! tip "用法四"
    ```sh
        <plugin>
            <groupId>org.owasp</groupId>
            <artifactId>dependency-check-maven</artifactId>
            <version>4.0.2</version>
            <executions>
                <execution>
                    <goals>
                        <goal>update-only</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    ```

#### 四、与 Jenkins 集成

!!! abstract "与 Jenkins 集成"
    * Jenkins中需要安装插件：Static Analysis Utilities 和 Dependency-Check
    * 该插件具有执行依赖关系分析和构建后查看检查结果的功能。

执行依赖分析配置：

![与Jenkins集成](../img/question/dependency1.png){ width="95%" }

查看检查分析结果配置：

![与Jenkins集成](../img/question/dependency2.png){ width="95%" }

#### 五、与代码质量管理平台 SonarQube 7.x 以上的版本集成

!!! abstract "与 SonarQube 集成"
    将插件（jar文件）复制到$SONAR_INSTALL_DIR/extensions/plugins并重新启动SonarQube。

!!! tip "但需要添加以下配置"
    ```sh
        sonar.dependencyCheck.reportPath = ${WORKSPACE}/dependency-check-report.xml
        ##以Jenkins为例报告.xml路径
        sonar.dependencyCheck.htmlReportPath = ${WORKSPACE}/dependency-check-report.html
        ##以Jenkins为例报告.html路径
    ```

!!! tip "问题严重性分数设定"
    ```sh
        sonar.dependencyCheck.severity.blocker = 9.0
        sonar.dependencyCheck.severity.critical = 7.0
        sonar.dependencyCheck.severity.major = 4.0
        sonar.dependencyCheck.severity.minor = 0.0
    ```

#### 六、报告查看

!!! abstract "报告查看"
    样本报告demo：https://jeremylong.github.io/DependencyCheck/general/SampleReport.html

![报告查看](../img/question/dependency3.png){ width="95%" }

![报告查看](../img/question/dependency4.png){ width="95%" }
