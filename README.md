# 简介
Bazel是一个开源的构建和测试工具，类似于Make、Maven和Gradle。 它使用人类可读的高级构建语言。 Bazel支持多种语言的项目，并为多种平台构建输出。 Bazel支持跨多个存储库和大量用户的大型代码库。  

这个工程是使用bazel来完成java、go的编译实验

[官网简介](https://docs.bazel.build/versions/main/bazel-overview.html)

# 安装

[官网安装](https://docs.bazel.build/versions/4.2.1/install.html)

## Windows安装
### 步骤 1: 检查操作系统
版本要求：

- 64 bit Windows 7 or newer

- 64 bit Windows Server 2008 R2 or newer

### 步骤 2: 安装的前置条件
需要安装 [Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

### 步骤 3: 下载 Bazel
从GitHub上下载安装包
[Bazel binary (bazel-<version>-windows-x86_64.exe)](https://github.com/bazelbuild/bazel/releases)

### 步骤 4: 设置环境变量
要使默认情况下从命令提示符或PowerShell轻松访问Bazel，可以将Bazel二进制文件重命名为Bazel.exe，并将其添加到默认路径中。

```shell
set PATH=%PATH%;<path to the Bazel binary>
```

您还可以更改系统PATH环境变量，使其永久存在

### 步骤 5: 验证是否完成
成功安装Bazel。要检查安装是否正确，请尝试运行:

```shell
bazel version
```

看到如下结果即可证明安装完成

```shell
Build label: 4.2.1
Build target: bazel-out/x64_windows-opt/bin/src/main/java/com/google/devtools/build/lib/bazel/BazelServer_deploy.jar
Build time: Mon Aug 30 15:19:20 2021 (1630336760)
Build timestamp: 1630336760
Build timestamp as int: 1630336760
```

## macOS 安装
### 步骤 1: 安装 Homebrew 
安装Homebrew(一次性步骤):

```shell
/bin/bash -c "$(curl -fsSL \
https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### 步骤 2: 通过Homebrew安装Bazel
通过Homebrew安装Bazel包如下:

```shell
$ brew install bazel
```

验证是否完整成功

```shell
$ bazel --version
```

安装完成后，您可以使用以下命令升级到Bazel的新版本

```shell
$ brew upgrade bazel
```

# java工程构建
[参考资料](https://docs.bazel.build/versions/4.2.1/tutorial/java.html)

## BUILD文件

```shell
load("@rules_java//java:defs.bzl", "java_binary")

java_binary(
    name = "ProjectRunner",
    srcs = glob(["src/main/java/com/example/*.java"]),
)
```

## 构建

执行如下命令进行构建
```shell
bazel build //:ProjectRunner
```
构建成功：
```shell
D:\workspace\bazel-demo\java-tutorial>bazel build //:ProjectRunner
Starting local Bazel server and connecting to it...
INFO: Analyzed target //:ProjectRunner (22 packages loaded, 722 targets configured).
INFO: Found 1 target...
Target //:ProjectRunner up-to-date:
  bazel-bin/ProjectRunner.jar
  bazel-bin/ProjectRunner.exe
INFO: Elapsed time: 19.324s, Critical Path: 3.79s
INFO: 7 processes: 4 internal, 2 local, 1 worker.
INFO: Build completed successfully, 7 total actions

```

## 运行

执行命令：
```shell
bazel-bin\ProjectRunner.exe
```
结果：
```shell
D:\workspace\bazel-demo\java-tutorial>bazel-bin\ProjectRunner.exe
Hi!
```

# go工程构建
[参考资料](https://github.com/bazelbuild/rules_go)

## BUILD文件
```shell
load("@io_bazel_rules_go//go:def.bzl", "go_binary")

go_binary(
    name = "hello",
    srcs = ["hello.go"],
)
```

## 构建
执行：
```shell
bazel build //:hello
```

结果：
```shell
D:\workspace\bazel-demo\go-tutorial>bazel build //:hello
Starting local Bazel server and connecting to it...
INFO: SHA256 (https://golang.org/dl/?mode=json&include=all) = ffb4b98349ec783eb9a19e8790ff46365907aa1aca03e41b28
ef5b2a8f6d0afa
INFO: Analyzed target //:hello (37 packages loaded, 7832 targets configured).
INFO: Found 1 target...
Target //:hello up-to-date:
  bazel-bin/hello_/hello.exe
INFO: Elapsed time: 27.521s, Critical Path: 3.58s
INFO: 9 processes: 5 internal, 4 local.
INFO: Build completed successfully, 9 total actions

```
## 运行
执行
```shell
bazel-bin\hello_\hello.exe
```
结果
```shell
D:\workspace\bazel-demo\go-tutorial>bazel-bin\hello_\hello.exe
hello bazel go
```