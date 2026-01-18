# Downloaded Datasets

This directory contains datasets for the research project "Do LLMs behave differently when the prompter is human vs another LLM?".

## Dataset 1: HC3 (Human ChatGPT Comparison Corpus)

### Overview
- **Source**: [Hello-SimpleAI/HC3](https://huggingface.co/datasets/Hello-SimpleAI/HC3)
- **Format**: JSONL
- **Task**: Text Generation, Classification (Human vs ChatGPT)
- **Splits**: `open_qa`, `wiki_csai`, `finance`, `medicine`, `reddit_eli5`
- **Location**: `datasets/HC3/`

### Downloaded Files
- `open_qa.jsonl` (2.8 MB)
- `wiki_csai.jsonl` (2.1 MB)

### Download Instructions
```bash
wget https://huggingface.co/datasets/Hello-SimpleAI/HC3/resolve/main/open_qa.jsonl -O datasets/HC3/open_qa.jsonl
wget https://huggingface.co/datasets/Hello-SimpleAI/HC3/resolve/main/wiki_csai.jsonl -O datasets/HC3/wiki_csai.jsonl
```

### Loading
```python
import json
data = []
with open('datasets/HC3/open_qa.jsonl', 'r') as f:
    for line in f:
        data.append(json.loads(line))
# Each item has 'question', 'human_answers', 'chatgpt_answers'
```

### Sample Data
See `datasets/HC3/samples.json` (if created) or inspect the JSONL files directly.

## Dataset 2: M4 (Recommended)

### Overview
- **Source**: [mbzuai-nlp/M4](https://github.com/mbzuai-nlp/M4) / Hugging Face (see paper)
- **Task**: Multi-generator text detection
- **Notes**: Larger dataset, code available in `code/M4`.
