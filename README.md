# VMware Workstation Ops

用 Codex 管理 VMware Workstation 虚拟机，需要时处理克隆、快照和 SSH 连接，并核实每一步的实际结果。

Use Codex to manage VMware Workstation VMs, handle clones, snapshots, and SSH sessions when needed, and verify each result against the running system.

## 适用范围 | What it covers

- 检查虚拟机状态，按请求启动或关闭虚拟机。<br>
  Check VM status and start or stop VMs when requested.
- 查看快照、克隆和虚拟磁盘之间的关系。<br>
  Review snapshot, clone, and virtual disk relationships.
- 通过实际安装的工具和版本选择操作方式。<br>
  Choose commands based on the installed tools and version.
- 按需使用 MobaXterm，并分别确认网络、SSH 登录和终端会话。<br>
  Use MobaXterm when needed, checking network access, SSH login, and the terminal session separately.

本 skill 面向 VMware Workstation 和 Windows 上的 MobaXterm。具体命令随产品版本和本机配置变化；使用前请查看本机帮助与官方文档。

This skill focuses on VMware Workstation and MobaXterm on Windows. Commands vary by product version and local setup, so check local help and the official documentation before use.

## 安装 | Install

在 Codex 中，使用 Skill Installer 从本仓库安装；也可以把仓库目录复制到用户级 skills 目录 `$HOME/.agents/skills/vmware-workstation-ops`。目录已存在时，选择新的安装目录，让已有 skill 保持原样。

In Codex, use Skill Installer to install from this repository, or copy the repository folder to `$HOME/.agents/skills/vmware-workstation-ops`. If that folder already exists, use a new location and keep the current skill as it is.

仓库根目录的 `SKILL.md` 是双语入口，详细说明放在 `references/` 中。

The root `SKILL.md` is the bilingual entry point. Detailed guidance lives in `references/`.

## 结构 | Files

- `SKILL.md` — Codex skill instructions / Codex skill 入口与操作说明
- `references/workstation-operations.md` — Workstation、快照、克隆与验证 / Workstation, snapshots, clones, and verification
- `references/windows-powershell.md` — Windows 命令、编码与结果记录 / Windows commands, encoding, and result capture
- `references/mobaxterm-ssh.md` — MobaXterm 与 SSH 会话 / MobaXterm and SSH sessions
- `CONTRIBUTING.md` — contribution guidance / 贡献说明

## 参考资料 | Sources

- [Codex: Build skills](https://learn.chatgpt.com/docs/build-skills)
- [Broadcom: VMware Workstation Pro documentation](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/25H2/using-vmware-workstation-pro.html)
- [MobaXterm documentation](https://mobaxterm.mobatek.net/documentation.html)
- [GitHub: Licensing a repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)

## 许可与商标 | License and trademarks

本项目使用 MIT License，是一份独立维护的操作指南。VMware、Workstation 和 MobaXterm 是其各自权利人的商标。

This project is an independently maintained guide under the MIT License. VMware, Workstation, and MobaXterm are trademarks of their respective owners.
