# 生物医学工程课程流程图

一个可交互的多院校生物医学工程课程流程图，用于展示八学期安排及课程之间的先修、共修和后续依赖关系。

> 本项目是对课程流程图交互方式的独立复现，仅用于学习、展示和产品原型验证，不是任何院校的官方选课工具。课程要求、课程替代和毕业审核请以学校最新目录及学业导师意见为准。

## 功能

- 可在纽约州立大学布法罗分校和上海交通大学两个培养方案之间切换
- 展示八个学期的推荐课程安排、学分和课程性质
- UB 支持新生、转学生和衔接转学三种视图
- 上海交大支持完整路径、必修主干、选修与方向、WSU 风格先修关系图四种视图
- WSU 风格视图按课程类别配色；默认隐藏关系线，选中课程后使用 SVG 动态避障最短折线展示相关先修与共修关系
- 在先修关系图中点击课程，可突出显示 PRE、CO 及它解锁的后续课程
- 鼠标悬停课程时临时预览依赖关系
- 点击课程后固定高亮，再次点击或点击“清除高亮”可取消
- 展示课程的直接先修、完整先修链、共修及后续课程
- 响应式布局，可在桌面和移动设备上使用

## 颜色含义

| 颜色 | 含义 |
| --- | --- |
| 深蓝色 | 当前选中的课程 |
| 浅绿色 | 完整先修课程链 |
| 深绿色 | 直接先修课程 |
| 浅紫色 | 共修关系链 |
| 深紫色 | 直接共修课程 |
| 深青色 | 后置共修课程 |
| 浅蓝色 | 后续课程链 |
| 半透明灰色 | 与当前课程没有直接依赖关系 |

## 如何启动

项目不使用框架，也不需要安装依赖。页面所需的 HTML、CSS、JavaScript 和课程数据都包含在 `dist/index.html` 中。

### 方法一：直接打开

下载或克隆项目后，进入 `dist` 文件夹，双击 `index.html` 即可。

如果浏览器限制本地文件运行，请使用下面的本地服务器方式。

### 方法二：使用 Python 启动本地服务器（推荐）

macOS 或 Linux：

```bash
cd ub-course-flowsheet
python3 -m http.server 8000 --directory dist
```

Windows：

```powershell
cd ub-course-flowsheet
py -m http.server 8000 --directory dist
```

然后在浏览器打开：

```text
http://localhost:8000
```

按 `Ctrl + C` 可以停止服务器。

### 方法三：使用 VS Code Live Server

1. 用 VS Code 打开项目文件夹。
2. 安装 **Live Server** 扩展。
3. 右键点击 `dist/index.html`。
4. 选择 **Open with Live Server**。

## 部署到 GitHub Pages

仓库已包含 `.github/workflows/pages.yml`。它会在 `main` 分支更新后，把 `dist` 文件夹自动发布到 GitHub Pages。

首次启用：

1. 打开 GitHub 仓库的 **Settings**。
2. 在左侧选择 **Pages**。
3. 在 **Build and deployment** 中，将 **Source** 设为 **GitHub Actions**。
4. 打开仓库的 **Actions** 页面，等待 `Deploy static site to GitHub Pages` 工作流完成。
5. 返回 **Settings → Pages** 查看公开网址。

以后每次向 `main` 分支提交修改，网站都会自动重新发布。

## 项目结构

```text
ub-course-flowsheet/
├── .github/
│   └── workflows/
│       └── pages.yml       # GitHub Pages 自动部署
├── dist/
│   └── index.html          # 完整网页和课程数据
├── .gitignore
└── README.md
```

## 修改课程数据

课程数据位于 `dist/index.html` 底部 `<script>` 中的 `ubCourses` 和 `sjtuCourses` 数组。每门课程使用以下结构：

```javascript
C('课程代码', '课程名称', 学分, 学期, ['先修课程'], ['共修课程'], '课程说明', '课程性质')
```

例如：

```javascript
C('MTH 142', '微积分 II', 4, 2, ['MTH 141'])
```

修改后刷新浏览器即可看到结果。若已启用 GitHub Pages，提交并推送到 `main` 分支后会自动更新线上页面。

## 技术栈

- HTML5
- CSS3
- 原生 JavaScript
- GitHub Actions / GitHub Pages

项目没有第三方运行时依赖，也不需要数据库或后端服务。

## 数据与使用说明

- UB 课程安排基于公开课程流程图整理。
- 上海交大课程名称、代码、学分、性质和建议学期来自《2025年级生物医学工程专业课程设置一览表》。
- 上海交大培养方案 PDF 没有给出完整先修课程表，页面中的先修、共修及后续关系为根据课程内容和建议学期推定的演示数据。
- WSU 风格视图是对横向课程关系图交互方式的独立复现，不包含 WSU 课程数据或原站源码。
- 不保证课程编号、先修要求、学分或开课学期持续有效。
- 请勿将本项目作为正式选课或毕业审核的唯一依据。
