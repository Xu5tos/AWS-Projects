# DeepSeek LLM Exploration

This repository documents my exploration of the **DeepSeek R1** large language model (LLM), 
including setup, local hosting via **Ollama**, visual interaction using **Chatbox**, 
and comparison with **OpenAI** models. The goal was to evaluate DeepSeek's reasoning, token efficiency, 
and overall viability as a cost-effective LLM solution.

## What’s inside

- **Step-by-step local setup guide** in [`docs/DEEPSEEK_GUIDE.md`](docs/DEEPSEEK_GUIDE.md)
- Comparisons between **DeepSeek R1** and OpenAI models
- Temperature setting experiments for creativity control
- Observations on offline vs online usage
- Model size accuracy testing (1.5b vs 8b parameters)

## Prerequisites

- A computer with sufficient RAM and storage (for running LLMs locally)
- Installed:
  - [Ollama](https://ollama.com/) (for local model management)
  - [Chatbox](https://chatboxapp.com/) (for visual interface)
- Internet connection (for initial downloads; not needed for offline use)
- Terminal/Command Line access

## Quick start

1. **Install Ollama** on your machine (follow the official instructions for your OS).
2. **Pull DeepSeek R1 model**:

   ```bash
   ollama pull deepseek-r1:8b
   ```

   > Replace `8b` with another size (e.g., `1.5b`) if you have limited resources.

3. **Run DeepSeek locally**:

   ```bash
   ollama run deepseek-r1:8b
   ```

4. **Connect via Chatbox**:
   - Set API to `Ollama API`
   - Choose your installed DeepSeek model (`1.5b` or `8b`)

5. **Experiment with prompts** (see [`docs/DEEPSEEK_GUIDE.md`](docs/DEEPSEEK_GUIDE.md) for detailed tests).

## Repository structure (example)

```
.
├── docs/
│   └── DEEPSEEK_GUIDE.md
├── README.md
└── experiments/
    ├── temperature_tests.md
    ├── model_size_comparison.md
    └── offline_usage.md
```

## Notes & tips

- The `8b` model gives more accurate and detailed answers than `1.5b` but requires more memory.
- Higher temperature settings = more creative but less predictable output.
- Offline mode ensures privacy but requires local compute resources.

## License

MIT (or choose another license for your repo).