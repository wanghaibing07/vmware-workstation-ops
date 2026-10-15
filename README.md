# VMware Workstation Ops

**中文：** 让支持 Agent Skills 的 AI 助手协助管理 Windows 上的 VMware Workstation 虚拟机：查看运行状态、开关机、检查快照与克隆、核对磁盘和 SSH 连接。每项操作都以本机实际结果为准。

**English:** A reusable Agent Skill for AI assistants working with VMware Workstation on Windows. Inspect VMs, handle power operations, review snapshots and clones, check disks and SSH connections, and verify results on the host.

[中文说明](#能帮你做什么) · [English guide](README.en.md) · [Skill instructions / 操作规则](SKILL.md)

## 能帮你做什么

| 你想做的事 | 这个 Skill 提供的帮助 |
| --- | --- |
| 管理多台虚拟机 | 找到目标虚拟机、确认运行状态，并使用本机可用工具执行开关机操作 |
| 克隆虚拟机、整理快照 | 检查源虚拟机、快照、父磁盘与克隆关系，核对操作前后的文件和状态 |
| 准备 Linux / Kubernetes 节点 | 检查克隆机的主机名、IP、MAC、系统标识和 SSH 主机密钥，避免节点身份重复 |
| 连接和排查 SSH | 区分网络是否可达、SSH 是否认证成功、终端是否真正登录；按需使用 MobaXterm |

**它是什么？** 一份遵循 [Agent Skills 开放格式](https://agentskills.io/specification)的可复用操作指南。AI 助手会根据任务读取 `SKILL.md` 和相关参考文档，选择本机可用的工具执行、检查并汇报。无需绑定某一家 AI 产品。

## 快速开始

**准备条件：** Windows、VMware Workstation、支持 Agent Skills 的 AI 助手，以及该助手访问本机工具和目标虚拟机的权限。MobaXterm 只在需要图形化 SSH 会话时使用。

**1. 安装 Skill**

将**整个仓库目录**放到你所用 AI 工具支持的 skills 目录下，保持 `SKILL.md` 与 `references/` 的相对位置不变。

例如，使用支持 `~/.agents/skills/` 的工具时，在 Windows PowerShell 中运行：

```powershell
New-Item -ItemType Directory -Force "$HOME/.agents/skills" | Out-Null
git clone https://github.com/wanghaibing07/vmware-workstation-ops.git "$HOME/.agents/skills/vmware-workstation-ops"
```

不同工具识别 Skill 的目录可能不同。**Cursor、GitHub Copilot 等**可使用 `.agents/skills/`；**Claude Code** 常用 `~/.claude/skills/`。请以各工具当前文档为准，必要时调整上面的目标路径。

**2. 向 AI 助手提出具体任务**

可以直接复制这些请求（把虚拟机名称或路径换成自己的）：

- “使用 vmware-workstation-ops，列出当前运行的 VMware 虚拟机，并告诉我各自的 VMX 路径；先只检查，不修改。”
- “检查这台虚拟机的快照、克隆和磁盘依赖，再告诉我怎样安全地创建一个独立副本。”
- “检查刚克隆的三台 Linux 虚拟机，确认主机名、IP、MAC、machine-id 和 SSH 主机密钥不会冲突。”
- “检查这台虚拟机为什么连不上 SSH，分清是网络、认证还是 MobaXterm 会话问题。”

**3. 看实际结果**

AI 助手应说明：识别到了哪台虚拟机、用了哪些本机工具、观察到什么结果，以及是否完成请求。安装 Skill 只是提供操作方法；**能否实际控制虚拟机，取决于 AI 工具的本机访问能力与权限**。

## 运行方式与边界

- 面向 **Windows 上的 VMware Workstation**；主要使用已安装且适用于当前版本的 `vmrun`、`vmware.exe`、`vmware-vdiskmanager`、PowerShell 等工具。
- 可选配合 **SSH / MobaXterm** 连接虚拟机内的操作系统。虚拟机运行、网络通、SSH 登录成功是三件不同的事。
- 对克隆、磁盘和网络变更，先核实源文件、依赖关系与可用空间，再执行并复查；涉及破坏性操作时先确认目标和影响。
- **本仓库提供操作指引，不包含常驻服务或独立的 VMware 控制程序。** 不会仅凭安装 Skill 就获得远程访问权限。

## 仓库文件

- [`SKILL.md`](SKILL.md)：AI 助手读取的核心操作规则（中英双语）
- [`references/workstation-operations.md`](references/workstation-operations.md)：虚拟机、开关机、快照、克隆与磁盘
- [`references/windows-powershell.md`](references/windows-powershell.md)：Windows 工具调用、文件修改与结果验证
- [`references/mobaxterm-ssh.md`](references/mobaxterm-ssh.md)：MobaXterm、SSH 连接与会话检查
- [`CONTRIBUTING.md`](CONTRIBUTING.md)：问题反馈与贡献方式

## 官方资料

- [Agent Skills specification](https://agentskills.io/specification)
- [Cursor: Agent Skills](https://cursor.com/docs/skills)
- [GitHub Copilot: Add agent skills](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills)
- [Claude Code: Skills](https://code.claude.com/docs/en/skills)
- [Broadcom: VMware Workstation Pro](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/25H2/using-vmware-workstation-pro.html)
- [MobaXterm documentation](https://mobaxterm.mobatek.net/documentation.html)

## 许可

采用 [MIT License](LICENSE)。本项目为独立维护的 Agent Skill；VMware、Workstation、MobaXterm 是其各自权利人的商标。
