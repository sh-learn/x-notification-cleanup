---
name: x-notification-cleanup
description: X notification moderation workflow for checking a logged-in X/Twitter notifications page, identifying likely porn, sex-service, spam, or scam accounts from notification replies, presenting a candidate account list for user confirmation, then reporting and blocking only confirmed accounts. Use when the user asks to clean X notifications, find porn/escort/spam replies, inspect suspicious X accounts in notifications, or report and block nuisance accounts from X.
---

# X Notification Cleanup

## Core Rule

Use a two-stage workflow:

1. **Read-only screening:** Inspect the user's logged-in X notifications, identify suspicious accounts, and present a candidate list with evidence.
2. **Confirmed enforcement:** Only after the user explicitly confirms, report and block the confirmed accounts.

Never report, block, mute, unfollow, or otherwise modify the user's X account during the screening stage.

## Browser Setup

Prefer the Chrome plugin because X requires the user's logged-in browser session.

- Use the Chrome skill/workflow for browser automation.
- If Chrome extension communication fails, follow the Chrome plugin recovery steps. Do not fall back to unrelated browser-control mechanisms for account actions unless the user explicitly asks for that fallback.
- Claim an existing `https://x.com/notifications` tab when available. Otherwise open `https://x.com/notifications`.
- Keep browser discovery read-only until the user confirms enforcement.

## Screening Workflow

Collect visible notification articles from the notifications timeline and scroll a few screens as appropriate. Extract:

- handle, display name, and profile URL
- notification text and reply text
- visible profile signals if opened for verification, such as bio, follower counts, join date, external links, and repeated templates

Flag an account as high confidence when multiple signals appear:

- display name or bio contains terms like `同城`, `上门`, `约`, `私聊`, `福利`, `外围`, `妹妹`, `线下`, or similar sex-service phrasing
- reply is mostly emoji, blank/hidden characters, repeated symbols, or template-like filler
- profile bio links to Telegram or other off-platform contact funnels for sexual services
- very low-quality profile: random handle, zero/few followers, recent join date, many repetitive replies
- several notifications share the same template, style, link, or wording

Avoid low-confidence or ambiguous enforcement:

- Do not flag normal likes, follows, or topical replies without a clear spam/sexual-service signal.
- Do not treat random-looking handles alone as enough.
- When uncertain, put the account in a separate "possible but not recommended" section or omit it.

## Candidate Output

Before taking action, summarize candidates in Chinese when the user's conversation is in Chinese:

```text
我检查了通知列表，建议处理这些账号：

- @handle，昵称「...」：证据...

这些账号是否执行举报 + 屏蔽？
```

Include the intended report category if known, such as `成人色情内容` or `垃圾信息`. Prefer `成人色情内容` for explicit sex-service or porn-funnel profiles; prefer `垃圾信息` for non-sexual spam, phishing, or bulk promotion.

## Enforcement Workflow

After explicit user confirmation:

1. Open each confirmed profile page.
2. Open the profile "更多" menu (`userActions` when available).
3. Click `举报 @handle`.
4. Choose the closest category:
   - `成人色情内容` for porn/escort/sex-service accounts.
   - `垃圾信息` for bulk spam, scams, or phishing without sexual content.
5. Submit the report. Treat text like `已提交` or `感谢你帮助 X` as report success.
6. Click the report-completion `屏蔽 @handle` option when shown, or return to the profile menu and choose `屏蔽 @handle`.
7. Verify blocking with text like `已成功屏蔽`, `已屏蔽`, or `@handle 已被屏蔽`.

If an automation click fails, inspect current visible buttons/menu items and continue from the current state. Do not retry blindly in a way that might click unrelated accounts.

## Final Response

Report exactly what happened:

- accounts reported and blocked
- accounts skipped, if any, and why
- any accounts where report or block status could not be verified

Keep the final answer concise. Do not expose unrelated notification contents.
