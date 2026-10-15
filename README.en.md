# VMware Workstation Ops

**English:** A reusable Agent Skill for AI assistants working with VMware Workstation on Windows. Inspect VMs, handle power operations, review snapshots and clones, check disks and SSH connections, and verify results on the host.

**中文：** 让支持 Agent Skills 的 AI 助手协助管理 Windows 上的 VMware Workstation 虚拟机：查看运行状态、开关机、检查快照与克隆、核对磁盘和 SSH 连接。每项操作都以本机实际结果为准。

[English](#what-can-it-help-with) · [简体中文](README.md) · [Skill instructions / 操作规则](SKILL.md)

## What can it help with?

| Your goal | How this skill helps |
| --- | --- |
| Work with multiple VMs | Find the correct VM, inspect its power state, and use supported local tools to start or stop it |
| Clone VMs or review snapshots | Check the source VM, snapshots, parent disks, clone dependencies, and resulting files |
| Prepare Linux / Kubernetes nodes | Check each clone's hostname, IP, MAC, system identity, and SSH host key before joining a cluster |
| Connect over SSH | Separate network reachability, SSH authentication, and a logged-in terminal; work with MobaXterm when useful |

**What is it?** A reusable operating guide based on the open [Agent Skills specification](https://agentskills.io/specification). A compatible AI assistant reads `SKILL.md` and relevant references, then uses tools available on the Windows host to perform and verify the requested task. It is **not tied to one AI product**.

## Quick start

**Requirements:** Windows, VMware Workstation, an Agent Skills-compatible AI assistant, and permission for that assistant to access the host tools and target VMs. MobaXterm is optional for graphical SSH sessions.

**1. Install the skill**

Copy the **entire repository folder** into a skills directory recognized by your AI tool. Keep `SKILL.md` and `references/` together.

For tools supporting `~/.agents/skills/`, this Windows PowerShell example installs it for the current user:

```powershell
New-Item -ItemType Directory -Force "$HOME/.agents/skills" | Out-Null
git clone https://github.com/wanghaibing07/vmware-workstation-ops.git "$HOME/.agents/skills/vmware-workstation-ops"
```

Supported locations depend on your agent: **Cursor and GitHub Copilot**, for example, recognize `.agents/skills/`; **Claude Code** commonly uses `~/.claude/skills/`. Consult your agent's current documentation and change the destination path if needed.

**2. Ask for a specific task**

Replace VM names or paths with your own:

- "Use vmware-workstation-ops to list running VMware VMs and their VMX paths. Inspect only; make no changes."
- "Review this VM's snapshots, clone relationships, and disk dependencies, then explain how to create an independent copy."
- "Check the three cloned Linux VMs for duplicate hostnames, IP addresses, MAC addresses, machine IDs, or SSH host keys."
- "Find out why this VM is unreachable over SSH. Check network access, authentication, and the MobaXterm session separately."

**3. Confirm the actual outcome**

The assistant should identify the target VM, explain which local tools it used, present observed evidence, and state whether the requested action completed. Installing the skill provides **instructions**, while actual VM control depends on the agent's host access and permissions.

## How it works and what it covers

- Designed for **VMware Workstation on Windows** using available, version-supported tools such as `vmrun`, `vmware.exe`, `vmware-vdiskmanager`, and PowerShell.
- Optionally uses **SSH / MobaXterm** to access the operating system inside a VM. A running VM, a reachable network port, and a successful SSH login are separate facts.
- For clone, disk, or network changes, checks the source, dependencies, and free space first; verifies the result afterwards. Potentially destructive operations require explicit identification of the target and impact.
- **This repository provides instructions, not a standalone VM management service.** Installing it does not grant remote access on its own.

## Repository layout

- [`SKILL.md`](SKILL.md) — bilingual instructions read by AI agents
- [`references/workstation-operations.md`](references/workstation-operations.md) — VM power, snapshots, clones, and disks
- [`references/windows-powershell.md`](references/windows-powershell.md) — Windows commands, file changes, and verification
- [`references/mobaxterm-ssh.md`](references/mobaxterm-ssh.md) — MobaXterm and SSH connection checks
- [`CONTRIBUTING.md`](CONTRIBUTING.md) — feedback and contributions

## Official references

- [Agent Skills specification](https://agentskills.io/specification)
- [Cursor: Agent Skills](https://cursor.com/docs/skills)
- [GitHub Copilot: Add agent skills](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills)
- [Claude Code: Skills](https://code.claude.com/docs/en/skills)
- [Broadcom: VMware Workstation Pro](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/25H2/using-vmware-workstation-pro.html)
- [MobaXterm documentation](https://mobaxterm.mobatek.net/documentation.html)

## License

Released under the [MIT License](LICENSE). This independently maintained Agent Skill is not affiliated with the owners of the VMware, Workstation, or MobaXterm trademarks.
