# 260527 关于全栈开发、网络通信和前端基础的笔记。

---

## 一、JavaScript 全栈开发

**核心概念**：JavaScript 不仅可以写前端，通过 Node.js 还可以写后端，实现"一门语言走天下"。

| 层级 | 技术栈 | 作用 |
|------|--------|------|
| 前端 | HTML/CSS/JS + 框架(Vue/React/Angular) | 用户界面、交互逻辑 |
| 后端 | Node.js + Express/Koa/Nest.js | 服务器、业务逻辑、数据库操作 |
| 数据库 | MongoDB/MySQL/PostgreSQL + ORM(Prisma/Sequelize) | 数据持久化存储 |

**全栈优势**：减少上下文切换、统一数据格式(JSON)、前后端代码复用。

---

## 二、网络通信基础

### 1. DNS 解析（Domain Name System）

```
用户输入: www.example.com
           ↓
    DNS 服务器查询
           ↓
    返回 IP 地址: 192.168.1.1
           ↓
    浏览器向该 IP 发送请求
```

**补充说明**：
- DNS 是**分布式数据库**，全球多台 DNS 服务器协作解析
- 解析过程：浏览器缓存 → 系统缓存 → 路由器缓存 → ISP DNS → 根域名服务器 → 顶级域服务器 → 权威域名服务器
- 常用命令：`nslookup www.baidu.com` 或 `ping www.baidu.com`

### 2. TCP 协议（Transmission Control Protocol）

**特点**：
- **面向连接**：通信前需"三次握手"建立连接
- **可靠传输**：数据包丢失会自动重传，保证数据完整有序
- **全双工**：双方可同时发送和接收数据

**三次握手过程**：
```
客户端 → SYN(请求建立连接) → 服务端
客户端 ← SYN + ACK(确认) ← 服务端
客户端 → ACK(确认) → 服务端
连接建立，开始数据传输
```

**对比 UDP**：TCP 可靠但慢，UDP 快但不可靠（适合视频直播、游戏）

---

## 三、前后端分离架构

### AJAX（Asynchronous JavaScript and XML）

**核心机制**：页面**无需刷新**即可与服务器交换数据并更新部分内容。

```javascript
// 现代用法：Fetch API
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => {
    // 用返回的数据更新页面，不用刷新整个页面
    document.getElementById('list').innerHTML = render(data);
  });

// 旧用法：XMLHttpRequest（你提到的 XML 技术的来源）
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/data', true); // true = 异步
xhr.send();
```

**为什么叫 XML？** 早期数据格式用 XML，现在基本都用 **JSON**（更轻量、易解析）。

### 后端接口（API）

**Easy Mock**：一个在线 Mock 数据平台，前端开发时后端接口还没写好，先用假数据模拟接口返回，不阻塞前端进度。

**接口调用流程**：
```
前端页面 ──HTTP请求──→ 后端服务器(IP:端口)
   ↑                        ↓
展示数据 ←──JSON数据──── 数据库查询/业务处理
```

**RESTful API 规范**（常用）：
| 方法 | 路径 | 含义 |
|------|------|------|
| GET | /users | 获取用户列表 |
| GET | /users/1 | 获取 ID 为 1 的用户 |
| POST | /users | 创建新用户 |
| PUT | /users/1 | 更新 ID 为 1 的用户 |
| DELETE | /users/1 | 删除 ID 为 1 的用户 |

---

## 四、HTML 标签分类

### 三类元素对比

| 类型 | 特性 | 常见标签 | CSS 设置宽高 |
|------|------|----------|--------------|
| **块级元素** | 独占一行，宽度默认100% | `div`, `p`, `h1-h6`, `ul`, `li`, `section`, `header`, `footer` | ✅ 有效 |
| **行内元素** | 不独占行，宽高由内容决定 | `span`, `a`, `strong`, `em`, `label`, `code` | ❌ 无效（设置不生效） |
| **行内块元素** | 不独占行，但可以设宽高 | `img`, `input`, `button`, `textarea`, `select` | ✅ 有效 |

### 转换方法

```css
span {
  display: block;      /* 行内 → 块级 */
  display: inline;     /* 块级/行内块 → 行内 */
  display: inline-block; /* 行内 → 行内块（最常用） */
}
```

---

## 五、`<ul>` 标签详解

```html
<ul>
  <li>项目一</li>
  <li>项目二</li>
</ul>
```

**默认样式**（浏览器自带）：
- `margin-top: 1em; margin-bottom: 1em;`（上下外边距）
- `padding-left: 40px;`（左内边距，留给列表符号）
- 列表符号：`disc`（实心圆）

**清除默认样式**（CSS Reset）：
```css
ul {
  margin: 0;
  padding: 0;
  list-style: none;  /* 去掉列表符号 */
}
```

---

## 六、HTML 标签结构

### 基本语法

```html
<!-- 双标签（有开有闭） -->
<<标签名 属性="值">内容</标签名>
<p class="text">这是一段文字</p>

<!-- 单标签（自闭合） -->
<<标签名 />
<img src="photo.jpg" alt="描述" />
<br />      <!-- 换行 -->
<hr />      <!-- 水平线 -->
<input type="text" />
<meta charset="UTF-8" />
```

### 常用全局属性

| 属性 | 作用 |
|------|------|
| `class` | 类名（可多个，用空格分隔，用于 CSS/JS 选择）|
| `id` | 唯一标识（页面中不能重复）|
| `style` | 行内样式（优先级最高，但不推荐多用）|
| `title` | 鼠标悬停提示文字 |
| `data-*` | 自定义数据属性（如 `data-user-id="123"`）|

---

## 七、补充：盒模型（Box Model）

你提到了 `margin` 和 `padding`，这是 CSS 盒模型的核心：

```
┌─────────────────────────────┐
│         margin（外边距）      │  ← 元素与其他元素的距离
│   ┌─────────────────────┐   │
│   │     border（边框）    │   │
│   │   ┌─────────────┐   │   │
│   │   │  padding（内边距）│   │  ← 内容与边框的距离
│   │   │   ┌─────┐   │   │   │
│   │   │   │content│   │   │   │  ← 实际内容（文字/图片）
│   │   │   └─────┘   │   │   │
│   │   └─────────────┘   │   │
│   └─────────────────────┘   │
└─────────────────────────────┘
```

**简写语法**：
```css
/* 四个值：上 右 下 左（顺时针） */
margin: 10px 20px 10px 20px;

/* 两个值：上下 左右 */
padding: 15px 30px;

/* 一个值：四边相同 */
margin: 0;
```

---

# 比如 Node.js 后端开发、HTTP 状态码、或者 CSS 布局（Flex/Grid）吗？
---

## 八、HTTP 协议详解

HTTP（HyperText Transfer Protocol）是前后端通信的**应用层协议**，基于 TCP。

### 请求报文结构

```
POST /api/login HTTP/1.1          ← 请求行（方法 + 路径 + 协议版本）
Host: www.example.com             ← 请求头（键值对）
Content-Type: application/json
Authorization: Bearer token123

{                                 ← 请求体（Body，GET请求通常没有）
  "username": "admin",
  "password": "123456"
}
```

### 响应报文结构

```
HTTP/1.1 200 OK                   ← 状态行（协议 + 状态码 + 状态描述）
Content-Type: application/json
Content-Length: 256

{                                 ← 响应体
  "code": 0,
  "data": { "id": 1, "name": "admin" },
  "message": "success"
}
```

### 常见 HTTP 状态码

| 状态码 | 含义 | 场景 |
|--------|------|------|
| **2xx 成功** |||
| 200 | OK | 请求成功，正常返回数据 |
| 201 | Created | 资源创建成功（如注册、新建）|
| 204 | No Content | 成功但无返回内容（如删除成功）|
| **3xx 重定向** |||
| 301 | Moved Permanently | 永久重定向（URL 已变更）|
| 302 | Found | 临时重定向 |
| 304 | Not Modified | 缓存有效，使用本地缓存 |
| **4xx 客户端错误** |||
| 400 | Bad Request | 请求参数错误/格式不对 |
| 401 | Unauthorized | 未认证（没登录/token 过期）|
| 403 | Forbidden | 无权限（已登录但无权访问）|
| 404 | Not Found | 资源不存在 |
| 405 | Method Not Allowed | 请求方法不被允许 |
| 422 | Unprocessable Entity | 参数校验失败 |
| **5xx 服务端错误** |||
| 500 | Internal Server Error | 服务器内部错误 |
| 502 | Bad Gateway | 网关错误（如 Nginx 连不上后端）|
| 503 | Service Unavailable | 服务暂时不可用（维护/过载）|

---

## 九、浏览器渲染原理

```
1. 输入 URL
      ↓
2. DNS 解析 → 获取 IP
      ↓
3. TCP 三次握手建立连接
      ↓
4. 发送 HTTP 请求
      ↓
5. 服务器返回 HTML 文档
      ↓
6. 浏览器解析 HTML，构建 DOM 树
      ↓
7. 解析 CSS，构建 CSSOM 树
      ↓
8. DOM + CSSOM → 合并为 Render Tree（渲染树）
      ↓
9. Layout（布局/回流）：计算元素位置和大小
      ↓
10. Paint（绘制）：将像素绘制到屏幕
      ↓
11. Composite（合成）：图层合并，最终显示
```

**关键概念**：
- **DOM（Document Object Model）**：HTML 的内存树形表示，JS 可操作的对象结构
- **CSSOM（CSS Object Model）**：CSS 规则的树形表示
- **Reflow（回流/重排）**：元素尺寸、位置变化时，重新计算布局（性能开销大）
- **Repaint（重绘）**：颜色、背景等不影响布局的属性变化，只需重新绘制

---

## 十、JavaScript 异步编程

AJAX 的 "A" 就是 Asynchronous（异步），JS 是**单线程**的，通过事件循环实现异步。

### 三种异步写法演进

```javascript
// 1. 回调函数（Callback）— 容易形成"回调地狱"
getData(function(a) {
  getMoreData(a, function(b) {
    getMoreData(b, function(c) {
      console.log(c);  // 嵌套太深，难以维护
    });
  });
});

// 2. Promise（ES6）— 链式调用，更清晰
getData()
  .then(a => getMoreData(a))
  .then(b => getMoreData(b))
  .then(c => console.log(c))
  .catch(err => console.error(err));

// 3. async/await（ES2017）— 同步写法，异步执行，最推荐
async function fetchData() {
  try {
    const a = await getData();
    const b = await getMoreData(a);
    const c = await getMoreData(b);
    console.log(c);
  } catch (err) {
    console.error(err);
  }
}
```

---

## 十一、前后端数据交互格式

### JSON（JavaScript Object Notation）

现在前后端几乎都用 JSON，取代了早期的 XML。

```javascript
// JSON 格式（键必须用双引号）
{
  "name": "张三",
  "age": 25,
  "isStudent": false,
  "hobbies": ["读书", "游泳"],
  "address": {
    "city": "北京",
    "zip": "100000"
  }
}

// JS 对象 ↔ JSON 字符串 转换
const obj = { name: "张三", age: 25 };
const jsonStr = JSON.stringify(obj);   // 对象 → JSON字符串
const parsed = JSON.parse(jsonStr);      // JSON字符串 → 对象
```

### 请求 Content-Type

| 类型 | 用途 | 示例 |
|------|------|------|
| `application/json` | 发送 JSON 数据 | `{"name":"张三"}` |
| `application/x-www-form-urlencoded` | 表单数据（键值对）| `name=张三&age=25` |
| `multipart/form-data` | 上传文件 | 包含 boundary 分隔符 |
| `text/plain` | 纯文本 | 简单字符串 |

---

## 十二、CSS 选择器优先级

你提到 `class` 和 `id`，它们的优先级不同：

```
优先级权重（从高到低）：

!important        → 最高，强制覆盖（尽量少用）
内联样式 style="" → 权重 1000
#id               → 权重 100
.class / [attr]   → 权重 10
标签名 div / p    → 权重 1
* 通配符          → 权重 0
继承样式          → 权重最低
```

**计算示例**：
```css
#nav .menu li a { color: red; }   /* 100 + 10 + 1 + 1 = 112 */
.nav li a:hover { color: blue; }  /* 10 + 1 + 1 + 10 = 22 */
```

---

## 十三、CSS 布局基础

### 1. 标准文档流

块级元素从上到下排列，行内元素从左到右排列。

### 2. 脱离文档流的方法

```css
.float-left { float: left; }      /* 浮动 — 文字环绕效果 */
.position-abs { position: absolute; }  /* 绝对定位 — 相对于最近定位祖先 */
.position-fix { position: fixed; }     /* 固定定位 — 相对于视口 */
```

### 3. Flex 布局（最常用）

```css
.container {
  display: flex;           /* 开启 Flex 布局 */
  flex-direction: row;      /* 主轴方向：row（默认）| column */
  justify-content: center;  /* 主轴对齐：flex-start | center | flex-end | space-between | space-around */
  align-items: center;      /* 交叉轴对齐：stretch（默认）| center | flex-start | flex-end */
  flex-wrap: wrap;          /* 是否换行：nowrap（默认）| wrap */
}

.item {
  flex: 1;                  /* 占据剩余空间的比例 */
  flex-shrink: 0;           /* 是否允许压缩：0 不允许 */
}
```

### 4. Grid 布局（二维布局）

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 2fr;  /* 三列：固定200px、1份、2份 */
  grid-template-rows: 100px auto;         /* 两行：固定100px、自适应 */
  gap: 20px;                              /* 网格间距 */
}
```

---

## 十四、浏览器存储

| 特性 | Cookie | localStorage | sessionStorage |
|------|--------|--------------|----------------|
| 容量 | ~4KB | ~5-10MB | ~5-10MB |
| 生命周期 | 可设置过期时间 | 永久（除非手动清除）| 关闭标签页即清除 |
| 服务端读取 | ✅ 随请求自动发送 | ❌ 仅客户端 | ❌ 仅客户端 |
| 用途 | 身份认证（token）| 持久化配置、缓存 | 临时数据 |

```javascript
// localStorage 用法
localStorage.setItem('username', 'admin');
const user = localStorage.getItem('username');
localStorage.removeItem('username');
localStorage.clear();  // 清空所有
```

---

## 十五、Node.js 后端基础

```javascript
// 最简单的 HTTP 服务器
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({ message: 'Hello World' }));
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```

**Express 框架（更常用）**：
```javascript
const express = require('express');
const app = express();

// 中间件：解析 JSON 请求体
app.use(express.json());

// 路由
app.get('/users', (req, res) => {
  res.json([{ id: 1, name: '张三' }]);
});

app.post('/users', (req, res) => {
  const { name } = req.body;
  res.status(201).json({ id: 2, name });
});

app.listen(3000);
```

---

## 十六、开发工具链

| 工具 | 用途 |
|------|------|
| **VS Code** | 代码编辑器（插件丰富）|
| **Chrome DevTools** | 调试 HTML/CSS/JS、网络请求、性能分析 |
| **Postman / Apifox** | API 接口测试工具 |
| **Git** | 版本控制 |
| **npm / yarn / pnpm** | 包管理器 |
| **Webpack / Vite** | 构建工具（打包、转译、优化）|
| **Nginx** | Web 服务器、反向代理、负载均衡 |

---

## 十七、学习路径建议

```
第一阶段：基础
  HTML → CSS → JavaScript（ES6+）

第二阶段：前端框架
  Vue 或 React → 组件化 → 状态管理 → 路由

第三阶段：后端
  Node.js → Express → 数据库 → RESTful API

第四阶段：工程化
  Git → Webpack/Vite → 测试 → CI/CD

第五阶段：进阶
  TypeScript → 性能优化 → 安全 → 微服务
```

---

还有什么想深入的方向？比如 **Vue/React 框架原理**、**数据库设计**、**部署上线**、或者 **TypeScript**？