# 配置参数

所有可调参数集中定义在代码顶部的常量区，方便修改游戏平衡性。

## 地图

| 常量 | 值 | 说明 |
|------|-----|------|
| TILE | 32 | 瓦片边长（像素） |
| COLS | 26 | 地图列数 |
| ROWS | 26 | 地图行数 |
| W | 832 | 画布宽度（像素） |
| H | 832 | 画布高度（像素） |

## 坦克

| 常量 | 值 | 说明 |
|------|-----|------|
| TANK_SIZE | 28 | 坦克碰撞箱边长（像素） |
| PLAYER_SPEED | 150 | 玩家移动速度（像素/秒） |
| ENEMY_SPEED | 90 | 敌人移动速度（像素/秒） |
| INVINCIBLE_TIME | 2000 | 复活无敌时间（毫秒） |

## 子弹

| 常量 | 值 | 说明 |
|------|-----|------|
| BULLET_SIZE | 6 | 子弹尺寸（像素） |
| BULLET_SPEED | 300 | 子弹速度（像素/秒） |
| MAX_PLAYER_BULLETS | 2 | 玩家同屏子弹上限 |

## 敌人

| 常量 | 值 | 说明 |
|------|-----|------|
| ENEMY_SHOOT_INTERVAL | 1500 | 敌人射击间隔（毫秒） |
| MAX_ENEMIES | 4 | 场上同时存在的敌人上限 |
| TOTAL_ENEMIES | 20 | 需要消灭的敌人总数 |
| RESPAWN_DELAY | 2000 | 敌人生成间隔（毫秒） |

## 道具

| 常量 | 值 | 说明 |
|------|-----|------|
| POWERUP_SIZE | 20 | 道具尺寸（像素） |
| POWERUP_DURATION | 8000 | 道具效果持续时间（毫秒） |
| POWERUP_INTERVAL | 12000 | 地图刷新道具间隔（毫秒） |

## 系统

| 常量 | 值 | 说明 |
|------|-----|------|
| MAX_DT | 50 | 帧时间上限（毫秒），防止跳帧 |
| CLEANUP_INTERVAL | 5000 | 清理死亡敌人间隔（毫秒） |
| SOUND_COOLDOWN.shoot | 80 | 射击音效冷却（毫秒） |
| SOUND_COOLDOWN.hit | 50 | 命中音效冷却（毫秒） |

## 主题 (THEME)

所有视觉颜色集中定义在 `THEME` 对象中，包括：

- `bg` — 背景
- `player` — 玩家坦克（body/track/turret/barrel）
- `enemy` — 敌人坦克（body/track/turret/barrel）
- `bullet` — 子弹颜色（player/enemy）
- `brick` — 砖墙（main/dark/border）
- `steel` — 钢墙（frame/mid/highlight）
- `water` — 水面（base/wave）
- `base` — 基地（main/inner）
- `hud` — HUD（color/shadow）
- `explosion` — 爆炸颜色数组（白→橙→红）
