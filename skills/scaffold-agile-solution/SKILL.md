---
name: scaffold-agile-solution
description: "Generate a lightweight, executable, iterative Scrum-Lite documentation set under .github/solutions/agile for a new capability or requirement. Use when: kicking off a new feature/solution, turning a requirement into a sprint-based delivery plan, setting up product backlog / roadmap / DoD / ceremonies, or standardizing agile docs in a repo. Produces requirement specs, a 4-sprint roadmap, backlog, Definition of Done, engineering practices, and metrics with cross-referenced links."
argument-hint: "Provide the capability/requirement name (e.g. 'S3 image resource management')"
---

# Scaffold Agile Solution Docs

按 Scrum Lite + 工程化实践范式，为一个新能力/需求生成一套**轻量、可执行、可迭代**的敏捷开发文档，落在 `.github/solutions/agile/` 下。

核心理念（来自 `agile/README.md`）：
- 用最少文档支撑稳定交付
- 以 Sprint 为单位滚动规划和复盘
- 用 Definition of Done 统一质量门槛
- 用指标驱动改进，而非追求形式

## When to Use

- 启动一个新功能/解决方案，需要从需求到交付的完整规划
- 把一条高优先级需求拆成 Sprint 级开发计划
- 为仓库建立标准化敏捷文档（backlog、roadmap、DoD、仪式、指标）
- 已有 `.github/solutions/` 但缺少敏捷流程文档

## When NOT to Use

- 只需要写一条需求 → 用 `create-project-req` skill
- 单纯记录架构现状 → 更新 `.github/ARCHITECTURE.md`
- 临时 bug 修复或单次任务，不涉及多 Sprint 交付

## 目标目录结构

```
.github/
├── ARCHITECTURE.md                     # 全局架构（被各文档引用，非本 skill 生成）
└── solutions/
    ├── INDEX.md                        # 敏捷文档总索引（必建）
    └── agile/
        ├── README.md                   # 敏捷实施总览：角色/节奏/原则/最小文档策略
        ├── product-backlog.md          # 产品待办与优先级（US-xxx）
        ├── roadmap.md                  # 4 个 Sprint 路线图
        ├── sprint-plan-template.md     # Sprint 计划与回顾模板
        ├── ceremonies.md               # 会议节奏与规则
        ├── definition-of-done.md       # 全局完成定义
        ├── engineering-practices.md    # 工程实践与分支策略
        ├── technical-selection.md      # 技术选型（DB/存储等）
        ├── metrics-kpis.md             # 敏捷与交付指标
        ├── risk-impediment-log.md      # 风险与阻塞日志
        ├── team-working-agreement.md   # 团队协作约定
        ├── req/
        │   ├── <PRIORITY>-<slug>.md             # 需求规格（含 FR/NFR/验收）
        │   ├── <priority>-<slug>-definition-of-done.md  # 需求专用 DoD
        │   └── database-schema.md               # 数据库表结构
        └── plan/
            └── requirement-development-plan.md  # 需求开发计划（聚合引用）
```

## 命名规范

- 需求文件：`<优先级大写>-<英文短标签>.md`，例：`HIGH-s3-image-resource-management.md`
- 需求专用 DoD：`<priority>-<slug>-definition-of-done.md`
- 用户故事 ID：`US-001`、`US-002`…，在 backlog、roadmap、plan 中保持一致
- 优先级：`HIGH` / `MEDIUM` / `LOW`

## 生成流程（建议步骤）

### 1️⃣ 明确范围（先问清，不要假设）
- 能力/需求名称、业务目标、责任角色（PO / Tech Lead / Dev / QA / PM）
- 交付节奏（默认 1 周 1 Sprint，共 4 Sprint）
- 技术约束（数据库、存储、部署环境）

### 2️⃣ 写需求规格 `req/<PRIORITY>-<slug>.md`
固定章节顺序：
1. 背景 → 2. 目标 → 3. 功能需求（FR-1…FR-n）→ 4. 非功能需求（量化指标）
→ 5. API 范围（MVP）→ 6. 数据与配置 → 7. 验收标准（Given-When-Then）
→ 8. 风险与约束 → 9. 优先级与计划（建议进入哪些 Sprint）

### 3️⃣ 拆解到 Sprint
- `roadmap.md`：4 Sprint 表格（Sprint | 时间 | 目标 | 主要故事 US-xxx | 里程碑）+ 范围控制 + 发布策略
- `product-backlog.md`：用户故事 + 优先级 + 验收摘要
- `plan/requirement-development-plan.md`：聚合文档，每节用「参考:」列出相对路径链接

### 4️⃣ 固化质量门槛
- `definition-of-done.md`（全局）+ `req/<priority>-<slug>-definition-of-done.md`（需求专用）
- `engineering-practices.md`：分支策略、PR 要求（验证步骤/风险评估/回滚方案）、CI 门禁

### 5️⃣ 运营文档
- `ceremonies.md`：Planning / Standup / Refinement / Review / Retro 的时间与规则
- `metrics-kpis.md`、`risk-impediment-log.md`、`team-working-agreement.md`

### 6️⃣ 建索引
- 更新 `solutions/INDEX.md`：列出每个文档的相对链接 + 一句话说明 + 使用建议

## 关键约定

- **交叉引用用相对路径**：每个 plan/计划类文档末尾用「参考:」块链接到需求、roadmap、DoD、`../../ARCHITECTURE.md`。务必核对相对路径层级（`./` vs `../` vs `../../`）。
- **最小文档策略**：
  - 必须维护：backlog、Sprint 计划、DoD、风险日志、指标
  - 可选：复杂特性的详细设计长文
  - 禁止：与代码状态长期不一致的重复文档
- **量化优先**：NFR 与验收标准必须可度量（成功率 ≥ 99.5%、P95 < 100ms 等），避免「速度快」这类模糊描述。
- **范围控制**：每 Sprint 预留 ~20% 容量给缺陷/紧急项；新需求默认进下个 Sprint，除非 P0 且 PO+Tech Lead 共同批准。

## Sprint 节奏模板（默认）

| 仪式 | 时间 | 时长 |
|---|---|---|
| Sprint Planning | 周一 10:00 | 60 min |
| Daily Standup | 每天 10:00 | 15 min |
| Backlog Refinement | 周四 16:00 | 45 min |
| Sprint Review | 周五 15:00 | 45 min |
| Sprint Retrospective | 周五 16:00 | 45 min |

## 完成检查清单

- [ ] `req/<PRIORITY>-<slug>.md` 含 FR/NFR/验收(Given-When-Then)/风险
- [ ] `roadmap.md` 4 Sprint，每个故事有 US-xxx 与里程碑
- [ ] `product-backlog.md` 故事 ID 与 roadmap 一致
- [ ] 全局 DoD + 需求专用 DoD 均存在
- [ ] `plan/requirement-development-plan.md` 用相对路径引用且链接有效
- [ ] `INDEX.md` 已更新，覆盖全部文档
- [ ] 所有相对链接经过校验（层级正确、文件名大小写一致）
