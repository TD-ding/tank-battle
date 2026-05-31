# 协作开发日志

本文档记录坦克大战项目的迭代开发历史。每轮工作在 `agent/dev` 分支上完成，通过 PR 合并至 `main`。

---

## 第 0 轮：项目初始化

**分支**: `main`
**日期**: 2026-05-31

| Commit | 说明 |
|--------|------|
| `655bbf8` | Initial commit — 创建仓库 |
| `62fb312` | feat: 实现坦克大战游戏（HTML5 Canvas） |
| `ce89d9f` | docs: 添加 README |

**主要内容**:
- 完成基础游戏：玩家坦克 WASD/方向键移动、空格射击
- 敌方 AI 坦克自动移动和射击
- 地图砖墙/钢墙障碍物
- 计分系统、游戏结束判定
- 编写 README.md

---

## 第 1 轮：修复游戏性问题

**分支**: `agent/dev`
**PR**: [#1 — 第1轮: feat - 初始版本](https://github.com/TD-ding/tank-battle/pull/1)
**日期**: 2026-05-31

| Commit | 说明 |
|--------|------|
| `2541bfd` | fix: 修复 6 个游戏性问题 |
| `9b55e0d` | Merge PR #1 |

**用户反馈 → 改动**:
1. 玩家出生卡在基地位置 → 调整出生点到底部中间上方
2. 切标签页回来坦克飞出去 → 添加 `MAX_DT` 上限防止 dt 跳变
3. 复活瞬间被打死 → 添加 2 秒无敌时间
4. 敌人撞墙一直不换方向 → 撞墙后立即换方向
5. 玩家无限发射子弹 → 限制同时 2 颗子弹
6. 基地周围保护墙不完整 → 补全 U 形砖墙

---

## 第 2 轮：代码质量优化

**分支**: `agent/dev`
**PR**: [#2 — 第2轮: refactor - 代码质量优化](https://github.com/TD-ding/tank-battle/pull/2)
**日期**: 2026-05-31

| Commit | 说明 |
|--------|------|
| `20b42be` | refactor: 集中主题配置，优化渲染，增强健壮性 |
| `c930f89` | fix: 优化水面渲染，改进敌人 AI 和复活安全 |
| `2868da6` | Merge PR #2 |

**用户反馈 → 改动**:
1. 颜色/字体分散各处 → 集中到 `THEME` 配置对象
2. 出错无提示 → 添加 `showError` + 底部 toast + `window.onerror`
3. 每帧重绘整个地图 → 离屏 canvas 缓存，仅在 `mapDirty` 时重绘
4. HUD 用 DOM 更新 → 改为 Canvas 直接绘制
5. 死亡敌人对象未清理 → 每 5 秒定时清理 `enemies` 数组
6. 水面瓦片渲染低效 → 只遍历水面瓦片索引
7. 复活可能和敌人重叠 → 多出生点轮询
8. 子弹幽灵问题 → 及时清理无效子弹
9. 敌人子弹无上限 → 每个敌人同时仅 1 颗子弹
10. 敌人撞墙不换路 → `triedDirs` 记忆已试方向
11. 敌人追踪太弱 → 自适应追踪概率（30%→80%）

---

## 第 3 轮：用户体验优化

**分支**: `agent/dev`
**PR**: [#3 — 第3轮: feat - 用户体验优化](https://github.com/TD-ding/tank-battle/pull/3)
**日期**: 2026-05-31

| Commit | 说明 |
|--------|------|
| `8adb6ba` | feat: 暂停功能、美化界面、爆炸粒子、详细 HUD |
| `b190d29` | fix: 帧率无关速度、暂停恢复修复、多项打磨 |
| `5bdb282` | Merge PR #3 |

**用户反馈 → 改动**:
1. 添加暂停功能（P / Esc）
2. 美化开始/胜利/失败界面（样式化 overlay、按键标签、道具说明）
3. 增强爆炸效果（碎片粒子 + 外圈光晕）
4. HUD 显示更多信息（场上敌人数、已消灭数）
5. 移动速度改为帧率无关（像素/秒）
6. 修复暂停恢复后 dt 跳变（恢复时 `lastTime = 0`）
7. 敌人生成被占时的回退逻辑
8. 无敌时坦克半透明闪烁（替代完全消失）
9. 敌人射击间隔加随机波动（±30%）

---

## 第 4 轮：功能增强

**分支**: `agent/dev`
**PR**: [#4 — 第4轮: feat - 功能增强](https://github.com/TD-ding/tank-battle/pull/4)
**日期**: 2026-05-31

| Commit | 说明 |
|--------|------|
| `64db449` | feat: 道具系统、音效、水面地形、移动优化 |
| `49a99fb` | Merge PR #4 |

**用户反馈 → 改动**:
1. 道具系统（加速 / 加命 / 基地护盾 / 增强火力），击毁敌人 25% 掉落 + 地图定时刷新
2. 音效系统（Web Audio API 合成：射击/爆炸/命中/道具/游戏结束）
3. 水面地形（不可通行，带波纹动画）
4. 移动网格对齐仅转向时触发，直行更顺滑
5. 爆炸动画改为时间驱动（elapsed/duration），不再依赖帧计数
6. 音效节流（同类音效最小间隔）
7. M 键静音切换

---

## 第 5 轮：Bug 修复

**分支**: `agent/dev`
**PR**: [#5 — 第5轮: fix - Bug修复](https://github.com/TD-ding/tank-battle/pull/5)
**日期**: 2026-05-31

| Commit | 说明 |
|--------|------|
| `677dd21` | fix: 数字 tankId、Esc 阻止默认行为、高分提前保存 |
| `657a205` | Merge PR #5 |

**用户反馈 → 改动**:
1. `tankId` 从对象引用改为数字 ID（`nextTankId++`），避免敌人销毁后子弹悬空引用
2. Esc 键添加 `preventDefault`，防止浏览器退出全屏
3. 最高分在游戏逻辑中（gameover/win 时）立即保存至 localStorage，而非仅在界面显示时

---

## 第 6 轮：项目文档

**分支**: `agent/dev`
**PR**: [#6 — docs: 添加项目文档](https://github.com/TD-ding/tank-battle/pull/6)
**日期**: 2026-05-31

| Commit | 说明 |
|--------|------|
| `ae5660a` | docs: 添加项目文档，更新 README |
| `c25b4cd` | Merge PR #6 |

**改动**:
1. 新增 `docs/gameplay.md` — 操作方式、道具、游戏规则、敌人 AI
2. 新增 `docs/architecture.md` — 技术栈、代码组织、核心设计决策
3. 新增 `docs/map-format.md` — 瓦片类型、地图布局、出生点
4. 新增 `docs/audio.md` — 音效合成、节流机制、静音
5. 新增 `docs/config.md` — 全部可调常量和 THEME 参数
6. 更新 `README.md` — 目录结构增加 docs/，道具表增加持续时间列，补充高分说明

---

## 协作流程

```
main ──────────────────────────────────────────→  生产分支
  │                                               （用户维护）
  ├── agent/dev ── PR #1 ──→ merge
  ├── agent/dev ── PR #2 ──→ merge
  ├── agent/dev ── PR #3 ──→ merge
  ├── agent/dev ── PR #4 ──→ merge
  ├── agent/dev ── PR #5 ──→ merge
  └── agent/dev ── PR #6 ──→ merge
```

每轮工作流程：
1. `git checkout main && git pull origin main`
2. `git checkout -b agent/dev`（从最新 main 创建）
3. 根据 用户反馈 修改代码
4. 提交到 `agent/dev`，推送到远程
5. 用户 创建 PR → review → merge 至 `main`
6. 下一轮重复
