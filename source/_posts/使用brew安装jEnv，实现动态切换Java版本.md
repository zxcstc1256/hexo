---
title: 使用 brew 安装jEnv，实现动态切换 Java 版本
date: 2017-12-31 12:11:15
tags:
---
+ **安装 brew**

参考[brew 官网](https://brew.sh)

+ **安装 jEnv**

参考[jEnv官网](http://www.jenv.be)

+ **配置 jEnv**

主要说明一下，官网中的 Install 中，以下是不需要的
```bash
$ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.bash_profile
```
关注下面这句
```bash
$ echo 'eval "$(jenv init -)"' >> ~/.bash_profile
```
这是配置每次都初始化，其实就是创建文件夹

+ **配置**

添加受 jEnv 托管的jdk
```bash
jenv add /Library/Java/JavaVirtualMachines/jdk-9.0.4.jdk/Contents/Home/
```
以上路径为 jdk 路径，可以通过以下命令查看当前已经安装的jdk
```bash
ls /Library/Java/JavaVirtualMachines
```
注意：如果不手动添加 jdk 是不会被 jEnv 识别的，并且注意通过`brew cask upgrade`更新 jdk 后，`java -version`可能会出现以下错误：

> jenv: version `1.8.0.152' is not installed

输入`jenv versions`也会提示以下错误：

> jenv: version `1.8.0.152' is not installed
    system

这是因为之前设置过`global`版本，需要手动清理，输入以下命令清空
```bash
rm ~/.jenv/version
```

- **使用**

上一节中如果已经成功添加了jdk，输入以下命令可以看到已经被 jEnv 托管的jdk
```bash
jenv versions
```
运行结果：
```text
* system (set by /Users/xxx/.jenv/version)
  1.8.0.162
  9.0.4
  oracle64-1.8.0.162
  oracle64-9.0.4
```

以上 1.8.0.162 其实就是 oracle64-1.8.0.162，只是简称。
jEnv的版本管理有三种模式：`global`,`local`,`shell`

> global 全局环境

顾名思义就是设置系统 jdk 默认版本，不管在任何地方，只要没有特殊指定，运行 java 都采用该版本，通过以下命令设置
```bash
jenv global 1.8.0.162
```

> local 本地(当前目录)环境

针对特定目录设置 jdk 版本，优先级大于`global`，当指定了当前目录的`local`版本，该目录则以`local`版本为准，忽略`global`版本，通过以下命令设置

```bash
jenv local 1.8.0.162
```

> shell 会话环境

针对当前窗口有效，最高优先级，大于`global`和`local`，只针对本次会话有效，关闭窗口则销毁设置，通过以下命令设置
```bash
jenv shell 1.8.0.162
```