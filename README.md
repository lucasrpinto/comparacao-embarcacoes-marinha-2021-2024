# Comparação de Embarcações (2021 vs 2024)

Projeto de **análise de dados** para comparar a **quantidade de embarcações da Marinha do Brasil, por tipo,** entre os anos **2021** e **2024**, identificando **crescimentos, quedas e estabilidade** por categoria.

A análise foi feita em um **Jupyter Notebook** (Python) e os gráficos foram gerados com **Plotly**.

---

## Fonte dos dados

Os dados foram baixados do Portal Brasileiro de Dados Abertos (dados.gov.br), no conjunto:

- https://dados.gov.br/dados/conjuntos-dados/embarcacoes

---

## Observações importantes

- Os arquivos originalmente estavam em **CSV**, mas foram convertidos para **XLSX** para corrigir problemas de leitura/encoding.
- Os gráficos do Plotly podem ser exportados em **HTML** (interativos), para abrir no navegador.

---

## Objetivo

- Comparar a quantidade de embarcações **por tipo** entre 2021 e 2024  
- Medir **diferença absoluta** e **variação percentual**  
- Destacar os **Top aumentos** e **Top quedas**  
- Visualizar os tipos com **maior mudança** comparando 2021 vs 2024

---

## Tecnologias e bibliotecas

- Python 3.10.9 
- pandas, numpy  
- openpyxl (leitura/escrita de `.xlsx`)  
- plotly (gráficos)  
- ipykernel (kernel do Jupyter)

Instalação:
```bash
pip install pandas numpy plotly openpyxl ipykernel
```

---

## Estrutura sugerida do projeto

```
project/
├─ data/
│  ├─ total_tipo_emb_2021.xlsx
│  ├─ total_tipo_emb_2024.xlsx
│  ├─ comparacao_embarcacoes_2021_2024.csv    (gerado)
│  ├─ comparacao_embarcacoes_2021_2024.xlsx   (gerado)
│  ├─ top_aumentos.html                       (gerado)
│  ├─ top_quedas.html                         (gerado)
│  └─ comparativo_2021_2024.html              (gerado)
└─ notebooks/
   └─ comparacao_embarcacoes_2021_2024.ipynb
```

---

## O que foi feito (resumo do fluxo)

### Passo 1 — Importar as bases
- Leitura dos arquivos de 2021 e 2024 a partir da pasta `data/` (formato `.xlsx`).

### Passo 2 — Visualizar e inspecionar
- Conferência de colunas, categorias e possíveis inconsistências.

### Passo 3 — Tratamento / padronização
- Ajuste de tipos (quantidade numérica).
- Padronização do texto em `TIPO_EMBARCACAO` (ex.: remover espaços extras).

### Passo 4 — Análise inicial
- Ranking (Top 10) por tipo em cada ano.
- Gráficos para entender distribuição e principais categorias por ano.

### Passo 5 — Análise detalhada
- **Merge** por `TIPO_EMBARCACAO` (outer), preenchendo ausências com **0**.
- Métricas:
  - `DIF = QTD_2024 - QTD_2021`
  - `VAR_%` (com tratamento quando `QTD_2021 = 0`)
  - `STATUS` (Aumentou / Diminuiu / Estável)
- Gráficos:
  - Top 10 aumentos
  - Top 10 quedas
  - Comparativo 2021 vs 2024 para os tipos com maior mudança

---

## Exportações

### Exportar tabela final (CSV e XLSX)
```python
comparacao.to_csv("../data/comparacao_embarcacoes_2021_2024.csv", index=False, encoding="utf-8-sig")
comparacao.to_excel("../data/comparacao_embarcacoes_2021_2024.xlsx", index=False)
```

### Exportar gráficos do Plotly (HTML interativo)
Coloque **logo após** criar o gráfico (antes ou depois do `fig.show()`):
```python
fig.write_html("../data/comparativo_2021_2024.html")
```

---

## Como executar

1. Instale as bibliotecas:
   ```bash
   pip install pandas numpy plotly openpyxl ipykernel
   ```

2. Abra o notebook:
   - VS Code (Jupyter) ou Jupyter Lab/Notebook

3. Execute as células na ordem do notebook.

---