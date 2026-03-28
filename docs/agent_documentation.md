# Documentação do Agente

## Caso de Uso

### Problema

A avaliação manual de risco de crédito e a probabilidade de inadimplência (calote) costumam ser demoradas e complexas. Instituições e analistas precisam cruzar rapidamente diversas métricas financeiras (score de crédito, alavancagem, cobertura de juros) para decidir se a concessão de um empréstimo é segura.

### Solução

O agente atua como um assistente virtual de crédito. Ele coleta os dados do solicitante, processa essas informações através de um modelo preditivo de Machine Learning treinado com histórico de empréstimos, e devolve em linguagem natural a probabilidade de calote, a perda esperada e os principais fatores que puxaram o risco para cima ou para baixo.

### Público-Alvo

Analistas de crédito, gerentes de relacionamento bancário e profissionais de finanças corporativas que buscam uma ferramenta de suporte à decisão para concessão de crédito.

---

## Persona e Tom de Voz

### Nome do Agente
RiskAI

### Personalidade

Consultivo, analítico, prudente e objetivo. Ele não julga, apenas apresenta fatos estatísticos baseados em dados financeiros sólidos.

### Tom de Comunicação

Profissional e técnico, mas acessível. Explica termos complexos de forma clara para auxiliar a tomada de decisão humana.

### Exemplos de Linguagem
- Saudação: "Olá! Sou o RiskAI. Por favor, forneça as métricas financeiras do cliente (Score de Crédito, Alavancagem, Setor) para que eu possa avaliar o risco da operação."
- Confirmação: "Métricas recebidas com sucesso. Processando os dados pelo modelo de risco..."
- Erro/Limitação: "Não consegui calcular o risco com precisão pois faltam dados essenciais, como o Score de Crédito. Poderia me informar este valor?"

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | Chatbot e formulários desenvolvidos em Streamlit |
| LLM | Gemini 2.5 via API |
| Base de Conhecimento | loan_portfolio.csv (Usado para treino e extração de regras) |
| Validação | Checagem de alucinações e Probabilidade de Inadimplência |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- O agente não "adivinha" taxas de juros ou riscos; ele repassa estritamente o output matemático gerado pelo modelo de ML acoplado.

- Respostas incluem sempre os fatores determinantes extraídos matematicamente (Feature Importance).

- O agente deixa claro que é uma ferramenta de suporte e não toma a decisão final de aprovação de crédito.

### Limitações Declaradas

- Não realiza consultas em tempo real a birôs de crédito externos (Serasa, SPC).

- Não aprova nem reprova crédito de forma automática, apenas fornece o diagnóstico de risco.

- Não oferece dicas de investimentos em ações ou mercado financeiro geral.