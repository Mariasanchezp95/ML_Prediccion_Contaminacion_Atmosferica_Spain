# Análisis y Predicción de la Contaminación Atmosférica en España (2022–2025)

Este proyecto analiza más de **5,6 millones de registros** de contaminación atmosférica en España y desarrolla un **modelo predictivo** capaz de estimar los niveles diarios de **PM10** por ciudad.  
Incluye un pipeline completo: carga masiva, limpieza avanzada, interpolación, eliminación de outliers, ingeniería de características, análisis exploratorio y modelado.

---

## 1. Descripción del problema

La contaminación atmosférica es uno de los principales riesgos ambientales para la salud.  
El objetivo del proyecto es:

- Integrar datos de múltiples estaciones y ciudades.
- Limpiar valores anómalos y faltantes.
- Generar series temporales diarias por ciudad.
- Predecir los niveles de **PM10**, un contaminante crítico para la salud respiratoria.
- Evaluar qué variables influyen más en su comportamiento.

Este tipo de predicción es útil para:
- Administraciones públicas (alertas de calidad del aire)
- Planificación urbana
- Estudios de impacto ambiental
- Sistemas de recomendación para población sensible

---

## 2. Dataset utilizado

- **Fuente:** Agencia Europea de Medio Ambiente (EEA)
- **Tipo:** Público
- **Volumen:** 5.627.952 registros horarios
- **Periodo:** 2022–2025
- **Ciudades:** Badajoz, Madrid, Barcelona, Valencia, Sevilla, Bilbao
- **Contaminantes:** PM10, PM2.5, NO2, O3

El dataset original se compone de archivos `.parquet` descargados desde la API oficial de la EEA.

**Acceso:**  
Los datos pueden obtenerse desde la API de la EEA o desde el repositorio del proyecto (solo muestra reducida por tamaño).

---

## 3. Solución adoptada

La solución se basa en un pipeline completo de Machine Learning:

### ✔️ Preprocesado
- Conversión de fechas
- Mapeo de contaminantes
- Pivotado a formato ancho
- Asignación automática de ciudad
- Agregación diaria por ciudad

### ✔️ Limpieza avanzada
- Conversión a float
- Eliminación de valores `-999` y negativos
- Interpolación por ciudad
- Eliminación de outliers mediante IQR

### ✔️ Feature Engineering
- Variables temporales (año, mes, día, semana)
- Estación del año
- Rolling windows (media móvil 7 días)
- Lags (valor del día anterior)
- Diferencias día a día

### ✔️ Modelado
Se entrenaron tres modelos:

- **Regresión Lineal**
- **Random Forest Regressor**
- **MLPRegressor (Red Neuronal)**

Evaluados con:
- **MAE**
- **RMSE**
- **R²**

---

## 4. Estructura del repositorio

📦 proyecto-contaminacion
│
├── src/
│   ├── data_sample/               # Muestra del dataset original
│   ├── data_totales/              # Archivos parquet originales (no incluidos por tamaño)
│   ├── img/                       # Gráficos generados (EDA y modelo)
│   ├── notebooks/                 # Jupyter Notebooks del pipeline completo
│   └── models/                    # Modelos entrenados (si aplica)
│
├── README.md                      # Descripción del proyecto
├── presentacion/                  # Presentación en PDF o PPT (pendiente)
├── video/                         # Vídeo de presentación (pendiente)
└── informe_proyecto.pdf           # Informe ampliado del proyecto

---

## 5. Tecnologías utilizadas

**Lenguaje:**  
- Python 3.10+

**Librerías principales:**  
- pandas  
- numpy  
- matplotlib  
- seaborn  
- scikit-learn  
- glob  
- datetime  

**Entorno:**  
- Jupyter Notebook  
- VS Code / Google Colab  

---

## 6. Instrucciones de reproducción

Sigue estos pasos para ejecutar el proyecto en tu propio entorno:
1. Clonar el repositorio:
   ```bash
   git clone https://github.com/usuario/proyecto-contaminacion.git
2. Crear un entorno virtual (opcional pero recomendable):
    python -m venv venv
    source venv/bin/activate   # Linux / Mac
    venv\Scripts\activate      # Windows
3. Instalar dependencias manualmente: Este proyecto no utiliza un archivo requirements.txt, por lo que las librerías deben instalarse manualmente.
    pip install pandas numpy matplotlib seaborn scikit-learn
Nota:  Si utilizas Jupyter Notebook, instala también:
    pip install notebook
4. Colocar los datos en la carpeta correspondiente: puedes usar la muestra incluida en:
    src/data_sample/
5. Ejecutar el notebook principal: Abre Jupyter Notebook y ejecuta lo siguiente:
    src/notebooks/main.ipynb
6. Visualizar gráficos y resultados: Los gráficos generados se guardarán automáticamente en:
    src/img/

Este proyecto es reproducible sin dependencias externas adicionales:
    - No se requiere acceso a APIs ni configuraciones especiales.
    - Solo necesitas Python 3.10+ y las librerías mencionadas arriba.

---

## 7. Principales resultados

### 🔹 Modelos entrenados
- Regresión Lineal  
- Random Forest Regressor  
- MLPRegressor (Red Neuronal)

### 🔹 Métricas obtenidas
| Modelo              | MAE   | RMSE  | R²   |
|---------------------|-------|-------|------|
| Regresión Lineal    | 3.12  | 4.77  | 0.68 |
| Random Forest       | **1.95** | **3.10** | **0.89** |
| MLPRegressor        | 2.10  | 3.25  | 0.87 |

### 🔹 Conclusiones
- El **Random Forest** fue el modelo con mejor rendimiento global.  
- Las variables temporales, los lags y las medias móviles mejoraron significativamente la predicción.  
- El dataset final es limpio, interpolado y sin outliers, lo que permitió un modelado estable.  
- El modelo captura correctamente la tendencia y variabilidad diaria del PM10 en todas las ciudades analizadas.

---

## 8. Autora

**María**  
- GitHub: https://github.com/Mariasanchezp95  
- LinkedIn: https://www.linkedin.com/in/maria-sanchez-96056016b 

---

## 9. Licencia

Este proyecto se publica con fines educativos como parte de un trabajo académico.  
El código y los materiales pueden reutilizarse libremente con fines formativos, citando la autoría original.
