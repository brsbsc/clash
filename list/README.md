# 📂 clash / list

## 前言

本目录存放**自维护的分流规则**，格式与 [blackmatrix7/ios_rule_script · rule/Clash](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash) 一致（Clash classical 纯文本，一行一条，不写策略名）。

- 上游已有且足够好的规则，**直接引用上游**，不在这里复制。
- 这里只放：上游没有的服务、需要比上游更全/更精简的版本、个人专用的代理/直连补充、IP 规则。
- 原 [brsbsc/nodnsleak](https://github.com/brsbsc/nodnsleak) 仓库的 list 已于 2026-11 合并到本目录（带提交历史）；订阅转换模板在 [../ini](../ini)。

规则链接统一格式：

```
https://raw.githubusercontent.com/BRSBSC/clash/refs/heads/main/list/<文件名>
https://cdn.jsdelivr.net/gh/brsbsc/clash@main/list/<文件名>
```

## 分类

| 🎯 自定义分流 |  |
| ---- | ---- |
| [Custom-Long](#custom-long) | [Custom-Temp](#custom-temp) |

| 🌐 IP 规则 |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- |
| [TargetIP](#targetip) | [SourceIP](#sourceip) | [GlobalIp](#globalip) | [CS2](#cs2) | [gn01](#gn01) |

| ✨ AI |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- |
| [AI](#ai) | [AI2](#ai2) | [ChatGPT](#chatgpt) | [Claude](#claude) | [Gemini](#gemini) |
| [Copilot](#copilot) | [Grok](#grok) | [MetaAi](#metaai) | [Perplexity](#perplexity) | [302](#302) |

| 🍎 Apple |  |
| ---- | ---- |
| [Apple](#apple) | [AppleAI](#appleai) |

| 🌏 代理 / 直连补充 |  |  |  |
| ---- | ---- | ---- | ---- |
| [Proxy](#proxy) | [Direct](#direct) | [Check](#check) | [Download](#download) |

| 📦 上游快照（来自 blackmatrix7） |  |
| ---- | ---- |
| [ChinaDomain](#chinadomain) | [PrivateTracker](#privatetracker) |

| 📺 媒体 / 娱乐 |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- |
| [YouTube](#youtube) | [Crunchyroll](#crunchyroll) | [huanlekan](#huanlekan) | [Popcorn](#popcorn) | [Sex](#sex--pornhub) |
| [Pornhub](#sex--pornhub) | | | | |

| 💰 加密货币 / 博彩 |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- |
| [Crypto](#crypto) | [xnb](#xnb) | [ww01](#ww01--ww02--ww03) | [ww02](#ww01--ww02--ww03) | [ww03](#ww01--ww02--ww03) |

| 🚫 Reject |
| ---- |
| [Block](#block) |

## 总览

| 文件 | 内容 | 规则数 | 上游对应规则 | 当前引用位置 |
| ---- | ---- | ---: | ---- | ---- |
| Custom-Long.list | 长期走代理的补充域名 | 193 | — | **smart.yaml → Custom-Long** |
| Custom-Temp.list | 临时 / 测试走代理的域名 | 9 | — | **smart.yaml → Custom-Temp** |
| TargetIP.list | 指定目标 IP | 5 | — | **smart.yaml → Custom-Long**、ini/nodnsleak4.ini（DIRECT） |
| SourceIP.list | 指定局域网源 IP 直连 | 1 | — | **smart.yaml → 国内**、ini/nodnsleak4.ini、ini/clashfull.list |
| GlobalIp.list | 全部 IPv4 | 1 | — | 未引用（备用） |
| AI.list | ChatGPT + Claude + Gemini + Copilot + Grok 等合集 | 36 | — | ini/clashfull.list |
| AI2.list | Meta AI + Perplexity | 3 | — | ini/clashfull.list |
| ChatGPT.list | OpenAI / ChatGPT | 16 | [OpenAI](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/OpenAI)（35） | 未引用（smart.yaml 用上游 OpenAI） |
| Claude.list | Claude / Anthropic | 8 | [Claude](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Claude)（3） | **smart.yaml → Claude** |
| Gemini.list | Gemini / AI Studio | 11 | [Gemini](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Gemini)（13） | 未引用（smart.yaml 用上游 Gemini） |
| Copilot.list | Copilot + Bing | 2 | [Copilot](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Copilot)（51） | 未引用（smart.yaml 用上游 Copilot） |
| Grok.list | Grok / xAI | 3 | 无 | **smart.yaml → Grok** |
| MetaAi.list | Meta AI + Genspark / Manus / Skywork | 5 | 无 | **smart.yaml → Meta AI** |
| Perplexity.list | Perplexity | 1 | 无 | 未引用 |
| 302.list | 302.AI 中转 | 1 | 无 | 未引用 |
| Apple.list | Apple Relay + Apple Intelligence | 11 | [AppleProxy](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/AppleProxy)（40） | 未引用 |
| AppleAI.list | Apple Intelligence | 7 | 无 | 未引用 |
| Proxy.list | 走代理的域名 + IP 段补充 | 307 | [Proxy](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Proxy)（6985） | ini/clashfull.list |
| Direct.list | 国内直连补充（机场域名、国内 DNS 等） | 584 | [Direct](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Direct)（267） | **smart.yaml → 国内** |
| Check.list | IP 检测 / 测速 / 分流测试站点 | 61 | [Speedtest](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Speedtest)（8） | **smart.yaml → Test**、ini/clashfull.list |
| Download.list | 国内下载直连（占位，空） | 0 | [Download](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Download)（34） | 未引用 |
| ChinaDomain.list | 国内域名（上游 China 快照） | 3700 | [China](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/China)（3721） | ini/nodnsleak4.ini、ini/nodnsleak5.ini |
| PrivateTracker.list | PT 站（上游快照） | 277 | [PrivateTracker](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/PrivateTracker)（248） | ini/nodnsleak2.ini |
| YouTube.list | YouTube 补充 IP 段 | 1 | [YouTube](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/YouTube)（183） | 未引用（smart.yaml 用上游 YouTube） |
| Crunchyroll.list | Crunchyroll | 3 | 无 | 未引用 |
| huanlekan.list | 欢乐看（台湾） | 2 | 无 | 未引用 |
| Popcorn.list | popcorn.plus | 1 | 无 | 未引用 |
| Sex.list | 成人站合集 | 3 | 无 | 未引用 |
| Pornhub.list | Pornhub | 1 | 无 | 未引用 |
| Crypto.list | 交易所（OKX / Binance / Bybit / Gate 等） | 21 | [Cryptocurrency](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Cryptocurrency)（43）、[Binance](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Binance)（12） | 未引用 |
| xnb.list | TronLink 钱包 | 1 | 无 | 未引用 |
| ww01 / ww02 / ww03.list | 博彩站点分组 | 9 / 4 / 8 | 无 | 未引用 |
| CS2.list | CS2 / Valve 游戏服务器 IP 段 | 619 | 无 | 未引用 |
| gn01.list | 指定专线 IP 段 | 3 | 无 | 未引用 |
| Block.list | Adobe 正版验证拦截 | 4 | [Adobe](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Adobe)（137） | **smart.yaml → REJECT** |

> - 规则数为去掉注释与空行后的有效行数，统计于 2026-11-16；上游括号内为上游 README 中的 TOTAL。
> - "未引用"指当前 smart.yaml 和 ini/ 都没有用到。远端历史版本里的 `Clash-*.ini`、`proxy/*.ini` 曾引用过其中一部分（AI、ChatGPT、Perplexity、YouTube、xnb、ww01~03、gn01 等），改名或删除前先确认这些 ini 是否还在使用。

---

## Custom-Long

#### 用途
长期需要走代理、但上游规则没有覆盖的域名。文件内按主题分段（`# === xxx ===`），新增条目请放进对应分段：

| 分段 | 内容 |
| ---- | ---- |
| AI、工具与软件服务 | 各类 AI 工具站、开发工具、软件官网 |
| PT、影视与资源站 | PT 站、影视站、资源下载站 |
| 红果 | 红果相关域名 |
| IDC、云服务与网络工具 | VPS 商家、云服务、网络测试工具 |
| 社区、论坛与交流 | 论坛、社区 |
| 游戏与其它 (含特定 CDN) | 游戏站点及其 CDN |
| 直播源 | 直播源域名 |
| 特定后端/接口 | 指定的 API / 后端 |
| 加密币 | 交易所、钱包等 |

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 183 |
| DOMAIN-KEYWORD | 10 |
| TOTAL | 193 |

#### 使用说明
- behavior: `classical`，format: `text`
- smart.yaml 中排在**第 3 位**（仅次于 TargetIP / SourceIP），优先级高于所有业务规则，可用来"强制覆盖"上游规则的分流结果。

---

## Custom-Temp

#### 用途
临时条目：测试某个站点是否需要代理、短期使用的服务。确认要长期保留后**移入 Custom-Long**；不再需要就删除。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 8 |
| DOMAIN-KEYWORD | 1 |
| TOTAL | 9 |

另有 1 条被注释的 `SRC-IP-CIDR`（临时让某台设备走 Custom-Temp 组）。

#### 使用说明
- smart.yaml 中紧跟 Custom-Long，对应独立策略组 **Custom-Temp**，可单独切换节点做测试。
- 该行目前用 `;` 注释；list 文件建议统一用 `#` 注释。

---

## TargetIP

#### 用途
按**目标 IP** 分流：访问这些 IP（自建 VPS、指定服务器等）时走 Custom-Long 组。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| IP-CIDR | 5 |

#### 使用说明
- behavior: `classical`（每行带 `IP-CIDR,` 前缀，不能配成 `ipcidr` behavior）
- 每条都带 `,no-resolve`，单个 IP 用 `/32`
- smart.yaml 中是**第 1 条规则** → Custom-Long（代理）
- ⚠️ ini/nodnsleak4.ini 中同一份文件指向 **DIRECT**，两边语义相反，修改时注意。

---

## SourceIP

#### 用途
按**局域网源 IP** 分流：指定网段的设备（当前 `10.10.10.224/27`）全部直连。

#### 使用说明
- behavior: `classical`，smart.yaml 中是第 2 条规则 → 国内；ini/clashfull.list 中 → ➡️ 国内
- 改网段时与路由器 DHCP 分配范围保持一致

---

## GlobalIp

`IP-CIDR,0.0.0.0/0`，匹配全部 IPv4。给需要"所有 IP 都走某个组"的模板备用，当前未引用。

---

## AI

#### 用途
AI 服务大合集，一个文件覆盖 ChatGPT、Claude、Gemini、Copilot、Grok、Groq、Dify、Genspark 等。适合**只想要一个 ✨ AI 策略组**的模板（如 ini/clashfull.list）。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 35 |
| DOMAIN | 1 |
| TOTAL | 36 |

#### 使用说明
- ⚠️ 包含 `googleapis.com`、`gstatic.com`、`x.com`、`bing.com` 这类**大范围域名**，引用后 Google / X 的大量普通流量也会进 AI 组。如果另有 Google、Twitter 组，要把 AI 放在它们后面，或删掉这些条目。
- 拆分版本：ChatGPT / Claude / Gemini / Copilot / Grok 各自单独的 list。新增 AI 域名时，**合集和拆分版都要改**。

## AI2

AI 补充：Meta AI（`meta.ai`、`metademolab.com`）+ Perplexity。与 AI.list 搭配使用。

---

## ChatGPT

#### 用途
OpenAI / ChatGPT。含 `DOMAIN-KEYWORD,openai`，以及登录、风控、支付依赖（auth0、arkoselabs、statsig、intercom、sentry、stripe）。

#### 使用说明
- smart.yaml 目前用上游 [OpenAI.list](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/OpenAI)（35 条，含 IP-ASN），比本文件更全；本文件留作备用 / 精简版。
- `stripe.com`、`sentry.io` 会把其他网站的支付、报错上报也带进 ChatGPT 组，属预期行为。

---

## Claude

#### 用途
Claude / Anthropic。已合并原 nodnsleak/claude.list，smart.yaml 的 **Claude** 组引用本文件。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 6 |
| DOMAIN-KEYWORD | 2 |
| TOTAL | 8 |

#### 使用说明
- 后缀：`anthropic.com`、`claude.ai`、`claude.com`、`clau.de`、`claudemcpclient.com`、`claudeusercontent.com`
- 关键字：`anthropic`、`claude`（兜住新出现的子域名/新域名，代价是可能误伤含这两个词的其他站点）
- 已有后缀规则时，不需要再为子域名单独加 `DOMAIN`。

---

## Gemini

#### 用途
Gemini、Bard、AI Studio、MakerSuite 及其 API（`generativelanguage.googleapis.com` 等）。

#### 使用说明
- ⚠️ 含 `googleusercontent.com`、`android.googleapis.com`，范围较大。
- smart.yaml 用的是上游 [Gemini.list](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Gemini)。

## Copilot

`DOMAIN,copilot.microsoft.com` + `DOMAIN-SUFFIX,bing.com`。上游 Copilot（51 条）更全，smart.yaml 用上游。

---

## Grok

#### 用途
Grok / xAI。已合并原 nodnsleak/grok.list，smart.yaml 的 **Grok** 组引用本文件。上游没有 Grok 规则。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 2 |
| DOMAIN-KEYWORD | 1 |
| TOTAL | 3 |

内容：`grok.com`、`x.ai`（含 api / auth / groksandbox 等子域名）、关键字 `grok`。

---

## MetaAi

#### 用途
Meta AI 及其他未单独分组的 AI 产品：`meta.ai`、`metademolab.com`、`genspark.ai`、`manus.im`、`skywork.ai`。smart.yaml 中对应 **Meta AI**。

新出现、又不值得单独建组的 AI 产品，可以先放这里。

## Perplexity

`DOMAIN-SUFFIX,perplexity.ai`。上游无对应规则。

## 302

`DOMAIN-SUFFIX,proxy302.com`（302.AI API 中转）。上游无对应规则。

---

## Apple

#### 用途
iCloud 专用代理（Private Relay）+ Apple Intelligence 相关域名，让 Apple Intelligence / Private Relay 走指定地区节点。

#### 使用说明
- 与 AppleAI.list 大部分重叠，额外包含 `DOMAIN-KEYWORD,apple-relay`、`gateway.icloud.com`、`apps.mzstatic.com`、`apple-dns.net`。
- **不要**与上游 Apple.list（1592 条、整体 Apple 服务）混为一谈；如需一起用，本文件要放在上游 Apple 之前。

## AppleAI

只含 Apple Intelligence 的 7 个域名（guzzoni、smoot、apple-relay 等），是 Apple.list 的精简版。

---

## Proxy

#### 用途
上游 Proxy / Global 没覆盖、但需要走代理的域名和 IP 段。文件内分段：

| 分段 | 内容 |
| ---- | ---- |
| IP段匹配 | 机场、VPS 等 IP 段（约 144 条） |
| AI | 零散 AI 站点 |
| capcut / 小牛 / ssrdog / 小牛机场 | 特定服务、机场官网 |
| 国外DNS | `dns.google`、`dns.quad9.net` 等 DoH |
| 其他网站 | 其余需要代理的站点 |

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 163 |
| IP-CIDR | 144 |
| TOTAL | 307 |

#### 使用说明
- smart.yaml 目前用上游 Proxy + Global，**没有引用本文件**；ini/clashfull.list 中 → 🌍 国外。

---

## Direct

#### 用途
国内直连补充：防止国内域名在 fake-ip 模式下未解析就落到代理。文件内分段：

| 分段 | 内容 |
| ---- | ---- |
| MyList | 个人站点、机场官网（快猫、火烧、猫耳、BestVPN、小牛、硅谷、无界、HK-Beup、冰云、牛逼、九游等） |
| 域名关键字匹配 | 少量 KEYWORD |
| IP段匹配 / VPS | 国内 VPS、指定 IP |
| 国内DNS | 国内 DoH / DNS 域名 |
| 360、58、Alibaba、Baidu、Bilibili、ByteDance、CCTV、HuaWei、Iqiyi、PDD… | 按厂商分段的国内服务 |

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 571 |
| IP-CIDR | 12 |
| DOMAIN-KEYWORD | 1 |
| TOTAL | 584 |

#### 使用说明
- smart.yaml 中对应 **国内**，位于规则末尾（上游 China 之前）。
- 因为位置靠后，**挡不住**前面的业务规则（例如某个国内 CDN 被上游 Google 规则命中）。需要抢优先级的直连：新建一个 list，在 smart.yaml 中放到 Custom-Temp 之后。
- 新增条目放进对应厂商分段，没有合适分段就放 MyList。

---

## Check

#### 用途
IP 归属检测、测速、分流测试站点（ipip.net、ipinfo.io、test-ipv6.com、vultr 测速等）。单独分到 **Test** 组，方便切换节点验证出口 IP / 解锁情况。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 58 |
| IP-CIDR | 2 |
| DOMAIN | 1 |
| TOTAL | 61 |

#### 使用说明
- smart.yaml 中对应 **Test**（规则集名 `TEST / Domain`）；ini/clashfull.list 中 → 🌍 国外。
- 注释掉的 Netflix 检测域名（`ichnaea-web.netflix.com` 等），需要测 Netflix 解锁时可临时打开。

## Download

占位文件，只有一行注释 `# 国内下载直连`。需要时参考上游 [Download](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Download)。

---

## ChinaDomain

#### 用途
国内域名直连。上游 [China](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/China) 在 **2024-11-17** 的快照（文件头注明），之后未同步。只给 ini/nodnsleak4、nodnsleak5 用；smart.yaml 直接引用上游 China。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 3676 |
| DOMAIN | 15 |
| DOMAIN-KEYWORD | 9 |
| TOTAL | 3700 |

#### 更新
```bash
curl -fsSL https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Clash/China/China.list -o ChinaDomain.list
```
或者把 ini 里的链接直接换成上游地址，然后删除本文件。

## PrivateTracker

PT 站点直连。上游 [PrivateTracker](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/PrivateTracker) 在 **2024-12-09** 的快照（277 条），只给 ini/nodnsleak2.ini 用。更新方式同 ChinaDomain（换成上游 `PrivateTracker/PrivateTracker.list`）。

---

## YouTube

`IP-CIDR,199.16.158.0/24,no-resolve`：上游 YouTube 规则之外的补充 IP 段。

## Crunchyroll

`crunchyroll.com`、`crunchyrollcdn.com`、`crunchyrollsvc.com`。上游无对应规则。

## huanlekan

欢乐看：`faintv.com.tw` + `120.241.29.0/24`。

## Popcorn

`popcorn.plus`。

## Sex / Pornhub

Sex.list：`t66y.com`、`pornhub.com`、`xvideos.com`；Pornhub.list 只有 `pornhub.com`（Sex 的子集，二选一引用即可）。

---

## Crypto

#### 用途
加密货币交易所与相关站点，按交易所分段：博彩（1win、stake、bc.game）/ OKX / Binance / Bybit / Gate。

#### 使用说明
- 上游 [Cryptocurrency](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Cryptocurrency)、[Binance](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Binance) 可作补充。
- 交易所对节点地区敏感，建议单独建组并固定到可用地区。

## xnb

`tronlink.org`（TronLink 钱包）。

## ww01 / ww02 / ww03

博彩站点分三组（便于分别指定节点）：

| 文件 | 域名 |
| ---- | ---- |
| ww01.list | beer555 / beer777 / beer111、tek789、colourhim、sbogogo、u16888、potato777、sbobet |
| ww02.list | isn99、isn88、whiskey1368、ps3838 |
| ww03.list | nova88、novabet88、nova866、webook88、po288、168111.net、nv9891、livebook88 |

---

## CS2

#### 用途
CS2 / Valve 游戏服务器 IP 段（619 条 IP-CIDR），游戏加速时让对战流量走指定节点。

#### 使用说明
- 第一条 `162.254.192.0/2` 掩码是 /2，范围约四分之一个 IPv4 空间，疑似笔误（Valve 的段通常是 `162.254.192.0/21`），启用前请核对。
- 上游 Steam / SteamCN 只管商店与下载，不含对战服 IP。

## gn01

3 个指定 IP 段（`49.0.228.0/24`、`49.0.236.0/24`、`119.13.94.0/24`），文件里写成 `x.x.x.1/24`，内核按 /24 处理。

---

## Block

#### 用途
拦截 Adobe 正版验证 / 统计：`adobe.com`、`adobedtm.com`、`adobe.io`、`omtrdc.net`。

#### 使用说明
- smart.yaml 中 → **REJECT**，位置在 AI / 业务规则之前。
- ⚠️ 会同时挡掉 Adobe 官网与登录；需要登录 Adobe 账户时临时关闭这条规则。
- 上游 [Adobe](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Adobe)（137 条）是"Adobe 全部服务"，不是拦截列表，别直接拿来 REJECT。

---

## 维护指南

### 规则写法

| 类型 | 示例 | 说明 |
| ---- | ---- | ---- |
| DOMAIN-SUFFIX | `DOMAIN-SUFFIX,example.com` | 匹配域名及所有子域名，**首选** |
| DOMAIN | `DOMAIN,api.example.com` | 只匹配完整域名 |
| DOMAIN-KEYWORD | `DOMAIN-KEYWORD,example` | 包含关键字即匹配，慎用 |
| IP-CIDR | `IP-CIDR,1.2.3.0/24,no-resolve` | 目标 IP，**必须加 no-resolve** |
| IP-CIDR6 | `IP-CIDR6,2001:db8::/32,no-resolve` | IPv6 |
| SRC-IP-CIDR | `SRC-IP-CIDR,10.10.10.0/24,no-resolve` | 局域网源设备 |

- list 里**不写策略名**；注释用 `#`。
- 同一服务的条目放一起，前面加 `# 服务名` 注释分段。
- 文件名首字母大写、与上游命名风格一致。macOS 文件系统不区分大小写，**不要建只有大小写不同的同名文件**（如 `claude.list` 与 `Claude.list`）。

### 新增一个域名该放哪

```
需要走代理？
 ├─ 是 AI 服务 ──────────── Claude / Grok / MetaAi 等对应 list
 ├─ 长期使用 ────────────── Custom-Long.list（放进对应分段）
 └─ 临时 / 不确定 ───────── Custom-Temp.list（确认后挪到 Custom-Long）
需要直连？
 └─ 国内站点 ────────────── Direct.list
需要拦截？
 └─────────────────────── Block.list
按 IP？
 ├─ 目标是某台服务器 ────── TargetIP.list
 └─ 来源是某台局域网设备 ── SourceIP.list
```

### 新建一个 list

1. 先到 [上游分类表](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash) 搜一下有没有现成规则；有就直接引用上游。
2. 上游没有 → 在本目录新建 `服务名.list`。
3. 在 smart.yaml 中加三处：
   ```yaml
   # proxy-groups
   - {name: 服务名, <<: *default}

   # rules（越靠前优先级越高，必须在 Proxy / Global / China / MATCH 之前）
   - RULE-SET,服务名 / Domain,服务名

   # rule-providers
   服务名 / Domain: {<<: *class, url: "https://raw.githubusercontent.com/BRSBSC/clash/refs/heads/main/list/服务名.list"}
   ```
4. 回到本 README，在「分类」和「总览」表里各加一行。

### 提交前自查

```bash
cd list
# 每个文件内的重复（有输出就去重）
for f in *.list; do d=$(grep -vE '^\s*(#|;|$)' "$f" | sort | uniq -d); [ -n "$d" ] && echo "== $f" && echo "$d"; done

# IP 规则漏了 no-resolve
grep -nE '^(IP-CIDR|IP-CIDR6|SRC-IP-CIDR),' *.list | grep -v 'no-resolve'

# 全角逗号 / 行尾空格
grep -nE '，|\s+$' *.list
```

> 当前存在的重复：
> - **Custom-Long.list**：`1000qm.vip`、`huangguoai.com`、`v2rayssr.com`、`workbuddy.ai`
> - **Check.list**：`incolumitas.com`、`vultr.com`
> - **Direct.list**：`apple-bing.sbs`、`hao123.com`、`maocf1.top`、`sevenka.top`、`smtcdns.net`、`zhunchuanpb.com`、`IP-CIDR,219.146.1.66/32`
> - **Proxy.list**：`asiassn.com`、`dns.google`、`dns.quad9.net`、`etcbbf.xyz`、`etcbbi.xyz`、`shittyurl.org`，以及 5 条 IP-CIDR（`189.79.31.0/24`、`49.205.113.0/24`、`62.181.50.0/24`、`90.21.198.0/24`、`94.241.215.0/24`，这几行还带行尾空格）

### 重命名 / 删除前

先搜引用，避免断链：

```bash
grep -rn "list/文件名" ../../smart.yaml ../ini/
```

### 生效

smart.yaml 的规则集 `interval: 86400`（每天自动更新一次）。急用时在 zashboard 的规则集页面手动更新，或重启内核。raw 链接有几分钟缓存，jsDelivr CDN 缓存更久。
