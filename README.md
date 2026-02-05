# Rive 动画演示

这是一个使用 [Rive](https://rive.app/) 框架创建的交互式动画演示项目，展示了如何通过状态机（State Machine）控制动画行为。

## 关于 Rive

[Rive](https://rive.app/) 是一个强大的实时动画设计工具和运行时框架，专为创建高质量的交互式动画而设计。它的主要特点包括：

- **实时渲染**：动画以高性能方式在浏览器和移动应用中实时渲染
- **状态机系统**：通过直观的状态机界面管理复杂的动画逻辑和交互
- **跨平台支持**：支持 Web（Canvas/WebGL）、iOS、Android、Flutter、React 等多个平台
- **小巧高效**：运行时包体小，性能优异
- **交互友好**：支持鼠标、触摸等多种交互方式

## 项目概述

本项目演示了 Rive 的状态机功能。动画包含一个名为 "Two mercenaries" 的状态机，实现了以下交互：

- 鼠标悬停时触发特殊动画效果
- 鼠标离开时恢复默认状态

## 技术栈

- **Rive Canvas Runtime**: `@rive-app/canvas@2.20.0`
- **HTML5 Canvas**: 用于渲染动画
- **纯 JavaScript**: 无需构建工具，开箱即用

## 如何运行

### 本地运行

1. 克隆项目：

```bash
git clone git@github.com:vaebe/rive-js-demo.git
cd rive-js-demo
```

1. 使用任意 HTTP 服务器打开 `index.html` 文件，例如：

```bash
# 使用 Python
python3 -m http.server 8000

# 或使用 Node.js 的 http-server
npx http-server
```

1. 在浏览器中访问 `http://localhost:8000`

### 在线预览

项目已配置自动部署到 GitHub Pages，每次推送到 `master` 分支时会自动更新。

访问地址：`https://vaebe.github.io/rive-js-demo/`

## 项目结构

``` bash
.
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions 部署配置
├── index.html              # 主页面文件
├── posture-animation.riv   # Rive 动画资源文件
└── README.md               # 项目说明文档
```

## 核心代码说明

项目核心在于 `index.html` 中的 JavaScript 部分：

```javascript
const r = new rive.Rive({
  src: "./posture-animation.riv",  // 动画文件路径
  canvas,
  autoplay: true,
  stateMachines: "Two mercenaries", // 状态机名称
  fit: rive.Fit.Contain,
  alignment: rive.Alignment.Center,

  onLoad() {
    // 获取状态机输入
    const inputs = r.stateMachineInputs("Two mercenaries");
    const hover = inputs.find(i => i.name.toLowerCase().includes("hover"));

    // 添加鼠标悬停事件
    canvas.addEventListener("mouseenter", () => {
      hover && (hover.value = true);
    });

    canvas.addEventListener("mouseleave", () => {
      hover && (hover.value = false);
    });
  }
});
```
