# Clasificación de emociones con Transformers

Proyecto de Procesamiento de Lenguaje Natural — **Grupo X-Ray**.

Este repositorio compara distintos enfoques de clasificación de texto sobre el dataset **dair-ai/emotion**, desde modelos base hasta Transformers preentrenados y ajustados.

## Objetivo

Clasificar textos cortos en inglés en seis emociones:

- sadness
- joy
- love
- anger
- fear
- surprise

## Modelos evaluados

El proyecto incluye:

1. **MLP baseline**
2. **Transformer desde cero con posiciones aprendibles**
3. **Transformer desde cero con codificación posicional sinusoidal**
4. **DistilBERT frozen**
5. **DistilBERT fine-tuned**

## Resultados principales

| Modelo | Accuracy | Macro F1 |
|---|---:|---:|
| MLP | 80.11% | 72.88% |
| Transformer sinusoidal | 86.00% | 82.36% |
| DistilBERT frozen | 59.12%* | 40.75%* |
| DistilBERT fine-tuned | 93.57%* | 90.96%* |

\* Métricas de validación registradas por Hugging Face Trainer. Los resultados finales de prueba y el análisis completo se encuentran en el notebook.

El modelo fine-tuned muestra la mejora más clara frente a mantener congelado el encoder preentrenado.

## Estructura del repositorio

```text
.
├── 2-transformers-text-classification-xray.ipynb
├── README.md
├── requirements.txt
├── .gitignore
├── emotion_tokenizer/
│   ├── tokenizer.json
│   ├── tokenizer_config.json
│   └── special_tokens_map.json
├── hf_finetuned/
│   ├── config.json
│   ├── model.safetensors
│   ├── special_tokens_map.json
│   ├── tokenizer_config.json
│   ├── tokenizer.json
│   ├── trainer_state.json
│   ├── training_args.bin
│   └── vocab.txt
├── hf_frozen/
│   ├── config.json
│   ├── model.safetensors
│   ├── special_tokens_map.json
│   ├── tokenizer_config.json
│   ├── tokenizer.json
│   ├── trainer_state.json
│   ├── training_args.bin
│   └── vocab.txt
├── checkpoints/
│   ├── MLP_42.pt
│   ├── MLP_43.pt
│   ├── MLP_44.pt
│   ├── Transformer posiciones aprendibles_42.pt
│   ├── Transformer posiciones aprendibles_43.pt
│   ├── Transformer posiciones aprendibles_44.pt
│   ├── Transformer sinusoidal_42.pt
│   ├── Transformer sinusoidal_43.pt
│   └── Transformer sinusoidal_44.pt
└── results/
    ├── comparacion_final.csv
    ├── entorno.json
    ├── experimentos_validacion.csv
    ├── predicciones_prueba.csv
    └── revision_datos.csv
```

## Dataset

Se utiliza **dair-ai/emotion**, un corpus de textos en inglés etiquetados en seis emociones.

Este proyecto clasifica etiquetas presentes en el corpus y **no debe interpretarse como una herramienta de diagnóstico psicológico**.

## Metodología

El notebook documenta:

1. definición del problema;
2. preparación del entorno y reproducibilidad;
3. revisión de calidad de datos;
4. análisis de distribución de clases;
5. tokenización;
6. entrenamiento de modelos base;
7. comparación entre codificaciones posicionales;
8. transferencia de aprendizaje con DistilBERT;
9. evaluación cuantitativa;
10. matrices de confusión y métricas por clase;
11. análisis cualitativo de errores;
12. exploración de atención;
13. prueba de negación;
14. demo de clasificación;
15. conclusiones y limitaciones.

## Reproducibilidad

Los modelos pequeños se evaluaron con varias semillas para reducir dependencia de una única inicialización. DistilBERT fue entrenado con una configuración más limitada por costo computacional.

Los artefactos generados se incluyen para conservar:

- tokenizer entrenado;
- configuración de los modelos;
- pesos de DistilBERT;
- estado del Trainer;
- checkpoints de modelos construidos desde cero;
- predicciones y métricas de evaluación;
- información del entorno de ejecución.

## Entorno

- Python 3.11
- PyTorch 2.8.0
- Transformers 4.57.6
- Datasets 4.4.1
- Tokenizers 0.22.2
- Accelerate 1.12.0
- NumPy 2.2.6
- Pandas 2.3.3
- Scikit-learn 1.7.2

Las versiones completas están definidas en `requirements.txt`.

## Instalación

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Después, abrir:

```text
2-transformers-text-classification-xray.ipynb
```

en JupyterLab, Jupyter Notebook o Google Colab.

## Métrica principal

La métrica principal es **Macro F1**, acompañada de:

- Accuracy
- F1 ponderado
- métricas por clase
- matrices de confusión
- análisis cualitativo de errores

## Tecnologías

Python · PyTorch · Hugging Face Transformers · Hugging Face Datasets · Scikit-learn · Pandas · NumPy · Matplotlib

## Referencias

- Hugging Face — dair-ai/emotion
- Vaswani et al. — Attention Is All You Need
- DistilBERT — distilbert-base-uncased
- Hugging Face Transformers Trainer
- Demszky et al. — GoEmotions

## Nota

Los resultados están acotados al dataset, configuración experimental y presupuesto computacional utilizados. El repositorio tiene fines académicos y de experimentación en NLP.
