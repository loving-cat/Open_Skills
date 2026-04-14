# Dev Experts Team Plugin

一个完整的开发专家团队插件，包含前端、后端、数据库、DevOps、测试、安全、文档、重构专家。

## 安装

```bash
# 方法1: 从本地路径安装
claude plugin install ~/.claude/plugins/dev-experts-team

# 方法2: 复制整个插件目录到目标机器
cp -r ~/.claude/plugins/dev-experts-team /path/to/destination/
```

## 包含内容

### 子智能体 (Agents)

| 智能体 | 调用方式 | 功能 |
|--------|----------|------|
| `dev-experts-team:frontend-expert` | 自然语言或 Agent 工具 | UI组件、页面开发、样式实现、API集成 |
| `dev-experts-team:backend-expert` | 自然语言或 Agent 工具 | API设计、业务逻辑、认证授权 |
| `dev-experts-team:database-expert` | 自然语言或 Agent 工具 | 数据建模、迁移脚本、查询优化 |
| `dev-experts-team:devops-expert` | 自然语言或 Agent 工具 | Docker、CI/CD、部署脚本 |
| `dev-experts-team:test-expert` | 自然语言或 Agent 工具 | 功能验证、测试报告 |
| `dev-experts-team:security-auditor` | 自然语言或 Agent 工具 | 安全漏洞扫描、OWASP Top 10 检测 |
| `dev-experts-team:code-reviewer` | 自然语言或 Agent 工具 | 代码审查、风格检查、bug 检测 |
| `dev-experts-team:doc-writer` | 自然语言或 Agent 工具 | 技术文档编写、API 文档 |
| `dev-experts-team:refactor-expert` | 自然语言或 Agent 工具 | 代码重构、复杂度优化 |

### 技能 (Skills)

| 技能 | 触发词 | 功能 |
|------|--------|------|
| `/Think` | `/Think`, `/专家团`, `启用专家团`, `专家团模式` | 启用专家团协作模式，规划→任务分解→专家执行→疑难调度→验收 |

## 使用示例

```bash
# 专家团模式
"/专家团 创建一个用户登录系统"

# 单独调用专家
"让 dev-experts-team:frontend-expert 实现登录页面"
"用 dev-experts-team:security-auditor 审计这个模块"
```

## 目录结构

```
dev-experts-team/
├── plugin.json          # 插件清单
├── README.md            # 说明文档
├── agents/
│   ├── frontend-expert.md
│   ├── backend-expert.md
│   ├── database-expert.md
│   ├── devops-expert.md
│   ├── test-expert.md
│   ├── code-reviewer.md
│   ├── security-auditor.md
│   ├── doc-writer.md
│   └── refactor-expert.md
└── skills/
    └── Think/
        └── SKILL.md
```

## 版本历史

- **1.1.0** - 新增 frontend/backend/database/devops/test 专家，修复工具名称错误
- **1.0.0** - 初始版本
