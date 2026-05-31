# 音效系统

## 概述

游戏使用 Web Audio API 实时合成音效，无需加载任何音频文件。所有音效通过振荡器（OscillatorNode）+ 增益节点（GainNode）生成。

## 音效类型

| 类型 | 波形 | 频率范围 | 时长 | 触发场景 |
|------|------|----------|------|----------|
| shoot | 方波 (square) | 600→200 Hz | 100ms | 玩家/敌人射击 |
| explode | 锯齿波 (sawtooth) | 150→40 Hz | 350ms | 坦克被摧毁 |
| hit | 三角波 (triangle) | 800→300 Hz | 60ms | 子弹命中墙壁 |
| powerup | 正弦波 (sine) | 500→1200 Hz | 200ms | 拾取道具 |
| gameover | 锯齿波 (sawtooth) | 400→80 Hz | 700ms | 游戏结束 |

## 节流机制

为防止密集交火时音频堆叠，同类音效设有最小触发间隔：

| 音效 | 冷却时间 |
|------|----------|
| shoot | 80ms |
| hit | 50ms |

`explode`、`powerup`、`gameover` 不设节流，因为这些事件频率较低。

## 静音

按 M 键切换静音状态。静音时 `playSound()` 直接返回，不创建音频节点。静音状态在 HUD 中显示提示。

## 实现细节

- AudioContext 延迟初始化（首次调用 `getAudioCtx()` 时创建），避免浏览器自动播放策略阻止
- 所有频率变化使用 `exponentialRampToValueAtTime` 实现平滑过渡
- 增益从初始值衰减到 0.001（避免归零导致指数运算异常）
- 音效代码包裹在 try-catch 中，AudioContext 不可用时静默降级
