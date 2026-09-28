# tModLoader 常见特效实现参考手册

> 整理了常见的视觉特效实现方式，每种特效都有可复制的代码示例。

---

## 目录

1. Dust 粒子系统基础
2. 常见粒子效果模板
3. 光照和颜色
4. 屏幕效果
5. 弹幕视觉效果
6. 武器挥舞效果
7. 简单 Shader 效果（入门）
8. 性能注意事项

---

## 1. Dust 粒子系统基础

### NewDust vs NewDustPerfect

NewDust：在区域内随机生成粒子
int dustIndex = Dust.NewDust(position, width, height, DustID.Fire);

NewDustPerfect：在精确位置生成一个粒子
Dust dust = Dust.NewDustPerfect(position, DustID.Fire);

### Dust 常用属性

dust.noGravity = true;     // 无重力
dust.velocity = new Vector2(3, 0); // 速度
dust.scale = 1.5f;         // 大小
dust.alpha = 128;          // 透明度（0=不透明，255=全透明）
dust.rotation = 0.5f;      // 旋转角度
dust.fadeIn = 0f;          // 淡入效果
dust.color = new Color(100, 200, 255); // 自定义颜色

### 发光粒子示例

for (int i = 0; i < 8; i++)
{
    Vector2 velocity = (MathHelper.TwoPi * i / 8f).ToRotationVector2() * 3f;
    Dust dust = Dust.NewDustPerfect(Projectile.Center, DustID.IceTorch);
    dust.velocity = velocity;
    dust.noGravity = true;
    dust.scale = 1.2f;
    dust.color = new Color(100, 180, 255);
}

---

## 2. 常见粒子效果模板

### 拖尾效果（弹幕飞行时留下尾迹）

Dust dust = Dust.NewDustPerfect(Projectile.oldPos[0], DustID.MagicMirror);
dust.noGravity = true;
dust.scale = 0.8f;
dust.alpha = 100;

### 爆发效果（命中/死亡时）

for (int i = 0; i < 20; i++)
{
    Vector2 velocity = Main.rand.NextVector2Circular(8f, 8f);
    Dust dust = Dust.NewDustPerfect(Projectile.Center, DustID.Torch);
    dust.velocity = velocity;
    dust.noGravity = false;
    dust.scale = Main.rand.NextFloat(0.8f, 1.5f);
    dust.color = Main.hslToRgb(Main.rand.NextFloat(), 1f, 0.6f);
}

### 环绕效果（粒子绕着目标旋转）

float angle = Projectile.ai[0] / 30f * MathHelper.TwoPi;
Vector2 offset = angle.ToRotationVector2() * 50f;
Dust dust = Dust.NewDustPerfect(Projectile.Center + offset, DustID.Shadowflame);
dust.noGravity = true;
dust.scale = 1f;
Projectile.ai[0] += 1f;

### 下雨/飘雪效果

if (Main.rand.NextBool(3))
{
    Dust dust = Dust.NewDust(new Vector2(Main.screenPosition.X, Main.screenPosition.Y - 10),
        Main.screenWidth, 10, DustID.Snow);
    dust.velocity = new Vector2(Main.rand.NextFloat(-2f, 2f), Main.rand.NextFloat(5f, 10f));
    dust.scale = 0.8f;
}

---

## 3. 光照和颜色

### 基础光照

Lighting.AddLight(Projectile.Center, 0.5f, 0.7f, 1.0f);

### 颜色渐变（Lerp）

float progress = Projectile.timeLeft / 60f;
Color color = Color.Lerp(Color.Red, Color.Blue, progress);
Dust dust = Dust.NewDustPerfect(Projectile.Center, DustID.MagicMirror);
dust.color = color;

### Glow Mask（发光贴图）

贴图文件名：YourItem_Glow.png
用 ModContent.Request<Texture2D> 加载

---

## 4. 屏幕效果

### 简单屏幕震动（思路）

通过修改 Main.screenPosition 偏移实现
注意：不要让玩家晕，震动幅度要小

常见实现：
Main.screenPosition.X += Main.rand.Next(-2, 3);
Main.screenPosition.Y += Main.rand.Next(-2, 3);

### 安全注意事项

- 震动幅度：±3 像素以内
- 持续时间：10~30 帧
- 不要在玩家死亡时触发剧烈震动

---

## 5. 弹幕视觉效果

### 透明度变化（淡入淡出）

// 淡入
Projectile.alpha = (int)MathHelper.Lerp(255f, 0f, Projectile.timeLeft / 30f);

// 淡出
Projectile.alpha = (int)MathHelper.Lerp(0f, 255f, Projectile.timeLeft / 30f);

### 缩放变化

// 从小变大
Projectile.scale = MathHelper.Lerp(0.5f, 1.5f, 1f - Projectile.timeLeft / 60f);

// 呼吸效果
Projectile.scale = 1f + (float)Math.Sin(Projectile.ai[0] * 0.1f) * 0.2f;

### 旋转效果

// 跟随速度方向
Projectile.rotation = Projectile.velocity.ToRotation();

// 自动旋转
Projectile.rotation += 0.1f;

### 残影效果（思路）

在 AI() 里记录历史位置到 Projectile.oldPos
然后在 Draw 里画旧位置的半透明版本

---

## 6. 武器挥舞效果

### Held Projectile（手持弹幕）

在 ModItem 的 HoldItem 里创建手持弹幕：
if (player.ownedProjectileCounts[ModContent.ProjectileType<HeldSword>()] < 1)
{
    Projectile.NewProjectile(..., ModContent.ProjectileType<HeldSword>(), ...);
}

### 刀光/剑气效果

在弹幕 AI 里生成挥舞粒子：
float progress = Projectile.ai[0] / 30f;
Vector2 offset = (Projectile.rotation + MathHelper.PiOver4).ToRotationVector2() * 40f;
Dust dust = Dust.NewDustPerfect(player.Center + offset, DustID.IceTorch);
dust.noGravity = true;
dust.scale = 1.5f;

---

## 7. 简单 Shader 效果（入门）

### 什么是 Shader

Shader 就是运行在显卡上的小程序，可以做普通代码做不了的视觉效果。

### tModLoader 里 Shader 的基本用法

在 Effects/ 文件夹下放 .fx 文件
Effect myShader = ModContent.Request<Effect>("PrendeckOddments/Effects/MyShader").Value;

在 Draw 里使用：
myShader.Parameters["uTime"].SetValue(Main.GlobalTime);
myShader.CurrentTechnique.Passes[0].Apply();
Main.EntitySpriteDraw(...);

### 简单的变色效果（不用 Shader）

Color color = Main.hslToRgb((Projectile.ai[0] / 60f) % 1f, 1f, 0.6f);
Main.EntitySpriteDraw(texture, position, rectangle, color, rotation, origin, scale, SpriteEffects.None, 0f);

### 参考资源

- ExampleMod 的 Effects 文件夹
- tModLoader 官方文档的 Shader 部分
- 灾厄的 Effects 文件夹

---

## 8. 性能注意事项

### 粒子数量控制

// ❌ 一次生成太多粒子会卡
for (int i = 0; i < 100; i++) { Dust.NewDust(...); }

// ✅ 分散到多帧生成
if (Main.rand.NextBool(3)) { Dust.NewDust(...); }

### Dust vs Projectile

视觉效果 → 用 Dust（推荐）
碰撞检测 → 必须用 Projectile
伤害判定 → 必须用 Projectile
持续时间短 → 用 Dust
持续时间长 → 用 Projectile

### 帧跳过优化

// 大型 Boss 战时跳过一半粒子
if (Main.rand.NextBool(2))
{
    Dust.NewDust(...);
}

---

*本教程由 T_T 为 Prendeck 编写，2026-09-19*
