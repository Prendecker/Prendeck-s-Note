# 代码问题清单

> 项目：`PrendeckOddments`
> 排查日期：2026-09-17
> 排查方式：逐个文件通读 + 用 `PrendeckTools/api_lookup.py` 查官方 API 文档查证

一共 **13 个问题**（2026-09-25 更新：**9 个已修**，剩 4 个 ⏸ —— 5/10/13 等武器正式化再处理，8 等手持弹幕写完），另有 **2 个查证后确认「不是问题」**（见文末，避免以后重复怀疑）。

严重程度分三档：
- 🔴 **玩家能直接看到不对**
- 🟠 **会误导自己**
- 🟡 **不影响运行，只影响整洁**

---

## 🔴 第一梯队：玩家能直接看到（2 个）

### 1. `Item.value` 连续赋值两次

**位置**：5 个武器文件各一处

| 文件 | 行 |
|---|---|
| `Content/Items/Weapons/Melee/Sigkin.cs` | 30-31 |
| `Content/Items/Weapons/Ranged/B_Gun.cs` | 26-27 |
| `Content/Items/Weapons/Magic/Test_One.cs` | 28-29 |
| `Content/Items/Weapons/Summon/Minions/Test_Two.cs` | 25-26 |
| `Content/Items/Weapons/Summon/Marking/The_Poorly_Painted_Brush.cs` | 29-30 |

**现象**：所有写法都是先 `sellPrice` 再 `buyPrice`，后一行把前一行**整个覆盖掉**。

其中「被鸽的画笔」最明显：

```csharp
Item.value = Item.sellPrice(0, 0, 7, 0);   // 想卖 7 银
Item.value = Item.buyPrice(0, 0, 0, 0);    // 结果被覆盖成 0
```

→ 这物品现在**一文不值**。

**原理**：`Item.value` 是**同一个字段**，赋值两次就是第二次赢。`buyPrice` 和 `sellPrice` 不是两种"设置方式"，而是两种**不同的意图**：

官方文档原文（用 `api_lookup.py Item.sellPrice` 查到的）：

- `buyPrice` — *"If assigned to `Item.value`, that item will be **bought** for the provided value."*
- `sellPrice` — *"If assigned to `Item.value`, that item will be **sold** for the provided value. This value is **five times larger** than `Item.buyPrice`."*

**关键**：`sellPrice` 的数值是 `buyPrice` 的 **5 倍**。所以你写两行，不只是"多写一行"，而是**把物品价格偷偷改成了 1/5**。

**怎么自己查证**：

```bash
python Tools/api_lookup.py Item.sellPrice
python Tools/api_lookup.py Item.buyPrice
```

**怎么改**：二选一，只留一行。

- 想让它**卖** 1 铂金 → 只写 `Item.sellPrice(1,0,0,0)`
- 想让它**买** 1 铂金 → 只写 `Item.buyPrice(1,0,0,0)`

> ⚠️ 五个文件改法**不完全一样**：「被鸽的画笔」要保留 `sellPrice`（因为 `buyPrice(0,0,0,0)` 让它变成 0 元，明显不是本意）；其余四个测试武器保留哪个都行，看你想让它值多少钱。

**当前状态**：✅ 已修

---

### 2. en-US 本地化的坏键引用

**位置**：`Localization/en-US_Mods.PrendeckOddments.hjson` 的 Buffs 段

```hjson
Buffs: {
    Soul_Burn_Buff: {
        DisplayName: Soul Burn
        Description: Mods.PrendeckOddments.Buffs.SoulBurnBuff.Description   # ← 这行
    }
}
```

**现象**：游戏里燃魂 Buff 的描述会**原样显示这串键名**（`Mods.PrendeckOddments.Buffs.SoulBurnBuff.Description`），而不是任何说明文字。

**原理**：tModLoader 的本地化键按**类名**索引，这个 Buff 的类名是 `Soul_Burn_Buff`（带下划线），而这里写的是 `SoulBurnBuff`（没下划线）——**指向了一个不存在的键**。

**顺带一提**：同一个错误在 `Projectiles` 段也有（见问题 4）。

**怎么改**：写正常的英文描述，或者干脆删掉这一行。

**当前状态**：✅ 已修（改成了正常英文）

---

## 🟠 第二梯队：会误导自己（3 个）

### 3. `SetWeaponValues` 参数注释标错

**位置**：多个武器文件

```csharp
Item.SetWeaponValues(114514, 1000, 100); //设置伤害，暴击率，射速   ← 注释是错的
```

**真实签名**（`api_lookup.py SetWeaponValues` 查证）：

```csharp
void SetWeaponValues(int dmg, float knockback, int bonusCritChance)
```

是**伤害、击退、暴击率**，不是"伤害、暴击率、射速"。三个参数里**错了两个**。

**为什么这条值得单列**：注释是写给未来的自己看的。参数顺序记错 + 注释也写错 = **双重误导**，以后照着注释写新武器就会把击退值填到暴击率的位置上。

**讽刺的是**：`The_Poorly_Painted_Brush.cs:20` 里你自己写对了（`//设置伤害，击退，暴击率`）——说明后来学会了，只是早期文件没回头改。

**怎么改**：改注释即可，**不要动数值**（动数值会改变手感）。

**当前状态**：✅ 已修

---

### 4. 畸形的重复键

**位置**：两个本地化文件都有

```hjson
Projectiles: {
    Projectiles.Sigma.DisplayName: 斯格玛    # ← 多了一层 Projectiles.
    Sigma.DisplayName: 斯格玛                # ← 正确写法
}
```

**现象**：无害，但脏。而且它和问题 2 是**同一种手滑**（键名写错），只是这个恰好没造成可见影响。

**当前状态**：✅ 已修（两个文件都删掉了畸形的那行）

---

### 5. 测试数值未平衡

**位置**：全局

| 物品 | 伤害 | 击退 |
|---|---|---|
| `Sigkin` 西格玛 | 114514 | 1000 |
| `B_Gun` B枪 | 131313 | 1000 |
| `Test_One` 装满中二语录的书书 | 5000 | 1000 |
| `Test_Two` 废物 | 5000 | 1000 |

**现象**：这些是**梗数值**，正式发布前必须处理。

**注意**：击退 `1000` 会让敌人**飞出去**，实战里可能比伤害还影响体验。原版武器的击退一般在 `0` ~ `20` 之间。

**当前状态**：⏸ 未处理（需要先定这模组的定位——你笔记里写的是"超模 + 娱乐向"，那数值偏高是合理的，但 11 万就纯粹是玩梗了）

---

## 🟡 第三梯队：不影响运行，只影响整洁（8 个）

### 6. XML 文档注释闭合标签写错

**位置**：`Content/LIVG_PIIU_GLue.cs:7-9` 和 `32-35`

```csharp
///<summary>
///修改原版3个骗伤弹幕并注入一些咒骂re的话
///<summary>          ← 开闭都写成 <summary>，少了个斜杠
```

**现象**：编译器不会报错，但 IDE 认不出这是文档注释，**鼠标悬停时不会显示这段说明**。等于白写。

**怎么改**：闭合标签应该是 `///</summary>`（多个斜杠）。

**当前状态**：✅ 已修（2026-09-25 用户自己修的，两处都改成了 `///</summary>`）

---

### 7. 未使用的 using

**位置**：

- `Content/Projectiles/Ammo_Proj/Gravel_Bullet_Proj.cs:2` —— `using System.Net.NetworkInformation;`（跟弹幕八竿子打不着，八成是 IDE 自动补全点错了）
- 3 个文件里的 `using Terraria.Graphics.Shaders;`（没写任何 shader）

**现象**：完全无害，但会让人以为这文件用了网络或着色器。

**当前状态**：✅ 已修（2026-09-25，删除 4 处：Gravel_Bullet_Proj 的 NetworkInformation + 3 个文件的 Shaders）

---

### 8. 未使用的贴图资源

**位置**：`Content/Projectiles/Held_Item_Proj/Shadow_Guny_Htelm_Glow.png`

**现象**：图在这，但**没有任何代码引用它**。参考 `Shadow_Guny.cs` 本体是写了 `_Glow` 发光层绘制的，手持弹幕这套没写。

**两种可能**：① 本来想做发光效果，鸽了；② 想删图忘了删。

**当前状态**：⏸ 未处理

---

### 9. 空重写

**位置**：`Content/Projectiles/Sigma.cs:46-49`

```csharp
public override bool PreKill(int timeLeft)
{
    return base.PreKill(timeLeft);   // 只调了 base，什么也没做
}
```

**现象**：删掉整个方法，行为**完全一样**。空重写会让人误以为这里有特殊逻辑。

**当前状态**：✅ 已修（2026-09-25 用户自己删的，git diff 确认 `PreKill` 已从 Sigma.cs 移除）

---

### 10. 注释掉的死代码

**位置**：4 处

- `Sigkin.cs:50-56`、`B_Gun.cs:61-67`、`Test_One.cs:52-58` —— 三个文件里躺着**一模一样的**土块配方模板
- `B_Gun.cs:46-49` —— 注释掉的 `ModifyShootStats`

**现象**：这是从模板复制粘贴留下的痕迹。不影响运行，但会让文件变长、干扰阅读。

**建议**：真想留着当参考，不如挪到笔记里；代码文件保持干净。

**当前状态**：⏸ 未处理

---

### 11. 缩进混用

**位置**：全项目

- `Sigkin.cs` 用 **Tab**
- 多数文件用 **4 个空格**
- 部分文件内部还混着两种

**现象**：在编辑器里看会歪歪扭扭。建议全项目统一成 4 空格。

**当前状态**：✅ 已修（2026-09-25，3 个文件 31 行 Tab → 4 空格：Sigkin.cs 25 行、Sigma.cs 2 行、PrendeckOddments.cs 4 行。全项目 `^\t` 已清零）

---

### 12. `AGENTS.md` 已过时

**位置**：`AGENTS.md` 里关于 `.csproj` 的那段

文档里写着：

> Line 17 links a texture from `F:\JAVA MODS\TRMOD开发\贴图\PNG贴图\Painted_Brush_BOOM.png`. This is a local path on the author's machine.

**实际上**：`PrendeckOddments.csproj` 现在**只有 20 行**，**根本没有这一行**，那个硬编码路径早就删掉了。

**现象**：文档和现实不符，以后照着文档排查会被带偏。

**当前状态**：✅ 已修（2026-09-25，「Hardcoded paths」节改写成现状：csproj 无硬编码路径；「Excluded directories」节补上 Tools/；目录树补了 Tools/ 一行）

---

### 13. 模板占位文案没换

**位置**：`description.txt`、`description_workshop.txt`

还是模板原文：`Modify this file with a description of your mod.`

**现象**：上架 Steam 时如果忘了改，玩家看到的就是这句英文模板。

**当前状态**：⏸ 未处理

---

# 附录：查证后确认「不是问题」的（2 个）

> 这两个我一度怀疑是坑，查证后发现是**对的**。记下来，避免以后重复怀疑。

## A. en-US 全是空 tooltip —— 有意推迟，不是疏忽

`en-US_Mods.PrendeckOddments.hjson` 里 10 个物品的 `Tooltip: ""`，显示名还带怪下划线（`Shadow_ Guny`）。

**这不是 bug**，是**有计划的推迟**：等正式版做机翻，然后挂 Steam 上求人工英化。

**但要注意**：问题 2 那个「坏键」和这个是两回事 —— 空 tooltip 是"没写"，坏键是"写错了指向不存在的键"，后者会**显示出原始键名**这种很显眼的错误。做英化时记得连它一起处理。

## B. `Toy_Knife` 的 `[0]` 占位符 —— 是正确写法

`Toy_Knife.cs:23-38` 用了两个不同的占位符，一度以为 `[0]` 是 tModLoader 1.3 的旧语法残留。

**实际上这是有意设计**：

```csharp
// {0} → 由 WithFormatArgs 注入「固定回蓝量」
public override LocalizedText Tooltip => base.Tooltip.WithFormatArgs(MANA_Regen);

// [0] → 由 ModifyTooltips 手动替换成「实际魔力消耗」
public override void ModifyTooltips(List<TooltipLine> tooltips)
{
    int R_MANA = (int)(MANA * player.manaCost);   // 算了玩家的魔力减免
    foreach (var item in tooltips)
        if (item.Text.Contains("[0]"))
            item.Text = item.Text.Replace("[0]", R_MANA.ToString());
}
```

**为什么必须这么写**：这两个值**不一样**。`{0}` 是固定的（`MANA/5`），而实际消耗要乘以玩家的 `manaCost` 减免 —— 那个值**只有生成 tooltip 时才拿得到**，静态的 `WithFormatArgs` 够不着。

所以「自定义占位符 + `ModifyTooltips` 替换」是**正解**，甚至可以说是这套 API 下的标准解法。

---

# 怎么自己查 API

配套工具在模组目录下的 `Tools/`：

```bash
python Tools/api_lookup.py ModItem.Shoot         # 查单个钩子
python Tools/api_lookup.py --type ModProjectile  # 列出一个类所有可 override 的钩子
python Tools/api_lookup.py --overridable OnHit   # 搜所有带 OnHit 的钩子
python Tools/api_lookup.py --ns                  # 列出所有命名空间
```

> `Tools/` 已在 `.csproj` 里整体排除，不会参与模组编译打包。

数据来自**本地**的 `tModLoader.xml`（官方文档）+ 反射 `tModLoader.dll`（拿准确签名），
和你的游戏版本严格一致，**零网络请求**。

输出里 `▸` 标记表示「**可以 override**」—— 这是模组开发最关心的信息。
