---
name: create-project-req
description: 'Create a well-structured project requirement. Use when: defining new features, collecting user stories, specifying acceptance criteria, and setting priority levels. Helps ensure requirements are clear, actionable, and traceable.'
argument-hint: 'Provide feature name or requirement title'
---

# Create Project Requirement

快速规范化地提出项目需求，确保所有信息完整且可追踪。

## When to Use

- 新增功能需求
- 收集用户故事
- 定义验收标准
- 优化现有功能

## Quick Checklist

### 1️⃣ 基本信息 (2 min)
- [ ] **需求标题** — 清晰简洁，动词开头
  - 例: "支持批量导入用户数据" 而不是 "用户"
- [ ] **优先级** — High / Medium / Low
- [ ] **提出者** — 你的名字或团队
- [ ] **日期** — 自动填充

### 2️⃣ 需求描述 (3 min)
- [ ] **1-3 句问题陈述** — 为什么需要这个？
- [ ] **用户角色** — 谁会用这个功能？
  - 例: "数据分析师"、"系统管理员"
- [ ] **使用场景** — 具体的使用场景

### 3️⃣ 验收标准 (5 min)
- [ ] 至少 3 条明确的验收标准
- [ ] 格式: Given-When-Then 或简单列表
  - ✅ "支持 CSV、Excel、JSON 三种格式"
  - ✅ "导入成功率 > 99%"
  - ❌ "速度快"（太模糊）

### 4️⃣ 相关资源 (1 min)
- [ ] 关联的 Issue / Discussion 链接
- [ ] 相关提案 (`../proposals/`)
- [ ] 相关决策 (`../adr/`)

### 5️⃣ 状态标记 (自动)
- [ ] **状态**: 提议中 → 审核中 → 已确认 → 开发中 → 完成

## 文件位置

```
.github/solutions/req/
├── <priority>-<req-title>.md     # 命名规范: HIGH-batch-import-users.md
└── template.md                    # 参考模板
```

## 命名规范

```
<优先级>-<功能英文标签>.md

示例:
HIGH-batch-import-users.md
MEDIUM-export-report-templates.md
LOW-ui-polish-dashboard.md
```

## 检查清单完成后

1. **自检** ✓
   - [ ] 标题清晰？
   - [ ] 为什么要做很明确？
   - [ ] 验收标准可度量？

2. **提交审查** 
   - 发给团队评论（如果是团队项目）
   - 或直接转进开发队列

3. **转为提案或 ADR**
   - 如果涉及技术决策 → 创建相应提案
   - 如果决策已定 → 引用相关 ADR

## 示例

```
# 需求：支持批量导入用户数据

**优先级**: 高  
**提出者**: 张三  
**日期**: 2026-06-17  
**状态**: 提议中

## 需求描述

系统管理员需要快速导入大量用户信息（>1000 人），
当前只支持单个添加，效率低下。

### 用户角色
- 系统管理员
- HR 部门负责人

### 使用场景
公司组织结构变化，需在 1 小时内导入新部门的 500+ 员工信息。

## 验收标准

- [ ] 支持 CSV、Excel、JSON 三种格式
- [ ] 单次导入 >5000 条记录，<30 秒完成
- [ ] 提供导入错误日志和失败原因分析
- [ ] 支持撤销/回滚最近一次导入

## 相关资源

- Issue: #123 「改进用户管理效率」
- 提案: `../proposals/user-management-redesign.md`
```

## Pro Tips

💡 **优先级判断**
- **HIGH**: 用户强烈反馈、影响主流程、安全问题
- **MEDIUM**: 改进用户体验、功能扩展
- **LOW**: 性能优化、文档改进、UI 细节

💡 **模糊需求的红旗**
- ❌ "快一点" → 改为 "响应时间 < 200ms"
- ❌ "更好的 UI" → 改为 "三栏布局，侧边栏收起按钮"
- ❌ "支持更多数据" → 改为 "支持百万级数据集"

💡 **快速更新**
需求确认后，更新状态头：`状态: 已确认` 或 `状态: 开发中`
