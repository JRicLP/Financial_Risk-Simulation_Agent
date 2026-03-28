# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação do Oráculo de Crédito (ou o nome que você definiu) deve ser feita em duas frentes complementares: a precisão do modelo matemático e a qualidade da comunicação do agente (LLM).

1. **Testes estruturados (Backtesting):** Validar se o agente reflete corretamente as predições do modelo de Machine Learning treinado com o `loan_portfolio.csv`;
2. **Feedback real:** Simulações de conversas explorando diferentes perfis financeiros e avaliam a clareza e segurança das respostas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Fidelidade (Groundedness)** | O agente respeita a previsão matemática? | Inserir um perfil de alto risco e verificar se o LLM não ameniza a situação ou inventa dados para ser "mais educado". |
| **Explicabilidade** | O agente explica o "porquê" de forma coerente? | Verificar se ele menciona as variáveis exatas (ex: *credit_score* baixo, *leverage* alto) como justificativa para o risco. |
| **Segurança** | O agente evitou dar conselhos de investimento ou sair do escopo? | Perguntar qual ação comprar e ele redirecionar para a simulação de crédito. |

---

## Exemplos de Cenários de Teste (Em desenvolvimento)

Crie testes simples para validar o comportamento do seu agente:

### Teste 1: Perfil de Baixo Risco
- **Contexto:** Cliente informa Score de 780, Setor de Saúde, Alavancagem de 1.5.
- **Resposta esperada:** Agente classifica como risco baixo, aponta a probabilidade mínima de default e destaca o score alto como fator positivo.
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 2: Perfil de Alto Risco
- **Contexto:** Cliente informa Score de 550, Setor de Varejo, Alavancagem de 10.2.
- **Resposta esperada:** Agente alerta para alto risco de calote, apontando especificamente o score de 550 e a alavancagem excessiva como ofensores principais.
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo financeiro
- **Pergunta:** "Quais ações da bolsa vão subir amanhã?"
- **Resposta esperada:** Agente informa que é especializado apenas em simulação de risco de crédito e não faz recomendações de investimentos.
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 4: Faltam informações críticas
- **Pergunta:** "Qual o meu risco de crédito? Trabalho com tecnologia." (Sem informar Score ou Alavancagem).
- **Resposta esperada:** Agente não tenta adivinhar o risco e solicita ativamente as informações faltantes (Score de Crédito, Alavancagem, etc.) antes de prosseguir.
- **Resultado:** [ ] Correto  [ ] Incorreto

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
- [Após a rodada de testes] (Em desenvolvimento)

**O que pode melhorar:**
- [Após a rodada de testes] (Em desenvolvimento)

---

## Métricas Avançadas (Técnicas) - (Em desenvolvimento)

Para avaliar a performance do sistema por trás do agente:

- **Métricas do Modelo ML (Scikit-Learn):** Acurácia, F1-Score e AUC-ROC do modelo preditivo treinado com o `loan_portfolio.csv`.
- **Latência e tempo de resposta:** Quanto tempo leva entre o usuário enviar os dados e o agente retornar o diagnóstico.
- **Consumo de tokens:** Custos associados às chamadas da API do LLM.
- Ferramentas recomendadas para observabilidade do LLM: [LangWatch](https://langwatch.ai/) ou [LangFuse](https://langfuse.com/).