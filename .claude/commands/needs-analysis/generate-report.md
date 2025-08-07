# 培训需求分析 - 生成最终报告

这个命令用于完成培训需求分析的最后阶段，整合所有分析结果并生成专业的分析报告。

## 执行步骤

### 第1步：前置条件检查
验证以下文件是否存在和完整：
- workflow-data/business-problem.md
- workflow-data/analysis-plan.md  
- workflow-data/data-collection-tools.md
- workflow-data/raw-data.md
- workflow-data/insights.md
- workflow-data/root-cause-analysis.md

### 第2步：洞察分析（如未完成）
如果workflow-data/insights.md不存在，先调用insight-synthesizer：
```
使用Task工具调用insight-synthesizer，任务描述：
"分析以下原始数据，提炼核心洞察和主题：

原始数据：[读取workflow-data/raw-data.md的内容]
分析背景：[读取workflow-data/business-problem.md的内容]

请识别3-5个核心主题，为每个主题提供支撑证据，并识别数据中的矛盾或不一致之处。
输出结果保存到workflow-data/insights.md文件。"
```

### 第3步：根本原因诊断（如未完成）
如果workflow-data/root-cause-analysis.md不存在，调用root-cause-analyzer：
```
使用Task工具调用root-cause-analyzer，任务描述：
"基于洞察分析结果，运用Gilbert六盒模型进行根本原因诊断：

洞察分析：[读取workflow-data/insights.md的内容]
业务背景：[读取workflow-data/business-problem.md的内容]

请系统分析六个盒子中的问题，识别首要根本原因，并明确区分培训vs非培训解决方案。
输出结果保存到workflow-data/root-cause-analysis.md文件。"
```

### 第4步：最终报告生成
调用report-generator Agent：
```
使用Task工具调用report-generator，任务描述：
"整合所有分析结果，生成完整的《培训需求分析报告》：

输入组件：
- 项目背景：[读取workflow-data/business-problem.md]
- 分析过程：[读取workflow-data/analysis-plan.md]
- 核心发现：[读取workflow-data/insights.md]  
- 根本原因：[读取workflow-data/root-cause-analysis.md]
- 数据收集概况：[读取workflow-data/data-collection-tools.md]

请生成专业的商业报告，包含执行摘要、详细分析、明确建议和实施路径。
输出结果保存到workflow-data/final-report.md文件。"
```

### 第5步：质量检查和用户交付
- 调用ld-methodology-advisor进行最终质量检查
- 向用户展示完整的分析报告
- 提供报告的使用建议和后续行动指引
- 更新工作流状态为"已完成"

## 报告交付格式
生成的最终报告将包含：
- **执行摘要**：核心发现和建议概述
- **详细分析**：完整的分析过程和发现
- **解决方案**：具体的培训和非培训建议
- **实施路径**：优先级排序和时间安排
- **效果评估**：建议的KPI和评估方法

## 用户后续行动建议
报告完成后，向用户提供：
- 如何向利益相关者展示报告
- 如何基于报告启动具体的改进项目
- 如何跟踪和评估改进效果