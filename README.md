# qzy-shadowrocket 规则

iPhone Shadowrocket 个人配置。参考 [Johnshall/Shadowrocket-ADBlock-Rules-Forever](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever) 的 `lazy_group.conf`，规则集用 [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)。分流方式和家里 OpenWrt OpenClash（sslink / oixCloud）保持一致。

## 导入

远程地址：

```
https://raw.githubusercontent.com/qianzhouyang/shadowrocket-rules/main/qzy-shadowrocket.conf
```

1. Shadowrocket → 底部「配置」→ 右上角「+」→ 粘贴上面的地址 → 下载。
2. 点一下刚下载的配置 →「使用配置」。
3. 首页「全局路由」选「配置」（也就是规则模式）。
4. 首页选一个节点当 `PROXY`。地区组（香港/日本/美国…）会按节点名关键词自动测速。

> 也可以用 URL Scheme 一键导入：`shadowrocket://config/add/https://raw.githubusercontent.com/qianzhouyang/shadowrocket-rules/main/qzy-shadowrocket.conf`

## 各段说明

| 段 | 作用 |
|---|---|
| [General] | 局域网和 Apple 验证域名不走代理，DNS 用阿里/腾讯 DoH，默认关闭 IPv6 |
| [Proxy Group] | 策略组：AI、YouTube、Netflix、Telegram、谷歌、微软、苹果、游戏、漏网之鱼，加上 6 个地区自动测速组 |
| 规则 0 个人覆盖 | 从 OpenClash `openclash_custom_rules.list` 同步过来，最先匹配。linuxdo.org 直连，speedtest 走漏网之鱼 |
| 1 局域网 | 内网 IP 直连 |
| 2 广告 | blackmatrix7 AdvertisingLite（轻量版），拒绝连接 |
| 3–8 海外服务 | AI → 流媒体 → Telegram/Google → SteamCN 直连/游戏 → 微软/苹果 → TikTok/Twitter/GitHub/Global |
| 9 国内 | ChinaMax 规则集 + `GEOIP,CN,DIRECT` |
| 10 兜底 | `FINAL,漏网之鱼`（默认 PROXY） |

## 更新

- 远程规则集（RULE-SET）Shadowrocket 会自动拉取。想马上更新：配置 → 点配置 →「更新」。
- 改个人覆盖：编辑 `qzy-shadowrocket.conf` 的「规则 0」段 → 推到 GitHub → 手机上点「更新」。
- OpenClash 自定义规则变了，记得同步到「规则 0」。
