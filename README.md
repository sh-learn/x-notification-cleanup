# X Notification Cleanup

这是一个用于清理 X/Twitter 通知里骚扰账号的 Codex skill。

它会让 Codex 使用你自己的 Chrome 登录态检查 X 通知列表，识别疑似色情、同城上门、Telegram 引流、垃圾信息或诈骗账号。流程默认分成两步：先只读筛选并列出候选账号，等你明确确认后，才执行举报和屏蔽。

## 功能

- 使用你自己的 Chrome X 登录状态。
- 第一阶段只读检查通知，不修改账号。
- 列出疑似账号、昵称和判断依据。
- 等你确认后才举报和屏蔽。
- 只处理明确确认的账号。
- 对正常点赞、关注、技术讨论回复保持保守，避免误伤。

## 安装

在终端运行：

```bash
cd /tmp
git clone https://github.com/sh-learn/x-notification-cleanup.git
mkdir -p ~/.codex/skills
rm -rf ~/.codex/skills/x-notification-cleanup
cp -R x-notification-cleanup ~/.codex/skills/
```

重启 Codex，或开启一个新会话，让 Codex 重新发现这个 skill。

如果以后要更新到最新版，可以重新运行上面的命令。

## 使用条件

- 使用支持 skills 的 Codex 环境。
- 已安装并启用 Chrome plugin / Codex Chrome Extension。
- 你已经在 Codex 可控制的同一个 Chrome Profile 里登录 X。

## 用法

可以这样对 Codex 说：

```text
用 x-notification-cleanup 检查我的 X 通知，先筛选疑似色情或垃圾账号给我确认，确认后再举报并屏蔽。
```

预期流程：

1. Codex 打开或接管 `https://x.com/notifications` 页面。
2. Codex 扫描通知列表，返回疑似账号候选列表。
3. 你确认要处理哪些账号。
4. Codex 只对你确认的账号执行举报和屏蔽。

## 安全边界

这个 skill 设计成保守流程。筛选阶段不应该举报、屏蔽、隐藏、取消关注，或执行任何会修改你 X 账号状态的动作。

当判断不确定时，它应该跳过或单独标注“低置信度”，而不是冒险屏蔽正常互动账号。
