# Stellar 2.0.0-rc.2 发布候选核查

> 核查日期：2026-09-07
> 发布基线：`2.0.0-rc.1`
> 候选版本：`2.0.0-rc.2`（`main` 最终工作树）

本页记录上一个公开 RC 到当前候选树的版本级净变化、迁移边界、文档覆盖与分发验证。它不累积逐任务记录，也不把已被最终实现替换的中间方案写成发布契约。

## 基线与审计方法

- 以 `git diff 2.0.0-rc.1..HEAD` 确定 5 个提交、34 个文件的最终差异，再沿默认配置、Schema、模型、模板、浏览器 Runtime 和 npm 包消费链核对。
- 配置迁移只面向公开 `2.0.0-rc.1` 树中存在的输入；不为未公开的中间候选保留别名、双读或自动转换。
- `_config.yml`、声明式 Schema、模型投影、`package.json` 和直接测试是机器契约；知识库和 CHANGELOG 解释当前用法与升级边界。

## 净变化覆盖

| 领域 | RC1 → RC2 最终状态 | 主要事实源 | 文档出口 |
| --- | --- | --- | --- |
| Profile 配置 | Notebook 列表、设置页和错误页专属配置收敛到 `profiles`；顶层根由 21 个收敛为 18 个 | `_config.yml`、`config-schema.js`、Page/Collection Model | 配置、安装、布局、Notebook 与错误页知识库 |
| 404 页 | 插图并入 `profiles.error.image`；新增默认关闭、可局部覆盖 Provider 的评论区 | `layout/404.ejs`、评论模型、Runtime Manifest | 错误页知识库、CHANGELOG |
| 可信注入 | 站点主题配置与页面 Front Matter 同时支持 `head_begin/head_end/body_begin/body_end` | Inject Schema、PageViewModel、head/shell 模板 | 配置与 Head/SEO 知识库、CHANGELOG |
| npm 依赖 | `hexo-front-matter` 成为直接依赖，源码配置与 `stellar new note` 不再依赖宿主传递依赖 | `package.json`、`package-lock.json`、`source-config.js` | CHANGELOG；行为由 tarball 集成门禁覆盖 |
| 项目入口与包元数据 | 中英文 README 同步重构，区分 npm、源码、Blueprint 与站点示例；增加包内图标并更新描述、关键词和作者字段 | `README.md`、`README_EN.md`、`assets/icon-v2-x512.webp`、`package.json` | README 本身、CHANGELOG |

## 迁移覆盖

`2.0.0-rc.1` 站点升级时需要进行以下直接移动或重命名：

| RC1 配置 | RC2 配置 |
| --- | --- |
| `notebook` | `profiles.notebook` |
| `settings.about` | `profiles.settings.about` |
| `error_page.image` | `profiles.error.image` |
| `profiles.notebook_index` | `profiles.notebooks` |
| `profiles.note_index` | `profiles.notebook` |

`profiles.note` 仍表示 Note 内容页，与新的 Notebook 列表页 `profiles.notebook` 是两个不同 Profile。RC1 字段不别名、不双读、不自动转换；结构化 Schema 会拒绝已移除路径，CHANGELOG 与配置知识库给出人工迁移目标。

## 文档覆盖

- `CHANGELOG.md` 仅陈述 RC1 到 RC2 的用户可见净变化与升级注意。
- 配置、安装、总览、页面路由、Notebook 和错误页知识库使用当前 18 个顶层根、13 个 Profile 及新路径。
- Head/SEO 知识库记录四个注入位置、字符串类型、站点在前／页面在后的合并顺序以及可信 HTML 边界。
- README 中英文内容保持同步，Blueprint 安装与站点示例保持独立信息架构。

## 验证命令

```sh
npm run release:check
npm run release:dry -- 2.0.0-rc.2
```

发布前以最终工作树和目标版本重跑同一 F3 门禁。本轮已取得的直接证据：

- lint、207 项单元测试、21 项 Contribution descriptor 和 Agent 文档引用检查通过。
- npm tarball 安装到 Post/Topic、Notebook、Wiki 和默认配置四个隔离站点；Doctor、生成、路由、搜索、HTTP 预览、HTML/CSS/JS 压缩与 Runtime ESM 保真通过。
- 首屏必载脚本相对 `1.44.0` 基线从 gzip 34,937 字节降为 22,601 字节，降幅 35.3093%，通过 30% 性能门槛。
- 知识库核查覆盖 62 页、936 个链接和 148 个配置引用。

## 发布维护

- `2.0.0-rc.2` 版本元数据由发布流程原子同步到 `package.json`、`package-lock.json` 与安装知识库；任一来源不一致或工作区存在无关改动时都在写入前失败。
- RC 使用 npm `rc` dist-tag，不替换无版本安装的 `latest` 入口。tag 使用不带 `v` 的纯版本号。
- 新增能力必须先进入对应 Schema／注册表的唯一事实源，再更新知识库与公开 Reference；不维护手写镜像清单。
