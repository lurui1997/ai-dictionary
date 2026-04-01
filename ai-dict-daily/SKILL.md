---
name: ai-dict-daily
description: 每日获取最新 AI 术语，以人类和程序友好的 markdown 形式记录并展示。当用户需要获取、记录或展示 AI 术语时使用此 skill。
---

# AI 术语每日记录 (AI Dictionary Daily)

## 概述

此 skill 用于每日获取最新的 AI 术语，并以结构化的 markdown 格式记录和展示。输出格式兼顾人类可读性和程序可解析性，方便后续的数据处理和展示。

适用场景：
- 获取当日最新 AI 术语
- 建立 AI 术语知识库
- 生成可供程序解析的术语数据

## 工作流程

### 1. 获取最新 AI 术语

使用网络搜索工具获取最新的 AI 术语信息：

```
搜索关键词建议：
- "AI 新术语 2024 2025"
- "人工智能 新名词 新概念"
- "machine learning new terms"
- "AI trending terminology"
- "大模型 新术语"
- "LLM new concepts"
```

### 2. 整理术语数据

对每个术语收集以下信息：

| 字段 | 说明 | 必需 |
|------|------|------|
| term_name | 术语英文名 | 是 |
| chinese_name | 术语中文名 | 是 |
| category | 分类 (如: 模型架构、训练方法、应用领域) | 是 |
| definition | 定义说明 | 是 |
| first_seen | 首次出现/流行时间 | 否 |
| related_terms | 相关术语 | 否 |
| usage_example | 使用示例 | 否 |
| reference_link | 参考链接 | 否 |

### 3. 生成 Markdown 文件

使用模板生成 markdown 文件：

**模板位置**: `assets/term_template.md`

**输出文件命名**: `YYYY-MM-DD-ai-terms.md`

**文件位置**: 当前工作目录或用户指定的目录

### 4. Markdown 格式规范

生成的 markdown 文件应遵循以下规范：

1. **元数据区域**: 文件顶部包含生成日期和数据来源
2. **术语条目**: 每个术语使用 H3 标题 (`###`)
3. **表格格式**: 术语属性使用表格展示，便于程序解析
4. **代码块**: 使用示例使用代码块包裹
5. **分隔线**: 术语之间使用 `---` 分隔
6. **注释标记**: 使用 HTML 注释标记术语条目开始和结束 (`<!-- 术语条目开始/结束 -->`)

## 分类体系

术语分类建议使用以下体系：

| 分类 | 说明 |
|------|------|
| 模型架构 | 如 Transformer、Diffusion Model 等 |
| 训练方法 | 如 RLHF、SFT、Pre-training 等 |
| 推理技术 | 如 Beam Search、Temperature Sampling 等 |
| 应用领域 | 如 CV、NLP、多模态等 |
| 基础设施 | 如向量数据库、模型部署等 |
| 评估指标 | 如 Perplexity、BLEU、ROUGE 等 |

## 使用示例

### 示例 1: 获取今日 AI 术语

用户请求: "获取今天的 AI 术语"

执行步骤:
1. 使用 web_search 搜索最新 AI 术语
2. 整理搜索结果，提取关键术语信息
3. 使用 `assets/term_template.md` 模板生成 markdown 文件
4. 保存为 `2024-01-15-ai-terms.md`
5. 展示文件内容给用户

### 示例 2: 获取特定分类术语

用户请求: "获取最新的模型架构相关术语"

执行步骤:
1. 使用 web_search 搜索模型架构相关术语
2. 筛选分类为"模型架构"的术语
3. 生成 markdown 文件
4. 展示结果

## 程序解析说明

生成的 markdown 文件支持程序解析：

1. **术语条目定位**: 通过 `<!-- 术语条目开始 -->` 和 `<!-- 术语条目结束 -->` 注释
2. **表格数据**: 标准 markdown 表格格式，可用任何 markdown 解析器处理
3. **元数据**: 文件顶部使用引用块 (`>`) 包含生成信息

示例解析代码 (Python):

```python
import re
import markdown
from bs4 import BeautifulSoup

def parse_terms(md_content):
    """解析 markdown 文件中的术语条目"""
    # 提取术语条目
    pattern = r'<!-- 术语条目开始 -->(.+?)<!-- 术语条目结束 -->'
    matches = re.findall(pattern, md_content, re.DOTALL)
    
    terms = []
    for match in matches:
        term = {}
        # 解析表格数据
        # ... 解析逻辑
        terms.append(term)
    
    return terms
```

## 资源文件

### assets/term_template.md

Markdown 模板文件，用于生成每日术语记录。包含以下占位符：

- `{{date}}`: 日期
- `{{datetime}}`: 完整日期时间
- `{{term_name}}`: 术语名称
- `{{chinese_name}}`: 中文名
- `{{category}}`: 分类
- `{{first_seen}}`: 首次出现时间
- `{{related_terms}}`: 相关术语
- `{{definition}}`: 定义
- `{{usage_example}}`: 使用示例
- `{{reference_link}}`: 参考链接
- `{{term_count}}`: 术语总数
- `{{new_terms}}`: 新增术语数
- `{{updated_terms}}`: 更新术语数
- `{{category_distribution}}`: 分类分布
