# Fiction Site Builder

一个 Claude Code Skill，用于**从 0 生成小说内容并构建移动优先的 H5 阅读站点**。输入一个题材或一句需求，输出完整的小说章节、封面、插图以及一个基于 Next.js 的静态阅读站。

---

## 目录

- [它能做什么](#它能做什么)
- [核心设计](#核心设计)
- [工作原理](#工作原理)
- [安装与启用](#安装与启用)
- [使用方法](#使用方法)
- [项目结构](#项目结构)
- [环境依赖](#环境依赖)
- [命令速查](#命令速查)
- [注意事项](#注意事项)

---

## 它能做什么

| 用户说的话 | 技能行为 |
|---|---|
| "写一本长篇 romance 小说" | Phase 0 → A0  niche 研究 → A1 长篇章节写作 → A3 去 AI 味质量 pass |
| "给我做一个小说 H5 站" | 完整 pipeline：内容 + 站点并行构建 |
| "继续写第 3 本书" | 定位现有项目，继续 A1 长篇章节 |
| "生成封面" / "Generate covers" | A2 单阶段：为所有书并行生成封面 |
| "加插图" / "Add illustrations" | A2.5 单阶段：为长篇书生成 5–7 张插图 |
| "导入我的手稿" | A1 import 模式：拆分章节、重建 outline/world/tracking |
| "审校一下 prose" | A3 审校阶段 |
| "只做站点" | B1 → B6 站点构建轨道 |

适用：

- 长篇连载小说、短篇故事
- 移动优先的小说阅读站 / web novel H5
- 多语言站点（英/西/日/韩等）

不适用：

- 作者后台、排行榜、书架平台
- 读者社区、评论、支付、订阅系统
- 这些功能只有用户明确请求时才会加入

---

## 核心设计

### 三个核心目标

1. **内容优先**：每句话都服务于情绪、剧情或角色；发布前必须去掉 AI 味。
2. **产品可用**：站点在移动设备上加载快、阅读舒服、转化路径清晰。
3. **阅读舒适优先于视觉复杂**：固定且优质的排版胜过一堆可能出问题的阅读器控件。

### 内容即站点

小说文件放在项目根目录的 `content/` 下：

```
content/{book-title}/chapters/ch-001-{title}.md
```

`next dev` / `next build` 会自动通过 `@content-collections` 读取并生成类型化集合。添加新书 = 新建目录 + 写章节 + 重新构建。

---

## 工作原理

技能把一次完整构建拆成 **Phase 0 + 双轨（Track A 内容 + Track B 站点）**，两轨在 Phase 0 之后并行跑。

```
Phase 0  Setup
    │
    ├─→ Track A 内容
    │     A0  Niche Research
    │     A1  Write（长/短/导入）
    │     A2  Cover
    │     A2.5 Illustrations（自动）
    │     A3  Quality Pass（自动）
    │
    └─→ Track B 站点
          B1  Stack
          B2  Design
          B3  Data
          B4  Build
          B5  Performance
          B6  QA
```

### Phase 0 — Setup

只在项目不存在时运行：

- 创建目录结构与命名约定
- 创建 GitHub 私有仓库
- 在父仓库注册为 submodule（路径按你的实际项目配置）

### Track A — 内容轨道

| 阶段 | 名称 | 产出 |
|---|---|---|
| A0 | Niche Research | `outputs/{site}/{book}/niche-research.json` |
| A1 | Write | 章节、大纲、世界观、tracking 文件 |
| A2 | Cover | `public/covers/{book-title}.webp` + `.json` |
| A2.5 | Illustrations | `public/illustrations/{book-slug}/ch-{NNN}.webp` |
| A3 | Quality Pass | 审校报告、去除 AI 味 |

- **A1 有三种模式**：长篇（long-form）、短篇（short-form）、导入（import），每会话只能选一种。
- **A3 对长篇自动运行**，不是可选项。
- **A2.5 在完整 pipeline 中自动运行**，无需用户主动要求。

### Track B — 站点轨道

| 阶段 | 名称 | 产出 |
|---|---|---|
| B1 | Stack | 技术栈与一句话理由 |
| B2 | Design | 视觉调性、配色、字体、logo、favicon |
| B3 | Data | content-collections schema |
| B4 | Build | 完整站点：首页、书目、详情、阅读页、sitemap、robots、llms.txt |
| B5 | Performance | Core Web Vitals、图片优化、广告 CLS/懒加载 |
| B6 | QA | Lighthouse、政策合规、截图验证 |

- B1 → B2 → B3 → B4 顺序执行。
- B5 与 B6 共享一次 `pnpm run build`，并行检查。
- B4 开始前必须至少有一本书 ≥ 10 章。

### 静态生成（SSG）

- 所有书目、章节路由使用 `generateStaticParams` 预渲染。
- 运行时不再读取文件系统。
- 章节内容按路由拆分，不会一次性打包。
- 滚动到 80% 深度时 `router.prefetch()` 预加载下一章。

---

## 安装与启用

### 推荐：配合 `CLAUDE.md` 使用

这个 Skill 默认使用作者的个人配置（GitHub 账号、父仓库路径、参考站点等）。**建议在你的项目根目录创建 `CLAUDE.md`**，用你自己的值覆盖默认配置，例如：

```markdown
# 项目级覆盖

- GitHub owner: `{your-github-username}`
- 父仓库路径: `{/path/to/your/fictions-parent}`
- 参考站点: `{your-reference-site}`
```

Claude Code 会同时读取 Skill 的 `SKILL.md` 和项目 `CLAUDE.md`；当两者冲突时，**以当前项目 `CLAUDE.md` 为准**。

### 方式一：手动 clone

**安装到 Claude Code 全局 Skills（所有项目可用）：**

```bash
git clone https://github.com/zisheng-ai/fiction-site-builder.git \
  ~/.claude/skills/fiction-site-builder
```

**安装到当前项目（仅该项目可用）：**

```bash
mkdir -p .claude/skills
git clone https://github.com/zisheng-ai/fiction-site-builder.git \
  .claude/skills/fiction-site-builder
```

### 方式二：通过 `npx skills` 安装

**全局安装：**

```bash
npx skills install fiction-site-builder --global
```

**安装到当前项目：**

```bash
npx skills install fiction-site-builder
```

### 注册与加载

Claude Code 会自动发现以下位置的 Skill：

- `~/.claude/skills/{skill-name}/`
- `{project-root}/.claude/skills/{skill-name}/`

本 Skill 的元数据定义在 `SKILL.md` 头部：

```yaml
---
name: fiction-site-builder
description: write fiction and build the reading site end-to-end...
---
```

启用后，Claude Code 会根据用户提问自动判断是否调用此 Skill。

### 环境变量

封面、logo、favicon 生成需要：

```bash
export APIYI_API_KEY=your_key_here
```

如果未设置，技能会跳过图片生成并发出警告，不会使用 SVG 占位图上线。

---

## 使用方法

### 完整 pipeline（新站）

```
用户：帮我做一个 werewolf 题材的阅读站
Claude：开始 Phase 0 → Track A + Track B 并行
```

新站默认生成 **5 本书**，每本书独立随机采样高需求题材。A0 五本书并行，A1 五本书并行。

### 完整 pipeline（现有站追加书）

```
用户：在这个站再加一本 vampire romance
```

技能会跳过 Phase 0，直接为单本书跑 A0 → A1 → A2 → A2.5 → A3，然后更新站点数据与页面。

### 单功能触发

可以直接用 slash 命令或自然语言触发单阶段：

| 需求 | 触发 |
|---|---|
| 生成长篇小说 | `/story-long-write` 或 "继续写 xxx" |
| 生成短篇 | `/story-short-write` 或 "写个短篇" |
| 生成封面 | `/story-cover` 或 "生成封面" |
| 生成插图 | "Add illustrations" / "Generate illustrations" |
| 导入手稿 | `/story-import` |
| 审校 prose | `/story-review` 或 "审校一下" |
| 只构建站点 | "Build the site" |

### Scope-to-Phase 映射

| 用户意图 | 执行阶段 |
|---|---|
| "写小说" / "继续写" / `/story-long-write` | 0（如不存在）→ A1 长篇 → A3 |
| "写短篇" / `/story-short-write` | 0（如不存在）→ A1 短篇 |
| "新增一本书" | A1 长篇（单本）→ A2 |
| "生成封面" / `/story-cover` | A2 |
| "加插图" | A2.5 |
| "导入手稿" / `/story-import` | A1 import |
| "审校 prose" / `/story-review` | A3 |
| "完整建站" / full pipeline | 0 → Track A + Track B（A2.5 自动） |

---

## 项目结构

```
{site-name}/
├── README.md                         # 站点信息卡（中文）
├── TODO.md                           # 待办事项（中文）
├── content/                          # 所有小说内容
│   └── {book-title}/
│       ├── chapters/                 # ch-001-{title}.md ...
│       ├── world/                    # worldbuilding.md, characters/, map.md
│       ├── outline/                  # outline.md
│       └── tracking/                 # context.md, threads.md, timeline.md
├── public/
│   ├── covers/                       # {slug}.webp（每本书一张）
│   ├── illustrations/                # {book-slug}/ch-{NNN}.webp
│   ├── logo.png
│   ├── favicon-32x32.png
│   └── llms.txt                      # AI 爬虫 manifest
├── src/
│   ├── app/
│   │   ├── page.tsx                  # 首页：书目列表
│   │   ├── book/[slug]/page.tsx      # 书目详情
│   │   └── book/[slug]/chapter/[n]/page.tsx  # 章节阅读页
│   ├── components/
│   │   ├── BookCard.tsx
│   │   ├── ChapterNav.tsx
│   │   ├── ThemeToggle.tsx           # DaisyUI data-theme
│   │   └── IllustrationBlock.tsx
│   └── lib/
├── content-collections.ts            # @content-collections schema
├── next.config.ts
├── vercel.json
└── package.json
```

**读者不可见目录**：`outline/`、`world/`、`tracking/`、`reference/`、`resources/`、`teardowns/` 不会出现在任何路由或导航中。

---

## 环境依赖

### 必需

- Claude Code 会话（技能会首先验证 Bash 工具是否可用）
- Node.js + pnpm
- Git + GitHub CLI `gh`（用于创建私有仓库与 submodule）

### 可选但推荐

| 用途 | 变量/工具 |
|---|---|
| 封面 / logo / favicon 生成 | `APIYI_API_KEY` |
| 部署 | Vercel CLI 或 Vercel Git 集成 |

---

## 命令速查

开发站点：

```bash
pnpm dev
```

构建站点：

```bash
pnpm build
```

图片生成（由技能自动调用，也可手动验证）：

```bash
[ -n "$APIYI_API_KEY" ] && echo "ok" || echo "skip"
```

---

## 注意事项

### 质量红线（技能不会交付以下状态）

- 出现 lorem ipsum 或占位文本
- 移动端正文小于 17px
- 阅读页背景为纯白/纯黑或偏粉/玫瑰色
- 缺少 "Next →" 按钮或按钮高度不足 60px
- 阅读页出现 Previous 按钮
- 缺少目录按钮

### Pre-Launch Gate（上线前必须满足）

- ≥ 5 本书
- 每本书 10–20 章，且**任意两本书章节数不能相同**
- 每本书都有封面
- `outline/outline.md` 与 `world/worldbuilding.md` 存在且非空
- 长篇书在完整 pipeline 中应已生成插图

### 模型选择

- 所有小说内容生成通过 `Agent` 工具委托，使用 `haiku` 模型。
- 站点构建轨道继承当前会话模型，不强制覆盖。

---

## 参考文档

所有参考文档位于 `references/`，按阶段按需加载：

- `story-setup.md` — 项目初始化
- `story-long-write.md` — 长篇写作
- `story-short-write.md` — 短篇写作
- `story-import.md` — 手稿导入
- `story-review.md` / `story-deslop.md` — 审校与去 AI 味
- `story-cover.md` / `cover-styles.md` / `cover-allure-elements.md` — 封面
- `story-illustrations.md` — 插图
- `tech-stack.md` / `design-system.md` / `data-contract.md` — 站点基础
- `ui-components.md` / `reader-ux.md` — UI 与阅读体验
- `performance.md` / `qa-checklist.md` / `lighthouse-qa.md` — 性能与 QA
- `seo.md` / `geo.md` — SEO 与 AI 爬虫优化
- `vercel-operations.md` — 部署运维

---

## License

MIT License
