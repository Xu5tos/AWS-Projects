# End-to-End Guide — DeepSeek R1 LLM Exploration (Local + Visual Interface)

This guide covers installing DeepSeek locally using Ollama, connecting it to Chatbox, testing model sizes, 
and experimenting with temperature settings.

---

## 1) Understanding DeepSeek R1

- **DeepSeek R1** is an open-source large language model with performance comparable to OpenAI’s o1 model.
- Being open source, it can be run locally for privacy and offline use.

Why: Running locally removes dependency on internet connectivity and reduces latency.

---

## 2) Install Ollama

Ollama simplifies downloading, installing, and managing open-source LLMs.

- **macOS**: Install via `brew install ollama`
- **Windows**: Download installer from [ollama.com](https://ollama.com/)
- **Linux**: Follow the package instructions on the Ollama site

Verify installation:

```bash
ollama --version
```

---

## 3) Download DeepSeek R1

Choose model size based on your hardware:

```bash
ollama pull deepseek-r1:1.5b  # Smaller, faster
ollama pull deepseek-r1:8b    # More accurate, needs more RAM
```

---

## 4) Run DeepSeek Locally

Example for `8b` model:

```bash
ollama run deepseek-r1:8b
```

To test offline mode:

1. Turn off Wi-Fi
2. Run the same command
3. Observe that responses still work

---

## 5) Install & Configure Chatbox

Chatbox provides a GUI for chatting with locally hosted models.

1. Download and install from [chatboxapp.com](https://chatboxapp.com/).
2. Open Chatbox and go to **Settings → API**.
3. Select **Ollama API** as the provider.
4. Choose your installed DeepSeek model (`1.5b` or `8b`).

---

## 6) Model Size Comparison

Prompt used for testing:

```
How many r's are in strawberry?
```

- **1.5b** → Incorrectly answered **2**
- **8b** → Correctly answered **3**

Conclusion: Larger models give better accuracy.

---

## 7) Temperature Setting Experiments

- **Low temperature (0.2)** → More factual, predictable responses
- **High temperature (0.9)** → More creative, diverse responses

Test case: Generate a recipe with both settings and compare.

Observation: High temperature output had more unusual ingredients and elaborate steps.

---

## 8) OpenAI vs DeepSeek

- **DeepSeek advantages**: Open source, offline capable, low cost
- **OpenAI advantages**: Polished outputs, integration ecosystem, high availability

I use both depending on the task.

---

## 9) Troubleshooting

- **Model fails to run**: Check RAM usage; try smaller model
- **Chatbox not connecting**: Verify API settings match Ollama config
- **Slow response times**: High load or insufficient CPU/GPU

---

## Security considerations

- Running locally keeps prompts and responses private.
- Be mindful of system resources and background processes when hosting large models.

---

## Appendix — Quick commands

```bash
ollama pull deepseek-r1:8b
ollama run deepseek-r1:8b
ollama list   # List installed models
```