Aquí tienes un `README.md` que documenta paso a paso el flujo de trabajo que realizaste con tu dataset de texto, desde la carga hasta el entrenamiento y guardado del modelo con SVM:

---

## 🧠 Clasificación de Texto con SVM (Procesamiento NLP)

Este proyecto utiliza un pipeline de procesamiento de lenguaje natural (NLP) para clasificar mensajes en categorías como **Petición**, **Queja** y **Reclamo**, usando un modelo supervisado SVM entrenado con datos textuales.

---

### 📁 Estructura del Dataset

El dataset de entrada tiene tres columnas principales:

- `Tipo`: Categoría del mensaje (Petición, Queja, Reclamo).
- `Descripción`: Texto que contiene la solicitud o comentario del usuario.
- `Respuesta`: Texto que se usaría como respuesta automática (no se usa para entrenamiento).

> **Nota**: Algunos datos vienen en una sola columna con comillas, por lo que es necesario repararlos antes del análisis.

---

### 🧼 1. Limpieza y Preparación del Dataset

1. **Carga del CSV**  
   Se usa `pandas.read_csv()` con parámetros especiales (`quotechar='"'`, `engine="python"`) para manejar correctamente los delimitadores.

2. **Reparación de columnas**  
   Si los datos vienen en una sola columna, se dividen usando expresiones regulares para reconstruir `Tipo`, `Descripción` y `Respuesta`.

3. **Limpieza del texto**  
   - Se convierte todo a minúsculas.
   - Se eliminan puntuaciones.
   - Se tokeniza el texto.
   - Se eliminan stopwords en español.
   - Se vuelve a unir el texto limpio.

   Esto se aplica en una nueva columna: `Descripción_Limpiada`.

---

### 🏷️ 2. Etiquetado y División de Datos

- Se define `X` como el texto limpio (`Descripción_Limpiada`).
- Se define `y` como la clase (`Tipo`).
- Se divide el dataset en conjunto de **entrenamiento (80%)** y **prueba (20%)**.

---

### 🛠️ 3. Pipeline de Clasificación

Se construye un `Pipeline` de `scikit-learn` con:

- `TfidfVectorizer`: Convertir texto en vectores numéricos, considerando unigramas y bigramas.
- `SVC`: Clasificador SVM con kernel lineal y ajuste fino de parámetros (`C=10`, `gamma='scale'`).

---

### 🧪 4. Entrenamiento y Evaluación

- Se entrena el modelo con `pipeline.fit()`.
- Se evalúa con `accuracy_score` y `classification_report`.
- Se imprime el rendimiento del modelo.

---

### 💾 5. Guardado del Modelo y Datos

- El modelo SVM entrenado se guarda con `joblib` como `modelo_svm.pkl`.
- El dataset con columna limpia se guarda como `datatxt_procesado.csv`.

---


### 📦 Requisitos

- Python 3.7+
- Pandas
- NLTK
- scikit-learn
- joblib

Instala con:

```bash
pip install pandas nltk scikit-learn joblib
```

---

¿Quieres que agregue también un ejemplo de uso en consola en el `README.md`?