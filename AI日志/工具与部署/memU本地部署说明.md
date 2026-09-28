# memU 本地部署说明

> 装机日期：2026-09-28 ｜ 模式：**local（本地）** ｜ 装机者：T_T 代跑，Prendeck 亲手填 key
> 本文档是查档入口，忘了怎么用就回来看。

---

## 一、memU 是什么

一个"文件柜 + 图书管理员"式的 agent 记忆系统，存三类东西：

| 类型 | 是什么 | 存放位置 |
|---|---|---|
| **memory（记忆）** | 关于 Prendeck 的稳定事实（项目状态、规矩、偏好） | `C:\Users\xjtx2\.memu\memory\*.md` |
| **skill（技能）** | 可复用的工作流程（如"三源验证 API 是否存在"） | `C:\Users\xjtx2\.memu\skill\*.md` |
| **resource（资源）** | 本机文件的索引（路径 + 一句话描述），不存内容 | 记录在库内，描述清单在 `hosts\agent\resources.md` |

memory 和 skill 都是**普通 Markdown**，记事本直接看；库本体是 SQLite（二进制，别直接开）。

## 二、运作原理（两个循环）

```
【记】整理循环（每天最多触发一次）
  Cherry 会话日志
    ── prepare（切片）──▶ hosts\agent\sessions\ 会话快照 → jobs\ 任务包
    ── 我读会话蒸馏 ──▶ 写成 memory / skill 的 .md
    ── commit ──▶ 调模力方舟把文本变向量 ──▶ 存入 memu.sqlite3

【用】检索循环（每个新会话开场）
  用户提问 ── memu-agent retrieve "关键词" ──▶ 三层结果：
    segments = 最对味的原文切片
    files    = 完整记忆/技能文档（含可打开的 path）
    resources= 本机相关文件线索
    ──▶ 我当背景知识，再开始回答
```

核心原理一句话：**文本变成向量（一串数字），意思相近的数字也相近**——所以问"星星炮"能捞出"弹药变体设计"。

## 三、文件地图

```
C:\Users\xjtx2\.memu\
├─ config.env              配置 + 模力方舟令牌（权限已锁为仅本人可读，别外传）
│                          内容：local 模式 / SQLite 路径 / ai.gitee.com 端点 /
│                          模型 WeMM-Embedding-4B / MEMU_API_KEY
├─ memu.sqlite3            记忆库本体（向量 + 元数据）
├─ memory\                 ⭐ 记忆正文（给你看的）
├─ skill\                  ⭐ 技能正文（给你看的）
└─ hosts\agent\
   ├─ sessions\            从 Cherry 切出的会话快照（原料，只读）
   ├─ jobs\                每轮蒸馏任务包（处理完即历史残留）
   ├─ memory\ skill\       蒸馏时的工作副本（commit 后同步到上面两层）
   ├─ resources.md         资源描述清单（--- 分隔的 path/description 记录）
   ├─ bridge-prompt.txt    整理流水线完整指令（每日桥接时我读它）
   └─ .last-bridge         上次整理时间标记（超 24h 我才再跑）
```

散装的三处：

1. **`SOUL.md`（T_T 的身份文件）两块内容**：
   - `<!-- memu:begin -->` 托管块 = "回答前先 retrieve" 指令，**不要手改**
   - 块外"memU 每日桥接"小节 = T_T 自维护的触发规则（本环境没有定时器工具的替代方案）
2. **程序本体**：`Python312\Scripts\memu-agent.exe`（命令行工具）+ `site-packages\memu\`（源码）
3. **Cherry 会话日志**：`C:\Users\xjtx2\AppData\Roaming\CherryStudio\Data\`（memorization 缝挖这里）

## 四、常用口令（跟 T_T 说人话即可）

| 你想干嘛 | 说 |
|---|---|
| 看存了什么 | "给我看看 memU 里存了什么" |
| 查某主题 | "memU 里关于 X 怎么说的" → 跑 `memu-agent retrieve "X"` |
| 读某条原文 | "读一下那个记忆/技能文件" |
| 手动整理一次 | "跑一遍 memU 桥接" |
| 卸载 | "Follow `memu-agent docs uninstall` to uninstall memU"（记忆默认保留） |

## 五、装机时抓到的两个 bug（重要备忘）

1. **本机 pip 曾被杀软/清理工具咬坏**（`pip\_vendor\cachecontrol\caches\` 源码被删只剩 pyc，2026-09-07），安装必崩。已用官方 `get-pip.py --force-reinstall` 修复（23.2.1 → 26.2.1）。若以后 pip 又怪，先查这个目录。
2. **memU 的 Windows 路径 bug**：`memu\hosts\bridging\resources.py` 里过滤条件只认 `/` 和 `~` 开头的 POSIX 路径，导致 `verify-resources` 在 Windows 上把所有 `C:\...` 路径全扔掉（表现为 "0 resource(s)"）。已在本机改为 `path.startswith("~") or os.path.isabs(path)`。**包升级会覆盖此补丁**，复发就重打，并值得给上游提 issue。

## 六、当前状态与验收计划

- 2026-09-28 首跑完成：6 个会话 → 13 个任务 → 10 条记忆/技能 + 10 个资源入库
- 检索回路冒烟测试通过（三层结果正常返回）
- **待办：开个新会话跑"10 题存取考试"**——存过的事实隔会话能不能捞回来。考不过就按约定卸载
- 每日桥接：距上次 >24h 且有新会话时自动跑；不开聊零消耗
- 四文件记忆系统（SOUL/USER/FACT/JOURNAL）**不受影响，照常并行**

## 七、选型时的旧账（为什么是 memU 不是 Hindsight）

- 三候选横评后，因性能顾虑（Hindsight 常驻服务）+ "先吃一口"决定先试 memU 本地
- "memU 被 mem0 曝虚假 benchmark"的评论**查证为大概率记混**（被锤的是 mem0 自己：Zep、MemGPT 作者都锤过它）
- Hindsight 仍是备胎：本地数据 + 第三方复现跑分，memU 验收不过就换它
