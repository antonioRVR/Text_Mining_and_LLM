# Text Mining y Large Language Models (LLMs) - Módulo 9

Proyecto académico enfocado en **Minería de Texto, Clasificación de Sentimiento y Aplicación de Grandes Modelos de Lenguaje (LLMs)**. Desarrollado en formato **RMarkdown** (`evaluacion_antonio_local.Rmd`), integrando R y Python mediante la librería `reticulate`.

---

## 📌 Contenido del Proyecto

### 1. Text Mining en Redes Sociales (Twitter / Museo del Prado)
- **Preprocesamiento Lingüístico**: Limpieza con expresiones regulares, filtrado por categorías gramaticales (`NOUN`, `ADJ`, `PROPN`) y lematización con **spaCy**.
- **Análisis Frecuencial y N-Gramas**: Detección de términos frecuentes, siglas y nombres propios compuestos mediante `spacy.matcher.Matcher`.
- **Colocaciones y Coocurrencias**: Cálculo de puntuaciones PMI y Likelihood Ratio con **NLTK**. Visualización de redes semánticas con **NetworkX** y grafos interactivos en HTML mediante **PyVis**.
- **Reconocimiento de Entidades Nombradas (NER)**: Extracción y categorización de entidades (`PER`, `LOC`, `ORG`, `MISC`).
- **Análisis Temático de Casos Específicos**: Estudio focalizado en las campañas expositivas de *Paolo Veronese* y *El Prado en Femenino*.
- **Word Embeddings**: Entrenamiento de un modelo **Word2Vec** (Skip-Gram) con Gensim y visualización del espacio vectorial 2D mediante **UMAP**.

### 2. Clasificación de Texto y Análisis de Sentimiento
- **Estrategia de Limpieza**: Conservación estricta de partículas de negación y polaridad (sin eliminación de stopwords).
- **Clasificación por Estrellas (1 a 5)**: Modelo supervisado en `fastText` (Accuracy ~64.5%).
- **Categorización por Sentimiento (3 Clases)**: Clasificación en `negativo`, `neutro` y `positivo` en `fastText` (Accuracy ~86.4%).
- **Clasificación Binaria (Positivo vs Negativo)**: Comparativa entre:
  - **fastText Binario**: Accuracy **97.48%**.
  - **Regresión Logística (DTM CountVectorizer)**: Accuracy **97.39%**.
  - **Naive Bayes Multinomial (DTM CountVectorizer)**: Accuracy **97.08%**.

### 3. Clustering y Clasificación con Grandes Modelos de Lenguaje (LLMs)
- **Clustéring de Embeddings (BERT vs Nomic)**:
  - **SentenceTransformers**: Representación densa con `hiiamsid/sentence_similarity_spanish_es` (768D), proyección UMAP 2D y agrupación K-Means ($k=8$).
  - **Nomic Embeddings (Ollama)**: Representación de alta fidelidad con `nomic-embed-text-v2-moe`, proyección UMAP 2D y K-Means ($k=8$).
- **Clasificación Generativa con Razonamiento (`qwen3:4b`)**:
  - Clasificación de 120 documentos con Ollama `qwen3:4b` manteniendo activado el razonamiento profundo (`think=True`) sin salidas estructuradas.
- **Análisis de Discrepancias Lingüísticas**: Comparativa detallada entre la agrupación no supervisada de similitud vectorial y la inferencia intencional del LLM generativo.

### 4. Extracción de Información Estructurada de la Web (Wikipedia)
- **Web Fetching Automatizado**: Recuperación e indexación del contenido en Markdown de 10 páginas web de personajes ilustres mediante la API **Ollama Web fetch**.
- **Modelado Estructurado con Pydantic**: Diseño de esquemas tipados (`BaseModel`, `PremioNobel`, `PersonajeIlustre`) soportando múltiples galardones (Marie Curie) y 0 premios Nobel (Mahatma Gandhi).
- **Inferencia en la Nube con Google Gemini (`chatlas`)**: Extracción estructurada utilizando `ChatGoogle(model="gemini-flash-lite-latest")` respetando pausas entre llamadas para control de cuota de API.
- **Inferencia Local con Ollama (`qwen3:4b`)**: Extracción forzada mediante gramática JSON Schema (`format=PersonajeIlustre.model_json_schema()`) en entorno local GPU con `think=False`.
- **Comparativa Directa**: Matriz de concordancia y análisis técnico comparativo entre modelos en la nube y modelos locales.

---

## 📂 Estructura del Repositorio

```
.
├── README.md                      # Presentación y documentación del repositorio
├── .gitignore                     # Archivos ignorados por Git
├── evaluacion_antonio_local.Rmd   # Código fuente principal en RMarkdown (R + Python)
├── evaluacion_antonio.html        # Reporte interactivo completo renderizado
├── red_interactiva_prado.html     # Grafo interactivo PyVis de coocurrencias
├── clasificacion_qwen3.csv        # Clasificaciones de 120 documentos generadas por Qwen3:4b
├── wikipedia_contenidos.json      # Páginas de Wikipedia recuperadas con Ollama Web fetch
├── extraccion_gemini.json         # Datos biográficos estructurados extraídos con Gemini
├── extraccion_qwen3.json          # Datos biográficos estructurados extraídos con Qwen3:4b
├── prado.csv                      # Dataset de tuits del Museo del Prado
├── reviews.csv                    # Dataset de 13.000 críticas de alojamiento
├── documentos.csv                 # Dataset de oraciones categorizadas
├── evaluacion.RData               # Archivo binario con los datasets originales
└── lib/                           # Dependencias JavaScript/CSS para visualización HTML
```

---

## 🛠️ Requisitos e Instalación

Para ejecutar el código en **RMarkdown / RStudio**, asegúrate de tener instalado:

- **R** (>= 4.0) y **RStudio**
- **Python** (>= 3.10)
- **Ollama** con los modelos `qwen3:4b` y `nomic-embed-text-v2-moe`
- Librerías de R: `reticulate`, `readr`, `rmarkdown`, `knitr`
- Librerías de Python (en el entorno virtual `env_textmining`):
  ```bash
  pip install pandas regex spacy nltk scikit-learn gensim umap-learn matplotlib fasttext-wheel sentence-transformers ollama chatlas pydantic google-genai
  python -m spacy download es_core_news_sm
  ```

---

## ✒️ Autor
- **Antonio Ramón Vázquez Ramírez** (`antonioRVR`)

