# 输出结构

## 来源元数据

在主表之前输出：

```yaml
dataset_name: ""
dataset_version: "unknown"
dataset_date: "unknown"
source_type: "unknown"
sample_count: 0
analysis_skill: "feedback-to-product-insight"
```

不要猜测缺失字段。版本未知时，明确说明无法安全地区分同编号反馈的历史版本。

## Markdown 主表

使用以下列并保持顺序：

| 用户问题 | 结论类型 | 事实证据 | 需求推断 | 置信度 | 缺失信息 | 下一步 | 研究优先级 |
|---|---|---|---|---|---|---|---|

字段要求：

- `用户问题`：用用户障碍、目标或进展表述，不直接写功能。
- `结论类型`：已观察事实、需求推断、待验证假设、暂不支持结论。
- `事实证据`：列出反馈编号；无证据时明确写“当前材料无证据”。
- `需求推断`：写底层需要，不照抄用户提出的解法。
- `置信度`：高、中、低、无证据。
- `缺失信息`：列出会改变产品决策的未知项。
- `下一步`：写研究方法和具体要验证的内容。
- `研究优先级`：P0、P1、P2。

每项事实证据包含编号和短原文摘录。默认最多保留三个 P0；P0 必须会改变 MVP 核心价值判断、范围或安全边界。

## JSON 结构

批量处理或向外部系统传递时使用：

```json
{
  "source_metadata": {
    "dataset_name": "",
    "dataset_version": "unknown",
    "dataset_date": "unknown",
    "source_type": "unknown",
    "sample_count": 0,
    "analysis_skill": "feedback-to-product-insight"
  },
  "analysis_limits": [],
  "insights": [
    {
      "user_problem": "",
      "conclusion_type": "need_inference",
      "evidence_ids": ["F01"],
      "need_inference": "",
      "confidence": "medium",
      "missing_information": [],
      "next_research": [{"method": "", "question_to_answer": ""}],
      "research_priority": "P0"
    }
  ],
  "contradictions_or_segments": [],
  "relationship_hypotheses": [
    {
      "related_problems": [],
      "relationship_type": "correlated_hypothesis",
      "rationale": "",
      "validation_needed": ""
    }
  ],
  "unsupported_questions": []
}
```

只使用 `observed_fact`、`need_inference`、`hypothesis`、`unsupported` 作为 `conclusion_type`。
只使用 `high`、`medium`、`low`、`none` 作为 `confidence`。
只使用 `parallel`、`correlated_hypothesis`、`causal_hypothesis`、`supported_causal` 作为 `relationship_type`。
