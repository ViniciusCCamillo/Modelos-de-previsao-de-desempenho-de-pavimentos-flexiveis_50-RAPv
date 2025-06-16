# Modelos de Previsão de Desempenho de Pavimentos Flexíveis (50ª RAPv)

Este repositório contém os modelos preditivos desenvolvidos para o artigo apresentado na **50ª Reunião Anual de Pavimentação (RAPv)**, intitulado:

**"Desenvolvimento de modelos de previsão de desempenho de deformações plásticas em pavimentos flexíveis com uso de redes neurais"**

## 🧠 Objetivo

Desenvolver e disponibilizar modelos de redes neurais artificiais capazes de prever indicadores de desempenho de pavimentos flexíveis, com foco nas deformações plásticas (ATR e IRI), com base em dados reais de monitoramento. Atualmente contém os seguintes arquivos:
- `.pkl`: Arquivos de modelos treinados e objetos auxiliares (escalonador e PCA).
- `.txt`: Registros do processo de treinamento (perda, precisão, épocas).

## ▶️ Como Utilizar
1. Clone o repositório:
```
git clone https://github.com/ViniciusCCamillo/Modelos-de-previsao-de-desempenho-de-pavimentos-flexiveis_50-RAPv.git
cd Modelos-de-previsao-de-desempenho-de-pavimentos-flexiveis_50-RAPv
```
2. Instale as dependências:
```
pip install numpy pandas scikit-learn keras tensorflow
```
3. Execute um exemplo do IRI:
```
import pickle
import numpy as np

# Carregar scaler e modelo
with open("DNN+20-IRI Filtrado (Dados)-Training_metrics-scaler_x.pkl", "rb") as f:
    scaler = pickle.load(f)

with open("DNN+20-IRI Filtrado (Dados)-Model.pkl", "rb") as f:
    model = pickle.load(f)

# Dados de entrada de exemplo
X_novo = np.array([[...]])  # substitua pelos seus dados

# Pré-processar e prever
X_scaled = scaler.transform(X_novo)
y_pred = model.predict(X_scaled)

print("Previsão:", y_pred)
```
> [!CAUTION]
> ⚠️ Certifique-se de que os dados de entrada estejam no mesmo formato usado no treinamento descrito nos arquivos TXT na linha "NOMENCLATURA E ORDEM DAS ENTRADA:".

4. Exemplo de uso do ATR:
```
import pickle
import numpy as np

# Carregar scaler, PCA e modelo treinado
with open("DNN+PCA+0-ATRMED Filtrado-Training_metrics-scaler_x.pkl", "rb") as f:
    scaler = pickle.load(f)

with open("DNN+PCA+0-ATRMED Filtrado-Training_metrics-pca_model.pkl", "rb") as f:
    pca = pickle.load(f)

with open("DNN+PCA+0-ATRMED Filtrado-Model.pkl", "rb") as f:
    model = pickle.load(f)

# Dados de entrada de exemplo
X_input = np.array([[...]])  # substitua pelos seus dados

# Pré-processamento: escala + PCA
X_scaled = scaler.transform(X_input)
X_pca = pca.transform(X_scaled)

# Previsão
y_pred = model.predict(X_pca)
print("Previsão:", y_pred)
```
> [!CAUTION]
> ⚠️ Certifique-se de que os dados de entrada estejam no mesmo formato usado no treinamento descrito nos arquivos TXT na linha "NOMENCLATURA E ORDEM DAS ENTRADA:".

## 📈 Modelo IRI — Ordem de disposição das colunas e descrição das variáveis de entrada
| Variável                      | Descrição                                                                                                             |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Idade (Dados)**             | Tempo em anos desde a construção ou último reforço do pavimento. Não considera micro.                                 |
| **PSI (-1 Ano)**              | Índice de Serviçabilidade Presente (do ano anterior).                                                                 |
| **IDS (-1 Ano)**              | Índice de Defeitos Superficial (do ano anterior). Pode ser substituído pelo IGG.                                      |
| **D0 (-1 Ano)**               | Deflexão máxima medida com FWD (do ano anterior).                                                                     |
| **IRI-convertido (-1 Ano)**   | Índice de Irregularidade Internacional (do ano anterior). Convertido por que veio do QI, mas pode ser o IRI original. |
| **H1ORIGCM (ESTR)**           | Espessura da camada de revestimento (em cm) somando os reforços.                                                      |
| **H2CM (ESTR)**               | Espessura da camada de base (em cm).                                                                                  |
| **NAASHTO acumulado**         | Tráfego acumulado no método AASHTO. Considerar apenas apartir do início do monitoramento e não da vida da rodovia.    |
| **RESUMO\_REFOR.**            | Cm de reforço ou micro-asfalto feito antes do monitoramento.                                                          |
| **RESUMO\_PERCTARE**          | Percentual da área que recebeu obras antes do monitoramento.                                                          |
| **RESUMO (-1 Ano)\_REFOR.**   | Cm de reforço ou micro-asfalto feito no ano anterior.                                                                 |
| **RESUMO (-1 Ano)\_PERCTARE** | Percentual da área que recebeu obras no ano anterior.                                                                 |

## 📈 Modelo ATRMED — Ordem de disposição das colunas e descrição das variáveis de entrada
| Variável                      | Descrição                                                                                                             |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Idade (Dados)**             | Tempo em anos desde a construção ou último reforço do pavimento. Não considera micro.                                 |
| **PSI (-1 Ano)**              | Índice de Serviçabilidade Presente (do ano anterior).                                                                 |
| **D0 (-1 Ano)**               | Deflexão central medida com equipamento (do ano anterior).                                                            |
| **IRI-convertido (-1 Ano)**   | Índice de Irregularidade Internacional (do ano anterior). Convertido por que veio do QI, mas pode ser o IRI original. |
| **ATRMED (-1 Ano)**           | Deformação plástica média acumulada (do ano anterior).                                                                |
| **H1ORIGCM (ESTR)**           | Espessura da camada de revestimento (em cm).                                                                          |
| **H2CM (ESTR)**               | Espessura da camada de base (em cm).                                                                                  |
| **NAASHTO acumulado**         | Tráfego acumulado no método AASHTO. Considerar apenas apartir do início do monitoramento e não da vida da rodovia.    |
| **RESUMO\_REFOR.**            | Cm de reforço ou micro-asfalto feito antes do monitoramento.                                                          |
| **RESUMO\_PERCTARE**          | Percentual da área que recebeu obras antes do monitoramento.                                                          |
| **RESUMO (-1 Ano)\_REFOR.**   | Cm de reforço ou micro-asfalto feito no ano anterior.                                                                 |
| **RESUMO (-1 Ano)\_PERCTARE** | Percentual da área que recebeu obras no ano anterior.                                                                 |

## 📌 Requisitos
- Python 3.8+
- Keras / TensorFlow
- scikit-learn
- numpy, pandas

## 📖 Citação
Caso utilize este repositório, por favor cite o trabalho correspondente apresentado na 50ª RAPv.

## 📝 Licença
Este projeto está licenciado sob os termos da licença MIT. Veja o arquivo `LICENSE` para mais detalhes.
