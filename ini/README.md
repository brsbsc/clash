# 🧩 clash / ini

## 前言

subconverter 订阅转换用的**外部配置模板**（原 [brsbsc/nodnsleak](https://github.com/brsbsc/nodnsleak) 仓库，2026-11 合并到这里）。
用法：在订阅转换网站的「远程配置」里填本目录文件的 raw 链接：

```
https://raw.githubusercontent.com/BRSBSC/clash/refs/heads/main/ini/<文件名>
```

所有模板的核心思路都是**防 DNS 泄露**：国内规则尽量用域名规则直连，最后 `GEOIP,CN,no-resolve` + `FINAL` 兜底，避免为了判断 IP 归属而在本地解析国外域名。

> mihomo / OpenClash 直接使用的主配置是根目录的 `smart.yaml`，不依赖这里的模板。

## 分类

| 🧩 nodnsleak 系列 |  |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- | ---- |
| [nodnsleak](#nodnsleak-系列) | [nodnsleak1](#nodnsleak-系列) | [nodnsleak2](#nodnsleak-系列) | [nodnsleak3](#nodnsleak-系列) | [nodnsleak4](#nodnsleak-系列) | [nodnsleak5](#nodnsleak-系列) |

| 📄 其他 |  |
| ---- | ---- |
| [ACL4SSR_Online_Full.ini](#acl4ssr_online_fullini) | [clashfull.list](#clashfulllist) |

---

## nodnsleak 系列

| 文件 | 规则集 | 策略组 | 与上一版相比 |
| ---- | ---: | ---: | ---- |
| nodnsleak.ini | 13 | 2 | 基础版：🚀 节点选择 + ♻️ 自动选择，规则全部来自 ACL4SSR |
| nodnsleak1.ini | 13 | 9 | 规则同上；增加 🚀 手动切换 和 香港/日本/美国/台湾/狮城/韩国 url-test 分组 |
| nodnsleak2.ini | 19 | 9 | 增加 Epic 走代理；PrivateTracker、directIP ⚠️、SteamCN、Download、Apple 直连 |
| nodnsleak3.ini | 22 | 12 | 增加 🍎 苹果服务、💬 OpenAi（含 Claude/Gemini）、🎮 EPIC 三个分流组；引用 directIP ⚠️ |
| nodnsleak4.ini | 18 | 9 | 基于 2 版：国内域名换成本仓库 ChinaDomain；增加本仓库 SourceIP、TargetIP（均直连）；去掉 PrivateTracker |
| nodnsleak5.ini | 16 | 9 | 同 4 版，去掉 SourceIP、TargetIP |

#### 引用的本仓库 list

| 模板 | 引用 |
| ---- | ---- |
| nodnsleak2.ini | list/directIP.list ⚠️ |
| nodnsleak3.ini | list/directIP.list ⚠️ |
| nodnsleak4.ini | list/ChinaDomain.list ⚠️、list/SourceIP.list、list/TargetIP.list |
| nodnsleak5.ini | list/ChinaDomain.list ⚠️ |

> ⚠️ `directIP.list` 在合并前的 nodnsleak 仓库里就不存在；`ChinaDomain.list` 已在清理重复快照时删除（可改为上游 `China/China.list`），订阅转换时未修复的规则集会拉取失败。
>
> ⚠️ nodnsleak4.ini 中 TargetIP → **DIRECT**，而 smart.yaml 中 TargetIP → **Custom-Long**（代理），语义相反。

---

## ACL4SSR_Online_Full.ini

ACL4SSR 官方 Online_Full 模板的本地副本（32 个规则集、29 个策略组），作为参考 / 对照基线，一般不改。

---

## clashfull.list

名字是 `.list`，内容其实是 **subconverter ini 片段**（`ruleset=` / `custom_proxy_group=`），**不能**当作 rule-provider 引用。

结构分 4 段：`;1、域名组` → `;2、策略组` → `;3、节点组` → `;4、启用规则集`。
引用了本仓库的 list/SourceIP、Claude、MetaAi、Grok、Check、Proxy ⚠️（`Proxy.list` 已删除，可直接移除该行），以及上游的 OpenAI、Copilot、Gemini、Telegram、GitHub、TikTok、Amazon、Apple、Microsoft、Steam、Epic、EA、Blizzard、UBI、Sony、Nintendo、Global 等。

---

## ini 语法速查

```ini
[custom]
ruleset=策略组名,规则链接                  ; 引用远程 list
ruleset=策略组名,[]DOMAIN-SUFFIX,xxx.com   ; 内联单条规则
ruleset=策略组名,[]GEOIP,CN,no-resolve
ruleset=策略组名,[]FINAL                   ; 兜底，必须放最后

custom_proxy_group=组名`select`[]组A`[]组B`[]DIRECT
custom_proxy_group=组名`url-test`(正则)`http://www.gstatic.com/generate_204`300,,50

enable_rule_generator=true
overwrite_original_rules=true
```

- `;` 开头是注释（ini 中合法）。
- `ruleset` 的顺序就是最终规则顺序，越靠前优先级越高。
- `url-test` 末尾 `300,,50`：测速间隔 300 秒，容差 50 毫秒。
- 引用本仓库 list 时用 `https://raw.githubusercontent.com/BRSBSC/clash/refs/heads/main/list/<文件名>`。
