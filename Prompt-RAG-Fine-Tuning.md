# Prompt Aplicado
Chat GPT Compartilhado > [Guia RAG e Fine Tuning](https://chatgpt.com/share/68ca1ff9-d834-8013-9691-d254b576e0ce)

# Prompt
## Copie e cole o texto abaixo em uma IA Generativa

Crie um guia detalhado com foco em **RAG bem feito** e **fine-tuning leve (LoRA/QLoRA)**, cobrindo os 9 tópicos abaixo:

## Hardware
* **Linux:** Ubuntu 22.04 LTS / RHEL 9, base para drivers NVIDIA + Docker 
* **CPU:** CPU i7+ ou Ryzen 7+ ingestão de documentos + pré-processamento 
* **RAM:** 16–32 GB, suportar embeddings + cache/contexto 
* **GPU:** RTX 3060 12GB+, 5090 32GB, inferência rápida, batching no vLLM 

## Software
* **Qdrant:** banco vetorial para RAG 
* **BGE-M3:** embeddings multilíngues para geração e busca de vetores 
* **BGE-reranker-v2:** Refinamento, melhora a precisão da busca vetorial 
* **Modelo:**  LLM base (open-weights) para geração de respostas 
* **Ollama e vLLM:** Efetua a inferência, consulta do modelo 
 

## 1) Contexto e premissas

* **Objetivo do usuário:** `{descreva seu caso de uso em 1–2 linhas}`
* **Stack/infra disponível (assuma como base):**

  * **Linux:** Ubuntu 22.04 LTS ou RHEL 9 — base para drivers NVIDIA + Docker/Podman.
  * **CPU:** i7+ ou Ryzen 7+ — ingestão e pré-processamento.
  * **RAM:** 16–32 GB — embeddings + cache/contexto.
  * **GPU:** RTX 3060 (12 GB) → 5090 (32 GB) — **inferência** e **batching** (vLLM).
  * **Vetores (RAG):** **Qdrant**.
  * **Embeddings:** **BGE-M3** (multilíngue; denso/esparso/híbrido).
  * **Reranker:** **bge-reranker-v2** (refina relevância).
  * **Servidores de inferência:** **Ollama** (local/protótipo) e **vLLM** (OpenAI-compatible, alto throughput).
  * **Modelo base:** LLM **open-weights** (ex.: Llama 3.1 / Mixtral / Qwen).
  * **Fine-tuning leve (se necessário):** **LoRA**/**QLoRA**.
* **Premissas de trabalho:**

  * Priorize **RAG** (indexar, recuperar, rerankear, só então gerar).
  * Se faltar **estilo/terminologia**, proponha **LoRA/QLoRA** (custo controlado).
  * Sempre explicite **latência**, **tok/s**, **cache hit** e **custo por resposta**.

## 2) Saída esperada

Entregue um **documento único** com as seções abaixo (tabelas e checklists quando fizer sentido):

1. **Diagnóstico rápido** (RAG já resolve? quando considerar LoRA/QLoRA? quando full fine-tuning é desaconselhado).
2. **Arquitetura mínima** (diagrama texto → `ingestão → embeddings (BGE-M3) → Qdrant → reranker (bge-v2) → vLLM/Ollama → resposta`; cite pontos de cache e batch).
3. **Passo a passo operacional**

   * **Ingestão**: chunking, metadados, dedupe.
   * **Indexação**: criação de collections no Qdrant, schema e métricas de distância.
   * **Busca**: top-k inicial + **reranker** para reordenação final.
   * **Geração**: chamada via **vLLM** (API OpenAI-compatible) ou **Ollama** (local).
4. **Configurações-chave** (valores iniciais recomendados para chunk size/overlap, top-k, thresholds do reranker, batch size de inferência).
5. **Métricas e SLOs** (TTFT, latência p95, tok/s, custo por resposta, qualidade do RAG por nDCG/Recall\@k).
6. **Riscos e mitigação** (drift de dados, alucinações, latência de I/O, falta de GPU, privacidade).
7. **Quando usar fine-tuning**

   * **Leve (LoRA/QLoRA):** gatilhos, dados mínimos, tempo/custo estimado.
   * **Pesado (full/continual):** por que **não** é a via padrão; requisitos de GPU/tempo/dados.
8. **Plano B offline** (Ollama + GGUF; o que cai de qualidade e como compensar).

## 3) Estilo de resposta

* **Tom:** pragmático, direto, PT-BR.
* **Formato:** listas curtas, tabelas, **valores sugeridos** e **por quês**.
* **Evite** genérico; diga **o que configurar e por que**.
* Quando houver incerteza, proponha **testes A/B** e métricas para decidir.
* **Explique trade-offs** (latência × custo × qualidade) com 1–2 frases por decisão.

## 4) Extras (ao final do documento)

* **Glossário enxuto:** RAG, embeddings, reranker, LoRA, QLoRA, KV-cache, batching.
* **Cheatsheet de comandos:** exemplos mínimos para subir Qdrant, chamar BGE-M3, rodar vLLM (OpenAI-compatible) e testar no Ollama.
* **Checklist de produção:** logs/telemetria (OpenTelemetry), limites de taxa, RBAC por índice, backups de vetores, testes de relevância.
* **Perguntas frequentes:** “Quando RAG falha?”, “Quando LoRA compensa?”, “Como reduzir custo?”.

## 5) Conteúdo específico para este caso (preencha)

* **Domínio/Fontes de dados:** `{ex.: PDFs de políticas, base de conhecimento, código}`
* **Idiomas:** `{ex.: PT-BR e EN}`
* **Latência alvo:** `{ex.: p95 ≤ 1500 ms}` | **Usuários simultâneos:** `{ex.: 100}`
* **Restrições:** `{ex.: offline, dados sensíveis, sem nuvem}`

> **Importante:** Se algo for inviável na stack descrita, proponha **ajustes mínimos** (ex.: reduzir top-k, quantizar modelo, mover reranker para CPU) e **explique o impacto**.

---

[1]: https://docs.llamaindex.ai/en/stable/getting_started/concepts/?utm_source=chatgpt.com "High-Level Concepts - LlamaIndex"
[2]: https://huggingface.co/docs/peft/main/en/conceptual_guides/lora?utm_source=chatgpt.com "LoRA"
[3]: https://arxiv.org/abs/2305.14314?utm_source=chatgpt.com "QLoRA: Efficient Finetuning of Quantized LLMs"
[4]: https://docs.vllm.ai/en/latest/serving/openai_compatible_server.html?utm_source=chatgpt.com "OpenAI-Compatible Server - vLLM"
[5]: https://qdrant.tech/documentation/?utm_source=chatgpt.com "Qdrant Documentation"
[6]: https://huggingface.co/BAAI/bge-m3?utm_source=chatgpt.com "BAAI/bge-m3"
