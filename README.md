# Optimización evolutiva de disposición de moldes en una tela

Proyecto de la materia "Algoritmos Evolutivos I" (FIUBA). Implementa un Algoritmo Genético (usando DEAP) para optimizar la disposición de moldes textiles sobre una franja de tela de altura fija, minimizando el largo total usado.

Contenido
--------

- `informe.md` - Documento principal con la descripción del problema, el enfoque, operadores genéticos, resultados y conclusiones.
- `TP Final.ipynb` - Notebook con pruebas y visualizaciones (si existe).
- `img/` - Imágenes generadas por el proyecto (gráficos de convergencia, boxplots y layouts finales).
- `moldes/` - Carpeta con subcarpetas por prenda que contienen los PNG de los moldes:
	- `calzoncillo/`
	- `camisa/`
	- `remera/`
- `otros/` - Archivos o recursos adicionales.

Descripción breve
-----------------

Cada molde se representa como un contorno extraído desde imágenes PNG y convertido a polígonos reales (escala: 1 px = 1 cm usando un factor 160/432). El objetivo es colocar todas las piezas dentro de una franja de altura fija (STRIP_HEIGHT = 150 cm) sin solapamientos, minimizando el largo total ocupado.

Principales características
--------------------------

- Representación de individuos: lista de tuplas `(y, i, φ)` donde `i` es el índice del molde, `y` la posición vertical y `φ` el ángulo de rotación (0°, 90°, 180°, 270°).
- Operadores genéticos: PMX adaptado para permutaciones, mutación por swap y cambios locales en `y` o `φ`, selección por torneo (k=3).
- Evaluación: fitness = largo_usado + 0.001 * (1 - área_total / área_utilizada). El objetivo es minimizar el fitness.
- Dependencias: Python, DEAP, Shapely, OpenCV (cv2), Matplotlib.

Cómo ejecutar
-----------------------

El código está pensado para ejecutarse en un entorno Python (por ejemplo Google Colab). Pasos generales:

1. Crear y activar un entorno Python (recomendado Python 3.10+).
2. Instalar dependencias:

```bash
pip install deap shapely opencv-python matplotlib
```

3. Ejecutar el script principal (o el notebook) que realiza:
	 - carga de moldes desde PNG,
	 - inicialización del GA y su ejecución por prenda,
	 - generación de gráficos (`img/`) y layout final.

Resultados y artefactos
-----------------------

- Gráficos de convergencia y boxplots están en `img/` (por ejemplo `conv-calzoncillo.png`, `box-camisa.png`, `layout.png`).
- `informe.md` contiene el análisis detallado, parámetros usados, problemas encontrados y conclusiones.

Parámetros por defecto
----------------------

- Tamaño de población: 50
- Generaciones: 50
- Probabilidad de cruce: 0.7
- Probabilidad de mutación: 0.3
- Altura de la franja (STRIP_HEIGHT): 150 cm

Notas y recomendaciones
-----------------------

- El código asume que los PNG de moldes están en `moldes/<prenda>/` y que cada PNG contiene un único molde por archivo.
- Para reproducir resultados exactos conviene fijar semillas aleatorias cuando corresponda.
- Si se usa Colab, subir la carpeta del repositorio o montar Google Drive con los archivos.