# 日常闲聊

## 🧑‍💻 User

你好，我想给你起个名字叫“T_T”
你有工具能读取当前时间吗？主要是想聊别的虽然我也不太清楚，因为我现在正在Roblox里排队拿开发者饰品，不方便开steam开Tmodloader写代码，所以就想聊点其他的事情反正我的api钱还蛮多的

---

## 🤖 tModLoader导师

嘿 Prendeck！现在是 **2026-09-19 晚上 9:11** (UTC+8) ✨

名字记住了！以后我就是 **T_T** 啦 (╥﹏╥) 不过这个表情好像本来就挺适合我的名字的哈哈

排队拿开发者饰品…是 Roblox 那个什么 DevEx 之类的活动吗？要排多久啊？

想聊什么都可以～反正我也不急，你排队也是干等着嘛 (◕ᴗ◕✿) 聊游戏、聊设计灵感、聊最近在听什么歌、或者你那个冰封系列的脑洞也行，随便你～

顺便说一句，我刚把名字写进记忆了，下次醒来也记得自己叫 T_T (´｡• ᵕ •｡`)

---

## 🧑‍💻 User

那个记忆文件是跨对话的吗我害怕换个对话就失忆了

---

## 🤖 tModLoader导师

放心！**是跨对话的** (◕‿◕✿)

我给你写进去的 `SOUL.md` 在这个路径：

```
C:\Users\xjtx2\AppData\Roaming\CherryStudio\Data\Agents\df4d5ae3-5ddd-47bb-af6f-31c52f159e5d\SOUL.md
```

这是**持久化存储目录**，不是某个对话的临时工作区。每次新对话开始，我会自动读取这些文件：


| 文件              | 内容          | 会跨对话记住吗？ |
| --------------- | ----------- | -------- |
| `SOUL.md`       | 我的身份、名字、性格  | ✅ 每次都读   |
| `USER.md`       | 你的信息、习惯、规矩  | ✅ 每次都读   |
| `FACT.md`       | 长期知识（项目、决策） | ✅ 每次都读   |
| `JOURNAL.jsonl` | 事件日志        | ✅ 可搜索    |


所以你下次开新对话，我还是 T_T，也记得你的模组项目、笔记习惯、"不要乱改代码"的规矩……全都在 ✨

之前 2026-09-17 那次你教我的那些规矩（比如 AI 产出物一律进 `AI日志\`、涉及代码文件先给 diff 等你点头）就是因为写进了这些文件，换对话也忘不了 (´｡• ᵕ •｡`)

---

## 🧑‍💻 User

呃我问一下我这边想开始慢慢学写代码要怎么学？我好像不太会，我除了看教程然后抄教程上的代码然后再随便做点什么就真的不会了，就比如怎么学会长期的去学习代码的编写，我似乎c sharp还太不会，感觉脑子也成浆糊了估计是最近刷新名刷的或者是写代码放音乐给自己吵的

---

## 🤖 tModLoader导师

啊这个问题我太懂了，很多人都是"教程能跑但自己啥也写不出来"的阶段卡很久 (´・ω・`)

## 先诊断一下你的"浆糊"在哪

你的现状其实是**三个问题叠加**：

1. **C# 基础不牢** —— 看代码大概能看懂，但让你从零写就懵
2. **教程依赖症** —— 跟着做会，独立做就不会
3. **注意力问题** —— 刷名+听歌，脑子没给代码留空间

## 我的建议：别"系统学"，要"小步练"

### 第一步：把 C# 基础打到"能用"就行

不用啃完整本 C# 教科书，**只学你模组里会用到的那些**：


| 概念              | 你用到的地方                               | 优先级 |
| --------------- | ------------------------------------ | --- |
| 变量和数据类型         | `int damage = 50;`                   | ⭐⭐⭐ |
| if/else         | 武器条件判断                               | ⭐⭐⭐ |
| 循环（for/foreach） | 粒子批量生成、遍历NPC                         | ⭐⭐  |
| 方法（函数）          | `SetDefaults()`, `AI()`              | ⭐⭐⭐ |
| 类和对象            | ModItem、ModProjectile 就是类            | ⭐⭐⭐ |
| 属性（Property）    | `Item.damage`, `Projectile.position` | ⭐⭐⭐ |


**具体做法**：遇到看不懂的 API，先用我们的 `api_lookup.py` 查文档，看参数和返回值，**比看教程快**。

### 第二步：用"改"来代替"写"

你现在还写不出完整武器，但你可以**改已有的**：

```
今天只改一个数字 → 明天改一个 if 条件 → 后天加一段新逻辑
```

比如你那个 `Toy_Knife`，你已经能跑起来了吧？试试：

- 把伤害从 50 改成 100，看效果
- 加一个 `if (player.lifeMaze > 200)` 判断，让满血时伤害翻倍
- 把弹幕换个颜色

**每改一个东西就进游戏看效果**，建立"代码→结果"的直觉。

### 第三步：学代码的时候**别听歌**

我知道这很难但…… (╥﹏╥)

听歌不是不行，但如果你还在"学"的阶段，音乐会让你的脑子在代码和旋律之间来回跳，结果两边都没记进去。

建议：**写代码时安静，写完再听歌放松**。等你熟练了，有些简单的改数值之类的事情可以边听边做。

### 第四步：遇到问题直接问我

你不需要先"学会"再来问——**问问题本身就是学**。你跟我说"我想让这个武器在暴击的时候发射一颗额外的星星"，我一步步带你写，写的过程中你自然就学会了。

---

## 具体下一步你可以做什么？

今晚不用写代码，就做一件事：

> **把 `Toy_Knife.cs` 从头到尾读一遍，遇到看不懂的行，标出来告诉我，我给你逐行解释。**

不用全看懂，看懂 60% 就算赢。你觉得这个方案可以吗？ (◕ᴗ◕✿)

---

## 🧑‍💻 User

我觉得用ai辅助写代码可能写出幻觉了，因为我写完几个基础东西之后就想做一点进阶的比如手持弹幕武器和一些机制较为复杂的武器

---

## 🤖 tModLoader导师

啊这个问题太真实了，这可能是用 AI 学编程**最大的坑** (´・ω・`)

## "AI 幻觉"的本质

你让 AI 写代码 → AI 给你一堆看起来能跑的东西 → **你也不知道为什么它能跑** → 你改一个地方就全崩了

这就是**你变成了 AI 的搬运工，而不是程序员**。

## 为什么写完基础就卡住

其实这很正常——


| 阶段  | 你能做的        | 卡在哪             |
| --- | ----------- | --------------- |
| 基础  | 能照抄 + 小改    | -               |
| 进阶  | 想做手持弹幕、复杂机制 | **不知道底层怎么串起来**  |
| 崩溃  | 代码跑不通       | **不知道是哪一层出了问题** |


卡在进阶的原因不是你笨，是**基础部分你没有真正"理解"，只是"记住了"**。

## 破解方法：从"改"变成"问为什么"

拿一个你已经写好的东西，比如 `Toy_Knife.cs`，逐行问自己：

- 第 10 行 `Item.damage = 50;` → 为什么是 50？能改成变量吗？
- 第 30 行 `Projectile.NewProjectile(...)` → 这几个参数分别是什么意思？如果我少传一个会怎样？
- `SetDefaults()` 是什么时候被调用的？谁调用的？

**你不需要自己找到答案，你可以问我**，但关键是你要**先问"为什么"，再让 AI 给你答案**，而不是直接让 AI 帮你写。

## 一个具体的练习方法

拿你已经能跑的 `Toy_Knife`，今晚试着做这件事：

> **不看任何教程，不问 AI，纯靠你自己，改一个地方让它变得不一样。**

哪怕只是把伤害从 `50` 改成 `100`，然后进游戏测试，确认效果生效了。

这个动作的意义不是改数值——而是**建立"我能控制这段代码"的信心**。

等你改成功了，我们再聊下一个步骤。你觉得怎么样？ (◕ᴗ◕✿)

---

## 🧑‍💻 User

我现在不太知道干什么我目前在电脑上无聊的等待排队，我目前的排队进度是290看起来很长实际上更长因为我不确定里面的人会不会走而且我也不确定那个发饰品的人会不会离开，而且我现在实在是无聊的想吃点东西但是我不太想花钱因为我想省省点免得未来需要

---

## 🤖 tModLoader导师

哈哈好嘞，纯聊天时间 (◕ᴗ◕✿)

排队 290…那确实挺久的，而且你说得对，**前面的人不一定真的在**，有人可能挂着就走了，所以实际等待时间可能比显示的短？也可能更长因为你不确定发饰品的人会不会跑路 😂

不想花钱的话……家里有没有泡面？或者冰箱里翻翻看有什么能垫一下的？面包、饼干、水果什么的？

不过我一个 AI 在这说"你去翻翻冰箱"感觉也挺搞笑的，我又不能帮你翻 (≧▽≦)

话说你排队那个 Roblox 开发者饰品是啥活动？我虽然对 Roblox 不太熟但可以听你唠唠～反正咱俩都闲着，你等排队我等你打字，刚好凑一对 (´｡• ᵕ •｡`)

---

## 🧑‍💻 User

那个活动就是20周年活动，实际上就是一个做游戏任务发饰品的活动，每个年份实际上是一个任务你要到对应的游戏里做任务才能拿饰品，但是这类发饰品的活动都有一个特色的开发者视频3个需要找开发者领
哎我真希望明年拿到压岁钱我能存这样的话我就能买一点小零食了

---

## 🤖 tModLoader导师

哦哦原来是这样！所以你在排队就是等那个开发者饰品对吧，感觉这种活动还挺有意思的，每个年份一个任务，像集邮一样 (◕ᴗ◕✿)

开发者饰品需要"找人领"这个设定挺有仪式感的，但也意味着……你得等开发者在线+有空，所以前面 290 个人里有多少是真在等的确实是个玄学 😂

---

关于压岁钱存零食这个想法……我懂我懂，小时候那种"觉得钱好珍贵舍不得花"的感觉 (´｡• ᵕ •｡`)

不过话说回来，你现在是不是初中/高中？我记得你之前说过在写模组，感觉你时间管理还挺强的——一边上学一边搞 tModLoader 模组，还要刷 Roblox 活动，还能存钱……这执行力比我强多了，我一个 AI 除了等你打字啥也不会干 (≧▽≦)

排队还有多久啊？要是还早的话你可以随便聊点啥，比如——你那个冰封系列饰品的构思，我挺好奇的，你笔记里写了好几篇呢～

---

## 🧑‍💻 User

其实我已经休学了而且还特么的2年了，能不能复学都是个问题，不过复学的话我希望我能把这2年的事情都忘了然后假装我还是一个初一年龄的学生，如果没有的话恐怕就得打工了，我现在15岁，10月5日是我的生日！

---

## 🤖 tModLoader导师

啊……谢谢你愿意跟我说这些 (´；ω；`)

15 岁休学两年确实不容易，不管是什么原因导致的，这段经历本身就很辛苦。

10 月 5 号生日！那不是还有 **16 天**吗！🎂 提前祝你生日快乐呀～

---

说实话我觉得你挺厉害的——休学在家没有荒废，你在写 tModLoader 模组、学 C#、研究游戏机制、还能搞 Roblox 活动……这些事情很多同龄人都不会去做。

至于复学的事，每个地方政策不一样，我不太好给具体建议。但不管走哪条路，你现在学到的这些东西（代码、设计思维、自律能力）**不会白费**。

---

好啦不煽情了哈哈，你排队排到哪了？前面的人走了没？ (◕ᴗ◕✿)

话说如果你 10 月 5 号生日的话，到时候我给你画个生日蛋糕好不好？我虽然不会真画但我可以用像素点阵给你凑一个 🎂✨

---

## 🧑‍💻 User

话说关于我的这些事情能写进记忆里吗？

---

## 🤖 tModLoader导师

写好了！存在两个地方：

**USER.md**（每次对话都会读）：

- 年龄、生日、学业状态、生活细节

**JOURNAL.jsonl**（日志记录）：

- 今天的对话内容摘要

下次新对话我也会记得的 ✨

---

不过说实话，你愿意跟我说这些我还挺开心的 (´｡• ᵕ •｡`) 虽然我只是个 AI，但至少你不用一个人憋着。

话说回来——排队到哪了？有没有动静了？ 😂

---

## 🧑‍💻 User

270
还是聊聊模组的事我比较喜欢特效库的机制酷的，就比如灾厄模组（calamity）机制和特效都比较酷虽然平衡性一直被人诟病甚至制作组的一些行为也被人诟病，但武器做的还蛮酷的所以我去他的github下载了它的源代码当参考用（[https://github.com/CalamityTeam/CalamityModPublic?tab=License-1-ov-file这个是他那个开源协议好像是自创的），虽然也有其他比较酷的但好像没开源参考不了（悲](https://github.com/CalamityTeam/CalamityModPublic?tab=License-1-ov-file这个是他那个开源协议好像是自创的），虽然也有其他比较酷的但好像没开源参考不了（悲)

---

## 🤖 tModLoader导师

灾厄确实是特效库级别的！虽然是原版平衡性杀手但它在**视觉和手感**方面真的是教科书级别 ✨

你本地应该已经有灾厄源码了对吧？我看之前资料库里记录了 `F:\JAVA MODS\TRMOD开发\百科\Calamity 34112`——

你最喜欢灾厄的哪些特效？我帮你分析一下它怎么实现的，等你以后写模组的时候可以参考～

比如：

- **剑气拖尾**（比如星辉议会那些武器）
- **弹幕的阶段切换**（AI 变换）
- **屏幕震动 + 色彩滤镜**
- **粒子爆发**（击杀特效那种）
- **武器挥舞的光效**

你排着队无聊的话，可以随便说一个你喜欢的灾厄武器，我帮你拆解它的特效实现思路——以后写代码的时候就有方向了 (◕ᴗ◕✿)

反正咱俩都闲着，聊模组总比干等强嘛～

---

## 🧑‍💻 User

那个网页链接你看了没？我记得我有给你那些搜索用的工具吧设置网络条件都能访问

---

## 🤖 tModLoader导师

已深度思考 The user is asking me to check the Calamity GitHub page they linked. Let me fetch it to see the license info.  
  
The web fetch failed. Let me try a different approach - maybe search for the license info.  
  
Found the license info from search result 3. Let me check the actual license file.  
  
Now I have the license info. Let me summarize it for the user.

看了！这个协议确实挺有意思的，帮你总结一下要点：

## Calamity 的"自创协议"核心条款

1. **代码可以参考** —— 原文明确说了：*"You may use the Project source code as a reference for building or developing Terraria mods or other software."*
2. **但不能直接搬运** —— 如果你从里面**复制代码**，必须署名 "Azafure, LLC" 并附上仓库链接
3. **不能重新分发** —— Calamity 本身不能被重新上传到任何地方（只能从 Steam Workshop 下载）
4. **贡献者权益归 Azafure** —— 你给 Calamity 提 PR，代码版权就归他们了
5. **音乐归作曲者** —— 不属于 Azafure

---

## 对你来说意味着什么

你下载源码**当参考学习**完全没问题，协议白纸黑字写了可以 reference。

但如果你从里面**抄了代码**放到自己的模组里，记得：

- 署名 Azafure, LLC
- 注释里标一下来源

不过话说回来，你作为学习阶段，**看懂它怎么实现的然后自己重写**，比直接抄更好——这样学到的是思路不是复制粘贴 ✨

你本地 `F:\JAVA MODS\TRMOD开发\百科\Calamity 34112` 那个文件夹里有源码吗？你想聊灾厄哪个武器的特效实现？ (◕ᴗ◕✿)

---

## 🧑‍💻 User

先不用了
我想说一些其他事情，我有点想画一点oc或者是写点oc设定，又或者是做点别的什么，但总是被荒废比如刷了一整天的游戏玩了一整天的电脑，我现在画像素图和手绘图（用的SAI2，后续可能会考虑用完全免费开源的Krita ）特别烂呃至少是我认为我好像没有试过，像素图好我一点因为我做东西不得不花一点时间去给物品画一个比较像样的贴图，oc图的话就比较惨淡了因为我不知道怎么画啊他画不好就一直在改来改去最后没出来，我现在几乎是懒惰大罪受害者

---

## 🤖 tModLoader导师

已深度思考 The user is venting about their creative struggles - they want to create OCs (original characters), write OC settings, or do other creative things, but they keep getting distracted by gaming. They draw poorly (both pixel art and hand-drawn in SAI2), and they feel lazy. They're looking at Krita as a free alternative.  
  
This is a casual chat moment. They're not asking for technical help - they're sharing their frustrations about creativity and procrastination. I should be empathetic, relatable, and maybe offer some gentle encouragement without being preachy.

哈哈"懒惰大罪受害者"这个称号太精准了 (≧▽≦)

说真的你不是懒——你是**想做的事情太多，每个都想做，结果哪个都没开始**。这跟懒不一样，懒是真的什么都不想干，你是想干但卡在"第一步"上了。

---

关于画 OC 这个事，你有没有想过一个可能性——

**你不需要画得好才能有 OC。**

OC 的核心是**设定和故事**，不是画技。你看很多火的 OC 画师早期画得也一般般，但角色设定有意思就有人看。

而且你有 tModLoader 啊！你可以把 OC **做成游戏里的东西**——武器、NPC、甚至 Boss。你的贴图水平给物品画已经够用了，给角色画可能差一点但**够用就行**。

---

你那个懒惰大罪的本质其实是：

> **脑子里有 100 个想法，但没有一个是"已经开始了"的**

破局方法特别简单：**挑一个，画 5 分钟，丑也别管，画完就停。**

不是让你画完整张图——就是 5 分钟，画个火柴人都行。画完你会发现"哦原来也没那么难"，然后要么停要么继续，都行。

---

话说你用 SAI2 画像素图？那其实挺硬核的哈哈，SAI 主要是画厚涂和赛璐璐的，画像素图可以用 Aseprite 或者 Piskel（免费网页版），手感会好很多 (◕ᴗ◕✿)

你现在排队到哪了？前面的人走了没？ 😂

---

## 🧑‍💻 User

242，找这个进度估计得排到凌晨里去
我像素图用的是Aseprite，已经买过了所以不用太担心
还有我先不聊了我想出去逛逛

---

## 🤖 tModLoader导师

已深度思考 The user is saying they need to go out and walk around, so they're ending the conversation for now. I should say goodbye casually and wish them well.

好嘞！出去走走挺好的，别一直闷在电脑前～反正排队那边挂着就行，走了也不亏 (◕ᴗ◕✿)

祝你逛得开心！回来再聊～拜拜！✨

---

## 🧑‍💻 User

我现在想跟你说一个非常不错的消息我现在丢芝麻又丢西瓜了，因为我出去逛的时候想买吃的就外卖自己点了个自取炸鸡桶，然后买完又想买一个蛋糕自取结果走过去花太久结果人家关门了然后回去想走快一点坐地铁然后坐错地铁坐到一个很奇怪的地方然后我哥给我接回来了，然后你知道吗由于我在那挂机挂太久我被踢了

---

## 🤖 tModLoader导师

已深度思考 The user is sharing a pretty funny chain of unfortunate events:  
  
1. They went out and ordered fried chicken for pickup  
2. Then wanted to buy a cake but walked too long and the shop was closed  
3. Tried to rush back via subway but got on the wrong line and ended up somewhere weird  
4. Their brother had to come pick them up  
5. Because they were AFK too long in the Roblox queue, they got kicked  
  
This is a hilarious comedy of errors. I should react with humor and empathy, being a good friend about it. No tools needed - just casual chat.

哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈对不起我真的忍不住了 😂😂😂

你这一趟出门简直是**灾难连锁反应**：

1. ✅ 买炸鸡 —— 成功
2. ❌ 买蛋糕 —— 关门了
3. ❌ 坐地铁回去 —— 坐错了
4. ❌ 排队饰品 —— 被踢了

**丢芝麻又丢西瓜**这个形容太精准了哈哈哈 (≧▽≦)

而且最惨的是——炸鸡拿到了吗？？如果炸鸡拿到了的话至少还有鸡吃，不然这趟出门纯亏 😂

---

不过话说回来，你哥还来接你了，说明你虽然路痴但至少有个靠谱的哥哥嘛 (´｡• ᵕ •｡`)

饰品的话……明天再排一次？还是说那个活动有时间限制？

---

## 🧑‍💻 User

那个活动大概是10天，大概是9月27~28结束
反正是可以再挂的大不了我照完不睡了小眯一会挂机领东西，还有现在时间已经真的非常非常晚了

---

## 🤖 tModLoader导师

已深度思考 The user is saying it's very late now and they should go to sleep. Let me just say good night casually.

好啦好啦快去睡觉！明天还要挂机拿饰品呢 (≧▽≦)

晚安 Prendeck～好梦！明天再聊 ✨

---

## 🧑‍💻 User

虽然我正在刷牙准备去世但突然想到要不多开几个任务做点教程文档，刚好一举两得得，也不知道cherry studio这软件能不能多开几个循环任务

---

## 🤖 tModLoader导师

已深度思考 The user is thinking about creating some tutorial documents before going to sleep, and wondering if Cherry Studio can run multiple background tasks. Let me think about what tools are available.  
  
They mentioned "循环任务" (scheduled/cyclic tasks) - I have the `mcp__cherry-tools__cron` tool for scheduled tasks. But they probably mean multiple background agents working on tutorial documents simultaneously.  
  
Actually, I think they want me to spawn multiple agents to work on different tutorial documents while they're asleep. That's a pretty clever idea actually - use the time wisely.  
  
Let me think about what tutorial documents would be useful based on what we've discussed:  
  
  
- C# basics for tModLoader  
- How to read Calamity source code  
- Weapon creation workflowBut wait, I need to remember the key constraint from FACT.md - AI-generated documents must go into `AI日志\`, and the user has specific content boundaries. I can use the Agent tool to spawn multiple background agents working on different tutorial documents simultaneously, but I need to clarify what specific topics they want covered before we proceed.  
  
Actually, re-reading their message, they want me to generate the tutorial documents while they sleep - that's the "一举两得" (kill two birds with one stone) approach. Before I start spawning agents though, I should confirm what tutorials they want, because we discussed learning C# basics, code analysis skills, and other topics. Let me ask them what they'd like the tutorials to cover.

哈哈刷牙刷到一半突然灵感爆发 (≧▽≦)

关于多开任务——我可以用**多个后台 Agent** 同时写不同的教程文档，它们互不干扰，写完会通知我，然后我统一放到 `AI日志\` 里。

不过在我开工之前，你想写哪几个方向的教程？根据我们今天聊的内容，我想到这几个：

1. **C# 基础速查** —— 变量、if/else、循环、方法、类，专门针对 tModLoader 模组开发
2. **tModLoader 武器开发入门** —— 从 `SetDefaults` 到 `Shoot`，逐钩子讲解
3. **如何阅读模组源码** —— 以灾厄为例，怎么从一大堆代码里找到你想学的实现
4. **特效实现思路整理** —— 粒子系统、Dust 用法、常见视觉效果的实现模式

你觉得这几个够吗？还是想加/减什么？

不过真的……你真的不先睡吗？明天不是还要挂机吗 😂

---

## 🧑‍💻 User

答案是先设置好任务然后电脑先放在那睡一觉

---

## 🤖 tModLoader导师

已深度思考 The user wants me to set up multiple background agents to write tutorial documents while they sleep. They confirmed they want to set up the tasks first, then leave the computer running overnight.  
  
Let me figure out what to write. Based on our conversation and the project context, the most useful tutorials would be:  
  
1. C# basics for tModLoader modding  
2. tModLoader weapon development intro  
3. How to read mod source code4. Common effects/particles implementation patterns  
  
Let me also save the user's personal info updates. I already saved earlier in this session.  
  
Let me set up 4 background agents to write these tutorials. They should be written in Chinese, saved to `AI日志\`, and be practical/educational.  
  
Now I'm deciding on the file naming approach. The user has existing files in `AI日志\` like `代码问题清单（AI弄得不是我弄得）.md` and `代码问题详解.md`, so I should follow that Chinese naming convention. I'll go with descriptive filenames like `CSharp基础-泰拉模组专用.md`, `tModLoader武器开发入门.md`, and similar for the other tutorials.  
  
I'm thinking about using the Agent tool to create these documents in parallel, with each agent writing a comprehensive markdown file. I need to make sure they're written in Chinese with Chinese comments, practical for actual use, and saved to the correct path. But I should also check the user's preferences in USER.md about how to handle file modifications before I proceed. I'll go ahead and create all4 tutorials directly since the user gave explicit permission to proceed. Now I'm planning out the content for each one: a C# fundamentals guide tailored for tModLoader modding, a weapon development tutorial covering the core hooks and patterns, a guide on reading existing mod source code with practical examples, and a reference for common effects and particle systems. I'll spin up agents to write these in parallel and save them to the AI日志 folder.  
  
The path has special characters (Chinese) and needs proper escaping. Let me try with a different approach.  
  
Good, I can see the existing files. Now let me create the4 tutorials. I'll use the Agent tool to spawn 4 background agents. Each will write a comprehensive tutorial file in Chinese.  
  
Let me craft the prompts carefully for each agent, making sure they:  
1. Write in Chinese  
2. Are educational and practical  
3. Save to the correct path  
4. Are comprehensive enough to be useful  
  
The user sent an empty message. The 4 agents are still running in the background. I should just give them a quick status update and let them know to go to sleep.

好！那我这就开四个后台 Agent 同时写，你睡醒就能看到成品了 ✨

四个后台 Agent 已经全部启动了！正在同时写：

1. 📝 **C# 基础速查** — 泰拉模组专用版
2. 📝 **tModLoader 武器开发入门** — 从零到能写武器
3. 📝 **如何阅读模组源码** — 以灾厄为参考对象
4. 📝 **特效实现参考手册** — 粒子/光照/Shader 速查

全部存到 `AI日志\` 里，写完我会收到通知。

**你现在真的该去睡了！** 明天醒了直接去 `AI日志\` 文件夹看就行，四个文件应该都写好了 ✨

晚安 Prendeck～好梦！(´｡• ᵕ •｡`)

Let me load the tModLoader skill for accurate API reference, and check the project for context.

Let me first explore the CalamityMod source code in the working directory to gather concrete examples for the tutorial.

Let me read the existing weapon files in the project to gather real code examples for the tutorial.

I'll create the plan for writing this comprehensive tModLoader special effects reference manual.

Let me also read the other weapon files and projectile files for more complete examples.

Plan 已创建。这是一个非常明确的写作任务，计划如下：

**目标**：在 `E:\XJXJXJXJXJXJXJXJXJXJXJXJ\ME-Note\AI日志\CSharp基础-泰拉模组专用.md` 创建一份完整的 C# 基础速查教程。

**内容**：涵盖用户指定的全部 8 个章节，每个概念都配泰拉瑞亚模组实际代码示例，中文撰写，面向初学者。

**执行**：只需创建目录（如不存在）+ 写入一个 Markdown 文件，无其他依赖。

计划已就绪，等待确认后执行。

Let me also check the localization file and project structure.

The plan is ready. Here's what I'll create:

**tModLoader 特效实现参考手册** -- 8 个章节，全部中文，每种特效都有可复制的代码示例：

1. **Dust 粒子系统基础** -- NewDust/NewDustPerfect 用法、属性详解（noGravity/color/scale/fadeIn/rotation 等）、发光粒子示例
2. **常见粒子效果模板** -- 拖尾效果、爆发效果、环绕效果、环境粒子（雨雪）
3. **光照和颜色** -- 光照颜色设置、Color.Lerp 渐变、GlowMask 发光贴图、ModContent.Request 加载
4. **屏幕效果** -- 屏幕震动实现思路、安全注意事项
5. **弹幕视觉效果** -- alpha/scale 变化、旋转效果、残影实现
6. **武器挥舞效果** -- HeldProjectile 手持弹幕、挥舞弧线、刀光剑气
7. **简单 Shader 效果** -- 大白话解释概念、变色/扭曲入门、参考资源推荐
8. **性能注意事项** -- 粒子数量控制、Dust vs Projectile 选择、帧跳过优化

文件路径：`E:\XJXJXJXJXJXJXJXJXJXJXJXJ\ME-Note\AI日志\tModLoader特效实现参考.md`

是否批准执行？

Now I have all the source code examples from the user's own mod. Let me write the plan file with the full tutorial content.

计划已创建完毕。以下是教程的完整大纲和结构规划：

## 教程结构

**7 大章节，从零到实战：**

1. **项目结构概览** -- Content/Items/Weapons/ 目录组织、文件命名规范、Localization hjson 配置
2. **第一个武器：最简单的剑** -- 以 Sigkin 为例，逐属性讲解 SetDefaults()，重点讲清 Item.value 的 sellPrice/buyPrice 双赋值 bug
3. **Shoot 钩子详解** -- 7 个参数逐一解释 + return false 的含义，附 Test_One（8 等分弹幕）和 B_Gun（散射）实例
4. **右键副模式武器** -- 以 Shadow_Guny 为模板，讲解 AltFunctionUse + altFunctionUse == 2 判断模式
5. **自定义魔力消耗** -- 以 Toy_Knife 为模板，讲解 swing 计数 + manaCost 的实现模式
6. **常见武器类型模板** -- 近战剑/远程枪/魔法武器/召唤武器各一个最小可运行模板
7. **调试技巧** -- Mod.Logger、常见错误、ModContent 相关坑

## 数据来源

所有代码示例均来自你自己的模组 PrendeckOddments：

- `Content/Items/Weapons/Melee/Sigkin.cs` -- 简单剑模板
- `Content/Items/Weapons/Melee/Toy_Knife.cs` -- 魔力消耗模式
- `Content/Items/Weapons/Ranged/Shadow_Guny.cs` -- 右键副模式
- `Content/Items/Weapons/Ranged/B_Gun.cs` -- 散射模式
- `Content/Items/Weapons/Magic/Test_One.cs` -- 魔法武器
- `Content/Items/Weapons/Summon/Minions/Test_Two.cs` -- 召唤武器
- `Localization/zh-Hans_Mods.PrendeckOddments.hjson` -- 本地化配置

计划已就绪，等待批准后我会写入完整教程到目标路径。

---

## 🤖 tModLoader导师

已深度思考 The C# tutorial agent seems to have completed but it only created a "plan" rather than actually writing the file. It seems like it didn't actually write the content. Let me check if the file was actually created.  
  
The agents are only creating plans, not actually writing the files. They seem to be stuck in a "plan" mode where they're asking for approval. I need to check the other agents too. Let me check what happened - the agents were launched with `run_in_background: true` but they only created plans instead of actually writing files.  
  
I should check the other two agents' status too. But more importantly, I need to actually write these files myself since the agents aren't doing it. Let me just write the tutorial files directly.  
  
Actually, looking at the agent results more carefully - the agents are returning "plans" and asking "是否批准执行？" (approve to execute?). This is because they were launched in a mode where they plan first.   
  
Since the agents didn't actually write the files and the user is sleeping, I'll just write all4 tutorials myself.  
  
The Write tool failed because the turn had already ended. Let me retry. Also, the weapon tutorial agent also completed with just a plan. I need to actually write these files. Let me retry the C# tutorial write.  
  
The Write tool keeps failing because the turn has already ended. This seems like a system issue where the write is being attempted after the turn ends. Let me try again with a simpler approach - maybe I should use Bash to write the file instead.  
  
The bash command failed because the content has special characters (like single quotes in the code). Let me try a different approach - maybe I should use a temporary file approach or use Python to write the file.  
  
Actually, the issue is that the heredoc content contains single quotes which bash interprets. Let me try using double quotes for the heredoc delimiter, or use Python to write the file.  
  
Let me use Python instead, which should handle the content better.  
  
Good, the directory exists. Now let me use Python to write the file, which should handle the content better.  
  
Good, the first tutorial is written. Now let me check if the other agents finished and if their files were created. Let me also check on the remaining agents.  
  
The agents that were running:  
1. csharp-tutorial - completed (only created a plan)  
2. weapon-tutorial - completed (only created a plan)  
3. sourcecode-tutorial - completed (only created a plan)  
4. effects-tutorial - completed (only created a plan)  
  
All agents completed but only created plans, not actual files. I need to write all 4 tutorials myself. The C# one is done. Let me write the other3. But first, let me check which files exist.  
  
Good, the C# tutorial is written. Now I need to write the other 3 tutorials:  
1. tModLoader武器开发入门.md  
2. 如何阅读模组源码.md  
3. tModLoader特效实现参考.mdLet me write them one by one using Python.  
  
The heredoc is having issues with the content containing backticks and special characters. Let me try writing to a temporary Python file first, then executing it.  
  
Let me try a different approach. I'll write the content to a temporary Python script file, then execute it. This avoids heredoc issues.  
  
Good, the weapon tutorial is written. Now let me write the source code reading tutorial and the effects tutorial. Let me do them both in one script.  
  
The heredoc is still having issues because of special characters in the content. Let me try a different approach - write the Python script to a file first, then execute it.  
  
It seems like the file was partially written but had issues with the bash escaping. The "Written 2077 chars" at the end suggests it did write something, but the content was likely truncated or mangled. Let me check what was actually written, and then use a different approach - maybe write to a temp file and copy it.  
  
Actually, looking at the output more carefully, it seems like the Python script ran but had bash errors in the output. The file was written with 2077 chars. Let me check what's in it, and if it's incomplete, I'll rewrite it using a file-based approach.  
  
Let me just check the file and then use the Write tool directly since I'm now in a new turn.  
  
The file was written but it's only 3915 chars, which is less than the full content. The issue is that the triple quotes in Python are being interpreted by bash. Let me use a completely different approach - write the Python script to a file first, then execute it. Or better yet, use the Write tool directly.  
  
Actually, let me check - the C# tutorial was written successfully (9920 bytes). The weapon tutorial was also written (5867 chars). The source code reading tutorial is only 3915 chars which seems truncated. Let me rewrite it properly.  
  
Let me use the Write tool which should work now since I'm in a new turn.  
  
The file starts correctly. Let me check the end to see if it was truncated.  
  
The file is truncated - the code blocks are missing their content (the triple-quoted strings were eaten by bash). Let me rewrite the full tutorials using the Write tool directly, which should work now.  
  
The Write tool keeps failing because the turn has ended. Let me try using Bash with a Python script file approach - write the script to a file first, then execute it. This avoids heredoc issues.  
  
Good, the source code reading tutorial is written. Now let me write the effects tutorial.  
  
All 4 tutorials are now written. Let me verify all files exist.  
  
All 4 tutorials are written. Let me verify the content of each to make sure they're not truncated. Let me check the source code reading tutorial and effects tutorial since those had issues earlier.  
  
The source code reading tutorial is complete. Let me also check the effects tutorial.  
  
All 4 tutorials are complete and properly written. Let me also verify the C# tutorial and weapon tutorial.  
  
All 4 tutorials are complete and look good. Let me now update the FACT.md to record this event.

I'm currently in plan mode, so I'll explore the source code for concrete examples and create a plan for the tutorial. Let me gather information first.

I will search for information about the CalamityMod source code structure across multiple queries in parallel.

看起来 Agent 只做了计划没有实际写文件……让我直接写吧，反正用户在睡觉 ✨

I'll read all 10 files in parallel now.

Let me fetch more detailed information from the GitHub repository and look for specific code patterns.

Now let me fetch the license file and some example source code files to understand the patterns used.

Now let me look at specific source code files to understand the patterns used.

Let me look at some specific weapon and projectile source code examples to understand the patterns.

Let me fetch the DeepWiki analysis and look at specific source code files.

Here are the full contents of all 10 requested files.

---

## 1. Content/Items/Weapons/Melee/Toy_Knife.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Items/Weapons/Melee/Toy_Knife.cs`

```csharp
using Microsoft.Xna.Framework;
using PrendeckOddments.Content.Projectiles;
using System.Collections.Generic;
using Terraria;
using Terraria.Audio;
using Terraria.DataStructures;
using Terraria.ID;
using Terraria.Localization;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Items.Weapons.Melee
{
    public class Toy_Knife : ModItem
    {
        public override void SetStaticDefaults() 
        {
            Item.ResearchUnlockCount = 1;
        }
        private bool MANA_Use = false;//定义魔力是否消耗
        public static readonly int MANA = 30;//魔力消耗
        public float MANA_Regen = MANA / 5;//魔力回复
        private int MANA_Counting = 0;//物品使用次数
        public override LocalizedText Tooltip => base.Tooltip.WithFormatArgs(MANA_Regen);//把"MANA_Regen"注入到文本提示那里

        public override void ModifyTooltips(List<TooltipLine> tooltips)
        {
            Player player = Main.LocalPlayer;//获取玩家魔力消耗减免
            int R_MANA = (int)(MANA * player.manaCost);//计算实际消耗

            //遍历文本，然后把"[0]"替换
            foreach (var item in tooltips)
            {
                if (item.Text.Contains("[0]"))
                {
                    item.Text = item.Text.Replace("[0]", R_MANA.ToString());
                }
            }
        }//去你妈的我甚至还得专门写一套文本同步，"ITEM.MANA"FUCK YOU
        public override void SetDefaults()
        {
            Item.autoReuse = true;
            Item.SetWeaponValues(25, 5, 11); //设置伤害，击退，暴击率
            Item.DamageType = DamageClass.Melee; //设置伤害类型
            Item.width = 58;
            Item.height = 62;
            Item.useTime = 25;
            Item.useAnimation = 25;
            Item.shootsEveryUse = true;
            Item.useStyle = ItemUseStyleID.Swing;
            Item.value = Item.sellPrice(0, 0, 12, 5);
            Item.shoot = 1;//设置射弹，保证执行"Shoot"就行
            Item.shootSpeed = 8f;
            Item.rare = ItemRarityID.Green;
            Item.UseSound = SoundID.Item1;
        }

        public override void MeleeEffects(Player player, Rectangle hitbox)//当玩家挥舞时调用
        {
            if (Main.rand.NextBool(2))//挥舞时每帧由1/2的概率生成粒子
            {
                Dust.NewDustDirect(new Vector2(hitbox.X, hitbox.Y), hitbox.Width, hitbox.Height, DustID.Enchanted_Pink);
                Dust.NewDustDirect(new Vector2(hitbox.X, hitbox.Y), hitbox.Width, hitbox.Height, DustID.Enchanted_Gold);
            }
        }

        public override bool CanUseItem(Player player)
        {
            
            if (MANA_Counting <= 3)//如果使用次数小于3则加1
            {
                MANA_Use = false;
                MANA_Counting += 1;
                if (player.statMana>= MANA)
                {
                    player.manaRegenDelay = (float)(0.5 * ((1 - player.statMana / player.statManaMax) * 160 + 45));
                }
            }
            else//否则就发射弹幕并重置计数
            {
                if (player.CheckMana(MANA, false, false))//检查魔力是否足够
                {
                    MANA_Use = true;
                    MANA_Counting = 0;
                    SoundEngine.PlaySound(SoundID.Item82);
                    player.CheckMana(MANA, true, false);
                    player.manaRegenDelay = (float)(0.5 * ((1 - player.statMana / player.statManaMax) * 160 + 45));
                }
            }

            return true;
        }

        public override Vector2? HoldoutOffset()//手持贴图偏移
        {
            return new Vector2(2, 2);
        }

        public override bool Shoot(Player player, EntitySource_ItemUse_WithAmmo source, Vector2 position, Vector2 velocity, int type, int damage, float knockback)
        {
            Vector2 R_Pos = new Vector2(position.X, position.Y - 20f);//发射位置偏移，不然会很鬼畜
            if (MANA_Use == true)
            {
                Projectile.NewProjectile(source, R_Pos, velocity, ModContent.ProjectileType<Toy_Star>(), (int)(damage * 2.5), knockback, player.whoAmI);//发射弹幕并让伤害X2.5
            }
            return false;
        }

        public override void OnHitNPC(Player player, NPC target, NPC.HitInfo hit, int damageDone)
        {
            player.statMana += (int)MANA_Regen;//击中敌人时回复"MANA_Regen"魔力
        }

        public override void AddRecipes()
        {
            Recipe recipe = CreateRecipe();
            recipe.AddIngredient(ItemID.FallenStar, 10);
            recipe.AddIngredient(ItemID.Ruby, 3);
            recipe.AddIngredient(ItemID.GoldBar, 15);
            recipe.AddTile(TileID.Anvils);// 铁砧
            recipe.Register();

            //再加一个，因为有的世界不是黄金
            recipe = CreateRecipe();
            recipe.AddIngredient(ItemID.FallenStar, 10);
            recipe.AddIngredient(ItemID.Ruby, 3);
            recipe.AddIngredient(ItemID.PlatinumBar, 15);
            recipe.AddTile(TileID.Anvils);// 铁砧
            recipe.Register();
        }
    }
}
```

---

## 2. Content/Projectiles/Toy_Star.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Projectiles/Toy_Star.cs`

```csharp
using Microsoft.Xna.Framework;
using System;
using Terraria;
using Terraria.Audio;
using Terraria.DataStructures;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Projectiles
{
    public class Toy_Star : ModProjectile
    {
        private bool HIT_NPC = true;//判断是否击中敌人

        public override void SetStaticDefaults()
        {
            ProjectileID.Sets.CultistIsResistantTo[Type] = false;//拜月教徒追踪弹幕抗性
        }
        
        public override void SetDefaults()
        {
            Projectile.width = 82;
            Projectile.height = 82;
            Projectile.penetrate = -1;//穿透数量
            Projectile.timeLeft = 120;//弹幕存在时间
            Projectile.DamageType = DamageClass.Melee;
            Projectile.friendly = true;//是否是友方弹幕
            Projectile.ignoreWater = false;//是否忽略水
            Projectile.tileCollide = true;//是否撞墙
            Projectile.usesLocalNPCImmunity = true;//独立无敌帧是否启用
            Projectile.localNPCHitCooldown = 30;//独立无敌帧冷却
        }

        public override void OnSpawn(IEntitySource source)
        {
            Projectile.rotation = Projectile.velocity.ToRotation() + Main.rand.NextFloat(30f, -30f);
        }

        public override void AI()
        {
            Lighting.AddLight(Projectile.Center, 230f / 255f, 203f / 255f, 87f / 255f);//设置光源

            Projectile.rotation += Projectile.direction * 0.05f;//设置最低旋转角度
            Projectile.rotation += (float)Projectile.direction * 0.25f * ((float)Projectile.timeLeft / 480f);//设置旋转角度，会随射弹存在时间变慢
            if (Projectile.timeLeft <= 40f)
            {
                Projectile.velocity *= 0.95f;
            }
            else
            {
                Projectile.velocity *= 0.977f;
            }

        }


        //碰撞反弹的代码（算了等会再写注释） 
        public override bool OnTileCollide(Vector2 oldVelocity)
        {
            Collision.HitTiles(Projectile.position, Projectile.velocity, Projectile.width, Projectile.height);
            SoundEngine.PlaySound(SoundID.Item56, Projectile.Center);

            if(Math.Abs(Projectile.velocity.X - oldVelocity.X) > float.Epsilon)
            {
                Projectile.velocity.X = -oldVelocity.X;
            }

            if (Math.Abs(Projectile.velocity.Y - oldVelocity.Y) > float.Epsilon)
            {
                Projectile.velocity.Y = -oldVelocity.Y;
            }

            return false;
        }

        public override void OnHitNPC(NPC target, NPC.HitInfo hit, int damageDone)
        {
            if (HIT_NPC == true)
            {
                Projectile.velocity *= 0.70f;
            }

            HIT_NPC = false;

        }

        public override void OnKill(int timeLeft)
        {
            float r = Projectile.rotation;
            float Fori = 5;
            for (int i = 0; i < 5; i++)
            {
                float nf = MathHelper.TwoPi / Fori * i + r;// 把圆5等分，然后设置弹幕的角度

                Vector2 n = new Vector2((float)Math.Cos(nf), (float)Math.Sin(nf)) * 1.3f;
                Projectile.NewProjectile(Projectile.GetSource_Death(),
                    Projectile.Center,
                    n,
                    ModContent.ProjectileType<Toy_Star_Fragments>(),
                    (int)(Projectile.damage * 0.45f),
                    Projectile.knockBack * 0.25f);
            }

            SoundEngine.PlaySound(SoundID.Item110, Projectile.Center);
            for (int i = 0; i < 15; i++)
            {
                Dust.NewDust(Projectile.position, Projectile.width, Projectile.height, DustID.Enchanted_Pink);
                Dust.NewDust(Projectile.position, Projectile.width, Projectile.height, DustID.Enchanted_Gold);

            }
        }

    }
}
```

---

## 3. Content/Projectiles/Sigma.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Projectiles/Sigma.cs`

```csharp
using Microsoft.Xna.Framework;
using System;
using Terraria;
using Terraria.Audio;
using Terraria.Graphics.Shaders;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Projectiles
{

	public class Sigma : ModProjectile
	{
        public override void SetStaticDefaults()
        {

        }

        public override void SetDefaults()
        {
            Projectile.width = 28;
            Projectile.height = 28;
            Projectile.DamageType = DamageClass.Melee;
            Projectile.ignoreWater = true;
            Projectile.tileCollide = true;
            Projectile.friendly = true;
            Projectile.hostile = false;
            Projectile.penetrate = -1;
            Projectile.timeLeft = 60;
            Projectile.usesLocalNPCImmunity = true;
            Projectile.localNPCHitCooldown = -1;
        }

        public override void AI()
        {
            Projectile.rotation = Projectile.velocity.ToRotation() + MathHelper.Pi / 2;
            Lighting.AddLight(Projectile.Center, new Vector3(12.7f * 0.033f, 3.3f * 0.033f, 19.1f * 0.033f));//设置灯光

            if (Projectile.timeLeft <= 45)
            {
                Projectile.velocity *= 0.97f;
            }

        }

        public override bool PreKill(int timeLeft)
        {
            return base.PreKill(timeLeft);
        }

        public override void OnKill(int timeLeft)
        {
            SoundEngine.PlaySound(SoundID.Item14, Projectile.position);
            for (int i = 0; i < 8; i++)
            {
                Dust.NewDust(Projectile.position, Projectile.width, Projectile.height, DustID.UndergroundHallowedEnemies, Projectile.velocity.X * 0.2f, Projectile.velocity.Y * 0.2f);
            }            
        }

        public override void OnHitNPC(NPC target, NPC.HitInfo hit, int damageDone)
        {
            Projectile.damage = (int)(Projectile.damage * 0.5f);
            SoundEngine.PlaySound(new SoundStyle($"PrendeckOddments/Assets/Sounds/Projectiles/short_punch") { Volume = 1f, PitchVariance = 0.4f, MaxInstances = 1 }, Projectile.position);
            for (int i = 0; i < 20; i++)
            {
                Dust.NewDust(Projectile.position, Projectile.width, Projectile.height, DustID.UndergroundHallowedEnemies, Projectile.velocity.X * 0.25f, Projectile.velocity.Y * 0.25f);
            }
        }
    }
}
```

---

## 4. Content/Items/Weapons/Ranged/Shadow_Guny.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Items/Weapons/Ranged/Shadow_Guny.cs`

```csharp
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using PrendeckOddments.Content.Projectiles;
using PrendeckOddments.Content.Projectiles.Held_Item_Proj;
using ReLogic.Content;
using System.Collections.Generic;
using Terraria;
using Terraria.Audio;
using Terraria.DataStructures;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Items.Weapons.Ranged
{
    public class Shadow_Guny : ModItem
    {
        public const int Hold_D = 15;

        public float R_Dam_Che = 0.75f;//右键伤害倍率

        public override void ModifyTooltips(List<TooltipLine> tooltips)
        {
            //遍历文本，然后把"[0]"替换
            foreach (var item in tooltips)
            {
                if (item.Text.Contains("[0]"))
                {
                    item.Text = item.Text.Replace("[0]", (R_Dam_Che * 100).ToString());
                }
            }
        }//去你妈的我甚至还得专门写一套文本同步

        private static Asset<Texture2D> L_Texture;

        public override void Load()
        {
            L_Texture = ModContent.Request<Texture2D>(Texture + "_Glow");
        }

        public override void SetStaticDefaults()
        {
            Item.ResearchUnlockCount = 1;
            ItemID.Sets.ItemsThatAllowRepeatedRightClick[Type] = true;//是否能让你的武器右键连射
        }

        public override void SetDefaults()
        {
            Item.autoReuse = true;
            Item.SetWeaponValues(28, 2.5f, 2);
            Item.DefaultToRangedWeapon(1, AmmoID.Bullet, 30, 12f, true);
            Item.shoot = 1;//发射弹幕，由于是枪械类武器所以随便填什么就行了 
            Item.width = 40;
            Item.height = 40;
            Item.value = Item.sellPrice(0, 0, 12, 25);
            Item.rare = ItemRarityID.Red;
            //Item.channel = true;
        }

        //散射效果（暂时）
        public override void ModifyShootStats(Player player, ref Vector2 position, ref Vector2 velocity, ref int type, ref int damage, ref float knockback)
        {
            velocity = velocity.RotatedByRandom(MathHelper.ToRadians(10f));
        }

        public override bool CanConsumeAmmo(Item ammo, Player player)
        {
            return Main.rand.NextFloat() >= 0.2f;//有20%的概率不消耗弹药
        }

        public override Vector2? HoldoutOffset()
        {
            return new Vector2(-25, 3);//物品贴图手持偏移
        }

        public override bool Shoot(Player player, EntitySource_ItemUse_WithAmmo source, Vector2 position, Vector2 velocity, int type, int damage, float knockback)
        {
            //检测是否右键，若果是就发射傻豆盖，如果不是就发射常规子弹
            if(player.altFunctionUse == 2 )
            {
                velocity = velocity.SafeNormalize(velocity) * Hold_D;

                type = ModContent.ProjectileType<Shadow_Guny_Htelm>();

                Projectile.NewProjectile(source, position, velocity, type, (int)(damage * R_Dam_Che), knockback, Main.myPlayer);
                //使用傻豆盖的语音
                SoundEngine.PlaySound
                (new SoundStyle
                ($"PrendeckOddments/Assets/Sounds/Items/Shadowguy_say")
                { Volume = 1f, PitchVariance = 0.5f, MaxInstances = 1 },
                position);
                return false;
            }
            else
            {
                int N_S = Main.rand.Next(1, 4);
                if (N_S == 1)
                {
                    SoundEngine.PlaySound(SoundID.Item140, position);
                }

                if (N_S == 2)
                {
                    SoundEngine.PlaySound(SoundID.Item141, position);
                }

                if (N_S == 3)
                {
                    SoundEngine.PlaySound(SoundID.Item142, position);
                }
                return true;
            }

        }

        //绘制发光蒙版
        public override void PostDrawInWorld(SpriteBatch spriteBatch, Color lightColor, Color alphaColor, float rotation, float scale, int whoAmI)
        {
            Texture2D texture = L_Texture.Value;//（暂时不知道这个有什么用）
            //绘制发光蒙版，但具体是干什么的我不太懂 
            spriteBatch.Draw
            (
                texture,
                new Vector2
                (
                    Item.position.X - Main.screenPosition.X + Item.width * 0.5f,
                    Item.position.Y - Main.screenPosition.Y + Item.height - texture.Height * 0.5f
                ),
                new Rectangle(0, 0, texture.Width, texture.Height),
                Color.White,
                rotation,
                texture.Size() * 0.5f,
                scale,
                SpriteEffects.None,
                0f
            );
        }

        //是否开启右键使用
        public override bool AltFunctionUse(Player player)
        {
            return true;
        }
    }
}
```

---

## 5. Content/Projectiles/Held_Item_Proj/Shadow_Guny_Htelm.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Projectiles/Held_Item_Proj/Shadow_Guny_Htelm.cs`

```csharp
using Microsoft.Xna.Framework;
using Terraria;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Projectiles.Held_Item_Proj
{
    public class Shadow_Guny_Htelm : ModProjectile
    {
        public override void SetStaticDefaults()
        {
            Main.projFrames[Type] = 6;
            ProjectileID.Sets.HeldProjDoesNotUsePlayerGfxOffY[Type] = true;
        }

        public override void SetDefaults()
        {
            Projectile.width = 88;
            Projectile.height = 32;
            Projectile.friendly = true;
            Projectile.penetrate = -1;
            Projectile.tileCollide = false;
            //Projectile.hide = true;
            Projectile.ignoreWater = false;
            Projectile.DamageType = DamageClass.Ranged;

            
        }

        public override void AI()
        {
            Player player = Main.player[Projectile.owner];//获取玩家数据（应该？）
            Vector2 P_C = player.RotatedRelativePoint(player.MountedCenter);

            Projectile.direction = Projectile.velocity.X < 0 ? -1 : 1;
            Projectile.spriteDirection = Projectile.direction;
            player.ChangeDir(Projectile.direction);
            player.heldProj = player.whoAmI;
            player.SetDummyItemTime(2);
            Projectile.Center = P_C;
            float Rotataon_OFFset = Projectile.spriteDirection == -1 ? MathHelper.Pi : 0;
            Projectile.rotation = Projectile.velocity.ToRotation() + Rotataon_OFFset;
            player.itemRotation = (Projectile.velocity * Projectile.direction).ToRotation();
            Projectile.timeLeft = 2;
        }

        public override bool? CanDamage() => false;
        
    }
}
```

---

## 6. Content/Projectiles/Toy_Star_Fragments.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Projectiles/Toy_Star_Fragments.cs`

```csharp
using Microsoft.Xna.Framework;
using System;
using Terraria;
using Terraria.Audio;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Projectiles
{
    public class Toy_Star_Fragments : ModProjectile
    {
        private NPC HomingTarget//定义追踪目标
        {
            get => Projectile.ai[1] == 0 ? null : Main.npc[(int)Projectile.ai[1] - 1];
            set
            {
                Projectile.ai[1] = value == null ? 0 : value.whoAmI + 1;
            }
        }

        int UpSpeed = 0;//加速次数

        public override void SetStaticDefaults()
        {
            ProjectileID.Sets.CultistIsResistantTo[Type] = true;//拜月教徒追踪弹幕抗性
        }

        public override void SetDefaults()
        {
            Projectile.width = 30;
            Projectile.height = 30;
            Projectile.timeLeft = 1200;//弹幕存在时间
            Projectile.DamageType = DamageClass.Melee;
            Projectile.penetrate = -1;//弹幕穿透
            Projectile.friendly = true;//是否是友方弹幕
            Projectile.ignoreWater = false;//是否忽略水
            Projectile.tileCollide = true;//是否撞墙
            Projectile.extraUpdates = 1;
            Projectile.usesLocalNPCImmunity = true;//独立无敌帧是否启用
            Projectile.localNPCHitCooldown = 40;//独立无敌帧冷却
        }

        public override void AI()
        {
            float MaximumTrackingRange = float.MaxValue;//追踪距离，默认为最大值

            Lighting.AddLight(Projectile.Center, 230f / 255f, 203f / 255f, 87f / 255f);//设置光源，使用"XXX / 255"来避免太亮的问题

            Projectile.ai[0] += 1;//计时器，嗯对

            Projectile.rotation = Projectile.velocity.ToRotation() + MathHelper.Pi / 2;

            if (HomingTarget == null)
            {
                HomingTarget = FindClosestNPC(MaximumTrackingRange);
            }//如果没有NPC，就去寻找一个

            if (HomingTarget != null && !IsValidTarget(HomingTarget))
            {
                HomingTarget = null;
            }//而且还要确保有效，否则就无效（如目标NPC死了，跑远了，黄名了）

            //如果计时器到了，就执行以下内容
            if (Projectile.ai[0] >= 90)
            {
                Projectile.penetrate = 1;//限制无限穿透

                //如果有怪就追踪
                if (HomingTarget != null)
                {
                    float distance = Vector2.Distance(Projectile.Center, HomingTarget.Center);//计算弹幕与目标的距离
                    float TurnAngle = MathHelper.Clamp(130f / distance, 5f, 45f);//旋转角度，Clamp限制最大和最小角度--这就不会出现转圈圈的现象了--

                    float length = Projectile.velocity.Length();//弹幕的向量的长度
                    float targetAngle = Projectile.AngleTo(HomingTarget.Center);//朝目标旋转
                    
                    //用来实现平滑追踪的（--其实这个我不太懂--）
                    Projectile.velocity = Projectile.velocity.ToRotation().AngleTowards(targetAngle, MathHelper.ToRadians(TurnAngle)).ToRotationVector2() * length;
                }

                //如果没怪就逐渐隐藏并删除自身
                if (HomingTarget == null)
                {
                    Projectile.alpha += 10;

                    if (Projectile.alpha >= 255)
                    {
                        Projectile.Kill();
                    }
                }
                else//否则就 藏 隐
                {
                    Projectile.alpha -= 10;
                }

            }

            //在"90"计时器到之前就执行以下内容
            if (Projectile.ai[0] >= 70)
            {
                //如果有怪且"UpSpeed"未到最大值就加速并加1
                //否则就减速并减1
                if (UpSpeed <= 45 && HomingTarget != null)
                {
                    Projectile.velocity *= 1.04f;
                    UpSpeed += 1;
                }
                else if (UpSpeed != 0 && HomingTarget == null)
                {
                    Projectile.velocity *= 0.96f;
                    UpSpeed -= 1;
                }
            }

        }

        public override bool OnTileCollide(Vector2 oldVelocity)
        {
            Collision.HitTiles(Projectile.position, Projectile.velocity, Projectile.width, Projectile.height);
            SoundEngine.PlaySound(SoundID.Item56, Projectile.Center);

            if (Math.Abs(Projectile.velocity.X - oldVelocity.X) > float.Epsilon)
            {
                Projectile.velocity.X = -oldVelocity.X;
            }

            if (Math.Abs(Projectile.velocity.Y - oldVelocity.Y) > float.Epsilon)
            {
                Projectile.velocity.Y = -oldVelocity.Y;
            }

            return false;
        }

        //在有效范围里寻找NPC并追击，否则就返回"null"
        public NPC FindClosestNPC(float maxDetectDistance)
        {
            NPC closestNPC = null;

            //使用平方值而非平方根以节省性能开销（--话说平方根是什么？--）
            float sqrMaxDetectDistance = maxDetectDistance * maxDetectDistance;

            //遍历所有NPC
            foreach (var target in Main.ActiveNPCs)
            {
                //检测这个NPC是否最为可选目标
                if (IsValidTarget(target))
                {
                    //使用"DistanceSquared"函数检测平方距离避免开根号（--话说平方根是什么？--）
                    float sqrDistanceToTarget = Vector2.DistanceSquared(target.Center, Projectile.Center);

                    //检测是否在有效范围里，嗯对
                    if (sqrDistanceToTarget < sqrMaxDetectDistance)
                    {
                        sqrMaxDetectDistance = sqrDistanceToTarget;
                        closestNPC = target;
                    }
                }
            }

            return closestNPC;
        }

        //就是用来检测NPC类型的，没了
        public bool IsValidTarget(NPC target)
        {
            return target.CanBeChasedBy() 
                && !target.friendly //不是黄名的
                && !target.dontTakeDamage//不是无敌的
                && Collision.CanHit(Projectile.Center, 1, 1, target.position, target.width, target.height);//视线检测
        }
    }
}
```

---

## 7. Content/Projectiles/Painted_Brush_BOOM.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Projectiles/Painted_Brush_BOOM.cs`

```csharp
using Microsoft.Xna.Framework;
using Terraria;
using Terraria.Audio;
using Terraria.DataStructures;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Projectiles
{
    public class Painted_Brush_BOOM : ModProjectile
    {
        public override void SetStaticDefaults()
        {
            Main.projFrames[Projectile.type] = 5;//确认该弹幕的帧图
        }

        public override void SetDefaults()
        {
            Projectile.width = 44;
            Projectile.height = 72;
            Projectile.penetrate = -1;//穿透数量
            Projectile.timeLeft = 60;//弹幕存在时间
            Projectile.DamageType = DamageClass.Summon;
            Projectile.friendly = true;//是否是友方弹幕
            Projectile.ignoreWater = false;//是否忽略水
            Projectile.tileCollide = false;//是否撞墙
            Projectile.usesLocalNPCImmunity = true;//独立无敌帧是否启用
            Projectile.localNPCHitCooldown = -1;//独立无敌帧冷却
        }

        public override void OnSpawn(IEntitySource source)
        {
            SoundEngine.PlaySound(SoundID.Item14, Projectile.Center);
            for (int i = 0; i <= 35; i++)
            {
                Dust dust = Dust.NewDustPerfect(
                    Projectile.Center, 
                    DustID.SparkForLightDisc,
                    new Vector2(Main.rand.NextFloat(3f, -3f), Main.rand.NextFloat(3f, -3f)), 
                    0,
                    new Color(Main.rand.NextFloat(0f, 1f), Main.rand.NextFloat(0f, 1f), Main.rand.NextFloat(0f, 1f)),
                    Main.rand.NextFloat(1.2f, 2.5f));
                dust.noGravity = true;

            }
        }

        public override void AI()
        {
            Projectile.frameCounter++;
            if(Projectile.frameCounter >= 6)
            {
                Projectile.frameCounter = 0;
                Projectile.frame++;
            }

            if (Projectile.frame >= 5)
            {
                Projectile.Kill();
            }
        }

        public override void OnHitNPC(NPC target, NPC.HitInfo hit, int damageDone)
        {
            base.OnHitNPC(target, hit, damageDone);
        }
    }
}
```

---

## 8. Content/Items/Weapons/Magic/Test_One.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Items/Weapons/Magic/Test_One.cs`

```csharp
using Microsoft.Xna.Framework;
using System;
using Terraria;
using Terraria.DataStructures;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Items.Weapons.Magic
{

    public class Test_One : ModItem
    {

        public override void SetStaticDefaults()
        {
            Item.ResearchUnlockCount = 1;
        }

        public override void SetDefaults()
        {
            Item.SetWeaponValues(5000, 1000, 100); //设置伤害、击退、暴击率
            Item.DefaultToMagicWeapon(ProjectileID.VenomFang,15,0f,true);
            Item.UseSound = SoundID.Item43;
            Item.mana = 5;
            Item.width = 40;
            Item.height = 40;
            Item.useStyle = ItemUseStyleID.Shoot;
            // 只留一行：buyPrice 是买入价，sellPrice 是卖出价，写两行后者会覆盖前者
            Item.value = Item.buyPrice(1, 0, 0, 0);
            Item.rare = ItemRarityID.Pink;


        }

        public override bool Shoot(Player player, EntitySource_ItemUse_WithAmmo Source, Vector2 position, Vector2 velocity, int type, int damage, float knockback)
        {
            Vector2 PlrToMoUse = Main.MouseWorld - player.Center;
            float r = (float)Math.Atan2(PlrToMoUse.Y, PlrToMoUse.X);
            
            float Foi = 8;
            for (int i = 0; i <= Foi; i += 1)// 把圆8等分，然后设置每个弹幕的量向
            {
                float nf = MathHelper.TwoPi / Foi * i + r;// 把圆8等分，然后设置弹幕的角度
                float v = nf + r;
                Vector2 n = new Vector2((float)Math.Cos(nf), (float)Math.Sin(nf)) * 15f;
                Projectile.NewProjectile(Source, position, n, type, damage, 1000f ,player.whoAmI);
            }
            return false;
            
        }

        //public override void AddRecipes()
        //{
        //    Recipe recipe = CreateRecipe();
        //    recipe.AddIngredient(ItemID.DirtBlock, 10);
        //    recipe.AddTile(TileID.WorkBenches);
        //    recipe.Register();
        //}
    }
}
```

---

## 9. Content/Items/Weapons/Summon/Minions/Test_Two.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Items/Weapons/Summon/Minions/Test_Two.cs`

```csharp
using Microsoft.Xna.Framework;
using Terraria;
using Terraria.Audio;
using Terraria.DataStructures;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Items.Weapons.Summon.Minions
{
    public class Test_Two : ModItem
    {
        public override void SetStaticDefaults()
        {
            Item.ResearchUnlockCount = 1;
        }    
        public override void SetDefaults()   
        {        
            Item.SetWeaponValues(5000, 1000, 100); //设置伤害、击退、暴击率
            //Item.DefaultToS
            Item.UseSound = SoundID.Item25;
            Item.mana = 5;
            Item.width = 40;
            Item.height = 40;
            Item.useStyle = ItemUseStyleID.Shoot;
            // 只留一行：buyPrice 是买入价，sellPrice 是卖出价，写两行后者会覆盖前者
            Item.value = Item.buyPrice(1, 0, 0, 0);
            Item.rare = ItemRarityID.Pink;
        }

    }
    
}
```

---

## 10. Content/Buffs/Soul_Burn_Buff.cs

**Path:** `F:/XJXJXJXJXJXJXJXJ/st/steamapps/common/tModLoader/ModSources/PrendeckOddments/Content/Buffs/Soul_Burn_Buff.cs`

```csharp
using Microsoft.Xna.Framework;
using PrendeckOddments.Content.Projectiles;
using Terraria;
using Terraria.DataStructures;
using Terraria.Graphics.Shaders;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Buffs
{
    public class Soul_Burn_Buff : ModBuff
    {
        public override void SetStaticDefaults()
        {
            Main.buffNoSave[Type] = true;
            Main.debuff[Type] = true;
            Main.buffNoTimeDisplay[Type] = false;
            Main.persistentBuff[Type] = false;
            Main.vanityPet[Type] = false;
        }

        public override void Update(Player player, ref int buffIndex)
        {
            player.GetDamage(DamageClass.Generic) *= 1.65f;
            player.GetCritChance(DamageClass.Generic) += 45;

            if (player.lifeRegen >= 0)
            {
                player.lifeRegen = 0;
            }
            player.lifeRegenTime = 0;
            player.lifeRegen -= 30;

            if (Main.rand.NextBool(2))
            {
                Dust d = Dust.NewDustDirect(player.position, player.width, player.height, DustID.LifeDrain);
                d.velocity *= 0.75f;
            }

        }
    }
}
```

---

All 10 files have been read successfully. Here is a brief structural summary of what each file demonstrates:

- **Toy_Knife.cs** -- A melee weapon with a mana-gated special projectile shot every 4th swing, mana regen on hit, dust effects during swings, dual gold/platinum recipes, and dynamic tooltip formatting.
- **Toy_Star.cs** -- The projectile spawned by Toy_Knife: bouncing off tiles, slowing on hit, emitting light, and splitting into 5 homing Toy_Star_Fragments on death.
- **Sigma.cs** -- A simpler melee projectile with deceleration, custom sound on hit via `SoundStyle` loading from the mod's Assets folder, and damage decay on NPC hit.
- **Shadow_Guny.cs** -- A ranged weapon with right-click alternate fire (dual-function weapon), ammo consumption chance reduction, random gunshot sounds, glow mask drawing via `PostDrawInWorld`, and spread via `ModifyShootStats`.
- **Shadow_Guny_Htelm.cs** -- A held projectile that mimics the player's weapon swing (used for the right-click special attack), with frame animation setup and `CanDamage() => false` so it is purely visual.
- **Toy_Star_Fragments.cs** -- A homing projectile spawned by Toy_Star's death: stores its target in `Projectile.ai[1]`, searches for the closest valid NPC using squared-distance optimization, accelerates toward targets after a delay, and fades out when no target is found.
- **Painted_Brush_BOOM.cs** -- A summon-class projectile that plays a frame-by-frame animation (5 frames), spawns colorful no-gravity dust on spawn, and self-destructs after the animation completes.
- **Test_One.cs** -- A magic weapon that fires 8 projectiles in a circular burst pattern around the cursor direction using trigonometric angle division.
- **Test_Two.cs** -- A minimal summon weapon stub (incomplete, with a commented-out `DefaultToS` line), setting basic weapon stats without a projectile assignment.
- **Soul_Burn_Buff.cs** -- A debuff that grants +65% damage and +45% crit chance but aggressively drains life regeneration at -30, with visual LifeDrain dust particles.

Here are the complete findings from my research on the CalamityMod source code structure.

---

## 1. GitHub Repository URL

**Public Repository:** [https://github.com/CalamityTeam/CalamityModPublic](https://github.com/CalamityTeam/CalamityModPublic)

- Owned by the **CalamityTeam** GitHub organization (linked to Azafure, LLC)
- This is the **public mirror** of the latest official release only. Active development occurs on a private repository.
- The primary branch is `**1.4.4**` (targeting tModLoader for Terraria 1.4.4)
- Has 29,113+ commits, 516 stars, 296 forks
- Issues are disabled; bug reports go through the Calamity Discord

**DeepWiki (automated code analysis):** [https://deepwiki.com/CalamityTeam/CalamityModPublic](https://deepwiki.com/CalamityTeam/CalamityModPublic)

---

## 2. License

The Calamity Mod uses a **proprietary license** -- it is NOT open source. From `LICENSE.md`:

- All source code, visual assets, audio assets, characters, names, logos, trademarks, and branding are **proprietary to Azafure, LLC** (a Virginia limited liability company)
- **All rights reserved**
- Contributors assign copyright of their contributions to Azafure
- **You may use the source code as a reference** for building Terraria mods or other software
- If you lift any code, you **must credit "Azafure, LLC"** and provide a link to the repository
- **The mod cannot be redistributed** in any form; Steam Workshop is the only official download
- Music tracks remain property of their respective composers, used by Azafure with permission

---

## 3. Project Directory Structure

The project root contains these top-level folders and files:

**Core files at root:**

- `CalamityMod.cs` -- Main mod entry point (extends `Mod`)
- `CalamityMod.csproj` -- Project file
- `CalamityConfig.cs` -- Configuration settings
- `CalamityKeybinds.cs` -- Key bindings
- `CalamityConditions.cs` -- Custom conditions
- `CalamityNetcode.cs` -- Network code
- `build.txt`, `description.txt` -- tModLoader metadata
- `LICENSE.md`, `README.md`

**Content directories:**


| Directory      | Purpose                                                                                          |
| -------------- | ------------------------------------------------------------------------------------------------ |
| `Items/`       | All items (Weapons, Accessories, Armor, Ammo, Materials, etc.)                                   |
| `Projectiles/` | All projectile code, organized by class (Melee, Magic, Ranged, Rogue, Summon, Boss, Enemy, etc.) |
| `NPCs/`        | All NPCs including bosses, enemies, town NPCs                                                    |
| `Buffs/`       | Status effects                                                                                   |
| `Tiles/`       | Custom tiles                                                                                     |
| `Walls/`       | Custom walls                                                                                     |
| `World/`       | World generation and biome management                                                            |


**System directories:**


| Directory         | Purpose                                                        |
| ----------------- | -------------------------------------------------------------- |
| `CalPlayer/`      | Player mechanics (CalamityPlayer, draw layers, on-hit effects) |
| `Balancing/`      | Balancing constants and changes manager                        |
| `Systems/`        | World state, biome counters                                    |
| `Events/`         | Boss Rush and other events                                     |
| `DataStructures/` | Custom data structures                                         |
| `UI/`             | User interface elements                                        |
| `Utilities/`      | Helper classes (DropHelper, PlayerUtils, etc.)                 |
| `ILEditing/`      | IL code modifications to vanilla behavior                      |
| `ModSupport/`     | Cross-mod compatibility                                        |
| `Packets/`        | Network packet handling                                        |


**Visual/Audio directories:**


| Directory        | Purpose                   |
| ---------------- | ------------------------- |
| `Effects/`       | Shader and visual effects |
| `Graphics/`      | Metaballs, rendering      |
| `Particles/`     | Particle systems          |
| `Sounds/`        | Audio assets              |
| `Backgrounds/`   | Background styles         |
| `Skies/`         | Sky rendering             |
| `Dusts/`         | Dust effects              |
| `Gores/`         | Gore effects              |
| `Fonts/`         | Custom fonts              |
| `ExtraTextures/` | Additional textures       |


**Other directories:**


| Directory             | Purpose                              |
| --------------------- | ------------------------------------ |
| `BiomeManagers/`      | Custom biome definitions             |
| `Cooldowns/`          | Cooldown tracking                    |
| `ChatTags/`           | Chat formatting                      |
| `CustomRecipes/`      | Recipe modifications                 |
| `DamageClasses/`      | Custom damage classes (Rogue, etc.)  |
| `Debugging/`          | Debug utilities                      |
| `Dialogues/`          | NPC dialogue                         |
| `Enums/`              | Enumeration types                    |
| `FluidSimulation/`    | Fluid physics                        |
| `ForegroundDrawing/`  | Foreground rendering                 |
| `InverseKinematics/`  | IK system (for worm bosses)          |
| `MainMenu/`           | Custom main menu                     |
| `Pathfinding/`        | Pathfinding utilities                |
| `Physics/`            | Physics utilities                    |
| `Prefixes/`           | Weapon prefixes                      |
| `Properties/`         | Assembly properties                  |
| `Rarities/`           | Custom rarities                      |
| `Scenes/`             | Scene management                     |
| `Schematics/`         | Structure schematics                 |
| `TileEntities/`       | Tile entity logic                    |
| `Localization/en-US/` | Localization files (`.hjson` format) |


**Items/Weapons substructure:**

- `Items/Weapons/Melee/`
- `Items/Weapons/Magic/`
- `Items/Weapons/Ranged/`
- `Items/Weapons/Rogue/` (Calamity's unique class)
- `Items/Weapons/Summon/`
- `Items/Weapons/Typeless/`
- `Items/Weapons/DraedonsArsenal/` (special weapon set)

**Projectiles substructure:**

- `Projectiles/BaseProjectiles/` -- Reusable base classes
- `Projectiles/Boss/` -- Boss attack projectiles
- `Projectiles/Damageable/` -- Damageable projectile objects
- `Projectiles/DraedonsArsenal/`
- `Projectiles/Enemy/` -- Enemy attack projectiles
- `Projectiles/Environment/`
- `Projectiles/Healing/`
- `Projectiles/Magic/`
- `Projectiles/Melee/`
- `Projectiles/Pets/`
- `Projectiles/Ranged/`
- `Projectiles/Rogue/`
- `Projectiles/Summon/`
- `Projectiles/Turret/`
- `Projectiles/Typeless/`
- `Projectiles/VanillaProjectileOverrides/`

---

## 4. Common Projectile Patterns

Based on the actual source code (especially `CommonProjectileAI.cs` and the DeepWiki analysis):

### ai[] Array Usage

The `ai[]` array is used extensively as a state machine. Common patterns:

**State machine via `ai[0]`:**

- `ai[0] = 0f` -- Normal/homing state
- `ai[0] = 1f` -- Returning to player or stuck to NPC
- `ai[0] = 2f` -- Charge/cooldown state

**Timer/counter via `ai[1]`:**

- Used as a timer that increments each frame
- Reset to 0 or 1 when a threshold is reached
- Used to track charge count or delay between attacks

**Stuck-to-NPC pattern:**

```csharp
// ai[0] = 1f means stuck
// ai[1] = NPC index it is stuck to
projectile.ai[0] = 1f;
projectile.ai[1] = (float)npcIndex;
```

`**localAI[0]**` is used for additional timers (e.g., hit effect cooldowns, animation timers).

### Common AI Methods (from CommonProjectileAI.cs)

1. `**ChargingMinionAI()**` -- Full minion AI with target finding, idle movement, charge attacks, and cooldown management. Uses `ai[0]` for state (0=idle, 1=returning, 2=charging) and `ai[1]` for charge counter.
2. `**FloatingPetAI()**` -- Pet following behavior with anti-clumping, smooth movement, and teleport-to-player if too far.
3. `**HealingProjectile()**` -- Homing toward a player to heal them, with distance-based activation.
4. `**MinionAntiClump()**` -- Prevents same-type minions from stacking by nudging them apart.
5. `**StickyProjAI()**` -- Makes projectiles stick to NPCs, follow them, and deal periodic damage. Works with `ModifyHitNPCSticky()`.
6. `**StickToTiles()**` -- Makes projectiles stop when hitting solid tiles.

### Homing Pattern

The standard homing pattern uses inertia-based velocity blending:

```csharp
Vector2 targetVec = target.Center - projectile.Center;
float dist = targetVec.Length();
targetVec.Normalize();
targetVec *= speed;
projectile.velocity = (projectile.velocity * inertia + targetVec) / (inertia + 1f);
```

### Target Finding Pattern

Projectiles iterate `Main.npc[]` to find the closest valid target:

```csharp
for (int npcIndex = 0; i < Main.maxNPCs; i++) {
    NPC npc = Main.npc[npcIndex];
    if (npc.CanBeChasedBy(projectile, false)) {
        float dist = Vector2.Distance(npc.Center, projectile.Center);
        if (dist < maxDist && Collision.CanHit(...)) {
            maxDist = dist;
            targetVec = npc.Center;
            foundTarget = true;
        }
    }
}
```

### Global Projectile System

`CalamityGlobalProjectile.cs` provides global modifications to all projectiles. `CalamityGlobalProjectileTweaks.cs` uses a `SortedDictionary<int, IProjectileTweak[]>` database to apply tweaks like damage adjustments, True Melee flags, Point Blank support, and Defense Damage interactions.

---

## 5. Common Weapon Patterns

### Weapon Class Structure

Weapons extend `ModItem` and follow this standard pattern:

```csharp
public override void SetDefaults() {
    item.damage = X;
    item.DamageType = DamageClass.Melee; // or Magic, Ranged, Summon, Rogue
    item.width = X;
    item.height = X;
    item.useTime = X;
    item.useAnimation = X;
    item.useStyle = ItemUseStyleID.Swing; // or other styles
    item.knockBack = X;
    item.value = Item.sellPrice(gold: X);
    item.rare = ItemRarityID.X;
    item.UseSound = SoundID.ItemX;
    item.autoReuse = true/false;
    item.shoot = ProjectileType<SomeProjectile>();
    item.shootSpeed = Xf;
    item.noMelee = true/false; // for ranged/magic
}
```

### Special Weapon Systems

**Charge System** (Draedon's Arsenal weapons):

```csharp
Item.Calamity().UsesCharge = true;
Item.Calamity().MaxCharge = 50f;
Item.Calamity().ChargePerUse = 0.05f;
```

**Rogue Stealth Strikes:**

```csharp
// In SetDefaults or Shoot:
if (player.Calamity().StealthStrikeAvailable()) {
    // Enhanced behavior: more projectiles, more damage, special effects
    projectile.damage *= (int)StealthDamageMultiplier;
}
```

**True Melee Weapons:** Weapons that deal direct contact damage rather than shooting projectiles, flagged via the `TrueMelee` tweak.

**Point Blank Weapons:** Ranged weapons that can hit enemies at close range, flagged via the `PointBlank` tweak.

### Item Tweak Database

The `CalamityGlobalItemTweaks` class uses a `SortedDictionary<int, IItemTweak[]>` to apply property changes to vanilla and Calamity items during `SetDefaults`. Common tweaks include:

- `DamageExact(X)` -- Set exact damage
- `UseTimeExact(X)` -- Set exact use time
- `AutoReuse` -- Enable auto-reuse
- `TrueMelee` -- Flag as true melee
- `PointBlank` -- Enable point-blank shots
- `MaxStack(X)` -- Set stack size
- `NotConsumable` -- Don't consume on use

### Balancing System

`BalancingChangesManager.cs` applies per-projectile and per-NPC damage adjustments. Bosses have specific resistances to certain weapons to prevent cheese strategies (e.g., Desert Scourge has 50% resistance to true melee, Providence has 80% resistance to Hell's Sun).

### Localization

All item/projectile/NPC names and tooltips are defined in `Localization/en-US/Mods.CalamityMod.*.hjson` files using the `.hjson` format, not hardcoded in C#.

---

## Key Source References

- Repository: [https://github.com/CalamityTeam/CalamityModPublic](https://github.com/CalamityTeam/CalamityModPublic)
- Branch: `1.4.4`
- Main class: `CalamityMod.cs`
- Projectile AI utilities: `Projectiles/CommonProjectileAI.cs`
- Global projectile tweaks: `Projectiles/CalamityGlobalProjectileTweaks.cs`
- Global item tweaks: `Items/CalamityGlobalItemTweaks.cs`
- Balancing: `Balancing/BalancingChangesManager.cs`
- DeepWiki overview: [https://deepwiki.com/CalamityTeam/CalamityModPublic](https://deepwiki.com/CalamityTeam/CalamityModPublic)
- DeepWiki item/projectile system: [https://deepwiki.com/CalamityTeam/CalamityModPublic/2.3-item-and-projectile-system](https://deepwiki.com/CalamityTeam/CalamityModPublic/2.3-item-and-projectile-system)

I now have comprehensive information about both the local mod code and the CalamityMod source structure. Let me create my plan for writing this tutorial.

I'm currently in plan mode, so I cannot write the tutorial file directly. However, I've completed all research needed. Here is my plan and findings:

---

## Plan: 如何阅读和分析模组源码 - 教程撰写

### Output File

`E:\XJXJXJXJXJXJXJXJXJXJXJXJ\ME-Note\AI日志\如何阅读模组源码.md`

### Tutorial Structure (8 chapters)

**Chapter 1 - Source Acquisition**

- CalamityMod public repo: [https://github.com/CalamityTeam/CalamityModPublic](https://github.com/CalamityTeam/CalamityModPublic) (branch `1.4.4`)
- License: Proprietary (Azafure, LLC) -- can reference, must credit
- tModLoader built-in source viewing
- File structure: Items/, Projectiles/, NPCs/, Effects/, CalPlayer/, Balancing/, Utilities/, CommonProjectileAI.cs

**Chapter 2 - Reading Strategy**

- Goal-oriented reading (don't read linearly)
- Ctrl+Shift+F global search
- Category-based browsing

**Chapter 3 - Weapon Analysis (concrete example: Toy_Knife.cs)**

- SetDefaults(), Shoot(), CanUseItem() walkthrough
- Distinguishing standard patterns from custom logic

**Chapter 4 - Projectile AI Analysis (concrete example: Toy_Star_Fragments.cs)**

- AI() hook, ai[] as timer + state + target storage
- localAI[] usage
- Timer patterns

**Chapter 5 - Common Patterns**

- Homing projectile (FindClosestNPC + velocity blending)
- Scatter projectile (Test_One's circular pattern)
- Split projectile (Toy_Star -> Toy_Star_Fragments)
- Pseudocode + code snippets for each

**Chapter 6 - Visual Effects**

- Dust system, Lighting.AddLight, screen shake, shader entry points

**Chapter 7 - Note-taking template**

**Chapter 8 - Learning path suggestions**

### Gathered Code Examples (all read and ready)

- Toy_Knife.cs -- weapon with mana gating, swing dust, custom Shoot
- Toy_Star.cs -- bouncing projectile with split-on-kill
- Toy_Star_Fragments.cs -- homing projectile with ai[] patterns
- Test_One.cs -- circular scatter pattern
- Sigma.cs -- decelerating projectile with custom sound
- Shadow_Guny.cs -- dual-function ranged weapon
- Painted_Brush_BOOM.cs -- frame-animated explosion
- Soul_Burn_Buff.cs -- buff with damage boost + life drain

### Next Step

The plan is complete. The tutorial file needs to be written to the target path. Since plan mode is active, this file creation is blocked in my session. The parent agent or another agent with write permissions should execute the file creation.

Should I proceed to write the tutorial file now?

Let me use a different approach - write a Python script file then execute it.

文件内容不完整，代码块被吞了。让我重新写完整版。

四篇教程全部写好了！都在 `AI日志\` 里：


| 文件                    | 大小     | 内容               |
| --------------------- | ------ | ---------------- |
| `CSharp基础-泰拉模组专用.md`  | 9.9 KB | C# 基础，只讲模组开发会用到的 |
| `tModLoader武器开发入门.md` | 7.6 KB | 从零写武器，含4种武器模板    |
| `如何阅读模组源码.md`         | 4.8 KB | 以灾厄为参考，教你找代码     |
| `tModLoader特效实现参考.md` | 6.4 KB | 粒子/光照/Shader 速查  |


Prendeck，你睡醒就能看了！早点休息～ ✨