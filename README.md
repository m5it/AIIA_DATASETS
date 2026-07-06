# OurAI Training Datasets

Fine-tuning datasets for `meta-llama/Llama-3.2-3B-Instruct` (QLoRA) using the OurAI framework tool-calling patterns.

## Files

| File | Examples | Size | Description |
|------|----------|------|-------------|
| `ourai_clean.jsonl` | 315 | 2.6 MB | Filtered/cleaned combination of historical data. Used for **v7** training. |
| `ourai_train.jsonl` | 315 | 1.7 MB | Alias for `ourai_clean.jsonl` (identical content). |
| `ourai_merged.jsonl` | — | 1.9 MB | Merged combination of earlier datasets. Superseded by `ourai_clean`. |
| `ourai_new_data.jsonl` | 148 | 3.2 MB | Fresh data parsed from 11 HISTORY.md session transcripts (t7–t17, KosDB). Used for **v8** training. |
| `ourai_new_data.txt` | — | 3.2 MB | Human-readable plain-text version of the above (same content, no JSONL formatting). |
| `ourai_train.txt` | — | 1.7 MB | Human-readable version of `ourai_train.jsonl`. |

## Format (JSONL)

Each line is a Llama 3.2 Instruct-format conversation:

```json
{"messages": [
  {"role": "system", "content": "..."},
  {"role": "user", "content": "..."},
  {"role": "assistant", "content": "..."}
]}
```

Tool calls are embedded as JSON in the assistant content (OurAI framework convention).

## Source

Raw HISTORY.md session files are collected from `OurAI/playground/collecting_program_data/`. Each file records a real interactive coding session between a user and the OurAI agent, including tool calls (file reads, git operations, shell commands, etc.) and model responses.

## Usage

```bash
python ../../OurAI/OurAI/examples/train_ourai.py \
  --data ourai_new_data.jsonl \
  --output-dir models/ourai_v8 \
  --epochs 3 --lr 2e-4 \
  --lora-r 16 --lora-alpha 32 \
  --max-seq-length 2048
```
