# Ane Personal Interests Space

《Ane Personal Interests Space》是一个聚合电影、音乐、游戏与关于我叙事的 Astro 静态站。

---

## 1. 项目定位
- 将分散在豆瓣、Steam、Bangumi等平台的记录统一呈现。
- 以 Astro 构建零后端、可长期维护的个人空间。
- 主页聚合 blog、兴趣矩阵、About me 三大模块。

## 2. 核心能力
- **内容整合**：支持 Markdown/MDX 手动内容与 JSON 数据的混合管理。
- **兴趣矩阵**：动漫、游戏、音乐、电影、剧集等主题拥有独立页面与统计标签。
- **自动同步**：Node.js 脚本在 GitHub Actions 中定时抓取外部平台。
- **持续部署**：推送到主分支即触发构建并发布至 GitHub Pages。
- **可扩展交互**：按需加载组件，提供筛选、搜索等轻量交互。

## 3. 系统架构
- **前端层**：Astro 负责路由、布局、内容渲染，默认输出静态 HTML。
- **内容层**：`content/` 保存 Markdown 叙事，`data/` 保存脚本生成的结构化条目。
- **同步层**：`scripts/` 中的 Node.js 程序连接外部 API，将数据转化为统一结构。
- **CI/CD**：`.github/workflows/` 包含同步与部署工作流，自动提交更新并发布站点。

## 4. 技术栈说明
| 模块 | 方案 | 职责 |
| --- | --- | --- |
| 前端框架 | Astro | 输出零 JS 静态页，支持多框架组件 |
| 内容格式 | Markdown / MDX | 承载长文、影评、博客内容 |
| 数据存储 | JSON | 描述电影/音乐/游戏条目的统一结构 |
| 样式层 | 原子化 CSS（UnoCSS）或自定义样式 | 构建卡片、时间轴等界面 |
| 自动化 | Node.js + GitHub Actions | 同步外部平台并部署 |
| 托管 | GitHub Pages | 发布静态资源，全球 CDN |

## 5. 目录职责
- `src/pages/`：定义首页、blog、movies、music、games、about 等路由。
- `src/components/`：存放筛选、搜索、卡片等 island 组件。
- `src/layouts/`：统一站点框架、元信息与全局样式。
- `content/`：人工维护的专题或长文。
- `data/`：自动生成的 JSON 数据源。
- `scripts/`：外部数据同步任务与聚合脚本。
- `public/`：图片、图标、静态资源。
- `.github/workflows/`：同步与部署流水线。

## 6. 数据模型
- 所有条目遵循 Item 结构，包含 `id`、`type`（movie/music/game/book/note）、`title`、`description`、`tags`、`rating`、`date`、`cover`、`externalUrl`、`source` 等字段。
- 同步脚本需要将外部数据映射到该结构，保证前端模板可复用。
- 列表页面和详情页面均基于同一数据模型渲染，便于统计与聚合。

## 7. 页面模块
- **首页**：Hero 区介绍项目愿景，展示 blog/interest/about 卡片与时间线。
- **/blog**：记录文章与长评，支持分类、标签、查看全部。
- **/movies /music /games**：对应兴趣主题的卡片栅格，可扩展筛选与搜索。
- **/interests**：统筹兴趣矩阵与统计信息。
- **/about**：展示个人背景、关注方向、年度节点。
- 可选页面：`/tags` 标签聚合、`/[type]/[id]` 详情页、RSS/活动记录等。

## 8. 同步与自动化
- 同步任务集中在 `scripts/`，覆盖豆瓣电影、Steam、GitHub 活动等来源。
- GitHub Actions 中的 `sync.yml` 定时执行同步，写入 `data/` 并提交回仓库。
- `deploy.yml` 监听主分支推送，安装依赖、构建 Astro、上传产物并发布到 GitHub Pages。
- Secrets 存储各平台 API Token，确保流水线无明文凭证。

## 9. 部署与运行
- 主分支推送即可触发构建与发布，输出站点地址为 `https://<github-username>.github.io/<repository-name>/`。
- `astro.config.mjs` 需配置 `site`、`base`、`output=static` 以适配 GitHub Pages。
- 本地可通过 `npm install` 与 `npm run dev` 启动 HMR 开发体验，实时查看 Markdown/JSON 更新效果。

## 10. 未来规划
- 用户活动统计：年度观影总数、周度听歌时长、游戏进度趋势。
- Bilibili 同步：自动拉取观看历史，生成多媒体档案。
- RSS 聚合：订阅外部博客与频道，集中展示更新。
- 主题系统：明暗色与多配色切换，覆盖站点所有组件。
- 数据可视化：引入 D3.js / Chart.js 呈现曲线与雷达图。
- 照片墙：以兴趣周边与生活摄影扩展内容维度。

## 11. 可选交付
1. 生成完整的 Astro 项目模板，含示例数据与基础组件。
2. 编写面向终端用户的 README，聚焦使用方法与常见任务。
3. 提供同步脚本的 TypeScript 版本，包含错误处理与速率限制。
4. 构建更多页面模块（卡片组件、筛选器、搜索组件等）。

该文档由 AI 提供，仅作为建站开始前的参考
