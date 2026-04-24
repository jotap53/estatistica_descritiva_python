# Framework Analítico — Pensamento de Cientista de Dados

## O ponto de partida

Todo projeto começa com **uma pergunta de negócio**, e tudo que você faz é para respondê-la.

Exemplos de perguntas de negócio:
- "O produto A performa melhor que o produto B?"
- "Qual grupo de clientes gasta mais?"
- "O tratamento reduziu o tempo de recuperação?"

---

## Passo 1 — Traduza a pergunta em métrica

Você não analisa os dados brutos. Você analisa **o que os dados te dizem sobre a pergunta**.

Se a pergunta é "qual tratamento é mais eficaz?", a métrica pode ser:

```
Redução = Valor Antes - Valor Depois
```

Se a pergunta é "qual campanha gerou mais retorno?", a métrica pode ser:

```
ROI = (Receita Gerada - Custo da Campanha) / Custo da Campanha
```

```python
# Exemplo genérico
df['metrica'] = df['coluna_antes'] - df['coluna_depois']
```

> **Regra:** Antes de codificar qualquer coisa, pergunte — qual número, se calculado, responde minha pergunta?

---

## Passo 2 — Leia as medidas descritivas com intenção

Nunca olhe os números soltos. Para cada medida, pergunte: **"o que isso me diz sobre a minha pergunta?"**

| Medida | O que pergunta |
|---|---|
| **Média** | Qual é o valor típico do grupo? |
| **Mediana** | Metade das observações está acima de quanto? |
| **Desvio padrão** | Os resultados são consistentes ou variam muito? |
| **CV (%)** | Qual grupo tem resultado mais previsível? |
| **Amplitude** | Qual foi o pior e o melhor caso? |

### Regras práticas

- **CV abaixo de 25%** → dado homogêneo, a média representa bem o grupo.
- **CV acima de 25%** → há muita variação, a média sozinha engana.
- **Mediana muito diferente da média** → existem outliers puxando a média para cima ou para baixo.

---

## Passo 3 — Leia os gráficos com intenção

Cada gráfico responde uma pergunta diferente. Nunca gere um gráfico sem saber qual pergunta ele responde.

### Boxplot
- A caixa (IQR) mostra onde estão 50% das observações.
- A linha do meio é a mediana.
- Os pontos fora dos "bigodes" são outliers (casos atípicos).
- **Pergunte:** qual grupo tem mediana maior? Qual tem mais outliers?

### Histograma
- Mostra o formato da distribuição.
- Simétrico (forma de sino) → distribuição normal.
- Assimétrico à direita → a maioria teve valores baixos, poucos tiveram valores altos.
- Assimétrico à esquerda → a maioria teve valores altos.
- **Pergunte:** a distribuição é parecida entre os grupos que estou comparando?

### Gráfico de barras (médias)
- Comparação direta entre grupos.
- **Cuidado:** a média esconde a variação. Use sempre junto com o boxplot.

### Boxplot por categoria
- Mostra se uma variável categórica influencia o resultado.
- **Pergunte:** os grupos respondem de forma diferente? Isso é relevante para a conclusão?

---

## Passo 4 — Monte o argumento

Com os números e gráficos na mão, você constrói a narrativa. A estrutura é sempre a mesma:

1. **O que a média diz?** — comparação direta entre grupos.
2. **O que a dispersão diz?** — qual grupo é mais consistente?
3. **O que a visualização confirma?** — o gráfico bate com os números?
4. **Existe algum caso atípico?** — outliers que merecem investigação.

### Exemplo de raciocínio
> "O grupo A teve média de X, contra Y do grupo B — X% superior em média.
> O desvio padrão do grupo A foi menor (Z vs W), indicando resultado mais consistente.
> No boxplot, a mediana do grupo A está visivelmente acima do grupo B,
> e há menos outliers — o que reforça a consistência do resultado."

---

## Passo 5 — Aponte as limitações

Todo bom cientista de dados sabe o que os dados **não** provam. Isso é tão importante quanto a análise em si.

Perguntas que você deve sempre fazer:

- **A amostra é representativa?** O tamanho é suficiente para generalizar?
- **Há viés no experimento?** A forma de coleta dos dados pode ter distorcido o resultado?
- **O que não foi medido?** Quais variáveis relevantes ficaram de fora?
- **Descrição vs. Inferência:** descritivas mostram padrões, mas para *provar* que uma diferença é real, é necessário um teste de hipótese.

---

## O ciclo mental resumido

```
Pergunta → Métrica → Descritiva → Visualização → Argumento → Limitações
```

Repita esse ciclo para cada análise. Com o tempo e a prática diária, isso vira instinto.

---

## Próximos passos na jornada

| Etapa | O que aprender |
|---|---|
| Análise descritiva | Medidas de posição e dispersão ← *você está aqui* |
| Visualização | Escolher o gráfico certo para cada pergunta |
| Probabilidade | Entender incerteza e distribuições |
| Testes de hipótese | Provar estatisticamente se uma diferença é real |
| Correlação e regressão | Entender relações entre variáveis |
