<div align="center">

# Emotion Classification with Transformers

### NLP · Grupo X-Ray

**Comparación experimental entre MLP, Transformers desde cero y DistilBERT para clasificación multiclase de emociones.**

`PyTorch` · `Transformers` · `Hugging Face` · `Scikit-learn` · `Python 3.11`

</div>

---

## Descripción

El proyecto estudia la clasificación automática de textos cortos en inglés usando el corpus **dair-ai/emotion**. Cada observación pertenece a una de seis categorías:

| ID | Emoción |
|---:|---|
| 0 | sadness |
| 1 | joy |
| 2 | love |
| 3 | anger |
| 4 | fear |
| 5 | surprise |

El objetivo no es únicamente obtener una métrica final: el notebook desarrolla un recorrido experimental desde un baseline neuronal hasta transferencia de aprendizaje con DistilBERT, incluyendo reproducibilidad, análisis de errores y comparación de arquitecturas.

## Experimentos

### 1. MLP baseline
Modelo neuronal de referencia utilizado para establecer una línea base antes de introducir mecanismos de atención.

### 2. Transformer desde cero
Se entrenan Transformers pequeños y se compara el tratamiento de posición mediante:

- positional encoding sinusoidal;
- positional embeddings aprendibles.

Los modelos pequeños se ejecutan con varias semillas para observar estabilidad entre entrenamientos.

### 3. DistilBERT frozen
Se utiliza DistilBERT preentrenado manteniendo congelado el encoder y entrenando el clasificador.

### 4. DistilBERT fine-tuned
Se ajusta el modelo preentrenado sobre el corpus de emociones, permitiendo adaptar sus representaciones al problema específico.

## Resultados

| Modelo | Accuracy | Macro F1 | Evaluación |
|---|---:|---:|---|
| MLP | 80.11% | 72.88% | Test |
| Transformer sinusoidal | 86.00% | 82.36% | Test |
| DistilBERT frozen | 59.12% | 40.75% | Validación |
| DistilBERT fine-tuned | **93.57%** | **90.96%** | Validación |

> Las métricas de DistilBERT de esta tabla corresponden al estado de validación registrado por Hugging Face Trainer. El notebook contiene el flujo completo de evaluación y el análisis experimental.

La comparación muestra que congelar el encoder limita considerablemente el desempeño en esta tarea, mientras que el fine-tuning permite adaptar DistilBERT a las seis clases del corpus.

## Flujo experimental

```text
dair-ai/emotion
       │
       ▼
Revisión y preparación de datos
       │
       ├──────────────► MLP baseline
       │
       ├──────────────► Transformer + posición aprendible
       │
       ├──────────────► Transformer + posición sinusoidal
       │
       └──────────────► DistilBERT
                          ├── Frozen
                          └── Fine-tuned
                               │
                               ▼
                 Accuracy · Macro F1 · errores
```

## Contenido del notebook

El notebook principal cubre de extremo a extremo:

- definición del problema y alcance;
- semillas y reproducibilidad;
- revisión de calidad del dataset;
- distribución de clases;
- tokenización y longitud de secuencia;
- construcción de MLP y Transformer;
- entrenamiento con varias semillas;
- comparación de codificación posicional;
- DistilBERT frozen y fine-tuned;
- matrices de confusión y métricas por clase;
- análisis cualitativo de errores;
- exploración de atención;
- prueba de negación;
- clasificador de demostración;
- conclusiones y limitaciones.

## Estructura

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── emotion_tokenizer/
│   ├── special_tokens_map.json
│   └── tokenizer_config.json
├── hf_finetuned/
│   ├── config.json
│   └── trainer_state.json
├── hf_frozen/
│   ├── config.json
│   └── trainer_state.json
├── checkpoints/
│   └── README.md
└── results/
    └── README.md
```

Esta sección refleja **únicamente los archivos que ya están versionados en GitHub**. Los artefactos binarios y el notebook se incorporan de forma separada para evitar documentar archivos inexistentes.

## Instalación

```bash
git clone https://github.com/cris-bytes/Mini-Proyecto-de-clasificaci-n-de-texto-con-Transformers.git
cd Mini-Proyecto-de-clasificaci-n-de-texto-con-Transformers

python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

## Stack

| Componente | Tecnología |
|---|---|
| Deep Learning | PyTorch 2.8 |
| Transformers | Hugging Face Transformers 4.57.6 |
| Dataset | Hugging Face Datasets |
| ML / métricas | Scikit-learn |
| Manipulación | Pandas · NumPy |
| Visualización | Matplotlib |
| Modelo preentrenado | DistilBERT |

## Reproducibilidad

El experimento conserva configuración, estados de entrenamiento y artefactos para poder reconstruir las ejecuciones. Los modelos pequeños fueron comparados usando múltiples semillas; DistilBERT se ejecutó con un presupuesto computacional más restringido.

## Uso responsable

Las etiquetas representan las categorías del corpus. La salida de estos modelos **no constituye una evaluación clínica ni permite inferir de forma fiable el estado psicológico de una persona**.

## Autoría

**Grupo X-Ray**  
Proyecto académico de Procesamiento de Lenguaje Natural.

---

<div align="center">

**NLP · Transformers · Transfer Learning · Emotion Classification**

</div>
