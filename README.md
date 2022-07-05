本仓库保存了 [hummerrisk 项目]() 的 [官方文档](https://docs.hummerrisk.com)，该文档使用 [MkDocs]() 文档框架下的 [Material for MkDocs]() 主题进行构建。

## 本地开发

### 克隆本仓库

```sh
git clone https://github.com/hummerrisk/hummerrisk-docs.git
```

### 安装依赖

```sh
cd docs
pip3 install -r requirements/requirements.txt
```

### 修改文档内容

本文档的文档结构定义在 `mkdocs.yml` 文件中，文档的具体内容均在 `docs` 目录中。

```yaml
..........
nav:
  - 系统介绍:
      - 整体介绍: index.md
      - 快速安装: system/setup_by_fast.md
      - 升级文档: system/upgrade.md
  - 用户手册:
      - 使用流程: user/process.md
      - 系统设置: user/settings.md
      - 检测规则: user/rule.md
      - 云账号: user/account.md
      - 检测结果: user/resource.md
      - 首页: user/dashboard.md
  - 常见问题:
      - 开发文档: question/dev_manual.md
      - 等级保护: question/grade_protection.md
      - 开启企业微信通知: question/weixin_settings.md
      - 开启钉钉消息通知: question/dingtalk_settings.md
      - 解决云账号校验失败问题(Custodian): question/account.md
      - 如何自定义规则(Custodian): question/rule.md
      - 自定义阿里云监控规则示例(Custodian): question/example.md
      - 自定义漏洞检测规则(Nuclei): question/nuclei.md
      - 快速了解AWS检测规则(Prowler): question/prowler.md
  - 关于我们:
      - 资源下载: about/download.md
      - 更新说明: about/changelog.md
      - 联系我们: about/contact.md
..........
```

文档内容使用 markdown 语法编写，若要添加新的文档，需要先在 `mkdocs.yml` 文件中的 `nav` 部分增加对应章节导航。

### 本地调试文档

```sh
pip3 install mkdocs 
mkdocs --version
pip3 install mkdocs-material
mkdocs serve
```

执行上述命令后，可通过 `http://127.0.0.1:8000` 地址查看生成的文档内容，当修改文档后，页面内容会自动更新。

### 构建文档

```sh
mkdocs build
```

执行上述命令后，会在 `site` 目录下生成文档站点的静态文件，将目录中的内容复制到任意 HTTP 服务器上即可完成文档的部署。

## 帮助完善文档

### Fork 文档仓库

点击仓库右上角的 `fork` 按钮，复制本仓库到自己的 github 账号。

### 克隆 fork 后的仓库

```sh
git clone https://github.com/your-github-account/docs.git
```

### 本地修改并调试

### Push 修改内容到 GitHub 仓库

### 提交 Pull Request 到本仓库
