# Prompt Aplicado

Chat GPT Compartilhado > **\[Dicionário Termos IA Generativa]**

# Prompt

## Copie e cole o texto abaixo em uma IA Generativa

Quero um guia **prático e comparativo** sobre **Dicionário de Termos de IA Generativa**. Cubra os tópicos a seguir para **cada termo** da lista:

* LLM (Large Language Model): Modelo de linguagem de larga escala, treinado em bilhões de tokens, capaz de gerar e compreender texto.​
* Prompt: Entrada de texto usada para guiar o modelo.​
* Context Window (Janela de Contexto): Quantidade máxima de tokens que o modelo consegue ler em uma chamada.​
* Token: Unidade mínima de texto processada pelo modelo (≈ pedaço de palavra).​
* Chunk / Chunking: Divisão de documentos longos em partes menores para indexação em RAG.
* Embedding: Representação numérica (vetor) de um texto, usada para calcular similaridade semântica.​
* Vector DB (Banco Vetorial): Banco de dados otimizado para armazenar embeddings e buscar por proximidade (ex.: Qdrant, Milvus).​
* RAG (Retrieval-Augmented Generation): Pipeline onde o modelo consulta dados externos via embeddings antes de gerar resposta.​
* Reranker: Modelo auxiliar que reordena os resultados recuperados, melhorando a precisão do RAG.​
* Fine-tuning: Ajuste dos pesos do modelo com novos dados.
* LoRA (Low-Rank Adaptation): Técnica de fine-tuning leve: treina só matrizes extras em vez de todos os pesos.​
* QLoRA: Versão do LoRA aplicada em modelo quantizado (4 bits), reduzindo custo de treino.​
* Quantização: Compressão de pesos do modelo (ex.: float16 → int4) para caber em GPUs menores, com perda mínima de qualidade.​
* GGUF: Formato otimizado de modelos quantizados para rodar em CPU/GPU via llama.cpp/Ollama.​
* Inference (Inferência): Processo de rodar o modelo para gerar respostas (fase de uso, não de treino).
* Batching: Processar várias requisições em paralelo para aumentar throughput em GPU.​
* KV-Cache (Key/Value Cache): Memória que guarda estados anteriores da geração, acelerando prompts longos e conversas.​
* Throughput (tok/s): Taxa de tokens gerados por segundo pelo modelo.​
* Latency (TTFT, p95):​
  * TTFT (Time To First Token): tempo até o primeiro token sair.​
  * p95: latência que 95% das requisições não ultrapassam.

#### Definição em uma frase
* **Por que importa** (3–5 bullets)
* **Como funciona** (use diagramas ASCII simples quando útil)
* **Exemplo mínimo** (1–2 frases ou pseudo-código)
* **Boas práticas** (5 bullets)
* **Armadilhas comuns** (5 bullets)
* **Custo & performance** (impacto e dicas: batch, quantização, KV-cache)
* **Checklist “pronto para usar/produção”** (6–8 itens marcáveis)

### Termos a cobrir

LLM (Large Language Model); Prompt; Context Window (Janela de Contexto); Token; Chunk / Chunking; Embedding; Vector DB (Banco Vetorial); RAG (Retrieval-Augmented Generation); Reranker; Fine-tuning; LoRA (Low-Rank Adaptation); QLoRA; Quantização; GGUF; Inference (Inferência); Batching; KV-Cache (Key/Value Cache); Throughput (tok/s); Latency (TTFT, p95); **Hallucination** (adicione este termo).

#### Público & contexto

* Público: **devs, arquitetos de software, estudantes avançados**.
* Stack alvo: **open-weights + RAG + modelos quantizados**, com vetores (Qdrant/Milvus) e serving local/cluster.
* Idioma: **PT-BR** com termos técnicos em inglês quando canônicos.
* Cenário: estudo rápido + consulta durante projeto/palestra.

#### Formato de saída (siga esta estrutura para **cada** tópico)

1. **Definição em uma frase**
2. **Por que importa**
3. **Como funciona**
4. **Passo a passo curto** (5–8 passos)
5. **Exemplo mínimo**
6. **Boas práticas** (5)
7. **Armadilhas comuns** (5)
8. **Custo & performance**
9. **Checklist “produção”** (6–8 itens)

#### Requisitos específicos por tema

Use as bases abaixo para manter a terminologia correta e consistente nas definições e exemplos:

* **LLM / Tokens / Context Window:** defina *token* e *janela de contexto* de forma operacional (ex.: 1 token ≈ pedaço de palavra; limites práticos da janela). ([OpenAI Help Center][1])
* **RAG:** explique que combina **memória não-paramétrica** (índice de vetores) + **gerador**; cite o trabalho clássico. ([arXiv][2])
* **Embedding / Vector DB:** descreva embeddings como vetores semânticos e bancos vetoriais como mecanismo de busca por similaridade; traga Qdrant como exemplo. ([qdrant.tech][3])
* **Reranker:** diferencie **bi-encoder** (recuperação) de **cross-encoder** (reranqueamento) e use **bge-reranker-v2** como referência. ([Hugging Face][4])
* **LoRA / QLoRA / Fine-tuning:** deixe claro que LoRA é **PEFT** (adapters de baixa dimensão) e QLoRA é fine-tuning **em modelo quantizado 4-bit**. ([Hugging Face][5])
* **Quantização / GGUF:** explique compressão de pesos (ex.: fp16 → int4) e cite GGUF no **llama.cpp**. ([Hugging Face][6])
* **Batching / KV-Cache / Throughput / Latency (TTFT, p95):** conecte *batching* e *KV-cache* à melhora de **tok/s** e **TTFT**. ([Hugging Face][7])

---

### Extras no final

Inclua:

* **Glossário resumido** com todas as definições em 1 linha.
* **Cheatsheet** de quando usar: *RAG vs Fine-tuning leve (LoRA/QLoRA) vs nada*.
* **Perguntas frequentes (FAQ)**:

  * Quando RAG falha?
  * Quando LoRA/QLoRA compensa?
  * Como reduzir TTFT e aumentar tok/s (batching, KV-cache)?
  * Como escolher top-k e thresholds de reranker?

> **Observação:** se algum termo ficar ambíguo, exemplifique com uma chamada mínima (pseudo-código) e cite a fonte acima usada para a definição.

---

### 🔎 Referências úteis para a IA considerar (para fundamentar o conteúdo)

* **RAG (paper original)** — *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*. ([arXiv][2])
* **Tokens / contagem** — Ajuda OpenAI e *tiktoken cookbook*. ([OpenAI Help Center][1])
* **Context window** — IBM / McKinsey explicadores. ([IBM][8])
* **Vector DB / Qdrant** — docs e artigos Qdrant. ([qdrant.tech][3])
* **BGE-M3 / Reranker v2** — modelos na Hugging Face. ([Hugging Face][4])
* **LoRA (PEFT)** — docs HF/PEFT e curso HF. ([Hugging Face][5])
* **QLoRA** — paper arXiv / versão ACM. ([arXiv][9])
* **KV-Cache** — docs Transformers. ([Hugging Face][7])
* **GGUF / llama.cpp** — docs HF / repositório. ([Hugging Face][6])

---

Quer que eu gere também uma **versão .MD** com este prompt (pronto para subir no seu repositório/handout)?

[1]: https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them?utm_source=chatgpt.com "What are tokens and how to count them?"
[2]: https://arxiv.org/abs/2005.11401?utm_source=chatgpt.com "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"
[3]: https://qdrant.tech/documentation/?utm_source=chatgpt.com "Qdrant Documentation"
[4]: https://huggingface.co/BAAI/bge-m3?utm_source=chatgpt.com "BAAI/bge-m3"
[5]: https://huggingface.co/docs/transformers/en/peft?utm_source=chatgpt.com "PEFT"
[6]: https://huggingface.co/docs/hub/en/gguf-llamacpp?utm_source=chatgpt.com "GGUF usage with llama.cpp"
[7]: https://huggingface.co/docs/transformers/en/cache_explanation?utm_source=chatgpt.com "Caching"
[8]: https://www.ibm.com/think/topics/context-window?utm_source=chatgpt.com "What is a context window?"
[9]: https://arxiv.org/abs/2305.14314?utm_source=chatgpt.com "QLoRA: Efficient Finetuning of Quantized LLMs"
