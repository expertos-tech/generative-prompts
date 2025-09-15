Quero um guia **prático e comparativo** sobre *deployment patterns*, cobrindo estes 8 itens:

1. **Canary Release** — liberar para uma fração dos usuários primeiro
2. **Blue-Green Deployment** — alternar entre duas versões em paralelo
3. **A/B Testing** — comparar versões com grupos de usuários diferentes
4. **Feature Flags / Toggles** — ativar/desativar funcionalidades sem redeploy
5. **Rolling Update** — atualizar gradualmente instâncias no cluster
6. **Shadow Deployment** — trafegar em paralelo para a nova versão sem impacto ao usuário
7. **Dark Launch** — feature ativa no backend, escondida do usuário
8. **Rollback Automático** — voltar à versão estável ao detectar falhas

### Contexto e premissas

* Público: times de **engenharia/SRE**.
* Plataforma principal: **Kubernetes** (ex.: AKS/EKS/GKE) com Ingress (NGINX/Traefik) ou service mesh (Istio) **e** alternativa para **serverless** (ex.: Azure Functions) quando aplicável.
* Foco: **redução de risco**, **observabilidade** (golden signals), **SLO/error budget** e **experimentos de caos** controlados.

### Saída esperada (estrutura obrigatória)

Para **cada padrão**, entregue as seções abaixo, nesta ordem:

**A. Em uma frase**: defina o padrão de forma clara e direta.
**B. Quando usar / Quando evitar**: 3–5 bullets para cada.
**C. Pré-requisitos**: arquitetura, ferramentas e permissões mínimas.
**D. Passos de implementação**: passo a passo objetivo (5–8 passos).
**E. Exemplos práticos**:

* **Kubernetes**: manifeste um exemplo mínimo (YAML) — pode usar *Istio VirtualService/Subset* ou *NGINX Ingress annotation*; onde fizer sentido, mostre **Argo Rollouts**.
* **Serverless (opcional)**: ilustre como simular o mesmo padrão usando **roteamento por peso** (ex.: Azure Front Door/Traffic Manager) ou **feature flags**.
  **F. Observabilidade & gates**:
* Métricas a observar (P95/P99 latência, taxa de erro, saturação, tráfego).
* **Abort/rollback conditions** (limiares numéricos).
* Exemplo de **SLO** relacionado.
  **G. Chaos Engineering (mini-experimento)**: 1 experiência simples para validar o padrão (ex.: injetar 300ms de latência, matar 1 pod, simular falha intermitente).
  **H. Riscos & armadilhas**: 5 bullets (ex.: *session stickiness*, thundering herd, vieses em A/B, flags órfãs).
  **I. Custo & complexidade**: baixo/médio/alto com 1 linha de justificativa.
  **J. Checklist de pronto-para-produção**: 6–8 itens marcáveis.

### Extras no final do documento

1. **Matriz comparativa** (tabela): Linhas = 8 padrões; Colunas = “Risco reduzido”, “Complexidade operacional”, “Requer tráfego elevado?”, “Rollback fácil?”, “Impacto no usuário”, “Compatível com serverless?”, “Ferramentas comuns”.
2. **Árvore de decisão** (texto): regras rápidas do tipo *Se risco alto + tráfego grande → Canary/Argo; se dark-feature → Flags + Dark Launch; se troca rápida sem downtime → Blue-Green*, etc.
3. **Snippets prontos**:

   * YAML **Argo Rollouts** para canário com pesos 5% → 25% → 50% + **rollbacks automáticos** por métrica.
   * **Istio** VirtualService com *traffic shifting* por subset.
   * Exemplo **Feature Flag** (SDK genérico) com *kill-switch* e expiração de flag.
4. **Guia de rollback seguro**: estratégias (imediato, progressivo, flag kill-switch), pré-requisitos e comando/YAML de exemplo.

### Estilo de resposta

* Seja **direto e acionável**.
* Use **código em blocos** e **listas curtas**.
* Evite jargão desnecessário; foque no que um time consegue **aplicar esta semana**.

Se algum contexto estiver faltando, **assuma padrões sensatos** (ex.: Istio presente; métricas via Prometheus/Grafana; logs centralizados) e siga. Produza a resposta completa.