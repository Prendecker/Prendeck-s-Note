# Geometry 几何学 —— tModLoader 官方 Wiki 中文翻译

> 原文：[https://github.com/tModLoader/tModLoader/wiki/Geometry](https://github.com/tModLoader/tModLoader/wiki/Geometry) （JavidPack 编辑，2024-03-14）
> 翻译说明：原文中的演示视频（.mp4）无法搬运，文中会标注 📹 原文视频位置；代码注释一并译成中文。

---

## 为什么要学几何

模组作者想实现的许多视觉上有趣的效果和行为，都需要一点点几何知识。本教程会讲解几何在 tModLoader 模组制作中最基础的用法。

比如：让尘埃或弹幕呈弧线散开、让敌人朝玩家开枪、编写追踪行为——这些全都用到几何。在讲完基础之后，本教程的后半部分会给出这些概念的实例。

## 前置知识

### 几何素养

作为一名程序员，尤其是对电子游戏有兴趣的程序员，几何是必不可少的技能。泰拉瑞亚是个 2D 游戏，所需的几何知识并不深，但**熟悉向量的基础用法是必须的**。

### 坐标

泰拉瑞亚使用好几套坐标系，如果你没有图形编程经验，X 和 Y 的方向可能会让你吃惊。请参阅 [Coordinates 坐标](https://github.com/tModLoader/tModLoader/wiki/Coordinates) 页面，熟悉世界坐标以及 X、Y 正方向的指向。

/

### 旋转

旋转用**弧度**表示，不是角度。如果你想要用角度，调用 `MathHelper.ToRadians` 方法即可。通常你只在"初始声明某个行为"时才用角度，比如声明"这把武器将以 30 度的扇形弧发射"。另外注意：**旋转 0 = 朝向右方**；旋转 90 度会指向正下方，因为 Y 轴向下。

---

## Vector2

`Vector2` 是一个结构体（struct），表示几何课上学的二维向量。一个 `Vector2` 包含 `X` 和 `Y` 两个字段，分别代表该二维向量在 X、Y 方向上的分量大小。

在 tModLoader 中，Vector2 有两个主要用途：

1. **位置**：`Player`、`Projectile`、`Dust`、`NPC` 等大量游戏元素的位置都用 `Vector2` 表示。
2. **速度（velocity）**：速度就是物体在 X 和 Y 两个方向上分别移动的快慢。

举个例子：如果玩家位置是 `(3, 7)`，速度是 `(4, 8)`，那么每次游戏更新位置时，玩家位置都会加上速度。这个例子中，更新 1 次后，玩家新位置是 `(7, 15)`，因为 `3 + 4 = 7`、`7 + 8 = 15`。可以看出，**向量相加就是对应分量分别相加**。

如果向量 A 代表位置，向量 B 代表速度，那么 X 个时间单位之后，新位置 = `A + X * B`。

📹 原文有一段演示视频（Slowmo.Velocity.Demonstration.mp4），展示了泰拉瑞亚坐标系下的这个概念——注意每个 tick 玩家位置的改变量恰好等于其速度。记住：**游戏每秒运行 60 次更新，所以速度的单位是"世界单位 / 每次更新"，不是"世界单位 / 每秒"**。

### 用向量表示"两点之差"

我们也可以用向量表示两个点之间的差。最常见的例子就是**敌人朝玩家开枪**：要让敌人射向玩家，代码需要知道射击方向。用 `npc.position` 减去 `player.position` 就能算出这个方向。

向量减法和加法一样简单：X 分量和 X 分量相减，Y 分量和 Y 分量相减。**从 A 指向 B 的向量 = `B - A**`。

想象一个敌人在 `(14, 4)`，玩家在 `(3, 12)`。用玩家位置减去敌人位置，得到 `(-11, 8)`。

⚠️ 在代码里我们**不能直接用这个向量**——它代表的是"位置的原始差值"，不是一个方向。想把它变成方向、进而用来生成弹幕，请继续看下面的 `Vector2.Normalize` 一节。

📹 原文图示展示了从敌人指向玩家的结果向量。

### Position vs Center（位置 vs 中心）

在上面的图示里你可能注意到，箭头的起点和终点都在实体的**左上角**。实际上 `Player.position` 指的确实就是左上角——游戏就是这么设计的。

这意味着：**代码里我们很少直接用 `Player.position**`，而是用 `Player.Center`，因为它指向实体的中心（所有实体都可以看作一个矩形碰撞箱）。`NPC.Center`、`Projectile.Center` 同理。

**从现在起，本教程一律使用 `.Center**`，因为这个位置更合理。

---

## 加速度（Acceleration）

游戏更新弹幕位置时，做的事很简单：拿当前速度加到当前位置上。每秒 60 次，在世界坐标系中进行。

对子弹这种弹幕来说这就够了，但我们还可以实现"**加速度**"——随时间持续影响速度，让弹幕走出有趣的轨迹。加速度通常写在各种 `AI` 方法和碰撞方法里，可以用来模拟**重力、空气阻力、追踪能力**。

### 重力

重力的模拟方式：每次更新给实体加一个**向下的（正 Y）速度**。

- 玩家：游戏默认就实现了重力
- NPC：`NPC.noGravity` 为 false 时受重力影响
- Dust：也有 `noGravity` 字段
- 弹幕：**不受重力影响**——想让弹幕受重力，必须自己在 `ModProjectile.AI` 里加

细节请看 [Basic Projectile 基础弹幕](https://github.com/tModLoader/tModLoader/wiki/Basic-Projectile#gravity) 教程的重力章节。

```csharp
Projectile.velocity.Y = Projectile.velocity.Y + 0.1f;
```

### 阻力 / 空气阻力

模拟空气阻力请看 [Basic Projectile](https://github.com/tModLoader/tModLoader/wiki/Basic-Projectile#wind-resistance) 教程。本质上就是：**把速度的某个分量乘以一个略小于 1 的数**，让它慢慢减小。

### 追踪（Homing）

最简形式的追踪，基本上就是"朝目标持续加速"。见 [Basic Projectile](https://github.com/tModLoader/tModLoader/wiki/Basic-Projectile#homing)。

### 碰撞与反弹

弹幕碰到实体方块时，速度瞬间反向，从而实现弹跳。详见 [Basic Projectile](https://github.com/tModLoader/tModLoader/wiki/Basic-Projectile#bounce-and-ontilecollide)。

### 加速度可视化示例

📹 原文有段视频（Acceleration.Visualization.Example.mp4）总结了上面大部分内容：

- **红色箭头 = 速度**，**蓝色箭头 = 加速度（受力）**
- 在飞镖（Shuriken）的例子中，加速度力略微指向左下方：向左的力来自空气阻力，向下的力来自重力
- 值得注意的是：飞镖刚生成后的 1/3 秒内**不受任何力**——这通过计时器实现（见 [delayed gravity 延迟重力](https://github.com/tModLoader/tModLoader/wiki/Basic-Projectile#delayed-gravity) 章节），让飞镖的运动更有趣
- 手雷没有空气阻力，所以只看到重力
- 手雷撞到方块的瞬间出现一个很大的力——这就是让速度反向的**碰撞力**

---

## Vector2.Normalize（向量归一化）

处理向量时，大多数时候我们**不关心向量的长度，只关心它指向的方向**。

想象：一个玩家距离敌人 100 单位，另一个玩家在同一方向上距离 1000 单位。分别计算"敌人 → 两个玩家"的向量，它们指向同一方向，但后者长 10 倍。

如果直接拿这两个向量去 `AI` 里生成弹幕射向玩家，**第二发弹幕会快 10 倍**！我们不想要这样——敌人的弹幕速度应该和玩家远近无关，保持恒定。

> 括号注：现在我们设想的是子弹类弹幕。如果你的敌人扔的是手雷之类抛物线道具，那确实要把距离考虑进去（直到敌人的最大投掷速度），但那种进阶 AI 不是这里要讲的。

**解决办法：把向量"归一化"（Normalize）。** 归一化就是把向量**缩放到长度为 1**，得到的结果叫**单位向量（Unit Vector）**。

你可以用学校学的勾股定理自己算，但幸运的是 `Vector2` 自带这个功能。不过——**不要直接用普通的 `Normalize` 方法**，因为它有可能除以零、把游戏搞崩。我们用这个方法：

```csharp
// 这段代码一般写在 ModNPC.AI 方法里
// 注意：player 在此之前已经通过某种方式定义好了，
// 很可能是 NPC.TargetClosest(); 加 Player player = Main.player[NPC.target];

// 第一步：用两个位置相减，算出"从 npc 指向玩家"的向量
// （从 A 指向 B 的向量 = B - A）
Vector2 vectorFromNpcToPlayer = player.Center - NPC.Center;

// 第二步：调用 SafeNormalize 把向量缩放到长度 1（即单位向量），
// 结果是一个"只代表方向"的向量
Vector2 directionFromNpcToPlayer = vectorFromNpcToPlayer.SafeNormalize(Vector2.UnitX);

// 第三步：给 npc 一个预设的射击速度。具体数值需要自己多试。
float shootVelocity = 10;

// 最后：用方向 × 速度生成弹幕
Projectile.NewProjectile(source, NPC.Center, directionFromNpcToPlayer * shootVelocity,
    ProjectileID.BombSkeletronPrime, 5, 0, Main.myPlayer);
```

---

## Vector2.ToRotation（向量转旋转角）

给定一个 Vector2（归一化与否都行），调用它的 `ToRotation` 方法可以算出一个旋转值。

很多飞行敌人会旋转着朝向目标，比如恶魔之眼（Demon Eye）。你可以用"敌人 → 玩家"的向量设置敌人旋转角，也可以用敌人当前速度来设置 `NPC.rotation`。

进阶情况：你可能想让 NPC **慢慢转过去**，而不是瞬间转到面向玩家。

```csharp
// 第一步：算出指向"你想看的东西"的向量
Vector2 vectorFromNpcToPlayer = player.Center - NPC.Center;

// 第二步：用 ToRotation 把 Vector2 变成 float（弧度制旋转角）
float desiredRotation = vectorFromNpcToPlayer.ToRotation();

// 第三步：两种做法选一个
// 做法一（最简单）：直接用这个旋转值
NPC.rotation = desiredRotation;

// 做法二：用它让 npc 在"最大转速限制"下慢慢转向目标。数值需要实验。
NPC.rotation = NPC.rotation.AngleTowards(desiredRotation, 0.02f);
```

---

## 向量乘法（Multiplying Vectors）

向量可以直接乘一个 float 来缩放。我们通常缩放的是归一化后的向量，就像上面 `Vector2.Normalize` 的例子：单位向量代表射击方向，乘上预设射击速度后，方向不变、长度变长。由于这个 `Vector2` 被用在 `Projectile.NewProjectile` 的 `velocity` 参数上，结果就是**弹幕以我们想要的速度、朝我们想要的方向生成**。

向量乘法也有别的用处。比如 [ExampleAdvancedFlailProjectile.cs](https://github.com/tModLoader/tModLoader/blob/stable/ExampleMod/Content/Projectiles/ExampleAdvancedFlailProjectile.cs#L328) 里，把弹幕速度乘以 `0.2f` 或 `0.4f`（`bounceFactor` 变量），等于把速度砍到原来的一小部分——这让链球类武器撞到方块反弹时有"沉重感"。

---

## Vector2 长度（Length）

不用掏勾股定理，直接调方法就能算出向量长度。这在很多场合都很有用。

例子：**敌人在玩家进入特定范围之前不开火**。检查"敌人 → 玩家"向量的长度，就能决定要不要生成弹幕。

```csharp
// 方法一：用 Vector2 的 Length 方法
Vector2 vectorFromNpcToPlayer = player.Center - NPC.Center;
float distanceBetweenPlayerAndNpc = vectorFromNpcToPlayer.Length();

// 方法二：用 Vector2.Distance 静态方法，直接算两个点的距离
float distanceBetweenPlayerAndNpc = Vector2.Distance(player.Center, NPC.Center);

// 然后在逻辑里用这个值
if (distanceBetweenPlayerAndNpc < 300) {
    // 玩家进入范围了，在这里生成弹幕
}
```

### 长度平方（Length Squared）

如果你在做**计算量大**的操作——比如遍历一大堆实体找最近的那个——要知道：用长度平方的方法效率更高。这种场合可以用 `Vector2.DistanceSquared` 或 `Vector2.LengthSquared`（因为开平方根比较费）。

---

## Vector2 旋转（Rotation）

旋转一个向量有很多用途。常见例子：**给武器加散布（不精准）**。

对原来的 `Vector2` 调用 `RotatedByRandom` 方法，可以算出一个"最多旋转指定弧度"的新 `Vector2`。实例见 [ExampleShotgun.cs](https://github.com/tModLoader/tModLoader/blob/stable/ExampleMod/Content/Items/Weapons/ExampleShotgun.cs#L38)。注意：它的随机分布**不是均匀的**，不过对这个效果来说刚刚好。

也可以按固定角度旋转——用 `RotatedBy` 方法。比如把一个向量旋转 `MathHelper.Pi / 2`（即 `MathHelper.ToRadians(90)`），就得到一个与原向量**垂直**的向量，可以用它做"分裂弹幕"。反复旋转一个向量，就能算出表示**一段弧线**的几个向量，实例见 [ExampleGun.cs](https://github.com/tModLoader/tModLoader/blob/stable/ExampleMod/Content/Items/Weapons/ExampleGun.cs#L79) 的吸血鬼飞刀例子。

```csharp
// Others?（原文此处代码缺失）
```

---

## 随机向量（Random Vectors）

用随机向量是给视觉效果和行为增加变化的简单办法。生成随机向量的方法有很多，下面几种方案都配有"分布示意图 + 游戏内生成若干 Dust 的实例演示"。

### 1. 圆内随机向量（Random Vector Within Circle）

模组作者最常用的方案，**分布均匀**。

```csharp
// 常规方案
Vector2 speed = Main.rand.NextVector2Circular(1f, 1f);

// 只在一段弧内生成向量
Vector2 speed = Main.rand.NextVector2Unit((float)MathHelper.Pi / 4, (float)MathHelper.Pi / 2) * Main.rand.NextFloat();

// NextVector2Circular 可以分别提供宽度和高度半径，生成椭圆分布
Vector2 speed = Main.rand.NextVector2Circular(0.5f, 1f);
```

📹 原文视频：Circular.mp4 / Arc.mp4 / Oval.mp4

### 2. 圆边随机向量（Along Circle Edge）

生成**到达圆边缘**的随机向量，也就是长度恒定（模长一致）的随机方向向量。

```csharp
// 常规方案
Vector2 speed = Main.rand.NextVector2Unit();

// 可选参数可以指定旋转范围。例：起始旋转为 Pi/4，最多再偏 Pi/2。
Vector2 speed = Main.rand.NextVector2Unit((float)MathHelper.Pi / 4, (float)MathHelper.Pi / 2);
```

📹 原文视频：Circle.Edge.mp4 / Circle.Edge.Arc.mp4

### 3. 正方形内随机向量（Within Square）

很多泰拉瑞亚老代码用一种奇怪的方式做随机向量——X、Y 各自独立随机：

```csharp
float xSpeed = Main.rand.NextFloat(-1f, 1f);
float ySpeed = Main.rand.NextFloat(-1f, 1f);

// 另一种写法
Vector2 speed = Utils.RandomVector2(Main.rand, -1f, 1f);
```

乍看没问题，但这种分布**很奇怪，可能不是你想要的**：它会生成比预期更长的向量，朝一个假想正方形的四个角延伸。看下面的图和视频，注意那个奇怪的形状。

📹 原文视频：Random.Within.Square.mp4

### 4. 正方形边随机向量（Square Edge）

不太有用。（原文原话：Not very useful.）

---

## 实例（Examples）

有了几何基础，也见识了各种 `Vector2` 方法，我们终于可以在模组里编出有趣的行为啦。

下面的例子用 Dust 或弹幕来演示，但两者是**可以互换**的——只要查清楚你调用的方法签名里每个参数是干嘛的就行。

### 例 1：随机爆发 / 圆环

这就是上面"随机向量"一节用的代码。用 **for 循环**生成 50 个 Dust，每个都带一个"沿圆边的随机向量"。注意向量乘了 5 来放大，让 Dust 飞出一段距离。

```csharp
for (int i = 0; i < 50; i++) {
    Vector2 speed = Main.rand.NextVector2CircularEdge(1f, 1f);
    Dust d = Dust.NewDustPerfect(Main.LocalPlayer.Top, DustID.BlueCrystalShard, speed * 5, Scale: 1.5f);
    d.noGravity = true;
}
```

再用一点简单的几何，把生成位置也散开：给 `Main.LocalPlayer.Top` 加上 `speed * 32`，Dust 就会先分布在一个小圆里再向外扩散，而不是全从同一点出发。

```csharp
Dust d = Dust.NewDustPerfect(Main.LocalPlayer.Top + speed * 32, DustID.BlueCrystalShard, speed * 2, Scale: 1.5f);
```

（这里速度调小了，方便看清效果。）

📹 原文视频：Circle.Burst.mp4

### 例 2：射向目标

[ExampleWormHead](https://github.com/tModLoader/tModLoader/blob/stable/ExampleMod/Content/NPCs/ExampleWorm.cs#L73) 展示了"敌人朝玩家开枪"的基本模式。

要点：**算出"从源头到目标"的向量 → 归一化 → 乘以射击速度**。并且要像示例里那样，确认攻击冷却、距离、视线检查都通过了才执行这段代码。

```csharp
// 朝目标射击的几何：
Vector2 direction = (target.Center - NPC.Center).SafeNormalize(Vector2.UnitX); // 指向目标的单位向量
Vector2 velocity = direction * 7f; // 射击速度
Projectile.NewProjectile(..., velocity, ...); // 把它用在 NewProjectile 的合适位置
```

### 例 3：朝向目标（贴图转身）

可以用 [Vector2.ToRotation](https://github.com/tModLoader/tModLoader/wiki/Geometry#vector2torotation) 让实体面向目标。

- 如果你的贴图**不是朝右画的**，可能需要额外加 `MathHelper.Pi / 2`（再转 90 度）
- 注意：弹幕或 NPC 朝左时有时会**翻转贴图**，这是通过 `spriteDirection` 这个 bool 实现的。如果该 bool 为 true，你可能需要再加 180 度补偿，即加上 `MathHelper.Pi`

```csharp
// 放在 ModProjectile.AI 的末尾
if (Projectile.spriteDirection == -1) {
    Projectile.rotation += MathHelper.Pi;
}
```

> 原文 TODO：解释哪些部分是自动完成的、各种 direction / spriteDirection 代码在弹幕和 NPC 里各该放哪。（官方自己也没写完 xD）

---

## 深入学习（Learn More）

掌握本教程后，学习碰撞（collision）会很有帮助。

> 原文 TODO：制作碰撞教程。（还是没写）

---

---

# 📝 Prendeck 的课后作业

> 结合你的进度（循环 → Dust → 弹幕 AI）设计的，每题 5–10 分钟量级，答案不用交给我，但写完了欢迎拿给我检查～
> 都在你自己的模组 `PrendeckOddments` 里做，不许直接抄上面的原题！

### 作业 1（循环 + Dust，热身）：甜甜圈爆发

写一个方法：在玩家位置生成 **3 圈** Dust，最内圈半径 16、中间 32、最外 48（用循环嵌套或一个循环里算半径都行），每圈 20 个，速度方向用 `NextVector2CircularEdge`。
✅ 检查点：三层圈要肉眼可见地分开，而不是糊成一团。

### 作业 2（向量减法 + 归一化）：谁离我最近？

写一段 AI 逻辑：NPC 每次更新时算出自己与玩家的距离，**小于 200 时才朝玩家发射弹幕**，发射用 `(player.Center - NPC.Center).SafeNormalize(Vector2.UnitX) * 8f`。
✅ 检查点：玩家离远了它就哑火，走近了才打你。
🤔 思考题：为什么必须用 `SafeNormalize` 而不是 `Normalize`？什么情况下会崩？

### 作业 3（速度 × 时间 + 循环）：你算得对吗？

泰君位置 `(100, 200)`，速度 `(2.5f, -1.5f)`，游戏跑了多少次更新后位置是 `(150, 170)`？
✅ 要求：**用代码验证你的答案**（写个循环累加，数一下跑了几 tick）——这正是"位置 += 速度"的逆向工程。
🤔 思考题：为什么答案是"多少 tick"而不是"多少秒"？怎么换算成秒？

### 作业 4（综合小设计，可分两天）：霰弹扇形

做一把武器（或临时测试弹），一次发射 **7 发弹幕**，形成 ±15 度的扇形：

- 用 `for` 循环
- 基准方向 × `RotatedBy(MathHelper.ToRadians(-15 + i * 5))` 之类的方式算出每发的方向
- 每发再加一点点 `RotatedByRandom` 随机散布
✅ 检查点：扇形要对称、密集均匀；把随机散布调成 0 再看一眼，确认扇形骨架是对的。

### 挑战题（选做）：重力手雷

让一个弹幕在 `AI` 里每 tick 执行 `velocity.Y += 0.1f`，再叠加一个 `velocity *= 0.98f` 的阻力，观察轨迹。
🤔 思考题：把 0.1f 改成 0.3f、把 0.98f 改成 0.9f，轨迹分别怎么变？哪个更像"石头"，哪个更像"羽毛"？

```

```

&nbsp;