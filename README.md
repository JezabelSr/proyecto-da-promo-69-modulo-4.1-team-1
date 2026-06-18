# 📺 NIÑOS Y PANTALLAS: Evolución del uso y su impacto

> *"Mamá, cinco minutitos más..."* — todos los niños, desde 2010 hasta hoy

---

## 🎯 ¿De qué va esto?

Este proyecto nació de una pregunta que cualquier padre o madre conoce bien: **¿qué están viendo realmente los niños cuando se sientan delante de una pantalla?** Y, sobre todo, **¿les está haciendo algo?**

Para responderlo, hemos dividido el análisis en dos partes complementarias:

- **Dashboard 1 — El ecosistema digital infantil**: ¿qué contenido tienen disponible los niños en las principales plataformas de streaming?
- **Dashboard 2 — El impacto en la salud mental**: ¿qué les está pasando a los niños que usan pantallas en exceso?

Spoiler: los resultados no son exactamente tranquilizadores.

---

## 👩‍💻 El equipo

| Quién | Qué ha hecho | GitHub | Tableau Public |
|---|---|---|---|
| **Julia Corada Montano** | Dashboard 1 — El ecosistema digital infantil | [juliacorada](https://github.com/juliacorada) | [Dashboard 1](https://public.tableau.com/app/profile/julia.corada/viz/Dashboard1Elecosistemadigitalinfantil/Elecosistemadigitalinfantil?publish=yes) |
| **Jezabel Sánchez Romero** | Dashboard 2 — Impacto en salud mental | [JezabelSr](https://github.com/JezabelSr) | [Dashboard 2](https://public.tableau.com/app/profile/jezabel.sanchez.romero/viz/DashboardNiosyPantallasSaludMentalyRiesgoDigital/Vistadetallada) |

---

## 📁 Estructura del proyecto

```
proyecto-da-promo-69-modulo-4.1-team-1/
|
├── Dashboard 1/
|   ├── Data/
|   |   ├── dataset_limpio_dashboard1.csv
|   |   ├── disney_plus_titles.csv
|   |   └── netflix_titles.csv
|   ├── Dashboard 1 El ecosistema digital infantil.twbx
|   ├── EDA1.ipynb
|   ├── ML_dashboard1.ipynb
|   └── SQL_dashboard1.ipynb
|
├── Dashboard 2/
|   ├── Datasets/
|   |   ├── RawData/
|   |   |   ├── data_dictionary.csv
|   |   |   └── train.csv
|   |   ├── data_dictionary.csv
|   |   ├── dataset_limpio_dashboard2.csv
|   |   └── feature_importance.csv
|   ├── Dashboard 1.png
|   ├── Dashboard Niños y Pantallas Salud Mental y Riesgo Digital.twb
|   ├── EDA.ipynb
|   ├── ML.ipynb
|   └── SQL.ipynb
|
├── .gitignore
└── README.md
```

---

## ⚙️ Herramientas necesarias

### Instalación de dependencias

```bash
pip install pandas numpy matplotlib seaborn scikit-learn sqlalchemy pymysql jupyter
```

### Versiones utilizadas

| Herramienta | Versión |
|---|---|
| Python | 3.14.3 |
| pandas | 1.5 o superior |
| numpy | 1.23 o superior |
| matplotlib | 3.6 o superior |
| seaborn | 0.12 o superior |
| scikit-learn | 1.2 o superior |
| SQLAlchemy | 2.0 o superior |
| pymysql | 1.0 o superior |
| Jupyter Notebook / JupyterLab | Cualquier versión reciente |
| Tableau Public | 2026.2.0 |

### Base de datos

Se requiere **MySQL** instalado en local (o acceso a un servidor MySQL) con permisos para crear bases de datos. Los notebooks crean y populan las bases de datos automáticamente — no es necesario crear nada a mano.

---

## 🚀 Orden de ejecución

> ⚠️ Los notebooks de SQL y ML dependen del dataset limpio generado en el EDA. Ejecutar siempre en el orden indicado dentro de cada dashboard.

### Dashboard 1
1. `EDA1.ipynb` — Limpieza, exploración y generación de `dataset_limpio_dashboard1.csv`
2. `SQL_dashboard1.ipynb` — Creación de la base de datos `dashboard1_pantallas` y consultas analíticas
3. `ML_dashboard1.ipynb` — Entrenamiento del modelo de clasificación de contenido

### Dashboard 2
1. `EDA.ipynb` — Limpieza, exploración y generación de `dataset_limpio_dashboard2.csv`
2. `SQL.ipynb` — Creación de la base de datos `dashboard2_pantallas` y consultas analíticas
3. `ML.ipynb` — Entrenamiento del modelo de predicción de riesgo digital

---

## 🗂️ Datos utilizados

### Dashboard 1
| Dataset | Fuente | Descripción |
|---|---|---|
| Netflix Movies & TV Shows | [Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows) | 8.807 títulos del catálogo de Netflix |
| Disney+ Movies & TV Shows | [Kaggle](https://www.kaggle.com/datasets/shivamb/disney-movies-and-tv-shows) | 1.450 títulos del catálogo de Disney+ |

Tras limpieza y filtrado de contenido infantil: **3.312 títulos analizados**

### Dashboard 2
| Dataset | Fuente | Descripción |
|---|---|---|
| Child Mind Institute — Problematic Internet Use | [Kaggle](https://www.kaggle.com/competitions/child-mind-institute-problematic-internet-use) | 3.872 participantes de 5 a 22 años con 82 variables |

---

## 🔍 Metodología

### Dashboard 1 — El ecosistema digital infantil

**🐍 Python — Limpieza y EDA** (`EDA1.ipynb`)
- Carga y exploración de los datasets de Netflix y Disney+
- Eliminación de nulos y corrección de errores (sí, había películas con la duración metida en la columna de rating... cosas que pasan)
- Filtrado de contenido infantil por ratings: TV-Y, TV-Y7, TV-Y7-FV, TV-G, G, PG, TV-PG
- Creación de columnas nuevas: `anio_agregado`, `clasificacion_edad`, `genero_principal`, `duracion_min`, `num_temporadas`
- Unificación de géneros con nomenclaturas distintas entre plataformas (porque Netflix llama "Comedies" a lo que Disney+ llama "Comedy")
- Dataset final: 3.312 títulos y 13 columnas

**🗄️ SQL — Consultas y análisis** (`SQL_dashboard1.ipynb`)
- Base de datos `dashboard1_pantallas` en MySQL
- Consultas con GROUP BY, window functions y UNION ALL
- Vista `vista_dashboard1` lista para conectar con Tableau

**🤖 ML — Modelo de clasificación** (`ML_dashboard1.ipynb`)
- Random Forest para predecir la clasificación de edad del contenido
- Variables: tipo de contenido, año de estreno, año de incorporación, plataforma
- Accuracy: 52%
- Hallazgo principal: el año de estreno es el predictor más importante (60% de importancia)

---

### Dashboard 2 — Impacto en la salud mental

**🐍 Python — Limpieza y EDA** (`EDA.ipynb`)
- Análisis del dataset del Child Mind Institute con 82 variables originales
- Selección de las 5 variables con mayor relevancia clínica y mejor calidad de datos
- Imputación de nulos con mediana
- Creación de variables derivadas: `Horas_Pantalla_Label` (categorización del uso diario en 4 tramos), `Uso_Saludable` (variable binaria), `Sexo_Label` (etiqueta legible)
- Dataset final: 3.872 participantes y 11 variables

**🗄️ SQL — Consultas y análisis** (`SQL.ipynb`)
- Base de datos `dashboard2_pantallas` en MySQL
- 13 consultas analíticas con GROUP BY, CASE WHEN, subconsultas y window functions
- Vista `vista_dashboard2` lista para conectar con Tableau

**🤖 ML — Modelo de predicción de riesgo digital** (`ML.ipynb`)
- Random Forest Classifier (100 árboles, `class_weight='balanced'` para compensar el fuerte desbalance de clases: 71% sii=0, solo 0.8% sii=3)
- Variable objetivo: `sii` (nivel de riesgo digital: 0=ninguno, 1=leve, 2=moderado, 3=severo)
- Variables predictoras: edad, sexo, horas de pantalla diarias, calidad del sueño (SDS), funcionamiento general (CGAS). Se excluye `PCIAT_Total` porque `sii` se deriva directamente de ella — usarla sería hacer trampa
- **Accuracy: 64,39%** (superior al 0% de detección en clases minoritarias que daría un modelo trivial que siempre prediga sii=0)
- El modelo distingue bien la clase mayoritaria (sii=0: precision 0.89, recall 0.73) y detecta una parte real de los casos leves y moderados (recall 0.47 y 0.39 respectivamente). No logra identificar casos severos (sii=3) debido a la extrema escasez de ejemplos (32 de 3.872)
- Hallazgo principal: el sueño es el predictor más importante (34%), por encima de la edad (26%), el funcionamiento general (25%), las horas de pantalla (10%) y el sexo (5%)

---

## 📊 Principales hallazgos

### Dashboard 1
- 🚀 Netflix multiplicó por **18** su catálogo infantil entre 2015 y 2020, y tiene más títulos infantiles en números absolutos (60,78%)
- 🏰 Disney+ dedica el **90%** de su catálogo a contenido infantil vs el **23%** de Netflix
- 🎬 Las películas dominan sobre las series en ambas plataformas (73% Disney+, 63% Netflix)
- 🎭 El género más frecuente es *Children & Family Movies*, seguido de *Action-Adventure*
- ⚠️ Solo el **19,4%** del contenido infantil es apto para todos los públicos sin restricciones
- ⚠️ La clasificación más frecuente es Familiar (supervisión recomendada) — la mayoría del contenido infantil requiere acompañamiento parental

### Dashboard 2
- 📉 El riesgo digital aumenta con la edad: el **82%** de los niños en infancia no muestra riesgo, frente al **57%** en adolescencia
- ⚠️ El **29%** de los participantes muestra algún nivel de riesgo digital (leve, moderado o severo)
- 📱 Los niños que usan pantallas más de 3h/día tienen el **doble de puntuación** en uso problemático que los que usan menos de 1h/día
- 😴 A más horas de pantalla, peor calidad del sueño — la relación es directa y estadísticamente significativa
- 🌿 Solo el **12,9%** de los participantes tiene un patrón de uso saludable, porcentaje que casi desaparece en las categorías de mayor uso
- 🤖 El modelo ML revela que **el sueño es el factor más predictivo del riesgo digital** — por encima de las propias horas de pantalla

---

## 🛠️ Tecnologías utilizadas

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=flat&logo=tableau&logoColor=white)

---

## 🎨 Paleta de colores

La paleta de colores es compartida entre los dos dashboards para mantener coherencia visual en todo el proyecto.

### Colores principales

| Color | Hex | Uso |
|---|---|---|
| 🔵 Azul grisáceo | `#5B7C99` | Color principal, títulos, fondos de cabecera |
| 🟢 Verde salvia | `#8FB996` | Indicadores positivos |
| 🟣 Lila suave | `#B8A4C9` | Indicadores de alerta moderada |
| 🔴 Terracota suave | `#D88C7A` | Indicadores de riesgo o negativos |
| ⚪ Gris cálido | `#E8E4E1` | Fondos, áreas neutras, separadores |
| ⚫ Gris oscuro azulado | `#3D4451` | Texto principal, ejes |

### Escala secuencial
Para variables de "menos a más" (ej: horas de pantalla 0-3):

`#C5D9E8` → `#8FB1C7` → `#5B7C99` → `#3D5A7A`

### Escala semántica
Para niveles de severidad (sii):

| Nivel | Color | Hex |
|---|---|---|
| 0 — Ninguno | 🟢 Verde salvia | `#8FB996` |
| 1 — Leve | 🟣 Lila muy claro | `#D4C5E0` |
| 2 — Moderado | 🟣 Lila suave | `#B8A4C9` |
| 3 — Severo | 🔴 Terracota | `#D88C7A` |

---

## 💭 Reflexión final

*"La mayoría del contenido infantil disponible en streaming requiere supervisión parental. La pregunta no es qué ven los niños — es si hay alguien mirando con ellos."*

Y si quieres saber qué les está pasando a los niños que pasan demasiado tiempo frente a una pantalla... el Dashboard 2 tiene la respuesta. Spoiler: no es muy buena.

---

## 📬 Contacto

Proyecto desarrollado como parte del bootcamp de **Data Analytics & AI en Adalab** — Junio 2026

---

*Hecho con 💙, muchísimo café, algún que otro momento de desesperación con Tableau y la firme convicción de que los datos pueden contar historias que importan.*
