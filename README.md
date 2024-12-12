# CodeBook-Ubuntu-sandbox

这是一个多用户的 SSH 服务沙箱，支持启动时动态加载用户列表，并可随时更新用户信息。每个用户仅能修改自己目录下的文件，确保了环境的安全性和隔离性。

## 我如何使用？

您可以直接下载镜像，或者使用 Docker 构建容器。

### 拉取镜像

```shell
docker pull beardedmanzhao/codebook-ubuntu-sandbox
```

### 准备用户列表

用户列表应保存在一个名为 users.txt 的文件中，格式如下：
```
username1:password1,username2:password2,username3:password3
```

### 构建容器

假设 `C:\Users\zhao\Downloads\users.txt` 是用户列表文件的路径，可以通过以下命令启动容器：

```shell
# 启动容器 22 端口是ssh服务端口，因此需要将其提供给外部访问 在这里我们是映射到宿主机 2222 端口
docker run -d -p 2222:22 --name codebook-ubuntu-sandbox \
  -v C:\Users\zhao\Downloads\users.txt:/users.txt \
  beardedmanzhao/codebook-ubuntu-sandbox
```

或者将上述命令压缩为一行：
```shell
docker run -d -p 2222:22 --name codebook-ubuntu-sandbox -v C:\Users\zhao\Downloads\users.txt:/users.txt beardedmanzhao/codebook-ubuntu-sandbox
```

### 直接使用

可以直接使用下面的命令登录机器！这里的用户名和密码都是 users.txt 中的！2222 代表的是容器的 22 端口

```shell
ssh username@localhost -p 2222
```

关键特性
- 动态用户管理：支持启动时动态加载用户列表，并可随时更新。
- 用户隔离：每个用户只能修改自己目录下的文件，确保数据安全。
- 简单易用：通过 Docker 快速部署，方便管理和维护。 