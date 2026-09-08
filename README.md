# jsonl-runner

Run a JSONL of prompts through an LLM, results to JSONL

## Examples

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## Features

- JSONL in, JSONL out: the input is streamed line by line
- Real rate limiting: sliding windows on requests/min and tokens/min
- Per-row overrides for model, system, temperature and max_tokens
- Idempotent: ids already in the output are skipped on a rerun
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- Progress, token counts and a cost estimate on stderr
- Failures go to a sidecar file with error type, message and status
- A bad input line is logged and skipped, never fatal

## Install

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Project structure

```text
├── .github/
│   └── workflows/
│       └── ci.yml
├── docs/
│   ├── development.md
│   ├── roadmap.md
│   ├── tradeoffs.md
│   └── usage.md
├── examples/
│   └── quickstart.md
├── tests/
│   └── test_smoke.py
├── .gitignore
├── CHANGELOG.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── SECURITY.md
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## Why

Needed this for myself; figured others might too.

## License

MIT - see [LICENSE](LICENSE).
