<div align="center">

# Clasificación de emociones con Transformers

### Procesamiento de Lenguaje Natural · Grupo X-Ray

Comparación experimental entre **MLP**, **Transformers desde cero** y **DistilBERT** para clasificación multiclase de emociones sobre `dair-ai/emotion`.

`Python 3.11` · `PyTorch 2.8` · `Hugging Face Transformers` · `Scikit-learn`

</div>

---

## Objetivo

Clasificar textos cortos en inglés en seis emociones:

| ID | Emoción |
|---:|---|
| 0 | sadness |
| 1 | joy |
| 2 | love |
| 3 | anger |
| 4 | fear |
| 5 | surprise |

El proyecto evalúa modelos de distinta complejidad y documenta reproducibilidad, métricas, análisis de errores y transferencia de aprendizaje.

## Modelos evaluados

1. **MLP baseline**
2. **Transformer con positional embeddings aprendibles**
3. **Transformer con positional encoding sinusoidal**
4. **DistilBERT frozen**
5. **DistilBERT fine-tuned**

## Resultados principales

| Modelo | Accuracy | Macro F1 | Split |
|---|---:|---:|---|
| MLP | 80.11% | 72.88% | Test |
| Transformer sinusoidal | 86.00% | 82.36% | Test |
| DistilBERT frozen | 59.12% | 40.75% | Validación |
| DistilBERT fine-tuned | **93.57%** | **90.96%** | Validación |

> Las métricas de DistilBERT mostradas arriba corresponden al estado de validación registrado por Hugging Face Trainer. El notebook contiene la evaluación completa y el análisis experimental.

## Estructura actual del repositorio

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── 2-transformers-text-classification-xray.ipynb
├── emotion_tokenizer/
│   ├── special_tokens_map.json
│   ├── tokenizer_config.json
│   └── tokenizer.json
├── hf_finetuned/
│   ├── config.json
│   ├── special_tokens_map.json
│   ├── tokenizer_config.json
│   ├── tokenizer.json
│   ├── trainer_state.json
│   └── vocab.txt
├── hf_frozen/
│   ├── config.json
│   ├── special_tokens_map.json
│   ├── tokenizer_config.json
│   ├── tokenizer.json
│   ├── trainer_state.json
│   └── vocab.txt
├── checkpoints/
│   └── README.md
└── results/
    ├── README.md
    ├── comparacion_final.csv
    ├── entorno.json
    ├── experimentos_validacion.csv
    ├── predicciones_prueba.csv
    └── revision_datos.csv
```

## Ejecución desde cero

### 1. Clonar el repositorio

```bash
git clone https://github.com/cris-bytes/Mini-Proyecto-de-clasificaci-n-de-texto-con-Transformers.git
cd Mini-Proyecto-de-clasificaci-n-de-texto-con-Transformers
```

### 2. Crear entorno virtual

macOS / Linux:

```bash
python3.11 -m venv .venv
source .venv/bin/activate
```

Windows PowerShell:

```powershell
py -3.11 -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Instalar dependencias

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 4. Registrar el kernel

```bash
python -m ipykernel install --user --name xray-transformers --display-name "X-Ray Transformers"
```

### 5. Abrir el notebook

```bash
jupyter notebook notebooks/2-transformers-text-classification-xray.ipynb
```

También puede abrirse desde VS Code, JupyterLab o Google Colab.

### 6. Ejecutar

Seleccionar el kernel creado y ejecutar:

**Run All**

La primera ejecución requiere conexión a internet porque el notebook descarga:

- el dataset `dair-ai/emotion`;
- DistilBERT preentrenado desde Hugging Face.

## Importante sobre las rutas

El notebook guarda artefactos de trabajo en una carpeta local llamada:

```text
artifacts/
```

Esa carpeta se crea automáticamente durante la ejecución.

Los archivos que ya están versionados en `results/`, `emotion_tokenizer/`, `hf_finetuned/` y `hf_frozen/` son artefactos de referencia del experimento original.

## Pesos grandes y checkpoints

Los pesos completos de DistilBERT (`model.safetensors`) pesan aproximadamente **268 MB por modelo**, por lo que superan el límite normal de GitHub para archivos individuales.

Por esa razón, este repositorio está preparado para **regenerar los modelos ejecutando el notebook desde cero**.

Los pesos grandes pueden versionarse posteriormente mediante **Git LFS** o almacenarse en Hugging Face Hub.

## Reproducibilidad

El experimento utiliza:

- Python 3.11
- PyTorch 2.8.0
- Transformers 4.57.6
- Datasets 4.4.1
- Tokenizers 0.22.2
- Accelerate 1.12.0
- NumPy 2.2.6
- Pandas 2.3.3
- Scikit-learn 1.7.2

Las versiones exactas están fijadas en `requirements.txt`.

Los modelos pequeños se entrenan con varias semillas para evaluar estabilidad entre ejecuciones.

## Flujo experimental

```text
dair-ai/emotion
      │
      ▼
Preparación y control de calidad
      │
      ├── MLP
      │
      ├── Transformer + posiciones aprendibles
      │
      ├── Transformer + posiciones sinusoidales
      │
      └── DistilBERT
            ├── Frozen
            └── Fine-tuned
                 │
                 ▼
       Accuracy · Macro F1 · Error analysis
```

## Contenido del notebook

El notebook incluye:

- planteamiento del problema;
- control de semillas;
- inspección y limpieza del dataset;
- análisis de distribución de clases;
- análisis de longitud y vocabulario;
- tokenización BPE;
- construcción del MLP;
- construcción del Transformer;
- comparación de codificaciones posicionales;
- entrenamiento multisemilla;
- DistilBERT frozen;
- DistilBERT fine-tuned;
- matrices de confusión;
- métricas por clase;
- análisis de errores;
- exploración de atención;
- prueba de negación;
- clasificador de demostración;
- conclusiones y limitaciones.

## Uso responsable

Las clases corresponden a etiquetas del dataset. Los modelos **no realizan diagnóstico psicológico** ni deben utilizarse para inferir de forma fiable el estado mental de una persona.

## Autoría

**Grupo X-Ray**  
Proyecto académico de Procesamiento de Lenguaje Natural.

---

<div align="center">

**Transformers · NLP · Transfer Learning · Emotion Classification**

</div>
