# Docker - 学习笔记

## 1. Docker简介
- Docker是容器管理工具；
- 解决问题：
	- 快速创建环境；
	- 整体交付；
	- 环境一致性保证；
	- 更好的完成devops；

## 2. Docker安装
- 使用`uname -r`检查Linux的内核版本，需要大于`3.10`；
- 安装`curl`程序；
- 使用`curl -sSL https://get.docker.com/ | sh`命令安装docker；
- 使用`docker -v`检查版本；
- 使用`systemctl start docker`启动docker服务；
- 使用`systemctl enable docker`设置为开机启动；
- 使用`ps -aux | grep docker`检查`docker`容器的运行情况；

## 3. Docker镜像
- Docker镜像：即为**把业务代码和运行环境进行整体打包**；
- 基础的Docker镜像：从公共仓库直接拉取，由原厂进行维护；
- 定制镜像：编写dockerfile，重新编译打包成镜像，是推荐的使用方式；
- Commit镜像：通过镜像启动容器，通过commit命令形成镜像；

### 3.1 镜像分层技术
- `AUFS(Another Union File System)`即为镜像分层技术，支持将多个目录挂载到同一个虚拟目录下；
- 镜像分为多个`layer`，每个`layer`ID和大小；
- 已构建的镜像会设置成只读模式，`read-write`写操作实在`read-only`上的一种增量操作，故不会影响`read-only`层；
