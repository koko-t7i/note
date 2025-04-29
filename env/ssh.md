# SSH 免密登录

## Linux

1. 生成公钥私钥

```shell
ssh-keygen
```

2. 复制公钥到服务器

```shell
ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.150.148
```

非roor用户可能会报错：参考 [login - Unable to use ssh-copy-id - mktemp: failed to create file via template - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/212098/unable-to-use-ssh-copy-id-mktemp-failed-to-create-file-via-template)

或者直接修改 `/root/.ssh/authorized_keys` 文件， 将 `id_rsa.pub` 文件内容手动复制到 `authorized_keys` 中

3. 测试登录

```shell
ssh root@192.168.150.148 -p 22
```

## Windows

1. 生成公钥私钥

```shell
ssh-keygen
```

2. 复制公钥到服务器

```shell
type $env:USERPROFILE\.ssh\id_rsa.pub | ssh root@192.168.150.148 "cat >> .ssh/authorized_keys"
```

或者直接修改 `/root/.ssh/authorized_keys` 文件， 将 `id_rsa.pub` 文件内容手动复制到 `authorized_keys` 中

3. 测试登录

```shell
ssh root@192.168.150.148 -p 22
```

# SSH 配置代理

> 场景：使用 ssh 连接国外服务器时，配置 ssh 走代理

## 使用 nmap 配置 ssh 代理
nmap：https://nmap.org/download.html#windows

配置文件 `.ssh/config`

```json
Host koko
  HostName 10.10.10.10 // 服务器公网 IP
  User koko
  Port 22
  IdentityFile "C:\Users\29434\.ssh\id_rsa"	// 免密
  ProxyCommand "D:\nmap\ncat" --proxy-type socks5 --proxy 127.0.0.1:7890 %h %p // 代理
```

参考

- [SSH远程免密登录的两种方式-阿里云开发者社区](https://chrisjhart.com/Windows-10-ssh-copy-id)
- [login - Unable to use ssh-copy-id - mktemp: failed to create file via template - Unix & Linux Stack Exchange](https://developer.aliyun.com/article/1132156)
- [unable-to-use-ssh-copy-id-mktemp-failed-to-create-file-via-template](https://unix.stackexchange.com/questions/212098/unable-to-use-ssh-copy-id-mktemp-failed-to-create-file-via-template)
