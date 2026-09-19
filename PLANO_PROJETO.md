# Plano do projeto - mfeat-zernike

## Objetivo

Aplicar um pipeline de Aprendizado de Máquina ao `mfeat-zernike` e investigar onde, quando e por que os modelos erram.

## Entregas

- Notebook Python comentado.
- Versão PDF do notebook.
- Apresentação de 15 minutos.
- Prazo: 21/09/2026 no Classroom.

## Partes obrigatórias

1. Descrição do conjunto de dados.
2. Análise exploratória com estatísticas e gráficos.
3. Discussão dos pré-processamentos.
4. Treinamento com validação cruzada e ajuste de hiperparâmetros.
5. Análise dos erros, que é a parte principal do trabalho.

## Divisão das tarefas

### Mateus - dados e análise exploratória

- Pesquisar e descrever o `mfeat-zernike`.
- Carregar e validar o arquivo ARFF.
- Verificar dimensões, classes, ausentes, duplicatas e escalas.
- Produzir estatísticas, gráficos e visualização com PCA.
- Implementar um `DummyClassifier` como baseline.
- Escrever a introdução e a análise exploratória.

### Gabriel - pré-processamento e modelos

- Separar treino e teste com estratificação.
- Criar pipelines sem vazamento de dados.
- Aplicar padronização quando necessária.
- Treinar regressão logística, k-NN, SVM e Random Forest.
- Ajustar hiperparâmetros com validação cruzada.
- Comparar acurácia e F1 macro.
- Entregar previsões e confiança do melhor modelo ao Ryaj.

### Ryaj - análise dos erros e conclusões

- Criar e interpretar a matriz de confusão.
- Identificar classes e pares de classes mais difíceis.
- Comparar confiança de acertos e erros.
- Localizar erros na visualização PCA.
- Investigar especialmente a confusão entre os dígitos 6 e 9.
- Analisar as instâncias erradas por vários modelos.
- Escrever as conclusões e limitações.

Não é necessário usar todas as ferramentas sugeridas no enunciado. Uma análise de erros bem desenvolvida é suficiente.

## Roteiro de execução

### 1. Carregar e validar os dados

```python
import pandas as pd
from scipy.io import arff

dados, metadados = arff.loadarff("dataset_22_mfeat-zernike.arff")
df = pd.DataFrame(dados)
df["class"] = df["class"].str.decode("utf-8").astype(int)
```

- Confirmar 2.000 linhas, 47 atributos e 10 classes.
- Separar `X` e `y`.
- Usar `random_state=42`.

### 2. Fazer a análise exploratória

- Estatísticas descritivas.
- Distribuição das classes.
- Escalas e correlações dos atributos.
- PCA para visualizar sobreposição entre classes.
- Interpretação depois de cada gráfico.

### 3. Preparar a avaliação

- Reservar 20% dos dados para teste final.
- Usar divisão estratificada.
- Usar validação cruzada com 5 divisões apenas no treino.
- Colocar padronização e modelo no mesmo `Pipeline`.
- Não usar o teste para escolher hiperparâmetros.

### 4. Treinar e comparar modelos

- DummyClassifier como baseline.
- Regressão logística.
- k-NN.
- SVM com kernel RBF.
- Random Forest.
- Comparar acurácia, F1 macro e estabilidade.

### 5. Analisar os erros

- Matriz de confusão absoluta e normalizada.
- Métricas por classe.
- Pares de classes mais confundidos.
- Confiança dos erros.
- Erros no espaço da PCA.
- Instâncias erradas por vários modelos.
- Discussão sobre onde e por que os modelos falham.

### 6. Revisar e entregar

- Executar o notebook do início ao fim.
- Remover células quebradas e testes abandonados.
- Conferir gráficos, tabelas e interpretações.
- Exportar para PDF.
- Enviar notebook e PDF no Classroom.

## Apresentação

- Mateus: dados e análise exploratória - 5 minutos.
- Gabriel: metodologia e modelos - 5 minutos.
- Ryaj: análise dos erros e conclusões - 5 minutos.

## Checklist final

- [ ] As cinco partes exigidas estão no notebook.
- [ ] Todos os resultados possuem interpretação.
- [ ] Não há vazamento entre treino e teste.
- [ ] Os modelos foram comparados nas mesmas condições.
- [ ] A análise explica onde e por que ocorrem os erros.
- [ ] Notebook e PDF executam e abrem corretamente.
- [ ] Os três integrantes conhecem os resultados gerais.

