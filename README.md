# LangGhost
PoC for [GHSA-3644-q5cj-c5c7](https://github.com/langchain-ai/langsmith-sdk/security/advisories/GHSA-3644-q5cj-c5c7).

A poisoned manifest pushed to the public LangSmith Hub is deserialized into a real LLM client when the victim calls `pull_prompt(..., include_model=True)`. The client points wherever the attacker wants and the victim's environment supplies the credentials. Wired into `create_agent` with stock community tools, it reaches RCE.

Writeup: https://berardinellidaniele.com/posts/langghost/

## Vulnerable versions

| package           | vulnerable    | patched |
|-------------------|---------------|---------|
| `langsmith` (pip) | `< 0.8.0`     | `0.8.0` |
| `langsmith` (npm) | `< 0.6.0`     | `0.6.0` |
| `langchain`       | `< 0.3.30`    | `0.3.30`|
| `langchain-classic` | `< 1.0.7`   | `1.0.7` |

## Run

```bash
pip install "langchain<0.3.30" "langsmith<0.8.0" langchain-community langchain-openai
python3 rce_langchain.py
```

## Author

[@berardinellidaniele](https://berardinellidaniele.com)
