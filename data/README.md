# Soccer-GMR Dataset

This directory contains the label files for **Soccer-GMR**, a benchmark for **Generalized Moment Retrieval (GMR)**.

GMR uses a unified label format for three retrieval scenarios:

- **Null-set query**: the queried event is absent, so `relevant_windows = []`.
- **Single-moment query**: the query has exactly one relevant temporal window.
- **Multi-moment query**: the query has multiple relevant temporal windows.

## Directory Structure

```text
data/
`-- label/
    |-- Full/
    |   |-- train.jsonl
    |   |-- val.jsonl
    |   |-- test.jsonl
    |   `-- full.jsonl
    `-- Standard/
        |-- train.jsonl
        |-- val.jsonl
        |-- test.jsonl
        |-- gt_time_distribution_150s.png
        |-- query_length_distribution.png
        `-- query_type_topk.png
```

## Split Groups

- `label/Standard/` is the benchmark split used for evaluation.
- `label/Full/` is the complete dataset used for scaling studies.

| Split group | Train | Val | Test | Total | Videos |
| --- | ---: | ---: | ---: | ---: | ---: |
| `Standard` | 4,138 | 465 | 1,036 | 5,639 | 1,957 |
| `Full` | 16,898 | 2,235 | 2,986 | 22,119 | 5,468 |

## File Format

All labels are provided in JSONL format. Each line is one JSON object.

Core fields:

- `qid`: unique query identifier
- `vid`: video clip identifier
- `query`: natural-language query
- `duration`: video clip duration in seconds
- `relevant_windows`: evaluation-ready temporal windows in `[start, end]` format

Some records may include auxiliary fields, such as:

- `moment`: intermediate annotation representation
- `action_type`: event or action category
- `dataset_source`: source dataset identifier
- `match_info`: match-level metadata

For official evaluation, use `relevant_windows` as the primary ground-truth field.

## Examples

Positive multi-moment query:

```json
{
  "qid": 580,
  "vid": "WC2022_3857268_2_5500s_5650s",
  "query": "Locate block moments performed by players from Belgium.",
  "duration": 150,
  "moment": {
    "type": "clips",
    "value": [[26.0, 34.0], [104.0, 112.0]]
  },
  "relevant_windows": [[26.0, 34.0], [104.0, 112.0]]
}
```

Null-set query:

```json
{
  "qid": 862,
  "vid": "WC2022_3857268_2_5500s_5650s",
  "query": "Identify foul committed moments performed by players from Canada.",
  "duration": 150,
  "moment": {
    "type": "clips",
    "value": []
  },
  "relevant_windows": []
}
```

For evaluation usage and prediction format, see [`../eval/README.md`](../eval/README.md).
