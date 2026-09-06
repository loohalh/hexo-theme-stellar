# Stellar v2 发布候选核查

> 核查日期：2026-09-07
> 发布基线：`1.44.0`
> 候选版本：`2.0.0-rc.1`（`main` 最终工作树）

本页记录最近公开 v1 到当前 v2 候选树的版本级净变化、文档覆盖与验证依据。它不累积开发期间逐任务记录，也不把已经被最终实现替换的候选字段、兼容分支或测试写成发布契约。

## 基线与审计方法

- 以 `git diff 1.44.0..HEAD` 和当前工作树确定最终文件集合，再从配置／内容生产者沿 Schema、模型、模板、浏览器 Runtime 和分发门禁核对消费链。
- 兼容范围只面向 `1.44.0` 发布树中真实存在的输入，以及仍有当前消费者的外部接缝。
- `_config.yml`、声明式 Schema、注册表、`package.json` 和测试是机器契约；知识库解释维护边界，公开 Wiki 提供用户任务与完整字段参考。
- 长期测试只保留架构、Schema、安全、Runtime、构建、迁移与分发契约；本次文档集合差异使用临时验收脚本，不把当前标题、顺序或文案固化进 CI。

## 净变化覆盖

| 领域 | 1.44.0 → v2 最终状态 | 主要事实源 | 文档出口 |
| --- | --- | --- | --- |
| 运行环境与分发 | Node.js >=22、Hexo >=8；Runtime 目录以原生 ESM 分发 | `package.json`、`source/js/runtime/`、包集成门禁 | 安装知识库、公开安装页、迁移指南 |
| 主题配置 | 21 个顶层配置根由声明式严格 Schema 管理；默认 YAML 与 Reference 由 Schema 生成 | `scripts/schema/config-schema.js`、`_config.yml` | 配置系统知识库、公开主题参考 |
| 内容配置 | Collection YAML 与 Front Matter 使用分组 Schema；未知字段、类型和枚举早失败 | `scripts/schema/content-config-schema.js` | 内容 Schema 知识库、Collection／Front Matter 参考 |
| 内容模型 | Post、Topic、Wiki、Notebook、Note 和索引页共用冻结的 Collection/PageViewModel | `scripts/lib/models/`、`scripts/filters/lib/page-view-model.js` | 内容系统知识库、内容指南 |
| 页面外壳 | Topbar、Leftbar、Rightbar Region；Brand、Menu、Widget、Footer 与 13 个 Profile | `_config.yml`、布局配置与 partial | 布局知识库、主题／Widget 参考 |
| 外观与交互 | 四种 preset、明暗模式、设计令牌、Reveal、Card Hover、Lightbox、数学与图表 | Appearance Schema、贡献注册表、CSS/ESM | 样式与 Extension 知识库、主题参考 |
| 搜索、评论与服务 | provider 配置与第三方 options 分离；数据服务和请求缓存按 Manifest 生命周期运行 | `contribution-registry.js`、`internal-constants.js` | 数据服务／评论知识库、主题参考 |
| 标签插件 | 公开目录完整列出 54 个名称／别名；新增 gist，移除 about/users，tip 改为单标签，quot 扩展直接图标／颜色 | `scripts/tags/index.js`、各 tag 实现 | 标签知识库、公开标签参考与迁移表 |
| Collection 行为 | Wiki Hero 支持三种效果；listed/searchable 分离；Collection 默认关闭分享，Notebook 级联统一 | Collection Schema、Hero 注册表、PageViewModel | Wiki／Notebook 知识库、Collection 参考 |
| CLI 与示例 | Doctor、new note；Blueprint 由 Examples 仓库维护 | `scripts/commands/stellar.js`、Examples catalog | 安装知识库、开始／Doctor／创建笔记指南 |
| 工程门禁 | lint、unit、复用、贡献、包集成、性能和知识库检查按风险分层 | `package.json`、`ci/`、`AGENTS.md` | 贡献指南、发布流程 |

## 迁移覆盖

公开迁移说明以 `1.44.0` 为入口，覆盖：

- 主题旧根、Profile、Region、Brand、Menu、Footer、内容默认值、Appearance、SEO、评论、搜索、标签与服务字段；
- Wiki、Topic、Notebook Collection 的身份、源码、路由、导航、列表、Region、Hero、可见性和受众字段；
- 页面归属、Banner、Article、Footer、评论 provider/options、渲染、SEO、菜单和可见性字段；
- 已移除标签、数据文件、适配器、内部资源路径、缓存策略及没有一对一替代项的处理；
- `poster` 等在 1.44.0 之前已移除的输入不重复伪装成 v2 专用兼容。

Schema 的 legacy 诊断映射与公开字段对照按同一基线核对：主题 13/13、Collection 35/35、Front Matter 38/38 均能回溯到 `1.44.0` 的声明或消费代码。`available` 映射为展示受众 `audience`，不再误写为可见性。浏览器 Runtime 的 request、copycode 与 toast 适配仍有当前消费者，因此保留；空的 `chat_users.yml` 与 Widget 样式占位文件没有生产者或行为，已从分发树删除。

## 文档覆盖

| 交付物 | 当前职责 | 核查结果 |
| --- | --- | --- |
| `CHANGELOG.md` | 只陈述 1.44.0 到候选树的用户可见净变化与升级注意 | 已落为 `2.0.0-rc.1` 章节，不记录中间迁移方案 |
| `docs/knowledge/` | 当前实现、架构边界、源码入口与维护规则 | 删除逐任务流水，改为版本级核查；修正失效路径、旧命令、旧配置与旧 Runtime API |
| 公开 Wiki | 从安装、首站、常用任务到完整 Reference、迁移和支持 | 注册表／Schema 集合差异检查无缺项；安装来源与 main 合并后的 v2 边界已明确 |
| `README.md` / `README_EN.md` | 项目定位、环境要求与最短 v2 体验路径 | 源码安装与主题依赖步骤一致；不把 npm 当前版本冒充 v2 |

公开文档的完整性检查以权威集合为左侧、文档出现集合为右侧，覆盖 21 个主题根、54 个注册标签及各自用法、8 个分享服务、13 个 Profile、9 个 Feature、6 个 Service、9 个标签配置根、6 个评论 Provider、12 个 Widget ID、11 个 Widget layout、3 种 Hero 效果、48 个效果参数、2 个运行策略和三类 v1 legacy 映射；集合差异均为空。该检查只作为本次发布验收，完成后删除临时脚本。

## 验证命令

```sh
node --test test/content-config.test.js
npm run knowledge:check
npm run release:check
npm pack --dry-run --json
cd /Users/xaoxuu/repos/xaoxuu.com && npm run g
```

发布前以最终工作树重跑这些命令，并分别检查主题仓库、公开 Wiki 子模块和主站仓库的 `git diff --check`。主站既有内容或 Doctor 告警若与本次文档无关，应单独报告，不能把它们算作文档验收通过或失败。

本轮最终结果：

- lint、203 项单元测试和 21 项 Contribution descriptor 通过；知识库检查覆盖 62 页、936 个链接和 140 个配置引用。
- npm tarball 以 `2.0.0-rc.1` 安装到 Post/Topic、Notebook、Wiki 与空配置场景，三语生成、预览、路由、搜索和压缩后的 Runtime ESM 通过。
- 公开 `1.44.0` 基线首屏脚本 gzip 为 34,937 字节，当前为 22,601 字节，下降 35.3093%，通过 30% 门槛。
- 主站生成 307 个文件并完成 HTML/CSS/JS 压缩；39 个当前 Wiki 页面、27 个跳转页、2,374 条内部链接、576 个锚点和 150 张图片检查通过。
- CI 发布元数据解析得到 `version=2.0.0-rc.1`；npm dry-run 包身份一致，且不再包含两个空残留文件。

## 发布维护

- `2.0.0-rc.1` 的版本元数据由发布流程原子同步到 `package.json`、`package-lock.json` 与安装知识库；任一来源不一致即在写入前失败，已暂存、未暂存与未跟踪的无关文件都会阻断发布。所有公开版本使用同一个 npm 安装与 Release 流程。
- v2 合并后公开源码链接统一指向 `main`，不再把 `v2` 分支写成长期安装契约。
- 新增能力必须先进入对应 Schema／注册表的唯一事实源，再更新知识库和公开 Reference；不维护手写镜像清单。
- 公开 Wiki 由独立仓库拥有，主题提交和 Wiki 提交分别交付；主站只在单独获准时更新子模块 gitlink。
