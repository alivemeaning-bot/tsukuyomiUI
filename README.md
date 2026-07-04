# TsukuyomiUI · Style.css 使用文档

> 原子化纯 CSS 工具类库。无需构建工具，引入即用，类名短小、语义清晰，适合快速搭建界面原型与轻量页面。

---

## 目录

- [快速开始](#快速开始)
- [设计令牌（CSS 变量）](#设计令牌css-变量)
- [基础 Reset](#基础-reset)
- [组件类](#组件类)
- [布局系统](#布局系统)
- [颜色工具类](#颜色工具类)
- [质感效果](#质感效果)
- [尺寸修饰](#尺寸修饰)
- [完整类名速查表](#完整类名速查表)
- [使用示例](#使用示例)

---

## 快速开始

在 HTML 中引入样式文件：

```html
<link rel="stylesheet" href="Style.css" />
```

随后通过组合工具类构建界面：

```html
<button class="btn bg-luv t-white f f-mc sd-luv">按钮</button>
```

---

## 设计令牌（CSS 变量）

所有颜色与尺寸都通过 `:root` 中的 CSS 变量定义，可在自定义样式里覆盖以实现主题化。

### 语义化主色

| 变量            | 默认值        | 含义                |
| --------------- | ------------- | ------------------- |
| `--c-secondary` | `gray`        | 次要（灰）          |
| `--c-default`   | `black`       | 默认（黑）          |
| `--c-primary`   | `#ff4444`     | 主色 / 危险（红）   |
| `--c-warning`   | `gold`        | 警告（金）          |
| `--c-info`      | `deepskyblue` | 信息（蓝）          |
| `--c-sakura`    | `#ffb7c5`     | 樱花粉              |
| `--c-success`   | `darkgreen`   | 成功（绿）          |

### 半透明 / 毛玻璃

| 变量      | 默认值                  | 用途              |
| --------- | ----------------------- | ----------------- |
| `--glass` | `rgba(255,255,255,0.8)` | 半透明白背景      |
| `--fg-bg` | `rgba(255,255,255,0.2)` | 毛玻璃背景        |
| `--tp-bg` | `rgba(255,255,255,0.5)` | 半透明背景        |
| `--angle` | `white`                 | 高亮阴影 / 边框色 |

### 尺寸 / 过渡

| 变量             | 默认值      | 用途             |
| ---------------- | ----------- | ---------------- |
| `--radius`       | `20px`      | 通用圆角         |
| `--radius-pill`  | `90px`      | 胶囊形圆角       |
| `--border-width` | `3px`       | 统一边框宽度     |
| `--shadow-blur`  | `8px`       | 阴影 / 毛玻璃模糊 |
| `--transition`   | `0.2s ease` | 统一过渡时长     |
| `--pad`          | `12px`      | 通用内边距       |

### 局部变量（可通过内联 `style` 覆盖）

`.card-r` / `.card-s`：

| 变量    | 默认值   | 用途       |
| ------- | -------- | ---------- |
| `--w`   | `200px`  | 卡片宽度   |
| `--h`   | `200px`  | 卡片高度   |
| `--pad` | `12px`   | 卡片内边距 |

`.g`：

| 变量    | 默认值 | 用途     |
| ------- | ------ | -------- |
| `--gap` | `12px` | 网格间距 |

> **自定义主题示例**
>
> ```css
> :root {
>   --c-primary: #2f88ff;   /* 把主色改成蓝色 */
>   --radius: 12px;         /* 减小圆角 */
>   --shadow-blur: 16px;    /* 更强的阴影 / 模糊 */
> }
> ```

---

## 基础 Reset

```css
*, *::before, *::after { box-sizing: border-box; }
body { margin: 0; }
```

- 全局启用 `border-box` 盒模型，避免 `padding` / `border` 撑破元素尺寸。
- 移除 `body` 默认外边距。

另外提供铺满视口的辅助类：

| 类      | 效果                |
| ------- | ------------------- |
| `.full` | `min-height: 100vh` |

---

## 组件类

### `.btn` 按钮

- `opacity: 0.85`，圆角 `--radius`，最小 `40px × 120px`，内边距 `0 18px`，鼠标指针。
- 过渡 `opacity / transform / box-shadow`，时长 `--transition`。
- 内置交互态：
  - `:hover` → 完全不透明
  - `:active` → 轻微缩放 `scale(0.96)`
  - `:focus-visible` → `--c-info` 蓝色描边（`outline-offset: 2px`）
  - `:disabled` → `opacity: 0.4`、禁用光标、取消缩放

### `.inp` 输入框

- 与按钮一致的圆角与最小尺寸，内边距 `0 14px`。
- 交互态：
  - `:hover` → 完全不透明
  - `:focus` → 去除默认 outline，添加 `--c-info` 蓝色发光阴影

### `.nav` / `.nav-fix` / `.nav-side` 导航

| 类          | 说明                                                                                                              |
| ----------- | ----------------------------------------------------------------------------------------------------------------- |
| `.nav`      | 宽度 100%，溢出隐藏                                                                                               |
| `.nav-fix`  | 顶部悬浮胶囊导航：`480px × 70px`，`max-width: 92vw`，`top: 5%`，水平居中                                          |
| `.nav-side` | 左侧竖排悬浮导航：`left: 16px`，垂直居中，`flex-direction: column`，`gap: 12px`，圆角 `--radius`，内边距 `16px 12px` |

### `.pan` 面板

圆角面板：`min-height: 360px`（内容可撑高），宽 `260px`，`max-width: 92vw`，内边距 `12px`。

### `.card-r` / `.card-s` 卡片

方形卡片，尺寸/内边距通过 CSS 变量控制，默认 `200px × 200px`、`padding: 12px`；`box-sizing: content-box`，`padding` 不计入宽高。

| 类        | 差异                |
| --------- | ------------------- |
| `.card-r` | 带 `--radius` 圆角  |
| `.card-s` | 直角（无圆角）      |

自定义单个卡片：

```html
<div class="card-r bg-fg" style="--w: 320px; --h: 180px; --pad: 20px;"></div>
```

### `.fix` 固定顶部

将元素固定在页面顶部并水平居中（`top: 3%`，`z-index: 999`）。

### `.bot` 底部推送

`margin-top: auto` + `margin-bottom: 6px`，配合 flex 容器把元素推到底部并留出下边距。

---

## 布局系统

### `.f` + 九宫格对齐

`.f` 表示 `display: flex`；后缀 `t/m/b` 控制垂直方向（`align-items`），`l/c/r` 控制水平方向（`justify-content`），可组合出九种对齐方式。

| 类      | `justify-content` | `align-items` | 位置 |
| ------- | ----------------- | ------------- | ---- |
| `.f-tl` | `flex-start`      | `flex-start`  | 左上 |
| `.f-tc` | `center`          | `flex-start`  | 上中 |
| `.f-tr` | `flex-end`        | `flex-start`  | 右上 |
| `.f-ml` | `flex-start`      | `center`      | 左中 |
| `.f-mc` | `center`          | `center`      | 正中 |
| `.f-mr` | `flex-end`        | `center`      | 右中 |
| `.f-bl` | `flex-start`      | `flex-end`    | 左下 |
| `.f-bc` | `center`          | `flex-end`    | 下中 |
| `.f-br` | `flex-end`        | `flex-end`    | 右下 |

> 使用时先加 `.f` 启用 flex，再叠加对齐类，例如 `<div class="f f-mc">内容</div>`。

### `.g` 居中网格

| 类     | 作用                                                                     |
| ------ | ------------------------------------------------------------------------ |
| `.g`   | `display: grid`，行/列内容与轴均居中；间距由 `--gap` 控制（默认 `12px`） |
| `.g-2` | 2 列网格：`grid-template-columns: repeat(2, auto)`                       |
| `.g-3` | 3 列网格：`grid-template-columns: repeat(3, auto)`                       |

---

## 颜色工具类

命名规则：`前缀-色名`。前缀决定作用于哪个 CSS 属性，色名对应设计令牌里的语义色。

| 前缀  | 作用     | CSS 属性                                     |
| ----- | -------- | -------------------------------------------- |
| `t-`  | 文字颜色 | `color`                                      |
| `bg-` | 背景色   | `background-color`                           |
| `bd-` | 边框     | `border: var(--border-width) solid <color>`  |
| `sd-` | 阴影     | `box-shadow: 0 0 var(--shadow-blur) <color>` |

### 语义色名

| 色名  | 对应变量        | 含义        |
| ----- | --------------- | ----------- |
| `ycy` | `--c-secondary` | 次要（灰）  |
| `def` | `--c-default`   | 默认（黑）  |
| `luv` | `--c-primary`   | 主色 / 危险 |
| `kgy` | `--c-warning`   | 警告        |
| `irh` | `--c-info`      | 信息        |
| `skr` | `--c-sakura`    | 樱花粉      |
| `stn` | `--c-success`   | 成功        |

### 中性色 & 特殊色

| 类                                      | 效果                                    |
| --------------------------------------- | --------------------------------------- |
| `.t-white` / `.bg-white`                | 纯白文字 / 背景                         |
| `.t-black` / `.bg-black`                | 纯黑文字 / 背景                         |
| `.bd-white` / `.sd-white`               | 白色边框 / 白色发光阴影                 |
| `.bd-black` / `.sd-black`               | 黑色边框 / 黑色阴影                     |
| `.bg-glass` / `.bd-glass` / `.sd-glass` | `--glass` 半透明白 背景 / 边框 / 阴影   |
| `.bg-fg`                                | 毛玻璃背景（`--fg-bg`）                 |
| `.bg-tp`                                | 半透明背景（`--tp-bg`）                 |
| `.bd-angle` / `.sd-angle`               | 高亮色 `--angle` 边框 / 发光阴影        |

使用示例：

- `.t-luv` —— 主色（红）文字
- `.bg-irh` —— 信息（蓝）背景
- `.bd-stn` —— 成功（绿）边框
- `.sd-kgy` —— 警告（金）发光阴影

---

## 质感效果

| 类    | 效果                                                                                                                                          |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `.fg` | 毛玻璃：`backdrop-filter: blur(var(--shadow-blur))` + 白色渐变高光 + 1px 半透明白边 + 深色阴影                                                 |
| `.tp` | 半透明：`backdrop-filter: blur(var(--shadow-blur))` + `background-color: var(--tp-bg)`                                                        |

> 两者均包含 `-webkit-backdrop-filter`，以兼容 Safari。

---

## 尺寸修饰

同时作用于按钮与输入框：

| 类                    | 效果                                          |
| --------------------- | --------------------------------------------- |
| `.btn-sm` / `.inp-sm` | 小号：`32px` 高、`88px` 宽、`0 12px` 内边距   |
| `.btn-lg` / `.inp-lg` | 大号：`48px` 高、`160px` 宽、`0 24px` 内边距  |

> 目前没有内置 `.w-full`；如需铺满，请自行在项目样式中定义，或用内联 `style="width:100%"`。

---

## 完整类名速查表

| 分类       | 类名                                                                                                                                                                                                       |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 组件       | `.btn` `.inp` `.nav` `.nav-fix` `.nav-side` `.pan` `.card-r` `.card-s` `.fix` `.bot` `.full`                                                                                                                |
| Flex 对齐  | `.f` `.f-tl` `.f-tc` `.f-tr` `.f-ml` `.f-mc` `.f-mr` `.f-bl` `.f-bc` `.f-br`                                                                                                                                |
| Grid 布局  | `.g` `.g-2` `.g-3`                                                                                                                                                                                         |
| 文字色     | `.t-ycy` `.t-def` `.t-luv` `.t-kgy` `.t-irh` `.t-skr` `.t-stn` `.t-white` `.t-black`                                                                                                                        |
| 背景色     | `.bg-ycy` `.bg-def` `.bg-luv` `.bg-kgy` `.bg-irh` `.bg-skr` `.bg-stn` `.bg-glass` `.bg-fg` `.bg-tp` `.bg-white` `.bg-black`                                                                                  |
| 边框       | `.bd-ycy` `.bd-def` `.bd-luv` `.bd-kgy` `.bd-irh` `.bd-skr` `.bd-stn` `.bd-glass` `.bd-white` `.bd-black` `.bd-angle`                                                                                        |
| 阴影       | `.sd-ycy` `.sd-def` `.sd-luv` `.sd-kgy` `.sd-irh` `.sd-skr` `.sd-stn` `.sd-white` `.sd-black` `.sd-glass` `.sd-angle`                                                                                        |
| 质感       | `.fg` `.tp`                                                                                                                                                                                                |
| 尺寸       | `.btn-sm` `.btn-lg` `.inp-sm` `.inp-lg`                                                                                                                                                                    |

---

## 使用示例

### 顶部悬浮导航栏

```html
<nav class="nav-fix fg f f-mc sd-angle">
  <span class="t-white">TsukuyomiUI</span>
</nav>
```

### 左侧竖排导航

```html
<aside class="nav-side fg sd-angle">
  <button class="btn btn-sm bg-luv t-white">主页</button>
  <button class="btn btn-sm bg-irh t-white">设置</button>
  <button class="btn btn-sm bg-stn t-white">关于</button>
</aside>
```

### 主色按钮（大号、居中）

```html
<button class="btn btn-lg bg-luv t-white f f-mc sd-luv">提交</button>
```

### 毛玻璃面板

```html
<div class="pan fg sd-angle f f-mc" style="flex-direction: column;">
  <input class="inp bd-glass" placeholder="请输入..." />
  <button class="btn bg-stn t-white bot">保存</button>
</div>
```

### 自定义卡片

```html
<div class="card-r fg sd-angle f f-mc"
     style="--w: 320px; --h: 180px; --pad: 20px;">
  <span class="t-white">自定义尺寸卡片</span>
</div>
```

### 3 列居中网格

```html
<div class="g g-3" style="--gap: 20px;">
  <div class="card-s bg-luv"></div>
  <div class="card-s bg-kgy"></div>
  <div class="card-s bg-irh"></div>
  <div class="card-s bg-skr"></div>
  <div class="card-s bg-stn"></div>
  <div class="card-s bg-ycy"></div>
</div>
```

### 铺满视口的居中容器

```html
<div class="full f f-mc bg-def">
  <div class="pan fg sd-angle">居中内容</div>
</div>
```

### 状态提示文字

```html
<p class="t-luv">操作失败，请重试</p>
<p class="t-stn">保存成功</p>
<p class="t-kgy">请注意输入格式</p>
<p class="t-irh">这是一条提示信息</p>
<p class="t-skr">Hello, sakura ~</p>
```

---

## 设计说明

- **短类名 + 语义变量**：类名保持 2–4 字符以便快速书写，语义信息集中在 CSS 变量（如 `--c-primary`）上，改主题只需覆盖变量。
- **组合优先**：组件类只处理形状/尺寸/交互，颜色、阴影、边框全部由独立工具类叠加，方便自由搭配。
- **可局部覆写**：卡片尺寸 (`--w` / `--h` / `--pad`) 与网格间距 (`--gap`) 均支持通过内联 `style` 单独调节，无需新增类。
