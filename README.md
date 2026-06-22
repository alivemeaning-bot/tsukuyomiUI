# TsukuyomiUI · Style.css 使用文档

> 原子化纯 CSS 工具类库。无需构建工具，引入即用，类名语义清晰，适合快速搭建界面原型与轻量页面。

---

## 目录

- [快速开始](#快速开始)
- [设计令牌（CSS 变量）](#设计令牌css-变量)
- [基础 Reset](#基础-reset)
- [组件类](#组件类)
- [布局助手](#布局助手)
- [颜色工具类](#颜色工具类)
- [语义化别名](#语义化别名)
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
<button class="btn bg-luv t-def m sd-luv">按钮</button>
```

---

## 设计令牌（CSS 变量）

所有颜色与尺寸都通过 `:root` 中的 CSS 变量定义，可在自定义样式里覆盖以实现主题化。

### 语义化主色

| 变量      | 默认值          | 含义              |
| --------- | --------------- | ----------------- |
| `--hcy`   | `gray`          | 次要 / 灰         |
| `--def`   | `black`         | 默认 / 黑         |
| `--luv`   | `#ff4444`       | 主色 / 危险（红） |
| `--kgy`   | `gold`          | 警告（金）        |
| `--irh`   | `deepskyblue`   | 信息（蓝）        |
| `--skr`   | `#ffb7c5`       | 樱花粉（sakura）  |
| `--stn`   | `darkgreen`     | 成功（绿）        |

### 半透明 / 毛玻璃

| 变量       | 默认值                       | 用途             |
| ---------- | ---------------------------- | ---------------- |
| `--glass`  | `rgba(255,255,255,0.8)`      | 半透明白背景/边框 |
| `--fg-bg`  | `rgba(255,255,255,0.2)`      | 毛玻璃背景       |
| `--tp-bg`  | `rgba(255,255,255,0.5)`      | 半透明背景       |
| `--angle`  | `white`                      | 高亮阴影色       |

### 设计令牌

| 变量            | 默认值      | 用途         |
| --------------- | ----------- | ------------ |
| `--radius`      | `20px`      | 通用圆角     |
| `--radius-pill` | `90px`      | 胶囊形圆角   |
| `--transition`  | `0.2s ease` | 统一过渡时长 |

> **自定义主题示例**
>
> ```css
> :root {
>   --luv: #2f88ff;   /* 把主色改成蓝色 */
>   --radius: 12px;   /* 减小圆角 */
> }
> ```

---

## 基础 Reset

```css
*, *::before, *::after { box-sizing: border-box; }
```

为所有元素启用 `border-box` 盒模型，避免 `padding` / `border` 撑破元素尺寸。

---

## 组件类

### `.btn` 按钮

- 默认 `opacity: 0.85`，圆角 `--radius`，最小尺寸 `40px × 120px`，鼠标指针。
- 内置交互态：
  - `:hover` → 完全不透明
  - `:active` → 轻微缩放 `scale(0.96)`
  - `:focus-visible` → 蓝色聚焦描边
  - `:disabled` → 半透明、禁用光标、取消缩放

### `.inp` 输入框

- 与按钮风格一致的尺寸与圆角。
- 交互态：
  - `:hover` → 完全不透明
  - `:focus` → 去除默认 outline，添加蓝色发光阴影

### `.nav` / `.nav-fix` 导航

| 类         | 说明                                                           |
| ---------- | -------------------------------------------------------------- |
| `.nav`     | 宽度 100%，溢出隐藏                                            |
| `.nav-fix` | 固定定位、胶囊圆角的悬浮导航条，水平居中，`max-width: 92vw` 自适应小屏 |

### `.pan` 面板

圆角面板，`min-height: 360px`（内容可撑高），宽 `260px`，`max-width: 92vw`，内边距 `12px`。

### `.card` 卡片

固定 `50px × 50px` 的小方块。

### `.fix` 固定定位

将元素固定在顶部并水平居中（`top: 3%`，`z-index: 999`）。

### `.bot`

`margin-top: auto`，配合 flex 容器把元素推到底部。

---

## 布局助手

| 类       | 作用                                                    |
| -------- | ------------------------------------------------------- |
| `.m`     | flex 居中（水平 + 垂直居中）                            |
| `.mgn`   | 外边距 `6px 6px`                                        |
| `.fxc`   | flex 纵向排列，`height: 100%`                           |
| `.fxcc`  | `align-items: center`（常与 `.fxc` 搭配实现纵向居中）   |

---

## 颜色工具类

命名规则：`前缀-色名`

| 前缀   | 含义     | CSS 属性             |
| ------ | -------- | -------------------- |
| `t-`   | 文字颜色 | `color`              |
| `bg-`  | 背景色   | `background-color`   |
| `bd-`  | 边框     | `border: 3px solid`  |
| `sd-`  | 阴影     | `box-shadow: 0 0 8px`|

可用色名：`hcy`、`def`、`luv`、`kgy`、`irh`、`skr`、`stn`

例如：

- `.t-luv` —— 红色文字
- `.bg-irh` —— 蓝色背景
- `.bd-stn` —— 绿色边框
- `.sd-kgy` —— 金色发光阴影

> **注意**：`.bg-hcy` 使用的是半透明白背景（`--glass`），而非纯灰色，用于毛玻璃风格的次要元素。

---

## 语义化别名

为提升可读性，推荐新代码使用语义化别名，与缩写类名等价。

### 文字颜色

| 别名           | 等价缩写  | 颜色   |
| -------------- | --------- | ------ |
| `.t-secondary` | `.t-hcy`  | 灰     |
| `.t-default`   | `.t-def`  | 黑     |
| `.t-primary`   | `.t-luv`  | 红     |
| `.t-danger`    | `.t-luv`  | 红     |
| `.t-warning`   | `.t-kgy`  | 金     |
| `.t-info`      | `.t-irh`  | 蓝     |
| `.t-sakura`    | `.t-skr`  | 樱花粉 |
| `.t-success`   | `.t-stn`  | 绿     |

### 背景颜色

| 别名          | 等价缩写  | 颜色   |
| ------------- | --------- | ------ |
| `.bg-default` | `.bg-def` | 黑     |
| `.bg-primary` | `.bg-luv` | 红     |
| `.bg-danger`  | `.bg-luv` | 红     |
| `.bg-warning` | `.bg-kgy` | 金     |
| `.bg-info`    | `.bg-irh` | 蓝     |
| `.bg-sakura`  | `.bg-skr` | 樱花粉 |
| `.bg-success` | `.bg-stn` | 绿     |

---

## 质感效果

| 类          | 效果                                          |
| ----------- | --------------------------------------------- |
| `.fg`       | 毛玻璃：`backdrop-filter: blur(12px)` + 半透明背景 |
| `.tp`       | 半透明背景（`--tp-bg`）                       |
| `.sd-angle` | 白色高亮发光阴影                              |

> `.fg` 同时包含 `-webkit-backdrop-filter`，以兼容 Safari。

---

## 尺寸修饰

适用于按钮与输入框：

| 类                  | 效果                                          |
| ------------------- | --------------------------------------------- |
| `.btn-sm` / `.inp-sm` | 小号：`32px` 高、`88px` 宽、`0 12px` 内边距   |
| `.btn-lg` / `.inp-lg` | 大号：`48px` 高、`160px` 宽、`0 24px` 内边距  |
| `.w-full`           | 宽度 100%                                     |

---

## 完整类名速查表

| 分类     | 类名                                                                 |
| -------- | -------------------------------------------------------------------- |
| 组件     | `.btn` `.inp` `.nav` `.nav-fix` `.pan` `.card` `.fix` `.bot`          |
| 布局     | `.m` `.mgn` `.fxc` `.fxcc`                                            |
| 文字色   | `.t-hcy` `.t-def` `.t-luv` `.t-kgy` `.t-irh` `.t-skr` `.t-stn`        |
| 背景色   | `.bg-hcy` `.bg-def` `.bg-luv` `.bg-kgy` `.bg-irh` `.bg-skr` `.bg-stn` |
| 边框     | `.bd-hcy` `.bd-def` `.bd-luv` `.bd-kgy` `.bd-irh` `.bd-skr` `.bd-stn` |
| 阴影     | `.sd-hcy` `.sd-def` `.sd-luv` `.sd-kgy` `.sd-irh` `.sd-skr` `.sd-stn` `.sd-angle` |
| 质感     | `.fg` `.tp`                                                          |
| 语义别名 | `.t-secondary` `.t-default` `.t-primary` `.t-danger` `.t-warning` `.t-info` `.t-sakura` `.t-success` `.bg-default` `.bg-primary` `.bg-danger` `.bg-warning` `.bg-info` `.bg-sakura` `.bg-success` |
| 尺寸     | `.btn-sm` `.btn-lg` `.inp-sm` `.inp-lg` `.w-full`                    |

---

## 使用示例

### 悬浮导航栏

```html
<nav class="nav-fix fg m fxcc sd-angle">
  <span class="t-default">TsukuyomiUI</span>
</nav>
```

### 主色按钮（大号、铺满）

```html
<button class="btn btn-lg bg-primary t-default w-full m">提交</button>
```

### 毛玻璃面板

```html
<div class="pan fg sd-angle fxc">
  <input class="inp w-full mgn" placeholder="请输入..." />
  <button class="btn bg-success t-default mgn bot">保存</button>
</div>
```

### 状态提示

```html
<p class="t-danger">操作失败，请重试</p>
<p class="t-success">保存成功</p>
<p class="t-warning">请注意输入格式</p>
<p class="t-info">这是一条提示信息</p>
```

---

## 设计说明

- **向后兼容**：缩写类名（如 `.t-luv`）与语义别名（如 `.t-primary