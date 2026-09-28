# tModLoader 武器开发入门教程

> 从零开始，一步步教你写泰拉瑞亚模组武器。每个钩子都有参数解释和返回值说明。

---

## 目录

1. [项目结构概览](#1-项目结构概览)
2. [第一个武器：最简单的剑](#2-第一个武器最简单的剑)
3. [Shoot 钩子详解](#3-shoot-钩子详解)
4. [右键副模式武器](#4-右键副模式武器)
5. [自定义魔力消耗（进阶）](#5-自定义魔力消耗进阶)
6. [常见武器类型模板](#6-常见武器类型模板)
7. [调试技巧](#7-调试技巧)

---

## 1. 项目结构概览

### 文件组织

```
Content/Items/Weapons/
├── Melee/        ← 近战武器（剑、矛、回旋镖）
├── Ranged/       ← 远程武器（枪、弓、火箭）
├── Magic/        ← 魔法武器（法杖、魔法书）
└── Summon/       ← 召唤武器（召唤杖）
```

### 文件命名规范

**文件名必须等于类名**，这是 tModLoader 的硬性要求：

```
火焰剑.cs          → 类名必须是 火焰剑
Shadow_Guny.cs     → 类名必须是 Shadow_Guny
Toy_Knife.cs       → 类名必须是 Toy_Knife
```

### Localization 配置

武器创建后，需要在 `Localization/zh-Hans_Mods.PrendeckOddments.hjson` 里添加本地化：

```hjson
Mods.PrendeckOddments.Items.Weapons.Melee.火焰剑.DisplayName: "火焰剑"
Mods.PrendeckOddments.Items.Weapons.Melee.火焰剑.Tooltip: "燃烧的利刃"
```

---

## 2. 第一个武器：最简单的剑

### 完整代码

```csharp
using Terraria;
using Terraria.ID;
using Terraria.ModLoader;

namespace PrendeckOddments.Content.Items.Weapons.Melee
{
    public class 火焰剑 : ModItem
    {
        public override void SetDefaults()
        {
            Item.damage = 50;
            Item.DamageType = DamageClass.Melee;
            Item.width = 40;
            Item.height = 40;
            Item.useTime = 20;
            Item.useAnimation = 20;
            Item.useStyle = ItemUseStyleID.Swing;
            Item.shoot = ProjectileID.None;
            Item.shootSpeed = 0f;
            Item.knockBack = 6f;
            Item.value = Item.sellPrice(gold: 1);
            Item.rare = ItemRarityID.Orange;
            Item.UseSound = SoundID.Item1;
        }
    }
}
```

### 逐行解释

```csharp
Item.damage = 50;
// 武器每次攻击造成50点伤害

Item.useTime = 20;
// 使用一次需要20帧（约0.33秒），越小=攻速越快

Item.value = Item.sellPrice(gold: 1);
// sellPrice 是卖价（商人收购价）
// buyPrice 是买价（商人出售价），sellPrice 的5倍
// ⚠️ 常见错误：连续两行 Item.value = ...，后者覆盖前者
```

### Item.value 陷阱

```csharp
// ❌ 错误：连续两行赋值
Item.value = Item.buyPrice(gold: 1);   // 被覆盖！
Item.value = Item.sellPrice(gold: 1);  // 只有这行生效

// ✅ 正确：只写一行
Item.value = Item.sellPrice(gold: 1);
```

---

## 3. Shoot 钩子详解

### 参数说明

```csharp
public override bool Shoot(
    Player player,                          // 使用武器的玩家
    EntitySource_ItemUse_WithAmmo ammo,     // 弹药来源信息
    Vector2 position,                       // 弹幕发射位置（鼠标位置）
    Vector2 velocity,                       // 弹幕初始速度
    int type,                               // 弹幕类型
    int damage,                             // 弹幕伤害
    float knockback                         // 击退力
)
```

### 返回值含义

```
return true  → 允许原版自动发射弹幕
return false → 你已经手动发射了，原版不要再射了
```

### 实际例子：发射多个弹幕

```csharp
public override bool Shoot(Player player, EntitySource_ItemUse_WithAmmo ammo,
    Vector2 position, Vector2 velocity, int type, int damage, float knockback)
{
    for (int i = 0; i < 3; i++)
    {
        Vector2 newVelocity = velocity.RotatedBy(MathHelper.ToRadians(-10 + i * 10));
        Projectile.NewProjectile(ammo, position, newVelocity, type, damage, knockback, player.whoAmI);
    }
    return false; // 已手动发射
}
```

---

## 4. 右键副模式武器

### 实现步骤

**第一步：启用右键**

```csharp
public override void SetDefaults()
{
    Item.altUse = true; // 启用右键功能
}
```

**第二步：在 Shoot 里判断**

```csharp
public override bool Shoot(Player player, ...)
{
    if (player.altFunctionUse == 2)
    {
        // 右键模式
        Projectile.NewProjectile(..., damage * 2, ...);
        return false;
    }
    else
    {
        // 左键模式
        return true;
    }
}
```

---

## 5. 自定义魔力消耗（进阶）

```csharp
// 近战武器消耗魔力强化攻击
public override void SetDefaults()
{
    Item.damage = 50;
    Item.mana = 10; // 消耗10点魔力
}

public override bool Shoot(Player player, ...)
{
    // 每攻击3次发射一次特殊弹幕
    player.GetModPlayer<MyPlayer>().swingCount++;
    if (player.GetModPlayer<MyPlayer>().swingCount >= 3)
    {
        Projectile.NewProjectile(...);
        player.GetModPlayer<MyPlayer>().swingCount = 0;
    }
    return false;
}
```

---

## 6. 常见武器类型模板

### 近战剑

```csharp
public override void SetDefaults()
{
    Item.damage = 50;
    Item.DamageType = DamageClass.Melee;
    Item.useTime = 20;
    Item.useAnimation = 20;
    Item.useStyle = ItemUseStyleID.Swing;
    Item.knockBack = 6f;
    Item.value = Item.sellPrice(gold: 1);
    Item.UseSound = SoundID.Item1;
}
```

### 远程枪

```csharp
public override void SetDefaults()
{
    Item.damage = 35;
    Item.DamageType = DamageClass.Ranged;
    Item.useTime = 8;
    Item.useAnimation = 8;
    Item.useStyle = ItemUseStyleID.Shoot;
    Item.shoot = ProjectileID.Bullet;
    Item.shootSpeed = 16f;
    Item.useAmmo = AmmoID.Bullet;
    Item.value = Item.sellPrice(gold: 2);
    Item.UseSound = SoundID.Item11;
}
```

### 魔法武器

```csharp
public override void SetDefaults()
{
    Item.damage = 45;
    Item.DamageType = DamageClass.Magic;
    Item.useTime = 15;
    Item.useAnimation = 15;
    Item.useStyle = ItemUseStyleID.Shoot;
    Item.shoot = ProjectileID.MagicMissile;
    Item.shootSpeed = 12f;
    Item.mana = 10;
    Item.value = Item.sellPrice(gold: 2);
    Item.UseSound = SoundID.Item20;
}
```

### 召唤武器

```csharp
public override void SetDefaults()
{
    Item.damage = 25;
    Item.DamageType = DamageClass.Summon;
    Item.useTime = 30;
    Item.useAnimation = 30;
    Item.useStyle = ItemUseStyleID.Swing;
    Item.shoot = ModContent.ProjectileType<MyMinion>();
    Item.buff = ModContent.BuffType<MyMinionBuff>();
    Item.mana = 20;
    Item.value = Item.sellPrice(gold: 1);
    Item.UseSound = SoundID.Item44;
}
```

---

## 7. 调试技巧

### 打印调试信息

```csharp
Mod.Logger.Info("弹幕ID是：" + type);
Mod.Logger.Info("伤害是：" + damage);
```

### 常见错误

| 错误现象 | 可能原因 | 解决方法 |
|---------|---------|---------|
| 武器不出现在物品栏 | 文件名和类名不一致 | 检查命名 |
| 武器没有贴图 | 贴图文件名不对 | 贴图名要和类名一致 |
| 弹幕不发射 | 没设 Item.shoot | 在 SetDefaults 里设置 |
| 射速奇怪 | useTime 和 useAnimation 不一致 | 通常设成一样的 |

---

*本教程由 T_T 为 Prendeck 编写，2026-09-19*
