# ⚽ Video Ball Tracker & Goal Scoring System

Este proyecto utiliza **YOLOv11** para detectar automáticamente **balones** y **arcos** en videos, con el objetivo de identificar posibles goles y asignar un **puntaje** basado en una grilla sobre el arco.

---

## 🎯 Objetivo

Analizar videos deportivos para:
- Detectar la presencia de balones y arcos.
- Seguir el balón cuando no pueda ser detectado en algunos frames.
- Dibujar anotaciones visuales en el video (cajas, texto y grillas).
- Calcular el puntaje del disparo si el balón entra al arco.

---

## 🔍 ¿Cómo funciona?

1. Se carga un modelo YOLOv11 previamente entrenado (`.pt`) para detectar dos clases:
   - `balon` (id 0)
   - `arco` (id 1)

2. Frame por frame:
   - Se detectan los objetos en el frame redimensionado.
   - Se dibujan cajas de colores sobre los objetos detectados.
   - Se realiza seguimiento del balón con `cv2.TrackerCSRT_create` si no es detectado.
   - Se divide el arco en una **grilla 3x3** para visualizar zonas con diferentes valores de puntaje.

3. Al finalizar:
   - Si el balón terminó dentro del área del arco, se calcula su posición dentro de la grilla y se asigna un puntaje según la celda.

---

## 🖼️ Salida

- Un nuevo video con las anotaciones visuales.
- Un mensaje en consola indicando el **puntaje del disparo** (si hubo).

---

## 📦 Requisitos

- Python 3.8+
- OpenCV
- NumPy
- torch
- ultralytics (YOLO)

Instalación rápida:
```bash
pip install opencv-python torch numpy ultralytics
```

## 🚀 Ejecución

```python

from tu_modulo import VideoProcessor

processor = VideoProcessor("ruta_al_modelo.pt")
processor.process_video("video_entrada.mp4", "video_salida.mp4")

```

## 📌 Notas
Asegúrate de que el modelo .pt esté entrenado con las clases balon y arco.

El puntaje se basa en una grilla estática de 3x3 con valores del 1 al 5.

## 🧠 Autor

Hecho Por Jhonatan Steven Morales y Carol Dayana Varela
