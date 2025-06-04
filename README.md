# Monte Carlo Drawdown Analysis 📈

Uma ferramenta Python para análise de risco de carteiras usando simulação Monte Carlo, focada na previsão de drawdowns futuros para diferentes estratégias de investimento.

## 🚀 Funcionalidades

- **Análise Histórica**: Calcula drawdowns históricos de ativos
- **Simulação Monte Carlo**: Prevê drawdowns futuros usando 10.000 simulações
- **Múltiplas Estratégias**: Suporte para Buy & Hold, Cruzamento de Médias Móveis e RSI Reversal
- **Visualizações Interativas**: Gráficos detalhados usando Plotly
- **Relatório de Risco**: Classificação automática de risco com métricas detalhadas


## 💡 Como Usar

### Exemplo Básico

```python
# Executa análise completa para BOVA11 com estratégia de cruzamento de médias
results = run_complete_drawdown_analysis("BOVA11.SA", strategy='ma_cross')
```

### Estratégias Disponíveis

1. **Buy & Hold** (`'buy_hold'`): Sempre comprado no ativo
2. **Cruzamento de Médias** (`'ma_cross'`): Compra quando MA20 > MA50
3. **RSI Reversal** (`'rsi_reversal'`): Compra em oversold (RSI < 30)

### Exemplo Personalizado

```python
# Carrega dados do ativo
data = load_stock_data("PETR4.SA", start_date="2020-01-01")

# Calcula retornos da estratégia
returns = calculate_simple_strategy_returns(data, strategy='buy_hold')

# Executa Monte Carlo (3 anos, 10.000 simulações)
max_drawdowns, final_values = monte_carlo_drawdown_simulation(
    returns, years=3, num_simulations=10000, initial_value=100000
)

# Gera relatório de risco
risk_metrics = generate_risk_report(max_drawdowns, final_values, "PETR4.SA", "Buy & Hold")
```

## 📊 Outputs

### 1. Gráficos Gerados

#### Análise Monte Carlo - Drawdowns Futuros
![Monte Carlo Analysis](https://github.com/user-attachments/assets/your-image-1-url)

- **Distribuição dos Drawdowns**: Histograma mostrando frequência dos drawdowns simulados
- **Box Plot**: Visualização dos quartis e outliers
- **Probabilidades Acumuladas**: Função de distribuição cumulativa (CDF)
- **Cenários de Risco**: Percentis P50, P75, P90, P95, P99

#### Análise Histórica - Evolução da Carteira
![Historical Analysis](https://github.com/user-attachments/assets/your-image-2-url)

- **Curva de Equity**: Evolução do valor da carteira ao longo do tempo
- **Drawdown Histórico**: Períodos de perdas e recuperação
- **Drawdown Máximo**: Maior perda registrada no período analisado

### 2. Relatório de Risco

```
RELATÓRIO DE RISCO MONTE CARLO
Ativo: BOVA11.SA | Estratégia: ma_cross
================================================================================
ESTATÍSTICAS DOS DRAWDOWNS FUTUROS (3 anos):
   • Drawdown médio esperado: 18.45%
   • Drawdown mediano: 16.32%
   • Desvio padrão: 12.89%
   • Mínimo (melhor caso): 2.15%
   • Máximo (pior caso): 67.43%

CENÁRIOS DE RISCO (Probabilidade de EXCEDER):
   • 50% chance de DD > 16.32% (cenário médio)
   • 25% chance de DD > 26.78% (cenário conservador)
   • 10% chance de DD > 38.94% (cenário muito conservador)
   •  5% chance de DD > 45.12% (cenário extremamente conservador)
   •  1% chance de DD > 58.67% (cenário catastrófico)

CLASSIFICAÇÃO DE RISCO: MÉDIO
   • Drawdowns significativos possíveis
```

## 🎯 **Exemplo de Análise - BOVA11.SA**

### Resultados da Simulação Monte Carlo

A análise do BOVA11 com estratégia de cruzamento de médias móveis revela:

- **Drawdown Histórico Máximo**: 17.24%
- **Drawdown Mediano Simulado**: ~22% (próximos 3 anos)
- **Cenário Conservador (P90)**: ~35% de drawdown máximo
- **Distribuição**: Normal com cauda direita, indicando risco de perdas extremas

### Interpretação dos Gráficos

O primeiro gráfico mostra que existe uma probabilidade de 10% de drawdowns superiores a 35%, enquanto o cenário mediano aponta para perdas máximas de 22%. A análise histórica demonstra períodos de volatilidade significativa, especialmente durante 2020 (COVID-19) e 2023.

---

### `load_stock_data(ticker, start_date, end_date)`
Carrega dados históricos do Yahoo Finance

### `calculate_simple_strategy_returns(data, strategy)`
Calcula retornos para diferentes estratégias de investimento

### `monte_carlo_drawdown_simulation(returns, years, num_simulations)`
Executa simulação Monte Carlo para prever drawdowns futuros

### `plot_drawdown_analysis(max_drawdowns, ticker, strategy_name)`
Gera visualizações interativas da análise de drawdown

### `generate_risk_report(max_drawdowns, final_values, ticker, strategy_name)`
Produz relatório detalhado com classificação de risco

## 📈 Metodologia

### Monte Carlo
- **Bootstrap**: Reamostragem dos retornos históricos
- **10.000 Simulações**: Para garantir robustez estatística
- **3 Anos Futuros**: Horizonte de análise (ajustável)

### Métricas de Risco
- **Drawdown Máximo**: Maior perda peak-to-trough
- **Percentis de Risco**: P50, P75, P90, P95, P99
- **Classificação**: Baixo, Médio ou Alto risco


## ⚠️ Limitações

- Assume que retornos futuros seguem padrões históricos e uma distribuição normal
- Não considera custos de transação
- Simulação baseada em bootstrap dos dados históricos
- Estratégias são simplificadas para fins demonstrativos


**Disclaimer**: Esta ferramenta é apenas para fins educacionais e de pesquisa. Não constitui aconselhamento financeiro. Sempre consulte um profissional qualificado antes de tomar decisões de investimento.