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

| 🎯 自定义分流 / 直连优先 |  |  |
| ---- | ---- | ---- |
| [Custom-Long](#custom-long) | [Custom-Temp](#custom-temp) | [Direct](#direct) |

| 🌐 IP 规则 |  |
| ---- | ---- |
| [TargetIP](#targetip) | [SourceIP](#sourceip) |

| ✨ AI |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- |
| [ChatGPT](#chatgpt) | [Claude](#claude) | [Gemini](#gemini) | [Grok](#grok) | [MetaAi](#metaai) |

| 🧪 检测 / 拦截 |  |
| ---- | ---- |
| [Check](#check) | [Block](#block) |

## 总览

| 文件 | 内容 | 规则数 | 上游对应规则 | 当前引用位置 |
| ---- | ---- | ---: | ---- | ---- |
| Custom-Long.list | 长期走代理的补充域名 | 153 | — | **smart.yaml → Custom-Long** |
| Custom-Temp.list | 临时 / 测试走代理的域名 | 9 | — | **smart.yaml → Custom-Temp** |
| Direct.list | 直连优先白名单（授时、国内公共 DNS 及自定义直连） | 9 | [Direct](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Direct) | **smart.yaml → 国内**（第 5 位） |
| TargetIP.list | 指定目标 IP | 5 | — | **smart.yaml → Custom-Long**、ini/nodnsleak4.ini（DIRECT） |
| SourceIP.list | 指定局域网源 IP 直连 | 1 | — | **smart.yaml → 国内**、ini/nodnsleak4.ini、ini/clashfull.list |
| ChatGPT.list | OpenAI / ChatGPT / Sora（含 Stripe 支付风控） | 12 | `geosite/openai.mrs` | **smart.yaml → ChatGPT** |
| Claude.list | Claude / Anthropic（含 Stripe 支付风控） | 12 | `geosite/anthropic.mrs` | **smart.yaml → Claude**、ini/clashfull.list |
| Gemini.list | Gemini / AI Studio / NotebookLM / Antigravity | 38 | `geosite/google-deepmind.mrs` | **smart.yaml → Gemini** |
| Grok.list | Grok / xAI | 6 | 无 | **smart.yaml → Grok**、ini/clashfull.list |
| MetaAi.list | Meta AI + Perplexity / Groq / Dify / Genspark / Manus / Skywork | 11 | 无 | **smart.yaml → Meta AI**、ini/clashfull.list |
| Check.list | IP 检测 / 测速 / 分流测试站点 | 59 | [Speedtest](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Speedtest)（8） | **smart.yaml → Test**、ini/clashfull.list |
| Block.list | Adobe 正版验证拦截 | 4 | [Adobe](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Clash/Adobe)（137） | **smart.yaml → REJECT** |

> 规则数为去掉注释与空行后的有效行数，统计于 2026-11-18。

---

## Custom-Long

#### 用途
长期需要走代理、但上游规则没有覆盖的域名。文件内按主题分段（`# === xxx ===`），新增条目请放进对应分段：

| 分段 | 内容 |
| ---- | ---- |
| AI、编程与中转服务 | AI 工具、编程助手、API 中转、SillyTavern 酒馆等 |
| NAS、系统与软件工具 | Unraid、Proxmox、MoviePilot、桌面与硬件工具等 |
| PT、影视、直播与网盘资源 | 各大 PT 站、Emby/影视站、IPTV 直播源、网盘资源 |
| 游戏与 Meta Quest VR | 游戏官网/CDN、Switch 模拟器、Meta / Oculus / SideQuest VR |
| 机场、VPS、CDN 与免费域名 | 机场订阅/面板、VPS 商家、Cloudflare、免费域名（`.edu.kg` / `.dpdns.org`） |
| 运营商、接码、跨境支付与加密货币 | 海外运营商/eSIM、接码平台、土耳其支付/虚拟卡（OlduBil/PayTR/Oyunfor）、交易所 |
| 社区、漫画、成人与其它站点 | 论坛社区（Linux.do / IDCFlare）、漫画站及其他杂项 |

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 143 |
| DOMAIN-KEYWORD | 10 |
| TOTAL | 153 |

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

---

## Direct

#### 用途
直连优先白名单：排在所有上游业务规则之前（`smart.yaml` 第 5 位），用于防止系统授时（`time.windows.com`）、国内公共 DNS 以及被上游代理规则误伤的国内域名走代理。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 3 |
| IP-CIDR | 6 |
| TOTAL | 9 |

#### 使用说明
- smart.yaml 中对应 **国内**，位于 `Custom-Temp` 之后、`TEST` 与所有业务规则之前，优先级高于上游规则。
- 以后遇到国内站点或自用服务器被上游规则误判走代理，直接加到本文件底部 `# === 自定义强制直连 ===` 即可立即抢回直连（注：`Custom-Long` 在第 3 位，若同一域名同时出现在两边则以 `Custom-Long` 为准）。

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

## ChatGPT

#### 用途
OpenAI / ChatGPT / Sora、高级语音实时通信（LiveKit 专属子域）及 Stripe 支付风控域名，已剔除 `sentry.io`、`intercom.io`、`challenges.cloudflare.com` 等无关第三方通用域名与废弃 Azure CDN。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 11 |
| DOMAIN-KEYWORD | 1 |
| TOTAL | 12 |

#### 使用说明
- 包含完整 Stripe 支付与反欺诈风控三件套：`stripe.com`、`stripe.network`（Radar 指纹与 IP 风控检测）、`stripecdn.com`。
- smart.yaml 的 **ChatGPT** 组引用本文件。

---

## Claude

#### 用途
Claude / Anthropic（含 Claude Code、Artifacts、官网静态资源 CDN 及 Stripe 支付风控域名）。smart.yaml 的 **Claude** 组引用本文件。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 9 |
| DOMAIN-KEYWORD | 2 |
| DOMAIN | 1 |
| TOTAL | 12 |

#### 使用说明
- 后缀：`anthropic.com`、`claude.ai`、`claude.com`、`clau.de`、`claudemcpclient.com`、`claudeusercontent.com` + Stripe 三件套（`stripe.com`、`stripe.network`、`stripecdn.com`），外加 `servd-anthropic-website.b-cdn.net`
- 关键字：`anthropic`、`claude`
- ⚠️ **支付风控注意**：ChatGPT 和 Claude 底层共用同一套 `stripe.*` 域名。由于 `smart.yaml` 中 `Claude` 排在 `ChatGPT` 前面，`stripe.*` 会优先命中风控更严的 `Claude` 组——日常给 Claude 续费天然同 IP；若给 ChatGPT 绑卡付款且两组节点不同，临时让 `Claude` 与 `ChatGPT` 指向同一节点即可。

---

## Gemini

#### 用途
Google AI 全家桶专属域名：Gemini、DeepMind、AI Studio、Generative Language API、NotebookLM、Jules、Google AI Labs、Stitch、Opal、Antigravity 与 Gemini Code Assist。已剔除误伤范围过大的 `googleusercontent.com`、`android.googleapis.com` 以及已废弃的 `bard` / `makersuite` 旧域名。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 38 |

#### 使用说明
- smart.yaml 的 **Gemini** 组引用本文件，确保 Google 搜索走香港节点时，Antigravity / AI Studio / NotebookLM 依然固定走解锁地区节点。

---

## Grok

#### 用途
Grok / xAI。smart.yaml 的 **Grok** 组引用本文件。上游没有 Grok 规则。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 5 |
| DOMAIN-KEYWORD | 1 |
| TOTAL | 6 |

内容：`grok.com`、`grok.x.com`（只匹配子域，不吞 `x.com`）、`grokusercontent.com`、`grokipedia.com`、`x.ai` 及关键字 `grok`。

---

## MetaAi

#### 用途
Meta AI 及其他未单独分组的 AI 产品：`meta.ai`、`metademolab.com`、`perplexity.ai`（含 `pplx.ai`、`pplx-res.cloudinary.com`）、`groq.com`、`dify.ai`（含 `difyai.com`）、`genspark.ai`、`manus.im`、`skywork.ai`。smart.yaml 中对应 **Meta AI**。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 10 |
| DOMAIN | 1 |
| TOTAL | 11 |

新出现、又不值得单独建组的 AI 产品，可以先放这里。

---

## Check

#### 用途
IP 归属检测、测速、分流测试站点（ipip.net、ipinfo.io、test-ipv6.com、vultr 测速等）。单独分到 **Test** 组，方便切换节点验证出口 IP / 解锁情况。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 56 |
| IP-CIDR | 2 |
| DOMAIN | 1 |
| TOTAL | 59 |

#### 使用说明
- smart.yaml 中对应 **Test**（规则集名 `TEST / Domain`）；ini/clashfull.list 中 → 🌍 国外。
- 注释掉的 Netflix 检测域名（`ichnaea-web.netflix.com` 等），需要测 Netflix 解锁时可临时打开。

---

## Block

#### 用途
拦截 Adobe 正版验证 / 统计：`adobe.com`、`adobedtm.com`、`adobe.io`、`omtrdc.net`。

#### 规则统计
| 类型 | 数量(条) |
| ---- | ---- |
| DOMAIN-SUFFIX | 4 |

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
 └─ 国内站点被误判 ──────── Direct.list（第 5 位优先直连）
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

   # rules（越靠前优先级越高，必须在 Global / China / MATCH 之前）
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

### 重命名 / 删除前

先搜引用，避免断链：

```bash
grep -rn "list/文件名" ../../smart.yaml ../ini/
```

### 生效与防 DNS 泄露要点

- **规则刷新**：smart.yaml 的规则集 `interval: 86400`（每天自动更新一次）。急用时在 zashboard 的规则集页面手动更新，或重启内核。raw 链接有几分钟缓存，jsDelivr CDN 缓存更久。
- **IP 规则防泄露**：所有 `IP-CIDR` / `IP-CIDR6` / `SRC-IP-CIDR` 条目末尾必须带 `,no-resolve`，防止为了匹配 IP 而在本地触发 DNS 解析。
- **上游 DoH 与 OpenClash 配合**：`smart.yaml` 中海外 `nameserver-policy` 仅保留纯 IP 形式 DoH（`1.1.1.1` / `8.8.8.8#所有-智选`），不使用域名形式（如 `dns.google`），避免被 `default-nameserver` 在国内解析；OpenClash 主路由建议将本地 DNS 劫持设为「防火墙转发」并在 LAN 的 DHCPv6 中不下发 IPv6 DNS，防止运营商 IPv6 DNS 抢答泄露。
