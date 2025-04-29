# Tmux

`tmux` 是一个非常强大又实用的终端复用器，简单来说就是可以让你在一个终端窗口里运行多个会话、分屏显示、后台运行任务等

tmux 主要用途：

- 通过在 tmux 中运行远程服务器上正在运行的程序来防止连接断开
- 允许从多台不同的本地计算机访问远程服务器上运行的程序
- 在一个终端中同时使用多个程序和 shell，有点像窗口管理器

## 概念

Tmux 由如下三个基础组成：

1. Session即会话，任务通常在 session 中运行，在断开连接后 session 仍会保持
2. Window即窗口，一个会话可以包含多个窗口。可以存在多个窗口
3. Pane即窗格，一个窗口可以包含多个窗格

## Session 会话

输入这个命令默认开启了一个 session name 为 0 的 Tmux 会话

```shell
tmux
tmux new -s [session-name] # 指定名称
tmux rename-session -t 0 <new-name> # 重命名
```

查看有多少会话

```shell
tmux ls
```

如果此时你的服务器断开，你可以使用下面这个命令重新连接，tmux 中的任务还会继续保持

```shell
tmux a -t 0
```

从该会话中退出，但是不会关闭这个会话

快捷键 **ctrl+b d**

```shell
tmux detach
```

删除这个会话:

```shell
tmux kill-session -t [session-name]
tmux kill-server # 删除所有
```

快捷键：进入窗口直接 **ctrl + d** 就可以直接关闭当前会话

## 窗口管理

Tmux 为了防止与全局快捷键冲突，大部分快捷键需要先需要输入前缀，默认为 **Ctrl + b**

新建一个窗口

```shell
Ctrl+b c
```

新建一个垂直窗口

```
Ctrl+b "
```

新建一个水平窗口

```
Ctrl+b %
```

选择一个窗口

```
Ctrl+b w 
```

关闭一个窗口

```
Ctrl + d
```

```
Ctrl+b x
```

在窗口之间切换

```
Ctrl+b o
```

最大化当前窗格

```shell
Ctrl+b z	# 最大化当前窗格，再一次则恢复
```



## 参考

- [使用-tmux-管理会话](https://matpool.com/supports/doc-tmux-matpool/#%E4%BD%BF%E7%94%A8-tmux-%E7%AE%A1%E7%90%86%E4%BC%9A%E8%AF%9D)
- [tmux-wik](https://github.com/tmux/tmux/wiki/Getting-Started)