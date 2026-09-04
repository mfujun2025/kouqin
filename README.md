# 口琴.中国 网站部署说明

## 文件结构

```
kouqin-site/
├── index.html          # 首页（英雄区+课程亮点+大纲+购买+资讯预览）
├── news.html           # 口琴资讯列表页
├── about.html          # 关于我们
├── css/
│   └── style.css       # 全站样式
├── news/
│   ├── article1.html   # 口琴选购指南
│   ├── article2.html   # 压音技巧教学
│   ├── article3.html   # 口琴保养攻略
│   └── article4.html   # 经典曲目推荐
└── README.md           # 本说明文件
```

## 一、替换必要信息（部署前必做）

### 1. 替换面包多购买链接

全站所有 `https://mianbaoduo.com/o/你的商品ID` 都需要替换为你实际的面包多商品链接。

涉及文件：
- `index.html`（3处：导航栏、英雄区、购买区）
- `news.html`（1处：导航栏）
- `about.html`（2处：导航栏、联系我们）
- `news/article1.html` ~ `article4.html`（各1处：导航栏+文末推荐）

批量替换方法：用编辑器全局搜索 `你的商品ID`，全部替换为面包多商品的实际路径。

### 2. 课程内容与网盘实际内容对齐

首页的"课程大纲"（8个阶段）和"课程亮点"是按通用口琴教程结构写的。请对照你百度网盘里的实际内容，调整以下部分：
- `index.html` 中 `.curriculum-list` 里的8个阶段标题和子项
- `index.html` 中 `.features-grid` 的6个亮点描述
- `index.html` 中价格（当前写的¥49，根据实际定价修改）
- 视频数量、曲谱数量等数字（当前为60+视频、120+曲谱）

网盘链接：`https://pan.baidu.com/s/1XIzNGROZr4CN36tkK7Nq7w?pwd=3o8x`

> 建议：在面包多发布商品时，商品详情里放网盘链接和提取码。用户付款后面包多会自动显示内容，网站只负责引流到面包多。

## 二、部署到 GitHub Pages

### 方法一：网页上传（最简单）

1. 登录 GitHub，点击右上角 `+` → `New repository`
2. 仓库名填 `kouqin`（或任意名字），选 `Public`，点击创建
3. 在仓库页面点击 `uploading an existing file`
4. 把 `kouqin-site` 文件夹里的**所有文件和文件夹**（index.html、css/、news/、about.html、news.html）拖进去
5. 点击 `Commit changes`
6. 进入仓库 `Settings` → 左侧 `Pages`
7. `Source` 选 `Deploy from a branch`，`Branch` 选 `main`，文件夹选 `/ (root)`，点击 `Save`
8. 等待1-2分钟，网站即可通过 `https://你的用户名.github.io/kouqin/` 访问

### 方法二：Git 命令行

```bash
# 进入网站目录
cd kouqin-site

# 初始化git
git init
git add .
git commit -m "口琴.中国网站初始版本"

# 添加远程仓库（替换为你的仓库地址）
git remote add origin https://github.com/你的用户名/kouqin.git
git branch -M main
git push -u origin main
```

然后在 GitHub 仓库的 Settings → Pages 中开启 Pages 服务。

## 三、绑定中文域名 口琴.中国

### 1. 中文域名转 Punycode

中文域名需要转换为 punycode 格式才能在 DNS 中配置。

`口琴.中国` 的 punycode 是：
- `口琴` → `xn--5ps18l.cn` （实际以转换工具结果为准）
- `.中国` → `.xn--fiqs8s`

完整 punycode：`xn--5ps18l.xn--fiqs8s`

> 请用在线 punycode 转换工具（如 punycoder.com）确认准确值。

### 2. DNS 解析配置

在你的域名注册商（如阿里云、腾讯云、西部数码）处添加解析：

| 记录类型 | 主机记录 | 记录值 |
|---|---|---|
| CNAME | @ | 你的用户名.github.io |
| CNAME | www | 你的用户名.github.io |

> 注意：CNAME 记录的主机记录填 `@` 表示根域名（口琴.中国），填 `www` 表示 www.口琴.中国。

### 3. GitHub 仓库配置自定义域名

1. 在仓库根目录创建一个名为 `CNAME` 的文件（无后缀），内容写：
   ```
   口琴.中国
   ```
   （写中文域名即可，GitHub 会自动处理 punycode）

2. 或者在 Settings → Pages → Custom domain 中填写 `口琴.中国`，点击 Save。

3. 勾选 `Enforce HTTPS`（需等 DNS 生效后才能勾选）。

### 4. 等待生效

DNS 解析通常需要几分钟到几小时。生效后，访问 `口琴.中国` 即可打开网站。

## 四、面包多商品发布要点

1. 登录面包多（mianbaoduo.com），点击"创作"→"创建作品"
2. 作品类型选"资料"或"图文"
3. 标题：口琴零基础到精通全套教程
4. 定价：建议 ¥29-¥69（根据内容量定）
5. 付费内容里放：
   - 百度网盘链接：`https://pan.baidu.com/s/1XIzNGROZr4CN36tkK7Nq7w`
   - 提取码：`3o8x`
   - 解压密码（如有）
   - 学习交流群入群方式
6. 免费预览部分放课程介绍和目录
7. 发布后复制商品链接，替换网站中所有 `你的商品ID`

## 五、后续更新维护

- **新增资讯文章**：在 `news/` 目录下新建 `article5.html`，复制 article 模板修改内容，然后在 `news.html` 和首页的资讯预览区添加链接
- **修改价格**：全局搜索 `¥49` 替换
- **修改课程大纲**：编辑 `index.html` 中 `.curriculum-list` 部分
- **更新网盘链接**：在面包多后台修改商品内容即可，网站无需改动

## 六、SEO 优化建议

- 每个页面的 `<title>` 和 `<meta description>` 已填写，可根据实际内容微调
- 百度收录中文域名需要主动提交：登录百度搜索资源平台，提交网站
- 可在页面底部添加百度统计代码（在 `</body>` 前插入）
- 资讯文章持续更新有助于搜索引擎收录和排名
