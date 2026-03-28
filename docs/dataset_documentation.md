# Base de Conhecimento

## Dados Utilizados

Os arquivos originais foram extraídos para formar a base analítica do agente. Os principais utilizados são:

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `loan_portfolio.csv` | CSV | Base principal para treinar o modelo de predição de risco, contendo o histórico de empréstimos, perfis financeiros e a variável alvo de inadimplência (`defaulted`). |
| `macro_stress_scenarios.csv` | CSV | Utilizado opcionalmente para simular como cenários econômicos adversos (estresse macroeconômico) afetariam a projeção de risco do cliente. |

---

## Adaptações nos Dados

Os dados sintéticos originais são bastante ricos, mas para a construção do modelo preditivo do agente, focamos a engenharia de recursos (feature engineering) nas variáveis que demonstraram maior correlação com o risco de calote. As principais adaptações e seleções incluem:

- **Seleção de Features Chave:** - `credit_score`: Pontuação de crédito.
  - `pd_annual`: Probabilidade anual de default.
  - `coupon_rate`: Taxa de juros aplicada.
  - `leverage` e `debt_to_equity`: Indicadores de alavancagem e saúde financeira.
- **Tratamento da Variável Alvo:** A coluna `defaulted` (0 ou 1) é o alvo de classificação do nosso modelo de Machine Learning.

---

## Estratégia de Integração

### Como os dados são carregados?
O LLM não realiza a leitura crua do arquivo CSV a cada pergunta do usuário, pois isso consumiria muitos tokens e seria ineficiente. Em vez disso:
1. O CSV foi utilizado previamente para treinar um modelo de Classificação (ex: Random Forest).
2. O agente coleta as respostas do usuário no chat.
3. O agente envia esses dados como parâmetros para o modelo treinado (via API ou função Python local).
4. O modelo retorna um JSON contendo o diagnóstico matemático (probabilidade).

### Como os dados são usados no prompt?
Os dados retornados pelo modelo de Machine Learning são injetados dinamicamente no contexto (prompt) do LLM. O *System Prompt* orienta o LLM a interpretar esse JSON bruto e transformá-lo em uma resposta humana, analítica e explicativa.

---

## Exemplo de Contexto Montado

Abaixo, um exemplo de como as informações chegam no *prompt* do LLM para que ele gere a resposta final ao cliente:

```text
[DADOS COLETADOS DO USUÁRIO]
- Score de Crédito: 610
- Setor: Tecnologia
- Taxa de Juros (Coupon Rate): 5.2%
- Alavancagem: 8.5

[OUTPUT DO MODELO PREDITIVO]
- Predição de Default: SIM (Risco Alto)
- Probabilidade de Inadimplência: 82%
- Fatores de maior peso: Score de Crédito baixo aliado a taxa de juros alta.

[INSTRUÇÃO PARA O LLM]
Gere um diagnóstico financeiro educado e analítico com base nos dados acima. Explique ao usuário os motivos do seu nível de risco sem emitir juízos de valor.