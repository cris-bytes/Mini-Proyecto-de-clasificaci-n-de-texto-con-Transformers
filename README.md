# Clasificación de emociones con Transformers

Proyecto de Procesamiento de Lenguaje Natural — **Grupo X-Ray**.

## Objetivo

Clasificar textos cortos en inglés en seis emociones:

- sadness
- joy
- love
- anger
- fear
- surprise

El proyecto utiliza el corpus `dair-ai/emotion` y compara un MLP de referencia, Transformers construidos desde cero y DistilBERT preentrenado.

## Contenido del proyecto

El notebook principal documenta:

1. Problema y objetivo.
2. Preparación y reproducibilidad.
3. Revisión de calidad y distribución de clases.
4. Tokenización y longitud de entrada.
5. Modelos desde cero.
6. Entrenamiento y selección mediante validación.
7. DistilBERT preentrenado.
8. Evaluación final en prueba.
9. Revisión de errores.
10. Exploración de atención y prueba de negación.
11. Demo de clasificación.
12. Conclusiones.
13. Referencias.

## Dataset

Se utiliza **dair-ai/emotion**, un corpus en inglés con seis etiquetas emocionales.

El modelo aprende las etiquetas del corpus; no determina el estado psicológico de quien escribe.

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

Las versiones completas se encuentran en `requirements.txt`.

## Ejecución

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Abrir después el notebook en Jupyter o Google Colab.

## Evaluación

La métrica principal es **Macro F1**, complementada con:

- Accuracy.
- F1 ponderado.
- Matrices de confusión.
- Métricas por emoción.
- Revisión cualitativa de errores.

Las conclusiones están acotadas al corpus, configuraciones y presupuesto de entrenamiento utilizados en el proyecto.

## Referencias

- https://huggingface.co/datasets/dair-ai/emotion
- https://arxiv.org/abs/1706.03762
- https://huggingface.co/distilbert/distilbert-base-uncased
- https://huggingface.co/docs/transformers/v4.57.1/en/main_classes/trainer
- https://aclanthology.org/N19-1357/
