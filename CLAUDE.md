# CLAUDE.md

本文件为 Claude Code 在本仓库工作时提供项目指引，每个 session 会全量进入上下文。

> **常规入口是 `../mockspark-dashboard`。** Claude Code 的项目级配置按**启动目录**解析：
> 从 dashboard 启动时，本仓库的 `.claude/settings.json` **不会**被加载，权限策略与 Supabase MCP 都由
> dashboard 的 `.claude/settings.json` 和 `.mcp.json` 提供（MCP 全工作区只定义那一份，避免多处漂移）。
> 本仓库的 `.claude/settings.json` 只在直接 `cd` 进来开会话时生效，作为兜底策略；那种情况下没有 Supabase MCP。
> 多仓配置分工见 `../mockspark-dashboard/docs/claude-multi-repo-setup.md`。

## 回复语言（务必遵守）

始终用**简体中文**回复用户，除非用户在当轮明确要求其他语言。禁止无故切换到日语或其他语言，包括结尾句、客套句、过渡句在内的每一句都必须是简体中文。

注意区分两件事：**跟用户沟通用中文，写进文档站的正文一律用英文**（站点面向海外商家，现有文档全部是英文）。

## 工作边界（务必遵守）

- 可以读取、修改和暂存项目文件，但不要执行 `git commit`、`git push` 或任何发布操作，除非用户在当前轮次明确授权。此仓库推送到默认分支会自动发布到生产。
- `git restore`、`checkout`、`switch`、`merge`、`rebase`、`stash`、`reset`、`clean`、删除重要文件、安装或卸载依赖，也必须先得到当前轮次的明确授权。
- 不清理、轮换、验证、迁移或重组现有凭据和生产配置；不要把凭据写进 `CLAUDE.md` 或 `.claude/`。
- 仓库文件是项目知识的唯一协作来源。本机会话记忆（`~/.claude/projects/*/memory/`）只是个人便签，任何需要别人或下一个 session 知道的结论，必须落到仓库里的 `CLAUDE.md` 或文档中。

## 这个仓库是什么

Mockspark 的**帮助中心**，线上地址 `help.mockspark.com`。用 Mintlify 搭建，内容是一堆 `.mdx` 文件。

它不是内部文档，是公开站点。Dashboard 前端（`../mockspark-dashboard`）的页脚、以及编辑器各面板的「文档」链接都指向这里，通过 `NEXT_PUBLIC_DOCS_HOST` 引用。改动会直接被商家和平台审核人员看到。

Mockspark 整体是一个 POD（print-on-demand）/ Mockup 生成 + 多销售平台电商 SaaS，销售平台支持 Shopify 和 Etsy，下游接 Printful / Printify 及私有履约。完整的全栈结构见 `../mockspark-dashboard/CLAUDE.md`。

## 写给谁看（最重要的一节）

每一篇文档都有**两类读者**，写的时候要同时照顾：

1. **使用 App 的商家。** 他们不懂技术，也不想懂。他们只想把眼前这件事办成：把店连上、把商品发出去、把订单发给工厂。
2. **第三方平台的审核人员。** 我们向 Etsy、Shopify 这类平台申请 App 上架或公开权限时，审核人员会拿帮助中心当作了解这个 App 的入口。他们要在几分钟内看明白：这个 App 到底做什么、要了哪些权限、数据怎么流转、有没有踩平台规则。

怎么兼顾：**正文按商家的视角写**，一步一步教他做事。凡是涉及**平台权限、数据去向、平台规则**的地方，顺手补一两句说明，让审核人员不用来问就能看懂。比如讲连接 Etsy 店铺时，顺带说清楚我们会读取哪些信息、用来做什么。这些话对商家也有用，不算给审核人员开小灶。

不要为了讨好审核人员写一篇专门的「合规说明页」，那样商家看着别扭，审核人员也会觉得是临时糊的。信息应该自然地长在正常文档里。

## 文案要求

### 语气

写得像一个懂行的同事在旁边带着做，不是像产品手册，更不能像 AI 生成的。

- 用 **you**，主动语态，短句。一句话说一件事。
- 先说**做什么**，再说**为什么**。商家赶时间的时候只看前半句就够了。
- 承认麻烦的地方。某一步确实繁琐或者容易出错，直说，别粉饰。商家卡住时看到「这一步有点绕」会踏实，看到「Simply click」会火大。
- 平台的规则和我们的功能要分清楚。是 Etsy 要求的就说是 Etsy 要求的，不要让商家以为是我们在为难他。

### 少用破折号

**不到万不得已不要用破折号**（`—` 或 `--`）。它是 AI 文风最明显的标志之一。

大多数破折号都能拆成两句话，或者换成逗号、冒号、括号。写完扫一遍，看到破折号就先想想能不能去掉。

### 别用这些词

营销腔和 AI 高频词，一律避开：

`seamlessly`、`effortlessly`、`unlock`、`leverage`、`utilize`、`robust`、`powerful`、`elevate`、`streamline`、`empower`、`in today's fast-paced world`、`whether you're X or Y`、`it's worth noting that`、`dive into`

也别用 `simply`、`just`、`easy`、`quick` 去形容操作步骤。它对顺利走通的人是废话，对卡住的人是挖苦。

不要用 emoji。

### 别写做不到的事

审核人员会照着文档去核对功能。文档说有的功能，App 里必须真的有，行为必须一致。功能还没上线就先别写，或者明确标注。

### 现有文风参考

`docs/connections/printify.mdx` 和 `docs/connections/printful.mdx` 是目前写得最完整的两篇，新文档照它们的结构和语气走。存量文档里有一些营销腔的句子（比如 introduction 里的 "Effortlessly create stunning..."），那是早期写的，不要拿来当范本，也不用专门去改。

## 图片规范

### 引用方式

图片放在 `images/` 下，按**文档的分组和页面**建子目录，路径与 `docs/` 对应：

```
docs/connections/printful.mdx   ->   images/connections/printful/
docs/products/products.mdx      ->   images/products/products/
docs/billing/credit.mdx         ->   images/billing/credit/
```

正文里用**以 `/` 开头的绝对路径**引用，不要用相对路径，并且用 `<Frame>` 包起来：

```mdx
<Frame>
  <img src="/images/connections/etsy/connect-shop.png" alt="Connecting an Etsy shop" />
</Frame>
```

习惯是**先写文字，图跟在它说明的那句话下面**，不要图在前文字在后。

存量截图的文件名是截图工具自动生成的（`PixPin_2025-05-06_12-04-21.png`），看不出内容。**新增图片请用语义化文件名**，比如 `connect-shop.png`、`production-partner-empty.png`，以后要替换某张图时能一眼找到。

`alt` 属性存量文档大多没写，新写的请补上，对无障碍和 SEO 都有用。

### 需要配图时怎么办

**不要自己编造图片路径然后当作图片已经存在。** 用户会亲自去截图或制作图片。

需要配图的位置，在正文里插入一条 MDX 注释占位，格式固定：

```mdx
{/* IMAGE-TODO | 路径: /images/connections/etsy/connect-shop.png | 内容: Etsy 连接页，鼠标停在 "Connect Etsy shop" 卡片上 */}
```

MDX 注释不会渲染到页面上，所以即使先合并也不会露馅。

然后**在回复用户时列一份清单**，逐条写清楚：文件应该放在哪个路径、这张图要拍什么内容、页面上要重点圈出什么。用户照着清单去截图，截完把文件丢进对应目录，再把占位注释换成 `<Frame>` 块。

## 技术方案与目录结构

### 技术栈

[Mintlify](https://mintlify.com)，一个托管式文档站服务。仓库里只有内容和配置，没有前端代码，没有构建产物，也没有 `package.json`。Mintlify 负责渲染、搜索、主题和部署。

### 配置文件 `docs.json`

站点的唯一配置入口，遵循 `https://mintlify.com/docs.json` 这份 schema。当前配置要点：

- `theme`: `maple`
- `name`: `MockSpark Help Center`
- `colors`: 主色 `#16A34A`（绿）
- `appearance`: `{ "default": "dark", "strict": true }`，即**只有深色模式**，写文档时不用考虑浅色适配
- `icons.library`: `lucide`，frontmatter 里的 `icon` 只能用 [Lucide](https://lucide.dev/icons/) 的图标名
- `navigation`: 按销售平台拆成 **Shopify** 和 **Etsy** 两个 dropdown，各自下分若干 group。共用页（`products/*`、`connections/printify`、`connections/printful`、`marketing/picture-collections`、`team/team-management`）在两个 dropdown 里各登记一次
- `navbar` / `footer`: 顶部 Support 邮箱与 Dashboard 按钮、底部官网与 YouTube 链接

### ⚠️ 新增页面必须登记到 navigation

Mintlify **不会**自动收录 `docs/` 下的文件。新建 `.mdx` 之后，必须同时把它的路径（不带 `.mdx` 后缀）加进 `docs.json` 的对应 `group.pages` 数组，否则文件在仓库里躺着，站上却没有任何入口。

这是这个仓库最容易踩的坑。目前就有一批文件因为漏登记而访问不到：

- `docs/connections/workflow.mdx`
- `docs/products/mockup-creator.mdx`
- `docs/team/account-settings.mdx`
- `docs/get-started/todo.mdx`、`docs/get-started/installation-guide.bak.mdx`（这两个像是草稿和备份）

另外 `api-reference/`、根目录的 `quickstart.mdx` 和 `development.mdx`、以及 `snippets/` 里的示例，都是 Mintlify starter kit 的模板残留，没有登记也不属于我们的内容。**不要照着它们的写法写正式文档。**

同一个坑还有一种更隐蔽的形式：**文件登记了，但只登记进了一个 dropdown**。**新增或调整共用页时，记得两个 dropdown 都要过一遍。**

### ⚠️ Etsy 商家目前没有计费文档（未解决）

2026-08-23 核对时发现 Etsy dropdown 缺整个 Payment and Billing 组和 `order-items/troubleshooting`。平台中立的两篇（`order-items/troubleshooting`、`billing/usages`）已补登记，但**另外三篇不能直接复用**：

| 文件 | 问题 |
| --- | --- |
| `billing/subscription-plans.mdx` | 通篇写 Shopify Billing：Shopify 收费确认页、「卸载 App 自动取消订阅」、开发店免费试用 |
| `billing/credit.mdx` | 「All credit purchases are still processed through Shopify Billing」 |
| `billing/purchases.mdx` | 让商家去 **Shopify Admin → Settings → Billing** 查账单 |

**Etsy 宇宙的计费走 Stripe，不走 Shopify Billing**（Checkout、Customer Portal 取消、invoice 续费，逐条差异见 `../mockspark-dashboard/docs/billing-universes-reference.md`）。把这三篇挂到 Etsy 下会给 Etsy 商家错误指引，比没有更糟。

正确做法是**另写 Stripe 版的三篇**，或者把现有三篇改写成双平台分段。另外注意：Stripe 侧当时仍是沙箱模式、注册入口未开放，写之前先确认线上已切正式，否则会违反本文「别写做不到的事」那条。

### 目录结构

```
docs.json              站点配置与导航（改动页面结构必须同步改这里）
docs/                  正文
  get-started/         introduction、installation-guide、quickstart
  connections/         销售平台与履约平台的接入文档
  products/            建品、建模、Personalizer
  order-items/         订单与履约、故障排查
  marketing/           图集等营销功能
  billing/             订阅、余额、用量、消费记录
  team/                团队与账号
images/                截图，子目录与 docs/ 结构对应
logo/                  站点 logo（light.png / dark.png）
snippets/              starter kit 残留，未使用
api-reference/         starter kit 残留，未使用
README.md              starter kit 自带的说明，内容与本项目关系不大
```

### 页面 frontmatter

每篇 `.mdx` 开头固定三个字段：

```mdx
---
title: Printful
description: "Seamlessly link your Printful store to streamline fulfillment"
icon: "link"
---
```

- `title`: 侧边栏和页面 H1 显示的标题，Title Case
- `description`: 一句话说明，会用于页面副标题和搜索结果
- `icon`: Lucide 图标名

**正文里的标题从 `##` 开始**，因为 `title` 已经渲染成 H1 了。`docs/get-started/installation-guide.mdx` 用了 `#`，那是个例外，不要跟着学。章节标题用 Title Case，和现有文档保持一致。

### 常用组件

Mintlify 内置组件，直接写在 mdx 里，不用 import。仓库里已经在用的（按使用频率）：

| 组件 | 用途 |
| --- | --- |
| `<Frame>` | 包裹截图，几乎每张图都用 |
| `<Warning>` | 会造成损失或不可逆的提醒，比如 token 只显示一次 |
| `<Tip>` | 锦上添花的小建议 |
| `<Info>` / `<Note>` | 补充说明 |
| `<Card>` / `<CardGroup>` | 导航卡片，用在 introduction 这类索引页 |
| `<Accordion>` / `<AccordionGroup>` | 折叠内容，用在 FAQ 和排错 |
| `<CodeGroup>` | 多语言代码块 |

别为了显得丰富而堆组件。一段普通的文字能说清楚，就用普通文字。

### 品牌名写法

仓库里 `Mockspark` 和 `MockSpark` 两种写法都有（44 : 37），历史遗留。**新写的内容统一用 `Mockspark`**，与 Shopify 应用商店里的 App 名称 `Mockspark Product Personalizer` 一致。存量的不用专门去改。

## 常用命令

```bash
# 安装 Mintlify CLI（全局，只需一次）
npm i -g mint

# 本地预览，必须在 docs.json 所在目录运行
mint dev

# CLI 版本过旧导致预览起不来时
mint update
```

注意 CLI 命令是 `mint`，不是旧版的 `mintlify`。仓库最近一次迁移就是干这个（commit `dacfce1`）。

页面 404 一般是两个原因：没在 `docs.json` 里登记，或者不在 `docs.json` 所在目录运行 `mint dev`。

## 部署

装了 Mintlify 的 GitHub App，**推送到默认分支（`master`）后自动部署到生产**。没有预发环境。

也就是说，合并即发布。改动前先 `mint dev` 在本地看一眼，尤其是有图片和组件的页面。

仓库：`git@github.com:rokeyzki/mockspark-docs.git`

## 提交约定

用户**手动提交和部署**。改完文件后只做 `git add` 暂存，**不要 `git commit`**，除非用户明确要求。
