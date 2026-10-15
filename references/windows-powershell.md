# Windows 与 PowerShell | Windows and PowerShell

## 调用本机程序 | Call native programs

在 PowerShell 中用独立参数调用程序，路径含空格时也保持参数边界清楚。使用 `ProcessStartInfo.ArgumentList` 等参数数组调用图形程序；把每次调用的退出码、标准输出、标准错误和超时结果分别记录。

In PowerShell, call programs with separate arguments so paths containing spaces remain unambiguous. Use an argument array such as `ProcessStartInfo.ArgumentList` for GUI programs. Record exit code, stdout, stderr, and timeout status separately.

根据本机可执行文件位置、版本帮助和官方文档确认用法。某些命令会输出可用帮助，同时以非零代码结束；阅读完整结果后再判断。

Check the executable path, version help, and official documentation for command syntax. Some commands print useful help and return a nonzero exit code; read the full result before assessing it.

## 编码与文件修改 | Encoding and file edits

修改 VMX 或其他本机配置前，读取原始字节并确认编码。备份后进行小范围修改，再用相同编码写回并读取验证。

Before editing a VMX or other local configuration, read its bytes and identify the encoding. Create a backup, make a focused change, write it with the same encoding, and read it back for verification.

用完整路径定位文件；通过临时文件完整写入后再替换，保持关键状态文件完整。报告只保留所需字段，并先脱敏认证信息与个人路径。

Use full paths to locate files. Write important state through a temporary file before replacement so the file stays complete. Keep reports focused and sanitize credentials and personal paths.

## 变更预览与记录 | Preview and record changes

对 PowerShell 修改脚本，支持 `-WhatIf` 或 `ShouldProcess`，让调用者在执行前查看计划。先验证目标路径和预期结果，再进行实际写入。

For PowerShell mutators, support `-WhatIf` or `ShouldProcess` so the caller can review a plan before execution. Validate the target path and expected result before writing.

涉及多个步骤时，每完成一项就保存可核对的状态；需要继续时，根据当前文件和实际运行状态确定下一步。

For multi-step work, record verifiable state after each action. When continuing, determine the next step from current files and running state.

## 凭据 | Credentials

密码、私钥、令牌和认证数据保存在专用的本机安全存储中。使用原生认证提示或支持的安全凭据接口；命令参数、调试输出和仓库只包含脱敏信息。

Store passwords, private keys, tokens, and authentication data in dedicated local secure storage. Use native authentication prompts or supported secure credential interfaces; keep command arguments, debug output, and repository files sanitized.
