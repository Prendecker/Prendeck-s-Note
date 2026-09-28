# C# 基础速查 — 泰拉模组开发专用版

> 这份教程只讲 tModLoader 模组开发会用到的 C# 知识，不讲无关内容。每个概念都配有泰拉瑞亚模组的实际代码示例。

---

## 目录

1. [变量和数据类型](#1-变量和数据类型)
2. [运算符](#2-运算符)
3. [条件判断](#3-条件判断)
4. [循环](#4-循环)
5. [方法（函数）](#5-方法函数)
6. [类和对象](#6-类和对象)
7. [属性（Property）](#7-属性property)
8. [常用语法速查](#8-常用语法速查)
9. [继续学习建议](#9-继续学习建议)

---

## 1. 变量和数据类型

变量就是一个**盒子**，里面装数据。每种数据有不同的"大小"和"类型"。

### 基本数据类型

```csharp
int damage = 50;          // 整数（最常用，武器伤害、弹幕伤害）
float speed = 8.5f;       // 小数（弹幕速度，注意末尾的 f）
double precise = 3.14159; // 更精确的小数（一般用不到）
bool isCritical = true;   // 布尔值（真/假，暴击判断）
string name = "火焰剑";   // 文字（武器名字、tooltip）
```

### tModLoader 常用类型

```csharp
Player player;   // 玩家对象（你的角色）
NPC npc;          // NPC/怪物对象
Projectile proj;  // 弹幕对象
Item item;        // 物品对象
```

### 常量 vs 变量

```csharp
// 变量：可以改
int mana = 20;
mana = 30; // ✅ 没问题

// 常量：不能改（用 const 修饰）
const int MaxMana = 100;
MaxMana = 200; // ❌ 编译错误！
```

### 变量命名规则

```csharp
int playerHealth;    // ✅ 驼峰命名（小写开头）
int PlayerHealth;    // ⚠️ 也行，但不太规范
int my-cool-weapon;  // ❌ 不能有连字符
int 2damage;         // ❌ 不能数字开头
```

---

## 2. 运算符

### 算术运算符

```csharp
int a = 10 + 5;   // 15 加法
int b = 10 - 3;   // 7  减法
int c = 10 * 2;   // 20 乘法
int d = 10 / 3;   // 3  整数除法（会截断小数！）
float e = 10f / 3; // 3.333... 浮点除法
int f = 10 % 3;    // 1  取余（10除以3余1）
```

**⚠️ 整数除法陷阱**：
```csharp
int result = 10 / 3;    // 结果是 3，不是 3.333
float correct = 10f / 3; // 结果是 3.333...
```

### 比较运算符

```csharp
// 用来比较两个值，返回 true 或 false
5 == 5   // true  等于
5 != 3   // true  不等于
5 > 3    // true  大于
5 < 3    // false 小于
5 >= 5   // true  大于等于
5 <= 3   // false 小于等于
```

**⚠️ 常见错误：== 和 = 搞混**
```csharp
if (damage = 50)  // ❌ 这是赋值，不是比较！
if (damage == 50) // ✅ 这才是比较
```

### 逻辑运算符

```csharp
// && 与：两个都为 true 才是 true
if (player.lifeMaze > 200 && player.manaMaze > 50)
{
    // 玩家生命值>200 且 魔力>50
}

// || 或：只要一个为 true 就是 true
if (npc.type == NPCID.Zombie || npc.type == NPCID.DemonEye)
{
    // 是僵尸 或者 是恶魔眼
}

// ! 非：把 true 变 false，false 变 true
if (!player.dead)
{
    // 玩家没死（不 等于 死）
}
```

### 三元运算符

```csharp
// 简写版的 if/else，适合简单判断
int damage = player.crit ? 50 * 2 : 50;
// 等价于：
// if (player.crit) { damage = 100; }
// else { damage = 50; }
```

---

## 3. 条件判断

### if / else if / else

```csharp
// 最基础的判断
if (player.lifeMaze > 400)
{
    Item.damage = 100;
}
else if (player.lifeMaze > 200)
{
    Item.damage = 75;
}
else
{
    Item.damage = 50;
}
```

### switch（多分支判断）

```csharp
switch (npc.type)
{
    case NPCID.Zombie:
        npc.damage = 15;
        break;
    case NPCID.DemonEye:
        npc.damage = 25;
        break;
    default:
        npc.damage = 10;
        break;
}
```

### 实际例子：右键武器判断

```csharp
// 在 Shoot 钩子里判断玩家是左键还是右键
public override bool Shoot(Player player, EntitySource_ItemUse_WithAmmo ammo,
    Vector2 position, Vector2 velocity, int type, int damage, float knockback)
{
    if (player.altFunctionUse == 2)
    {
        // 右键！发射特殊弹幕
        Projectile.NewProjectile(ammo, position, velocity * 1.5f,
            ModContent.ProjectileType<SpecialBullet>(), damage * 2, knockback);
        return false; // 已手动发射，不再自动发射
    }
    else
    {
        return true; // 让原版逻辑处理
    }
}
```

---

## 4. 循环

### for 循环（最常用）

```csharp
for (int i = 0; i < 10; i++)
{
    Console.WriteLine(i);
}
```

**tModLoader 实际用途：遍历所有 NPC**
```csharp
for (int i = 0; i < Main.maxNPCs; i++)
{
    NPC npc = Main.npc[i];
    if (npc.active && !npc.friendly)
    {
        float distance = Vector2.Distance(player.Center, npc.Center);
        if (distance < 300f)
        {
            // 怪物在300像素范围内
        }
    }
}
```

### foreach（遍历集合）

```csharp
foreach (Item item in player.inventory)
{
    if (item.type == ItemID.Wood)
    {
        // 玩家背包里有木头
    }
}
```

### while（不常用但了解一下）

```csharp
int count = 0;
while (count < 5)
{
    count++;
}
// ⚠️ 小心死循环！
```

---

## 5. 方法（函数）

方法就是**一段可以反复调用的代码**。

### 定义和调用

```csharp
public int CalculateDamage(int baseDamage, bool isCritical)
{
    int result = baseDamage;
    if (isCritical)
    {
        result *= 2; // 暴击伤害翻倍
    }
    return result;
}

int finalDamage = CalculateDamage(50, true); // 100
int normalDamage = CalculateDamage(50, false); // 50
```

### void 方法（没有返回值）

```csharp
public void HealPlayer(Player player, int amount)
{
    player.statLife += amount;
    if (player.statLife > player.statLifeMax2)
    {
        player.statLife = player.statLifeMax2;
    }
}
```

### tModLoader 中的钩子方法

```csharp
// SetDefaults：武器创建时自动调用
public override void SetDefaults()
{
    Item.damage = 50;
    Item.useTime = 20;
    Item.shoot = ProjectileID.PurificationPowder;
}

// Shoot：玩家攻击时自动调用
public override bool Shoot(Player player, ...)
{
    return false; // 已手动发射
}

// AI：弹幕每帧自动调用（每秒60次）
public override void AI()
{
    Projectile.rotation = Projectile.velocity.ToRotation();
}
```

---

## 6. 类和对象

### 类 = 模板，对象 = 实例

```csharp
// 类就像一个"蓝图"
public class Weapon
{
    public string name;
    public int damage;

    public void Attack()
    {
        Console.WriteLine($"{name} 攻击了！造成 {damage} 伤害");
    }
}

// 对象是用蓝图造出来的"实物"
Weapon sword = new Weapon();
sword.name = "火焰剑";
sword.damage = 50;
sword.Attack(); // 输出：火焰剑 攻击了！造成 50 伤害
```

### tModLoader 的类

```csharp
// ModItem 是一个类，你的武器继承它
public class Toy_Knife : ModItem { }

// ModProjectile 是一个类，你的弹幕继承它
public class Toy_Star_Fragments : ModProjectile { }

// Player、NPC、Projectile 也是类
Player player = Main.LocalPlayer;
NPC npc = Main.npc[i];
Projectile proj = Main.projectile[i];
```

---

## 7. 属性（Property）

属性就是**对象的特征**，可以读取也可以修改。

### 常用属性示例

```csharp
// 物品属性
Item.damage = 50;
Item.useTime = 20;
Item.shootSpeed = 12f;
Item.value = Item.sellPrice(gold: 1);

// 弹幕属性
Projectile.position = player.Center;
Projectile.velocity = new Vector2(5, 0);
Projectile.damage = 30;
Projectile.alpha = 128;     // 透明度（0=不透明，255=全透明）
Projectile.scale = 1.5f;

// 玩家属性
player.statLife          // 当前生命值
player.statLifeMax2      // 最大生命值
player.manaCost          // 魔力消耗倍率
player.crit              // 暴击率
player.Center            // 玩家中心位置
```

### 读取 vs 修改

```csharp
// 读取
int currentHealth = player.statLife;

// 修改
player.statLife += 50;

// ⚠️ 某些属性是只读的
// player.Center = new Vector2(0, 0); // ❌ 报错！
```

---

## 8. 常用语法速查

### null 检查

```csharp
NPC target = FindNearestNPC();
if (target != null)
{
    // 找到了目标
}
```

### 数组和列表

```csharp
// 数组：固定大小
int[] damages = new int[3];
damages[0] = 10;

// 列表：可以动态增减
List<int> damageList = new List<int>();
damageList.Add(10);
damageList.Count; // 2
```

### 字符串插值

```csharp
string msg = $"武器伤害是 {Item.damage}，暴击率是 {player.crit}%";
```

### using 语句

```csharp
using (var writer = File.CreateText("log.txt"))
{
    writer.WriteLine("Hello!");
}
// writer 自动关闭
```

---

## 9. 继续学习建议

### 你现在应该掌握的

- ✅ 变量声明和赋值
- ✅ if/else 条件判断
- ✅ for 循环遍历
- ✅ 方法定义和调用
- ✅ 类和对象的概念
- ✅ 属性读取和修改

### 下一步学什么

1. **Vector2 向量**：弹幕速度、方向计算必备
2. **MathHelper**：数学工具，角度转换、数值限制等
3. **Dust 系统**：粒子特效基础
4. **ModItem/ModProjectile 完整钩子**：深入每个钩子的参数和返回值

### 推荐学习方式

- 遇到看不懂的 API → 用 `python Tools/api_lookup.py` 查文档
- 想实现某个效果 → 先搜 ExampleMod 或灾厄源码找类似实现
- 不确定参数含义 → 读官方 XML 文档 + 反射索引

---

*本教程由 T_T 为 Prendeck 编写，2026-09-19*
