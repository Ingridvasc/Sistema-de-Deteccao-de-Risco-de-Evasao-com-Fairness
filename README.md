# Sistema de Detecção de Risco de Evasão com Fairness

## Sumário
- [Visão Geral](#visão-geral)
- [Problema](#problema)
- [Solução](#solução)
- [Tecnologias](#tecnologias)
- [Dataset](#dataset)
- [Metodologia](#metodologia)
- [Resultados](#resultados)
- [Autor](#autor)

## Visão Geral
Este projeto implementa um sistema de **Machine Learning com foco em Fairness** para prever o risco de evasão de estudantes universitários. A solução combina técnicas preditivas com análise de viés algorítmico para garantir equidade entre diferentes grupos demográficos, especialmente entre **bolsistas e não bolsistas**.

## Problema
As instituições de ensino superior enfrentam altas taxas de evasão estudantil, mas modelos preditivos tradicionais frequentemente apresentam **viés algorítmico**:
- Melhor desempenho para alunos de classe alta
- Pior desempenho para alunos bolsistas
- Disparidades significativas entre grupos demográficos

**Contexto real**: Estudo anterior identificou que modelo tinha performance **muito melhor para alunos de classe alta** (38.7% de acurácia na detecção) do que para **alunos bolsistas** (12.2%).

## Solução
Desenvolvemos um sistema que:
1. **Prediz evasão** com alta precisão (84.6% de acurácia)
2. **Analisa fairness** usando métricas como Equalized Odds
3. **Mitiga viés** através de threshold tuning por grupo
4. **Mantém transparência** em todas as decisões

## Tecnologias
- **Python 3.8+**
- **Machine Learning**: Scikit-learn, Logistic Regression
- **Fairness**: Métricas customizadas, threshold tuning
- **Análise de Dados**: Pandas, NumPy
- **Visualização**: Matplotlib, Seaborn
- **Relatório**: LaTeX para documentação técnica

## Dataset
| Característica | Valor |
|----------------|--------|
| **Registros** | 4.424 estudantes |
| **Variáveis** | 37 características |
| **Período** | Dados históricos 2008-2019 |
| **Target** | Dropout (32.1%), Graduate (49.9%), Enrolled (17.9%) |

**Principais features utilizadas**:
- Notas anteriores e de admissão
- Idade no ingresso
- Status de bolsa (24.8% bolsistas)
- Gênero (64.8% feminino, 35.2% masculino)
- Notas do 1º e 2º semestres
- Indicadores econômicos (desemprego, inflação, PIB)

## Metodologia
### 1. **Análise Exploratória (EDA)**
- Distribuição demográfica
- Correlações com evasão
- Identificação de possíveis viéses

### 2. **Modelo Baseline**
- **Algoritmo**: Regressão Logística com regularização L2
- **Class weight**: 'balanced' para lidar com desbalanceamento
- **Split**: 70% treino, 15% validação, 15% teste
- **Métricas**: Accuracy, Precision, Recall, F1, ROC-AUC

### 3. **Análise de Fairness**
- **Equalized Odds**: Disparidades em FPR (False Positive Rate) e FNR (False Negative Rate)
- **Demographic Parity**: Diferença nas taxas de predição positiva
- **Análise por subgrupos**: Bolsistas vs não bolsistas, gênero

### 4. **Mitigação de Viés**
- **Técnica**: Threshold tuning por grupo
- **Objetivo**: Equalizar taxas de erro entre grupos
- **Implementação**: Limites de decisão diferentes para bolsistas e não bolsistas

## Resultados
### Desempenho do Modelo
| Métrica | Valor | Interpretação |
|---------|-------|---------------|
| **Acurácia** | 84.64% | Excelente desempenho geral |
| **Precisão** | 76.30% | 76% dos preditos como evasão realmente evadem |
| **Recall** | 75.59% | 76% dos evadidos são identificados |
| **F1-Score** | 75.94% | Bom balanceamento |
| **ROC-AUC** | 89.54% | Excelente capacidade discriminativa |

### Análise de Fairness
| Grupo | Taxa de Evasão Real | Disparidade Demográfica |
|-------|-------------------|------------------------|
| **Não Bolsistas** | 38.7% | - |
| **Bolsistas** | 12.2% | 0.264 (26.4%) |
| **Feminino** | 25.1% | - |
| **Masculino** | 45.1% | 0.200 (20.0%) |

### Após Mitigação de Viés
| Métrica | Antes | Depois | Redução |
|---------|-------|--------|---------|
| **Disparidade FPR** | 15.2% | 5.1% | 66.4% |
| **Disparidade FNR** | 8.3% | 3.2% | 61.4% |
| **Acurácia** | 84.64% | 83.44% | 1.2% |

**Trade-off aceitável**: Redução de 1.2% na acurácia para ganho de >60% em fairness!

## Autor

**Ingrid Vasconcelos**  
[![GitHub](https://img.shields.io/badge/-Ingrid_Vasconcelos-181717?logo=github&logoColor=white)](https://github.com/Ingridvasc)
[![LinkedIn](https://img.shields.io/badge/-Linkedin-0A66C2?logo=linkedin)](https://www.linkedin.com/in/ingrid-vasconcelos-18635a230/)
