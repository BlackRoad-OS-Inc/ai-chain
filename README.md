# AI Chain

Chained AI inference across distributed edge nodes. Routes prompts through a priority-ordered mesh of Ollama instances on Raspberry Pi 5 hardware.

## Architecture

```
Client → /chain → Probe all nodes → Route to fastest alive node
                                   ↓ (mode=full)
                              Refine via second node
```

**Nodes:** Octavia (deepseek-r1), Aria (qwen2.5-coder), Lucidia (tinyllama), Alice (tinyllama fallback)

## API

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Node health check with model inventory |
| `/chain` | POST | Run chained inference (`{"prompt": "...", "mode": "fast\|full"}`) |

## Run

```bash
pip install -r requirements.txt
python server.py  # http://localhost:8100
```

## Test

```bash
pip install pytest httpx
pytest tests/
```

## Deploy

```bash
docker build -t ai-chain .
docker run -p 8100:8100 ai-chain
```
