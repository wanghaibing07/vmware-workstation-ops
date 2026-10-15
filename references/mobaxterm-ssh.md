# MobaXterm 与 SSH | MobaXterm and SSH

## 连接状态 | Connection state

分别核实下列状态：

1. 目标 VM 正在运行。
2. 虚拟机内操作系统的 SSH 服务可达。
3. 选定用户的 SSH 认证成功。
4. MobaXterm 打开了对应会话，终端显示已登录。

Check these states separately:

1. The target VM is running.
2. The SSH service in the Guest OS is reachable.
3. SSH authentication succeeded for the selected user.
4. MobaXterm opened the intended session and the terminal is logged in.

TCP/22 连通可以证明网络路径可用；SSH 命令成功可以证明该账号认证成功；终端窗口可见时，再检查其远端主机和登录用户。按用户提出的目标核实所需状态。

An open TCP/22 connection confirms network reachability. A successful SSH command confirms authentication for that account. When a terminal window is visible, check its remote host and logged-in user. Verify the states required by the user's request.

## 版本与会话 | Version and sessions

先定位正在运行的 MobaXterm 程序，确认版本、配置文件位置、会话名称和用户选定的认证方式。不同发行版的会话能力和配置格式可能不同；优先使用官方支持的命令行选项或应用界面。

Locate the running MobaXterm executable and identify its version, configuration path, session name, and the authentication method selected by the user. Session features and configuration formats vary between editions; prefer documented command-line options or the application UI.

MobaXterm 官方文档列出 `-bookmark "<name>"` 和 `-newtab "<command>"` 等启动选项。调用前读取本机版本对应的说明，并把每个参数单独传递。

MobaXterm's documentation lists launch options such as `-bookmark "<name>"` and `-newtab "<command>"`. Check the documentation for the installed version and pass each argument separately.

## 会话文件 | Session files

需要调整会话文件时，先退出 MobaXterm 并确认相关进程已经关闭，再备份文件，使用本机版本支持的格式做小范围更改。重开应用后，核对会话显示、远端主机和 SSH 登录状态。

When a session file needs an update, exit MobaXterm and confirm its related processes have closed. Back up the file and make a small change using the format supported by the installed version. Reopen the app and check the displayed session, remote host, and SSH login state.

密码保存应由用户明确选择；密钥内容和密码保留在本机安全存储中。共享会话配置时只包含不含秘密的连接字段。

Let the user choose whether passwords are saved. Keep key contents and passwords in local secure storage. Share only connection fields that contain no secrets.

## 官方资料 | Official documentation

- [MobaXterm documentation](https://mobaxterm.mobatek.net/documentation.html)
- [OpenSSH manual pages](https://www.openssh.com/manual.html)
