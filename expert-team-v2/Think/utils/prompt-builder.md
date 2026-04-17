# Prompt 构建工具

---
version: 1.0.0
purpose: 动态生成专家 Prompt
---

## 功能说明

将模板文件与任务参数结合，生成完整的专家执行 Prompt。

---

## 核心函数

### fillTemplate(templateId, params)

**参数**：

| 参数 | 类型 | 说明 |
|------|------|------|
| `templateId` | string | 模板 ID（common/frontend/backend/database/devops/security/test） |
| `params` | object | 参数对象 |

**params 结构**：

```javascript
{
  expert_name: string,       // 专家名称
  task_description: string,  // 任务描述
  project_path: string,      // 项目路径
  tech_stack: string,        // 技术栈
  dependency_results: object, // 前置任务结果
  plan_summary: string       // Plan 摘要
}
```

**返回值**：完整的 Prompt 字符串

---

## 实现逻辑

```javascript
function fillTemplate(templateId, params) {
  // 1. 加载模板文件
  const templatePath = `templates/${templateId}.md`;
  const template = readTemplate(templatePath);

  // 2. 提取 Prompt 模板部分（``` 代码块内容）
  const promptBlock = extractPromptBlock(template);

  // 3. 替换变量
  const filledPrompt = promptBlock
    .replace(/\{\{expert_name\}\}/g, params.expert_name || '')
    .replace(/\{\{task_description\}\}/g, params.task_description || '')
    .replace(/\{\{project_path\}\}/g, params.project_path || '')
    .replace(/\{\{tech_stack\}\}/g, params.tech_stack || '')
    .replace(/\{\{dependency_results\}\}/g, formatDependencyResults(params.dependency_results))
    .replace(/\{\{plan_summary\}\}/g, params.plan_summary || '');

  return filledPrompt;
}

function formatDependencyResults(results) {
  if (!results || Object.keys(results).length === 0) {
    return '无前置依赖';
  }

  return Object.entries(results)
    .map(([task, result]) => `- ${task}: ${result}`)
    .join('\n');
}
```

---

## 使用示例

### 基础调用

```javascript
const prompt = fillTemplate('backend', {
  expert_name: '后端专家',
  task_description: '实现用户认证 API',
  project_path: '{{project_path}}',
  tech_stack: 'Node.js + Express + PostgreSQL',
  dependency_results: { task1: '数据库表已创建' },
  plan_summary: '使用 JWT 进行身份认证'
});

// 输出完整 Prompt
```

### Agent 调用集成

```javascript
function dispatchExpert(expertType, taskId, params) {
  // 1. 获取专家配置
  const expertConfig = loadConfig('config/experts.yaml');
  const expert = expertConfig.experts[expertType];

  // 2. 构建 Prompt
  const prompt = fillTemplate(expertType, {
    ...params,
    expert_name: expert.name
  });

  // 3. 调用 Agent
  return Agent({
    subagent_type: 'general-purpose',
    description: `${expert.name}-${taskId}`,
    prompt: prompt
  });
}
```

---

## 批量并行调用

```javascript
function dispatchParallel(tasks) {
  // 任务格式：[{ id, expertType, params }]
  
  return tasks.map(task => dispatchExpert(
    task.expertType,
    task.id,
    task.params
  ));
  // 所有 Agent 同时启动
}
```

---

## 模板变量扩展

可扩展的额外变量：

| 变量 | 说明 | 来源 |
|------|------|------|
| `{{task_id}}` | 任务编号 | 调度器分配 |
| `{{wave_number}}` | 当前波次 | 调度器分配 |
| `{{deadline}}` | 截止时间 | 用户指定 |
| `{{constraints}}` | 约束条件 | Plan 阶段 |

---

## 错误处理

```javascript
function fillTemplateSafe(templateId, params) {
  try {
    validateParams(params);
    return fillTemplate(templateId, params);
  } catch (error) {
    return generateFallbackPrompt(params);
  }
}

function validateParams(params) {
  const required = ['task_description', 'project_path'];
  const missing = required.filter(key => !params[key]);
  
  if (missing.length > 0) {
    throw new Error(`缺少必要参数: ${missing.join(', ')}`);
  }
}
```