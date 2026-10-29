# Análisis de datos con Python: viviendas de California y mercado eléctrico de España

Dos análisis exploratorios hechos con pandas, desde los datos crudos hasta las conclusiones. El primero estudia qué se relaciona con el precio de las viviendas en California, y el segundo, cómo se comportan el precio, la demanda y la generación de electricidad en España entre 2014 y 2018. En ambos, cada decisión de limpieza se justifica con un control previo.

## Metodología

Los dos notebooks siguen el mismo recorrido:

1. **Exploración:** forma del dataset, tipos de variables, nulos y primeras preguntas.
2. **Limpieza y preprocesamiento:** primero se buscan los problemas (nulos, duplicados, valores topados, fechas corridas) y recién después se decide qué hacer con cada uno.
3. **Análisis simple:** distribuciones, comparaciones por grupo, gráficos de barras y líneas.
4. **Análisis complejo:** correlaciones, mapas de calor, dispersiones y series de tiempo.
5. **Conclusiones y limitaciones.**

## Estructura del repositorio

```
.
├── 01_california.ipynb         # Precios de viviendas en California
├── 02_energia_espana.ipynb     # Mercado eléctrico de España
├── housing.csv                 # Datos del notebook 1
├── spain_energy_market.csv     # Datos del notebook 2
└── .gitignore
```

## Hallazgos

### California (1990, una fila por zona del censo)

- El dataset trae 20.640 zonas; se eliminaron las 207 con datos faltantes en `total_bedrooms`, y quedaron 20.433.
- Varias columnas están **topadas**: el precio máximo (500.001) se repite en 958 zonas, y el ingreso y la edad de las viviendas también tienen un valor máximo artificial. Se tratan por separado para no distorsionar los promedios.
- El ingreso mediano es la variable más relacionada con el precio de la vivienda (r = [COMPLETAR: 0,69 / 0,64 según tus conclusiones]).
- La cercanía al mar y a las grandes ciudades también marca diferencias claras en el precio.
- Todo son asociaciones, no causas, y cada fila es una zona, no una vivienda.

### Energía en España (2014-2018, datos diarios)

- El dataset mezcla 20 series diarias (precios, demanda, generación por fuente y rentas de congestión) en una sola columna de valores. Se separan por nombre.
- Problemas corregidos: fechas corridas un día (se detectó con la demanda por día de la semana), 5.478 filas copiadas del `id` 600 y dos columnas geográficas que no aportaban información.
- La demanda tiene dos picos (febrero y julio) y dos valles (abril-mayo y octubre).
- El precio **no sigue** a la demanda: es más bajo en marzo y abril (unos 36) y más alto en octubre y diciembre (unos 56).
- La nuclear (150.840 de promedio diario) y la eólica (142.036) son las fuentes con mayor generación programada.
- El carbón es la fuente más relacionada con el precio (r = 0,71), y la eólica la más relacionada en sentido contrario (r = -0,50). Estas relaciones no indican causa.
- Limitaciones: la generación es programada y no real, el dataset no indica unidades, y algunas series tienen huecos.

## Tecnologías

Python [COMPLETAR versión], pandas, NumPy, Matplotlib, Seaborn y Jupyter.

## Cómo correrlo

```bash
git clone https://github.com/CarlosScura/reto-para-magos-de-datos.git
cd reto-para-magos-de-datos
python -m venv .venv
source .venv/bin/activate # en Windows: .venv\Scripts\activate
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook
```

Abrí cada notebook y ejecutá todas las celdas (*Restart and Run All*). Los datos ya están en el repositorio.

## Datos

- California: [Kaggle, `California Housing Prices`](https://www.kaggle.com/datasets/camnugent/california-housing-prices/data).
- España: [Kaggle, `Spanish Electricity Market: Demand, Gen. & Price`](https://www.kaggle.com/datasets/manualrg/spanish-electricity-market-demand-gen-price/data).

## Notebooks en Kaggle

- [California Housing: Exploración y análisis](https://www.kaggle.com/code/fedealarcnscura/california-housing-exploraci-n-y-an-lisis)
- [Mercado eléctrico de España: Precio, demanda y generación](https://www.kaggle.com/code/fedealarcnscura/mercado-el-ctrico-de-espa-a-precio-demanda-y-gen)

## Autor

**Fede Alarcón Scura** — Estudiante de Penguin Academy  
Challenge desarrollado como parte del programa de especialización en Data.

- [`Peril de Kaggel`](https://www.kaggle.com/fedealarcnscura)