# analise-dados-python
Projetos e análises desenvolvidos durante o curso de Engenharia Mecânica.

"""
Projeto: Análise de Dados
Autor: Nadiemerson Julho
Curso: Engenharia Mecânica
Descrição: Aplicação de análise de dados utilizando Python.
"""
#===================================
#1.IMPORTAÇÕES
#===================================
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

#===================================
#2.DADOS
#===================================
Ensaios = [410, 395, 402, 418, 390, 405, 399, 412, 407, 392, 415, 400]
serie = pd.Series(Ensaios)

Resistência_minima = 400

#===================================
#3.CÁLCULOS ESTATÍSTICOS
#===================================
media = serie.mean()
mediana = serie.median()
moda = serie.mode().values
maximo = serie.max()
minimo = serie.min()
desvio = serie.std()
amplitude = maximo - minimo
cv = (desvio / media) * 100
quantidade_aprovados = (serie >= Resistência_minima).sum()

#Z-score
z = (Resistência_minima - media) / desvio

#Probabilidade acumulada
probabilidade = norm.cdf(Resistência_minima, media, desvio)

#===================================
#4.RESULTADOS NUMÉRICOS
#===================================
print("===== RELATÓRIO ESTÁTISTICO ====\n")

print(f"Média: {media:.2f} MPa")
print(f"Mediana: {mediana:.2f} MPa")
print(f"Moda: {moda}")
print(f"Máximo: {maximo} MPa")
print(f"Mínimo: {minimo} MPa")
print(f"Desvio padrão: {desvio:.2f}")
print(f"Amplitude: {amplitude}")
print(f"Coeficiente de Variação: {cv:.2f}%")
print(f"Quantidade >= {Resistência_minima} MPA: {quantidade_aprovados}")

print("\n==== ANÁLISE DE NORMALIDADE =====")
print(f"Z-score (400 MPa): {z:.2f}")
print(f"Probabilidade de resistência < 400 MPa: {probabilidade*100:.2f}%")

#===================================
#5.GRÁFICO COM CURVA NORMAL
#===================================
x = np.linspace(minimo, maximo, 100)
y = norm.pdf(x , media, desvio)

plt.hist(serie, bins = 6, density=True, edgecolor='black')
plt.plot(x, y)
plt.axvline(media)
plt.axvline(Resistência_minima)

plt.title("Distribuição da resistência (MPa)")
plt.xlabel("Resistência (MPa)")
plt.ylabel("Densidade")
plt.grid(True)

plt.show()
plt.savefig("grafico_resistencia.png", dpi=300, bbox_inches="tight")
plt.show()

## 📊 Análise Estatística de Resistência de Material

Este projeto realiza análise estatística de ensaios de resistência mecânica.

### 🔧 Métodos utilizados
- Média, mediana e moda
- Desvio padrão
- Coeficiente de variação
- Z-score
- Curva normal

### 📈 Gráfico Gerado

![Distribuição de Resistência](grafico_resistencia.png)
