`git commit` 是 Git 中用于提交更改到本地仓库的命令。以下是一些常用的 `git commit` 参数及其说明：

### 常用参数

- **-m** 或 **--message**
  - 用于指定提交信息。
  - 示例：`git commit -m "Add new feature"`。
- **-a** 或 **--all**
  - 自动将所有已跟踪的文件（包括修改和删除的文件）添加到暂存区并提交。
  - 示例：`git commit -a -m "Update files"`。
- **-p** 或 **--patch**
  - 以交互模式选择性地添加部分更改到暂存区。
  - 示例：`git commit -p`。
- **-v** 或 **--verbose**
  - 在提交信息编辑器中显示已暂存的更改内容。
  - 示例：`git commit -v`。
- **--amend**
  - 修改最近一次提交的内容（包括提交信息和更改）。
  - 示例：`git commit --amend`。
- **--author**
  - 指定提交的作者信息（格式为 `Name <email>`）。
  - 示例：`git commit --author="John Doe <john@example.com>"`。
- **--no-edit**
  - 提交时跳过编辑提交信息的步骤，直接使用默认的提交信息。
  - 示例：`git commit --no-edit`。
- **--dry-run**
  - 显示即将提交的内容，但不实际提交。
  - 示例：`git commit --dry-run`。

### 高级参数

- **--date**
  - 指定提交的日期。
  - 示例：`git commit --date="2025-05-02 12:00:00"`。
- **--signoff** 或 **-s**
  - 在提交信息中添加 `Signed-off-by` 行，用于表明提交者同意某些规则（如贡献协议）。
  - 示例：`git commit -s`。
- **--gpg-sign** 或 **-S**
  - 使用 GPG 签名提交。
  - 示例：`git commit -S`。
- **--include**
  - 将指定的文件或路径添加到暂存区并提交。
  - 示例：`git commit --include path/to/file`。
- **--only**
  - 只提交指定的文件或路径，忽略其他未暂存的更改。
  - 示例：`git commit --only path/to/file`。

### 注意事项

1. **提交信息的重要性**：清晰、简洁的提交信息有助于团队协作和代码维护。
2. **使用 -a 参数时**：虽然方便，但可能会不小心提交未完成的更改，建议在提交前仔细检查。
3. **--amend 的使用**：修改历史提交可能会导致问题，尤其是在与他人协作的仓库中，需谨慎使用。

这些参数可以根据你的需求灵活组合使用，以满足不同的提交场景。