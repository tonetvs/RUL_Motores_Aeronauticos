
# Predição da Vida Útil de Motores Aeronáuticos (RUL)

Este projeto tem como objetivo desenvolver um modelo preditivo profissional para estimar a vida útil remanescente (RUL - Remaining Useful Life) de motores aeronáuticos, com base em sensores operacionais, configurações de voo e ciclos de operação. A solução adota uma abordagem híbrida que combina redes neurais recorrentes (LSTM) com o algoritmo XGBoost, visando capturar tanto os padrões temporais de degradação quanto as relações não-lineares entre variáveis.

Ao antecipar falhas críticas com precisão, o modelo oferece suporte para decisões de manutenção preditiva, aumentando a confiabilidade e eficiência dos motores em ambientes aeronáuticos.

## Objetivo

Prever a quantidade de ciclos restantes até a falha de cada motor, utilizando dados sensoriais reais. O foco está em criar uma solução robusta, aplicável em contextos industriais, e capaz de antecipar o ponto de falha com alta aderência à trajetória real de degradação.

## Dataset

- Fonte: NASA CMAPSS (FD001)
- Unidades monitoradas individualmente por ciclo
- Sensores técnicos com diferentes taxas de correlação com a falha
- Variável alvo: RUL
- Divisão temporal por motor: treino, validação e teste

## Metodologia

### 1. Pré-processamento:
- Leitura do dataset CMAPSS
- Cálculo da variável alvo RUL
- Remoção de sensores redundantes e com baixa variabilidade
- Engenharia de features:
  - Deltas e janelas temporais
  - Extração de últimos ciclos críticos
  - Aplicação de log1p(RUL)
- Padronização (StandardScaler)

### 2. Modelagem:
- LSTM (Keras) para aprendizado do padrão de degradação temporal
- XGBoost para correção dos picos e melhoria do ajuste fino
- Estratégia híbrida de combinação de previsões
- Avaliação com MAE, RMSE e R² em validação e teste

### 3. Visualização:
- Curvas reais vs previstas por motor
- Análise de erros nos últimos ciclos
- Visualização da distribuição dos resíduos

## Pipeline

```mermaid
flowchart LR
  A[Dados brutos] --> B[Engenharia de features]
  B --> C[Padronização]
  C --> D1[LSTM]
  C --> D2[XGBoost]
  D1 --> E[Predição Híbrida]
  D2 --> E
  E --> F[Avaliação final]
```

## Resultados

As métricas de desempenho serão apresentadas para o conjunto de validação e teste separadamente. Substitua abaixo pelos valores obtidos no notebook:

## Resultados

 Avaliação Geral (Modelo Híbrido — Blend α*)  
**Validação**  
- MAE  : 7.08  
- RMSE : 10.25  
- R²   : 0.9130  

**Teste**  
- MAE  : 12.81  
- RMSE : 21.82  
- R²   : 0.7534  

 Avaliação Focada nos Ciclos Finais (RUL ≤ 40)  
**Validação**  
- MAE  : 5.22  
- RMSE : 6.71  
- N    : 522  

**Teste**  
- MAE  : 5.57  
- RMSE : 7.95  
- N    : 491  

## Bibliotecas Utilizadas

- pandas  
- numpy  
- matplotlib  
- seaborn  
- scikit-learn  
- xgboost  
- tensorflow / keras  
- jupyter

## Execução

O notebook principal já está com os resultados executados e documentados. Pode ser aberto diretamente em qualquer ambiente compatível com Jupyter Notebook.  



## Estrutura

rul-motores-aeronauticos/  
├── data/                       
├── models/                    
├── RUL_motores_aeronauticos.ipynb  
├── requirements.txt  
├── README.md  
└── LICENSE

## Autor

Heitor Tonet  
Engenheiro de Controle e Automação e Cientista de Dados, com foco em manutenção preditiva industrial, especializado em modelos de RUL, detecção de falhas, séries temporais e simulações baseadas em física.

## Licença

Este projeto está sob a licença MIT.
