---
name: vmware-workstation-ops
description: >-
  Guide AI agents in inspecting and operating VMware Workstation VMs on Windows.
  Use when asked to check VM status, start or stop VMs, review snapshots, clones
  or virtual disks, prepare cloned Linux nodes, or troubleshoot SSH and optional
  MobaXterm sessions. / 面向 Windows VMware Workstation 的通用 AI Agent 操作指南，
  适用于虚拟机状态、开关机、快照、克隆、磁盘、Linux 节点身份以及 SSH 连接检查。
---

# VMware Workstation Ops | VMware Workstation 虚拟机管理

本 Skill 供**支持 Agent Skills 的 AI 助手**使用。根据本机实际环境检查和管理 VMware Workstation 虚拟机，按需处理快照、克隆、磁盘与 SSH 连接，并验证操作结果。

This is a **vendor-neutral Agent Skill**. Use the agent's available local tools to inspect and manage VMware Workstation VMs, snapshots, clones, disks, and optional SSH sessions. Verify each outcome on the actual host.

## 使用原则 | How to use

- 按用户使用的语言回复。先确定目标虚拟机、用户希望完成的操作与预期结果；只处理相关内容。
- 用当前 AI 助手**实际可用**的工具工作：PowerShell、命令行、文件访问或受支持的界面操作。不要假定任何指定的 AI 产品或工具集已经可用。
- 如果不能访问本机或某项工具，说明已验证的信息和缺少的能力；不要把建议执行的命令说成已执行。
- 对可能影响现有虚拟机、磁盘或网络的操作，先说明将修改什么以及影响；对尚未获授权的破坏性变更先取得确认。

- Reply in the user's language. Identify the target VM, requested action, and expected result; stay focused on that task.
- Use **the tools actually available** to the current agent: PowerShell, CLI, file access, or supported UI controls. Do not depend on a particular AI vendor or assume tool access.
- When host access or a required tool is unavailable, distinguish observations from proposed commands; never present a suggested command as executed.
- Explain the target and impact before changes to VMs, disks, or networks. Obtain approval before destructive changes that the user has not authorized.

## 执行流程 | Workflow

1. **识别环境。** 检查 Windows 主机、Workstation 版本、目标 `*.vmx` 路径以及可用命令。参考本机帮助与对应版本文档，不套用未经确认的旧参数。

   **Identify the environment.** Check the Windows host, Workstation version, target `*.vmx` path, and available tools. Read the installed help and relevant version documentation.

2. **读取现状。** 按任务检查虚拟机运行状态、快照与磁盘链、可用空间、虚拟机内系统及网络状态。区分磁盘文件、Workstation 显示状态与 Guest OS 状态。

   **Inspect the current state.** Check VM power, snapshots, disk dependencies, free space, Guest OS, and network state as relevant. Distinguish files on disk from Workstation UI and Guest OS state.

3. **选择操作并预览。** 选用当前版本支持的 `vmrun`、`vmware.exe`、`vmware-vdiskmanager`、PowerShell 或其他可用方式。修改关键文件前备份；涉及配置文件时保留编码，使用临时文件完整写入、核对后替换。

   **Choose and preview the action.** Use supported local commands or available UI controls. Back up important files before editing; preserve encoding and verify temporary-file writes before replacement.

4. **逐项执行并复查。** 完成一项后重新读取实际状态，再继续下一项。检查内容由任务决定：VMX、磁盘文件、运行状态、Guest 服务、网络连通性、SSH 认证或 MobaXterm 会话。

   **Execute and verify one step at a time.** Re-read actual state after each action. Depending on the task, verify VMX and disk files, power, Guest services, network reachability, SSH authentication, or an active MobaXterm session.

5. **清楚交付结果。** 报告做了什么、依据什么确认、哪些事项仍待处理；明确区分“已执行并验证”与“提供建议但未执行”。

   **Report the result.** State what changed, the evidence that confirms it, and anything still pending. Distinguish verified actions from unexecuted recommendations.

## 关键检查 | Important checks

- **完整克隆 / Full clone：** 需要独立副本时，优先在另一位置创建完整克隆，保留源虚拟机及原始磁盘链。 / Prefer a full clone in a separate location when an independent copy is needed; preserve the original VM and disk chain.
- **链接克隆 / Linked clone：** 使用前确认父虚拟机、快照及磁盘链持续可用。 / Ensure the parent VM, snapshot, and disk chain remain accessible.
- **集群节点 / Cluster nodes：** 克隆加入集群前，逐台核对主机名、IP、MAC、系统标识（如 machine-id）和 SSH 主机密钥的唯一性。 / Before joining clones to a cluster, verify unique hostnames, IPs, MACs, system IDs, and SSH host keys.
- **分层验证 / Layered checks：** 虚拟机开机、TCP 端口可达、SSH 认证成功、终端已登录是不同状态；按用户目标逐项核实。 / VM power, TCP reachability, SSH authentication, and an active terminal are separate facts.
- **凭据 / Credentials：** 密码、令牌与私钥留在本机安全存储；输出仅保留脱敏信息。 / Keep credentials in local secure storage and sanitize reports.

## 按需阅读 | Read references as needed

- [Workstation 虚拟机、快照、克隆与磁盘 / Workstation operations](references/workstation-operations.md)
- [Windows 命令、PowerShell 与文件验证 / Windows and PowerShell](references/windows-powershell.md)
- [MobaXterm 与 SSH 连接 / MobaXterm and SSH](references/mobaxterm-ssh.md)

Agent Skills 格式 / Agent Skills format: https://agentskills.io/specification
