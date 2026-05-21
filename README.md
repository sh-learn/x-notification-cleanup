# X Notification Cleanup

A Codex skill for cleaning nuisance accounts from X/Twitter notifications.

It helps Codex inspect a logged-in X notifications page, identify likely porn, escort-service, spam, or scam accounts, show a candidate list first, and only after explicit confirmation report and block those accounts.

## What It Does

- Uses your own Chrome login session for X.
- Screens notifications in a read-only first pass.
- Lists suspicious accounts with evidence.
- Waits for your confirmation before account actions.
- Reports and blocks only confirmed accounts.
- Skips normal likes, follows, and topical replies unless there is clear spam or sexual-service evidence.

## Install

Copy this folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R x-notification-cleanup ~/.codex/skills/
```

Restart Codex or start a new session so the skill is discovered.

## Requirements

- Codex with skills support.
- Chrome plugin / Codex Chrome Extension enabled.
- You are logged in to X in the same Chrome profile that Codex can control.

## Usage

Ask Codex:

```text
用 x-notification-cleanup 检查我的 X 通知，先筛选疑似色情或垃圾账号给我确认，确认后再举报并屏蔽。
```

The intended flow is:

1. Codex opens or claims `https://x.com/notifications`.
2. Codex scans notifications and returns a candidate list.
3. You confirm which accounts to handle.
4. Codex reports and blocks only those confirmed accounts.

## Safety

The skill is designed for a conservative workflow. It should not report, block, mute, unfollow, or otherwise modify your X account during the screening stage.

When in doubt, it should skip ambiguous accounts rather than risk blocking normal interactions.
