# Workstation 操作 | Workstation operations

## 选择工具 | Choose the tool

- `vmrun` 用于控制虚拟机和执行受支持的 Guest 操作。
- `vmware.exe` 用于打开 Workstation 界面中的虚拟机。
- `vmware-vdiskmanager` 用于受支持的虚拟磁盘维护操作。
- `vmrest` 等接口会引入服务、端口和认证设置；使用前先确认本机版本、接口状态和所需权限。

- `vmrun` controls VMs and runs supported Guest operations.
- `vmware.exe` opens a VM in the Workstation interface.
- `vmware-vdiskmanager` handles supported virtual disk maintenance.
- Interfaces such as `vmrest` introduce service, port, and authentication settings; first check the installed version, interface state, and required permissions.

使用 `Get-Command` 或安装目录定位工具，再查看该版本的帮助和官方说明。按操作所需选择工具，不根据旧版本的示例推断本机能力。

Use `Get-Command` or the installation directory to locate tools, then read their installed help and official documentation. Choose a tool for the task at hand and check the local version before applying examples.

## 快照、克隆与磁盘 | Snapshots, clones, and disks

开始前，确认源 VM、选定快照、所有父磁盘、目标位置、磁盘空间和当前电源状态。操作后确认目标 VMX 和磁盘文件都已生成。

Before starting, check the source VM, selected snapshot, parent disks, destination, available disk space, and current power state. Afterwards, confirm that the target VMX and disk files exist.

- 完整克隆包含独立磁盘副本，适合保留来源虚拟机或迁移副本。
- 链接克隆与父磁盘共享基础数据，适合短期使用；父机和磁盘链需要持续可用。
- 快照记录某一时刻的虚拟机状态；重要数据另存于独立备份中。

- A full clone has its own disk copy and suits cases where the source VM must remain intact or the copy will move independently.
- A linked clone shares base data with its parent and suits temporary use; keep the parent and disk chain available.
- A snapshot records a VM state. Keep a separate backup for data that must be recoverable.

需要保留源机时，在独立目录创建完整克隆；先读取并记录关键源文件信息，再比较操作前后的结果。编辑 VMX 时仅修改任务所需字段并保留原编码。先备份，把新内容写入临时文件，检查后再替换原文件。

When preserving the source VM, create a full clone in a separate directory. Record key source file details before the operation and compare them afterwards. For VMX edits, change only the requested fields and preserve the original encoding. Back up the file, write the new content to a temporary file, verify it, then replace the original.

## 虚拟机内系统与集群身份 | Guest OS and cluster identity

克隆启动后，逐台核对虚拟机内系统的主机名、IP、MAC、系统标识（例如 machine-id 或 product UUID）和 SSH 主机密钥指纹。所有节点身份唯一、网络配置合理后，再进行集群初始化。

After booting clones, check each Guest OS hostname, IP, MAC, system identifier (such as machine-id or product UUID), and SSH host key fingerprint. Initialize a cluster after every node has a unique identity and a valid network configuration.

VMware Tools 已安装与 Guest 内的 Tools 服务正在运行是两项不同信息；需要 Guest 操作时，检查实际服务状态和工具返回结果。

VMware Tools being installed and its service running inside the Guest are separate facts. For Guest operations, check the actual service state and tool result.

## 电源与 Workstation 库 | Power and Workstation library

通过 `vmrun list`、与目标 VMX 路径匹配的 VMware 进程、Workstation 库和实际 VMX 文件分别确认状态。这些信息回答的问题不同。

Check power state with `vmrun list`, VMware processes matching the target VMX path, the Workstation library, and the actual VMX files. Each observation answers a different question.

需要在 Workstation 库中显示虚拟机时，通过 Workstation 打开 VMX，再从界面或受支持的本地接口确认。把 Workstation 的清单作为只读状态查看，不手工写入其内部文件。

When a VM should appear in the Workstation library, open its VMX through Workstation and confirm it in the interface or a supported local interface. Read Workstation's inventory as state information and let Workstation manage it.

## 官方资料 | Official documentation

- [Broadcom: Using the vmrun command](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/25H2/using-vmware-workstation-pro/using-the-vmrun-command-to-control-virtual-machines.html)
- [Broadcom: Clone a virtual machine](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/25H2/using-vmware-workstation-pro/creating-virtual-machines-in-workstation-user-guide/cloning-virtual-machines/clone-a-virtual-machine.html)
- [Broadcom: Using linked clones](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/25H2/using-vmware-workstation-pro/creating-virtual-machines-in-workstation-user-guide/cloning-virtual-machines/using-linked-clones.html)
- [Broadcom: Using full clones](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/25H2/using-vmware-workstation-pro/creating-virtual-machines-in-workstation-user-guide/cloning-virtual-machines/using-full-clones.html)
