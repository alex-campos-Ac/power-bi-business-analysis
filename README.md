# NovaVarejo — Dashboard de Performance Comercial 📊

## 📋 Sobre o Projeto

Case real de uma distribuidora com 4 filiais, 3 canais de venda (Loja Física, Televendas, E-commerce) e 7 vendedores. O objetivo foi responder, com dados, a pergunta do gestor comercial: *"Estamos faturando, mas não sei de onde vem o dinheiro de verdade."*

O projeto cobre modelagem de dados, medidas DAX aplicando regras reais de negócio e um dashboard interativo no Power BI, com foco em precisão analítica — cada resposta é sustentada por número, não por leitura visual isolada.

## 🛠️ Tecnologias Utilizadas

- **Power BI (DAX):** modelagem de dados (estrela: 1 fato + 4 dimensões) e medidas de negócio.
- **Power Query:** conexão e preparação das bases de origem.

## 🗂️ Modelo de Dados

- `fVendas`: tabela fato com todas as transações (valor, status, vendedor, filial, canal, data).
- `dVendedor`, `dFilial`, `dCanal`, `dCalendario`: dimensões de apoio.

**Regra de negócio central:** apenas vendas com `Status = "Concluída"` representam faturamento real. Vendas Canceladas e Devolvidas são excluídas de todas as medidas financeiras — validado com uma medida auxiliar de contagem por status (88,2% Concluída, 7% Cancelada, 4,8% Devolvida).

## 📊 Principais Medidas DAX

- **Faturamento Total:** soma de vendas filtrando `Status = "Concluída"`.
- **% Faturamento Filial:** participação de cada filial no total, usando `ALL(dFilial)` para ignorar o filtro de contexto.
- **Faturamento Mês Anterior / Status Faturamento:** comparação mês a mês via `DATEADD`.
- **Faturamento Últimos 3 Meses / 3 Meses Anteriores:** comparação de blocos trimestrais via `DATESINPERIOD`, usada para avaliar tendência de crescimento.
- **Ticket Médio:** faturamento dividido pela quantidade de vendas concluídas.
- **Melhor Mês:** identifica dinamicamente o mês de maior faturamento, usando `SUMMARIZE` + `TOPN` (considerando mês **e** ano juntos, evitando somar o mesmo mês de anos diferentes).

## 🧠 Principais Insights

- **Loja Centro** lidera o faturamento (R$ 4,66 Mi, ~30% de participação), mas **Loja Sul está em queda** na comparação trimestral mais recente — sinal de atenção que passaria despercebido numa leitura só do total.
- **Diego Almeida** é o vendedor de maior faturamento (R$ 3,8 Mi); o ticket médio entre vendedores é bastante equilibrado (variação de apenas R$ 60 entre o maior e o menor).
- **Loja Física** ainda lidera a receita entre os canais, mas o **e-commerce mostra tendência de crescimento** ao longo do ano, mesmo com oscilações no meio do período.
- **Sazonalidade clara:** picos em outubro-dezembro se repetem em 2024 e 2025 (Black Friday e Natal), com estabilidade entre junho e setembro.
- Comparando os últimos 3 meses com os 3 anteriores, a empresa está em **crescimento** (~6% de aumento no faturamento).

## 📂 Estrutura do Repositório

- `dataset/`: bases originais (fVendas, dVendedor, dFilial, dCanal, dCalendario).
- `dashboard/`: arquivo `.pbix` e imagem do dashboard final.
- `readme.md`: respostas às perguntas de negócio do case, em texto.

## ⚠️ Nota Metodológica

Este projeto parte de um case estruturado de curso (Formação Analista de Dados — Educadados), com bases fornecidas prontas para importação. O foco de aprendizado foi a construção das medidas DAX e a precisão analítica das respostas às perguntas de negócio propostas.
