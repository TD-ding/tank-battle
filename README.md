# 坦克大战 (Tank Battle)

经典坦克大战小游戏的 HTML5 Canvas 复刻版，单文件实现，浏览器直接打开即可游玩。

## 简介

玩家操控坦克在地图上移动、射击，消灭所有敌方坦克即可获胜。地图上有可破坏的砖墙和不可破坏的钢墙作为障碍物，底部有需要保护的基地——基地被摧毁则游戏失败。

### 操作方式

| 按键 | 功能 |
|------|------|
| W / ↑ | 向上移动 |
| S / ↓ | 向下移动 |
| A / ← | 向左移动 |
| D / → | 向右移动 |
| 空格 | 射击 |
| Enter | 开始 / 重新开始 |

### 游戏规则

- 玩家拥有 3 条生命，被击中后复活
- 消灭一个敌方坦克得 100 分
- 共 20 个敌方坦克，全部消灭即为胜利
- 砖墙可被子弹摧毁，钢墙不可摧毁
- 基地被击中则游戏结束

## 技术栈

- HTML5 Canvas
- 原生 JavaScript（无框架依赖）
- CSS3

## 目录结构

```
tank-battle/
├── index.html   # 游戏主文件（包含全部 HTML/CSS/JS）
└── README.md    # 项目说明
```

## 如何运行

直接在浏览器中打开 `index.html` 即可，无需安装任何依赖或启动服务器：

```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Windows
start index.html
```

也可以用任意本地服务器运行：

```bash
# Python
python3 -m http.server 8080

# Node.js (npx)
npx serve .
```

然后访问 `http://localhost:8080`。
