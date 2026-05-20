# PAULA-tfm-galaxy10-deit-tiny
Aquí tienes el README para tu parte de DeiT-Tiny, con el mismo estilo que el de tu compañera pero adaptado a tu implementación:
TFM - DeiT-Tiny para clasificación morfológica de galaxias

Repositorio individual con el código correspondiente a la solución basada en DeiT-Tiny con ajuste fino desarrollada para el Trabajo Fin de Máster titulado "Comparativa de modelos de aprendizaje automático y profundo para la clasificación morfológica de galaxias".
Descripción

Este repositorio contiene la implementación, ejecución experimental y resultados de la solución basada en DeiT-Tiny (Data-efficient Image Transformer) aplicada a la clasificación morfológica multiclase de galaxias sobre el conjunto de datos Galaxy10 DECaLS.

La solución forma parte de una comparativa experimental en la que se evaluaron tres enfoques distintos:

    línea base clásica con HOG + PCA + Random Forest
    modelo convolucional profundo EfficientNetB0
    transformer de visión DeiT-Tiny

Este repositorio recoge únicamente la parte correspondiente a DeiT-Tiny, desarrollada de forma individual.
Estructura del repositorio

.
├── README.md
├── DeiT_Tiny_Galaxy10_DECaLS.ipynb
└── data/
    └── README_data.md

Requisitos

Se recomienda utilizar Python 3.11.

Instalación de dependencias:

pip install torch torchvision timm h5py scikit-learn matplotlib seaborn pillow numpy

La librería timm es imprescindible para la carga del modelo DeiT-Tiny preentrenado.
Dataset

La experimentación se realizó sobre el conjunto de datos Galaxy10 DECaLS, distribuido en formato HDF5.

Por motivos de tamaño, el archivo de datos no se incluye en este repositorio. Para ejecutar el notebook, el fichero debe colocarse en la misma carpeta con el nombre:

Galaxy10_DECals.h5

El dataset puede descargarse desde la documentación oficial de astroNN: https://astronn.readthedocs.io/en/latest/galaxy10.html
Ejecución

El código está organizado como un notebook de Jupyter ejecutable en VS Code o en cualquier entorno compatible. Para reproducir el experimento completo, ejecutar las celdas en orden desde el inicio.

Se recomienda disponer de GPU para reducir los tiempos de entrenamiento. En caso de error de memoria, reducir el parámetro BATCH_SIZE de 32 a 16 en la celda de configuración.
Configuración experimental

La solución se implementó con las siguientes características generales:

    arquitectura: DeiT-Tiny (deit_tiny_patch16_224)
    pesos preentrenados en ImageNet, cargados mediante la librería timm
    clasificación multiclase de 10 categorías morfológicas
    tamaño de entrada: 224 × 224 píxeles, con parches de 16 × 16
    optimizador: AdamW, recomendado para arquitecturas transformer
    estrategia de entrenamiento en dos fases:
        entrenamiento inicial de la cabeza clasificadora con backbone congelado (8 épocas, LR = 0,001)
        ajuste fino completo del modelo (12 épocas, LR = 0,0001)
    scheduler ReduceLROnPlateau para reducción adaptativa del learning rate
    uso de ponderación de clases para compensar el desbalanceo del dataset
    semilla fija de 42 para reproducibilidad
    evaluación final sobre partición estratificada de entrenamiento, validación y prueba (80/10/10)

Orden de clases

El orden de las clases en el fichero HDF5 utilizado fue verificado experimentalmente y difiere del orden mostrado en la documentación oficial. El orden correcto para este fichero es el siguiente:
Índice	Clase	Imágenes
0	Disturbed Galaxies	1.081
1	Merging Galaxies	1.853
2	Round Smooth Galaxies	2.645
3	In-between Round Smooth Galaxies	2.027
4	Cigar Shaped Smooth Galaxies	334
5	Barred Spiral Galaxies	2.043
6	Unbarred Tight Spiral Galaxies	1.829
7	Unbarred Loose Spiral Galaxies	2.628
8	Edge-on Galaxies without Bulge	1.423
9	Edge-on Galaxies with Bulge	1.873
Resultados principales

Resultados obtenidos sobre el conjunto de prueba:

    Accuracy: 0,7728
    Precision macro: 0,7520
    Recall macro: 0,7836
    F1 macro: 0,7516
    Loss: 0,6139
    Tiempo de evaluación: 8,55 segundos

Las clases con mejor rendimiento fueron Edge-on Galaxies with Bulge (F1 = 0,9010), Round Smooth Galaxies (F1 = 0,8777) y Edge-on Galaxies without Bulge (F1 = 0,8689). Las clases con mayor dificultad fueron Disturbed Galaxies (F1 = 0,4701) y Unbarred Loose Spiral Galaxies (F1 = 0,5693).
Archivos generados

Durante la ejecución del notebook se generan los siguientes archivos:

Figuras

    curvas_aprendizaje_deit.png
    matriz_confusion_deit.png
    f1_por_clase_deit.png
    distribucion_clases_deit.png
    ejemplos_clases_deit.png

Métricas

    classification_report_deit.txt

Modelo

    deit_tiny_galaxy10_best.pth

Autoría

Repositorio individual de trabajo correspondiente a la contribución personal de Paula Regalado de León dentro del Trabajo Fin de Máster.
Observaciones

Este repositorio se ha organizado con fines académicos y de reproducibilidad. En caso de reutilización del código o de los resultados, se recomienda citar adecuadamente el Trabajo Fin de Máster al que pertenece esta implementación.
