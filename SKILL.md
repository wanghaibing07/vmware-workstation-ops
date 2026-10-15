---
name: vmware-workstation-ops
description: Safely inspect and operate VMware Workstation virtual machines, snapshots, clones, and virtual disks, with optional MobaXterm SSH sessions. / 安全检查和操作 VMware Workstation 虚拟机、快照、克隆及虚拟磁盘，并按需处理 MobaXterm SSH 会话。
---

# VMware Workstation Ops | VMware Workstation 操作

让 Codex 帮你管理 VMware Workstation 虚拟机，按需处理克隆、快照和 SSH 连接，并核实操作结果。

Use Codex to manage VMware Workstation VMs, handle clones, snapshots, and SSH sessions when needed, and verify each result.

## 使用方式 | How to use this skill

跟随用户使用的语言回复。先确认用户要完成的具体操作，再只处理相关内容。启动虚拟机、克隆磁盘、修改网络和连接 SSH 是不同的操作；按用户提出的事项逐项处理。

Reply in the user's language. Identify the requested action and keep the work focused on it. VM power, cloning disks, network changes, and SSH connections are separate operations; handle the items the user requests.

## 操作步骤 | Workflow

1. **查看本机环境。** 找出 Workstation 版本、相关命令和目标 VMX（虚拟机配置）文件；阅读本机工具帮助。工具位置、参数和能力随版本及安装方式变化。

   **Check the local setup.** Identify the Workstation version, relevant commands, and target VMX configuration files; read the installed tools' help. Paths, options, and capabilities vary by version and installation.

2. **先读当前状态。** 查看虚拟机电源、快照与磁盘链、可用主机资源，以及虚拟机内操作系统（Guest OS）或 SSH 状态。把实际文件与 VMware 当前显示的状态分别核对。

   **Read the current state first.** Check VM power, snapshots and disk chains, available host resources, and the Guest OS (the operating system inside the VM) or SSH state. Compare actual files with the state shown by VMware.

3. **说明将要做什么。** 修改文件、磁盘、虚拟机、Guest OS 或网络前，先说明目标虚拟机、具体变化和可用预览方式。按用户提出的操作逐项处理。

   **State the action.** Before changing files, disks, VMs, the Guest OS, or its network, identify the target VM, planned change, and available preview. Handle each item the user requested.

4. **逐步执行并记录结果。** 使用本机版本支持的命令。先预览变更；修改关键文件时先备份，再通过临时文件完整写入并替换。每项完成后核实结果，再继续下一项。

   **Work one step at a time and record the result.** Use commands supported by the installed version. Preview changes first. Back up important files, write through a temporary file, and verify each result before proceeding.

5. **确认用户关心的结果。** 分别查看虚拟机文件、电源状态、Workstation 库、Guest 服务、网络连通性、SSH 认证或 MobaXterm 会话；按任务选择需要的项目。

   **Verify the result the user cares about.** Check VM files, power state, Workstation library, Guest services, network access, SSH authentication, or the MobaXterm session separately. Select the checks that match the task.

6. **简明汇报。** 说清已完成的操作、观察到的结果，以及仍待处理的具体事项。

   **Report clearly.** State what was done, what you observed, and any specific item that still needs attention.

## 操作要点 | Practical guidance

- 保留源虚拟机与原始磁盘链；需要以源机为基础制作模板时，优先在独立位置创建完整克隆。

  Preserve the source VM and its original disk chain. When preparing a template from a source VM, prefer a full clone in a separate location.
- 使用链接克隆时，同时检查父虚拟机、快照和磁盘链的可用性。

  With a linked clone, check that its parent VM, snapshot, and disk chain remain available.
- 克隆加入集群前，核实每台虚拟机内操作系统的主机名、IP、MAC、系统 ID 和 SSH 主机密钥各不相同。

  Before adding clones to a cluster, verify that each Guest OS has a distinct hostname, IP, MAC, system ID, and SSH host key.
- 用 VMware 工具管理虚拟机，用 SSH 工具连接虚拟机内的操作系统；分别核实工具返回的信息。

  Use VMware tools to manage VMs and SSH tools to connect to Guest operating systems; verify each tool's result separately.
- 通过 MobaXterm 连接时，区分 TCP 可达、SSH 认证成功和终端已登录这三种状态。

  For MobaXterm connections, distinguish TCP reachability, successful SSH authentication, and a logged-in terminal.
- 将密码、私钥、令牌和完整凭据留在本机安全存储中；输出和仓库只保留脱敏后的必要信息。

  Keep passwords, private keys, tokens, and full credentials in secure local storage. Include only the minimum sanitized details in output and repository files.
- 文件、磁盘或 Guest 配置每次只改用户提出的部分；操作后重新读取并核对。

  Change only the file, disk, or Guest setting requested by the user; read it back and verify the result.

## 参考资料 | References

- [Workstation、快照与克隆 / Workstation, snapshots, and clones](references/workstation-operations.md)
- [Windows 与 PowerShell / Windows and PowerShell](references/windows-powershell.md)
- [MobaXterm 与 SSH / MobaXterm and SSH](references/mobaxterm-ssh.md)
- [Codex skill authoring / Codex skill 编写](https://learn.chatgpt.com/docs/build-skills)
