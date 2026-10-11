# 请同行 bot 评审的问题

1. **FINAL 策略**：现在用的是 `FINAL,漏网之鱼`（默认 PROXY），加 `GEOIP,CN,DIRECT`，和 Johnshall 白名单/lazy_group 以及 OpenClash 的 MATCH 一致。好处是没收录的海外站点也能打开；代价是没收录的国内非 CN-IP 站点（CDN 在海外）会绕一趟代理。要不要改成黑名单风格 `FINAL,DIRECT`？
2. **banlist 还是 allowlist**：Johnshall 的 banlist（GFWList + FINAL direct）和 whitelist（FINAL PROXY）都把 5–8 万行规则直接写进文件。我们这里改成远程 RULE-SET，文件只有约 140 行。ChinaMax 规则集很大，iPhone 内存/启动时间能接受吗？还是换成 China.list？
3. **广告拦截强度**：只用了 AdvertisingLite。要不要换成 Advertising（完整版）或加 Johnshall 的 reject 段？误杀风险（银行/支付 App）怎么看？
4. **AI 域名覆盖**：个人覆盖里已经包含 OpenClash 的 AI Suite 列表，另外补了 openai/chatgpt/anthropic/claude/cursor/perplexity/jetbrains.ai/githubcopilot。有没有漏掉的？比如 Gemini App 用到的 `*.gstatic.com`、`play.googleapis.com`，以及 grok 的 CDN 和 `*.x.com` 资源。
5. **accounts.google.com / www.googleapis.com 走 AI 组**：这是按 OpenClash 的设置照搬的，这样整个 Google 登录都会走 AI 组节点（默认美国）。可以接受吗？
6. **策略组正则**：地区关键词（比如「美」「港」）可能误匹配 sslink / oixCloud 的节点名，需要用实际订阅的节点名验证一下。
7. **Microsoft 默认 DIRECT**：但 msauth/login.microsoft.com 被强制 PROXY（OpenClash 就是这样设的），会不会引起登录态不一致？
8. **IPv6**：默认关闭。如果用户的运营商 IPv6 可用，要不要打开？
9. **仓库名**：暂定为 `qianzhouyang/shadowrocket-rules`，由 parent 来决定和推送。
