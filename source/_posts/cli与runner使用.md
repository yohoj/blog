---
layout: gitlab
title: cli与runner使用
date: 2023-04-13 21:37:53
tags:
categories: [gitlab, runner, cli]
---
### 设置仓库

首先，在您的代码仓库根目录下创建.gitlab-ci.yml文件，该文件用于定义您的CI/CD流程。下面是一个示例文件：

```yml
stages:
  - build

job1:
  stage: build
  script:
    - make build
    - make dependencies
```

这个文件定义了一个build阶段和一个job1作业。在job1中，我们运行了两个脚本：make build和make dependencies。这些脚本将在build阶段中执行。

安装GitLab Runner

接下来，您需要在Windows 10上安装GitLab Runner。请按照以下步骤进行操作：

1. 从GitLab官网下载64位安装包。

2. 以管理员身份打开PowerShell，并进入安装包所在目录。

3. 运行以下命令安装GitLab Runner：

   ```shell
   ./gitlab-runner-windows-amd64.exe install -user ${username} --password ${password}
   ```

   如果您使用的是本地账户，则可以省略--user 和 --password参数。

4. 安装完成后，运行以下命令启动GitLab Runner：

   ```shell
   ./gitlab-runner-windows-amd64.exe start
   ```

5. 运行以下命令注册GitLab Runner：

   ```shell
   ./gitlab-runner-windows-amd64.exe register
   ```

   注册过程中，您需要提供一个Runner名称、GitLab实例的URL、注册Token以及运行环境（在这里输入shell）。

6. 注册完成后，GitLab Runner将生成一个config.toml文件。如果您没有安装PowerShell 7，则需要将shell=”pwsh”改为shell=”powershell”。

现在，您已经成功安装和配置了GitLab Runner。让它自动运行您的CI/CD流程。

