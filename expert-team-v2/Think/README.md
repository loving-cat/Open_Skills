# 专家团 Skills 项目

## 项目结构

```
Think/
├── skill.md              # 主入口文件
├── README.md              # 项目说明
├── config/
│   ├── experts.yaml       # 专家角色配置（硬编码）
│   ├── tools.yaml         # 工具规范配置
│   └── workflow.yaml      # 协作流程配置
├── templates/
│   ├── common.md          # 通用专家模板
│   ├── frontend.md        # 前端专家模板
│   ├── backend.md         # 后端专家模板
│   ├── database.md        # 数据库专家模板
│   ├── devops.md          # DevOps专家模板
│   ├── security.md        # 安全专家模板
│   └── test.md            # 测试专家模板
└── utils/
    └── prompt-builder.md  # Prompt 构建工具
```

## 配置文件说明

### experts.yaml
- 定义专家角色、技能、触发条件
- 硬编码专家数量配置
- 增援规则定义

### tools.yaml
- 工具使用规范
- 危险操作清单
- 禁止操作清单

### workflow.yaml
- 五阶段协作流程
- 并行调度规则
- 执行纪律红线

## 模板文件说明

每个专家模板包含：
- 专家技能定义
- Prompt 模板（带变量占位符）
- 验证清单
- 输出格式规范
- 调用示例

## 使用方式

1. 加载配置文件获取专家定义
2. 使用 prompt-builder 生成 Prompt
3. 调用 Agent 工具调度专家执行
4. 按波次并行执行无依赖任务
5. 遇到疑难自动增派专家

## 版本

- v1.0.0 - 初始版本，完整专家团配置