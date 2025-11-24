# Agriculture Yield Prediction with Monte Carlo Simulation

- 6 fazendas, cada uma com sua propria simulação
- os grãos a serem plantados em cada fazenda são pré definidos
- será calculada a safra média esperada por hectare

### a safra prevista será calculada a partir de 3 indices:
- indice climatico
- indice de manejo
- indice de fertilidade

### Índice Climático (baseado em dados históricos da região)
- Chuva
- Temperatura
- Incidencia Solar

### Índice de Manejo
- Falhas no plantio (quantidade de sementes/plantas que não germinaram)
- Herbicidas (eficácia do herbicida)
- Perdas de colheita (devido à operação não qualificada ou máquinas desgastadas)

### índice de Fertilidade
- Nitrogênio
- Fósforo
- Potássio
- Sódio (ruim)
- Matéria orgânica
- Compactação (ruim)


---
---
---

# Dados para Simulação Monte Carlo

## 1. Fazendas


| Fazenda                   | Localização       |
| ------------------------- | ----------------- |
| **Fazenda Maruim**        | Corupá – SC       |
| **Fazenda Gaúcha**        | Passo Fundo – RS  |
| **Fazenda Campos Gerais** | Ponta Grossa – PR |
| **Fazenda Pantanal**      | Dourados – MS     |
| **Fazenda Cerrado**       | Sorriso – MT      |
| **Fazenda Capital**       | Rio Verde – GO    |

---

## 2. Produção Ajustada por Grão (t/ha)

### As culturas com produtividade ajustada = **0** não entram na simulação.

**Fazenda Maruim – SC**

| Grão     | Prod. Ajustada |
| -------- | -------------- |
| Aveia    | 3.7            |
| Girassol | 0.72           |
| Milho    | 4.2            |
| Soja     | 2.51           |
| Sorgo    | 1.02           |
| Trigo    | 3.96           |

**Fazenda Gaúcha – RS**

| Grão     | Prod. Ajustada |
| -------- | -------------- |
| Aveia    | 3.92           |
| Girassol | 0              |
| Milho    | 6              |
| Soja     | 3.57           |
| Sorgo    | 0              |
| Trigo    | 4.2            |

**Fazenda Campos Gerais – PR**

| Grão     | Prod. Ajustada |
| -------- | -------------- |
| Aveia    | 5.6            |
| Girassol | 0.72           |
| Milho    | 1.56           |
| Soja     | 0.99           |
| Sorgo    | 1.02           |
| Trigo    | 6              |

**Fazenda Pantanal – MS**

| Grão     | Prod. Ajustada |
| -------- | -------------- |
| Aveia    | 0              |
| Girassol | 2.41           |
| Milho    | 8.64           |
| Soja     | 5.55           |
| Sorgo    | 4.54           |
| Trigo    | 0              |

**Fazenda Cerrado – MT**

| Grão     | Prod. Ajustada |
| -------- | -------------- |
| Aveia    | 1.01           |
| Girassol | 2.41           |
| Milho    | 6              |
| Soja     | 4.03           |
| Sorgo    | 4.54           |
| Trigo    | 1.08           |

**Fazenda Capital – GO**
(idêntica a Cerrado)

| Grão     | Prod. Ajustada |
| -------- | -------------- |
| Aveia    | 1.01           |
| Girassol | 2.41           |
| Milho    | 6              |
| Soja     | 4.03           |
| Sorgo    | 4.54           |
| Trigo    | 1.08           |

---

## 3. Solo — Valores Base (ppm, %, MPa)


| Fazenda            |  N |  P |   K | MO (%) | Na | Compactação (MPa) |
| ------------------ | -: | -: | --: | -----: | -: | ----------------: |
| Maruim – SC        | 28 | 14 | 110 |    3.2 |  2 |               1.6 |
| Gaúcha – RS        | 32 | 18 | 130 |    3.8 |  2 |               1.7 |
| Campos Gerais – PR | 30 | 16 | 120 |    3.5 |  2 |               1.9 |
| Pantanal – MS      | 24 | 12 | 105 |    2.8 |  4 |               1.8 |
| Cerrado – MT       | 20 | 10 |  95 |    2.3 |  2 |               2.1 |
| Capital – GO       | 22 | 11 | 100 |    2.5 |  2 |               2.0 |

---

## 4. Manejo — Distribuições Básicas


| Variável                      | Min | Max | Média |
| ----------------------------- | --: | --: | ----: |
| **Falha no plantio (%)**      |   4 |  14 |     8 |
| **Eficácia do herbicida (%)** |  70 |  90 |    80 |
| **Perdas de colheita (%)**    |   6 |  15 |     9 |

---

## 5. Clima — Parâmetros para Gerar Valores Anuais

#### Valores reais para gerar clima sintético por fazenda

### 🌧️ Chuva na Safra (mm)

| Fazenda            | Média | Desvio |
| ------------------ | ----: | -----: |
| Maruim – SC        |   900 |    180 |
| Gaúcha – RS        |   850 |    160 |
| Campos Gerais – PR |   950 |    200 |
| Pantanal – MS      |   780 |    170 |
| Cerrado – MT       |   820 |    220 |
| Capital – GO       |   860 |    210 |

### 🌡️ Temperatura Média da Safra (°C)

| Fazenda            | Média | Desvio |
| ------------------ | ----: | -----: |
| Maruim – SC        |  20.0 |    1.5 |
| Gaúcha – RS        |  19.0 |    1.8 |
| Campos Gerais – PR |  18.5 |    2.0 |
| Pantanal – MS      |  23.5 |    1.5 |
| Cerrado – MT       |  25.0 |    1.8 |
| Capital – GO       |  24.5 |    1.6 |

### ☀️ Radiação Média (MJ/m²/dia)

| Fazenda            | Média | Desvio |
| ------------------ | ----: | -----: |
| Maruim – SC        |    15 |    1.8 |
| Gaúcha – RS        |  15.5 |    2.0 |
| Campos Gerais – PR |  14.8 |    1.6 |
| Pantanal – MS      |    17 |    2.2 |
| Cerrado – MT       |  18.5 |    2.5 |
| Capital – GO       |    18 |    2.1 |

---

## 6. Saídas Desejadas da Simulação

* Produtividade média esperada
* Desvio padrão
* **Risco (CV = desvio/média)**
* Projeção para os próximos **4 anos**

---

