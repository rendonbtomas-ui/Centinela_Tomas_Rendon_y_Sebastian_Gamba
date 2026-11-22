# Bitácora de uso de IA y auditoría — Proyecto Centinela

Fases 1, 2 y 3 · Profundización I: Deep Learning · Maestría en Ciencia de Datos, USTA

**Integrantes:** *Tomás Rendón Bustamante* · *Juan Sebastián Gamba Aguirre* | **Fecha:** 2026-11-22

## 1. Declaración de uso de IA

Usamos IA generativa en las tres fases como asistente de programación y depuración. La herramienta principal fue Claude (Anthropic), en sesiones de trabajo conjuntas. **El diseño metodológico del proyecto —incluyendo la definición del problema, la selección de los modelos y arquitecturas a utilizar, el diseño de las funciones y el planteamiento de los experimentos— fue concebido e instruido directamente por nosotros.** La IA nos apoyó en la traducción de estas instrucciones a código, en la corrección de errores de sintaxis, lógica de programación o ejecución sobre nuestras propias propuestas, y en la estructuración de las salidas. La ejecución de los cuadernos en Colab, la lectura crítica de los resultados y la decisión de reportar los hallazgos negativos fueron completamente nuestras. Los enlaces de las fuentes los trajimos nosotros; algunos traían el parámetro `utm_source=chatgpt.com`, lo que indica que se consultaron previamente con otra herramienta de IA (entrada E-14). No usamos datos de Kaggle: los datos se descargaron de las fuentes primarias.

| Integrante | Fase 1 | Fase 2 | Fase 3 | Firma |
|---|---|---|---|---|
| *Tomás Rendón Bustamante* | Sí usó IA | Sí usó IA | Sí usó IA | *Tomás Rendón Bustamante* · 2026-11-22 |
| *Juan Sebastián Gamba Aguirre* | Sí usó IA | Sí usó IA | Sí usó IA | *Juan Sebastián Gamba Aguirre* · 2026-11-22 |

## 2. Entradas (ficha de 14 campos)

### E-1 · Fase 1 · Definición del caso

| Campo | Contenido |
|---|---|
| N.º de entrada | E-1 |
| Fecha | nov. 2026 (antes del 18-nov) |
| Fase y tarea | Fase 1 · Definición del caso |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Validar la viabilidad técnica y estructurar el alcance del problema multimodal planteado por el equipo. |
| Instrucción dada (resumen) | Se le presentó nuestra propuesta metodológica de trabajar con dos modalidades (imagen + serie temporal) con fuentes primarias para acotar la formulación técnica. |
| Respuesta de la IA (resumen) | Ayudó a formalizar y afinar el planteamiento del nivel del río Cauca en La Virginia con la serie del IDEAM, radar Sentinel-1 y HydroRIVERS, estructurando la pregunta de regresión a +12 h. |
| Qué se aceptó sin cambios | La formalización técnica del planteamiento y la articulación de las tres fuentes. |
| Qué se modificó o rechazó | El equipo definió la estación, las fuentes y el cliente hipotético; el profesor aprobó la propuesta el 2026-11-18. |
| Cómo se verificó | Se descargaron los datos directamente de los portales; se revisaron licencias y el profesor aprobó. |
| Resultado de la verificación | Aprobado por el docente (2026-11-18). |
| Dónde quedó en el proyecto | Propuesta de Datos (cuerpo y Anexos). |
| Riesgos o limitaciones | La IA no conoce el contexto hidrológico local de la estación: las decisiones metodológicas y de alcance son del equipo. |

### E-2 · Fase 1 · Propuesta de Datos y evidencias

| Campo | Contenido |
|---|---|
| N.º de entrada | E-2 |
| Fecha | 2026-11-22 |
| Fase y tarea | Fase 1 · Propuesta de Datos y evidencias |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Codificar las funciones de extracción de evidencias reales (anexos A, B y C) y formatear la plantilla de propuesta. |
| Instrucción dada (resumen) | Se instruyó generar el código para la prueba de acoplamiento de 10 filas, la huella SHA-256 del CSV y el checklist de Ley 1581 según la plantilla del curso. |
| Respuesta de la IA (resumen) | Codificó una celda de Colab que calcula SHA-256, estado de aprobación y la tabla de acoplamiento; ayudó a volcar la estructura en Word. |
| Qué se aceptó sin cambios | La estructura de la plantilla y la implementación del código de la celda. |
| Qué se modificó o rechazó | Se redactó como declaración del equipo (no como búsqueda con fecha) la ausencia de espejos en Kaggle; se usaron enlaces limpios de las fuentes. |
| Cómo se verificó | El equipo ejecutó la celda en Colab con el CSV real y comparó las 10 filas con el CSV crudo (todas coinciden). |
| Resultado de la verificación | 10/10 filas coinciden; SHA-256 y conteos (136 301 registros; 8,6 % definitivos) reproducidos. |
| Dónde quedó en el proyecto | Propuesta_de_Datos_Fase1_Centinela.docx / .md. |
| Riesgos o limitaciones | Las licencias se verificaron el 2026-11-22; pueden cambiar. |

### E-3 · Fase 1 · MLP V1/V2 y línea base

| Campo | Contenido |
|---|---|
| N.º de entrada | E-3 |
| Fecha | nov. 2026 |
| Fase y tarea | Fase 1 · MLP V1/V2 y línea base |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Implementar en código y depurar los modelos MLP de regresión a +12 h, persistencia y MLP binario diseñados por el equipo. |
| Instrucción dada (resumen) | Se le indicaron los modelos exactos a utilizar (MLP regresión, persistencia y clasificación binaria), la partición cronológica, el escalado y el uso de parada temprana para que escribiera y corrigiera errores en el código en PyTorch. |
| Respuesta de la IA (resumen) | Codificó y depuró las celdas en PyTorch siguiendo nuestras especificaciones (V1 con 11 predictores, V2 con 14) y el MLP binario con umbral en validación. |
| Qué se aceptó sin cambios | La implementación sintáctica del ciclo de entrenamiento y el cálculo de métricas MAE/RMSE/sesgo. |
| Qué se modificó o rechazó | El equipo evaluó los resultados, determinó que la formulación binaria no es adecuada metodológicamente y mantuvo la regresión como enfoque principal. |
| Cómo se verificó | Se ejecutó en Colab y se auditó el código para garantizar que el conjunto de prueba se leyera una sola vez y el escalado se ajustara solo en entrenamiento. |
| Resultado de la verificación | V1 ≈ persistencia en prueba; F1 binario 0,486 frente a 0,476 de “siempre sube”. |
| Dónde quedó en el proyecto | Cuaderno Centinela_Fase1_Fase2_FINAL, celdas 1.1 a 1.8. |
| Riesgos o limitaciones | Una sola corrida para V1/V2: no se afirma mejora. |

### E-4 · Fase 1 · Experimento de regularización (1.9)

| Campo | Contenido |
|---|---|
| N.º de entrada | E-4 |
| Fecha | nov. 2026 |
| Fase y tarea | Fase 1 · Experimento de regularización (1.9) |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Codificar el diseño experimental del equipo para comparar sobreajuste frente a Dropout, L2 y parada temprana. |
| Instrucción dada (resumen) | Se le indicó la estructura del experimento con las cuatro configuraciones definidas por nosotros y la función para medir la brecha entre validación y entrenamiento. |
| Respuesta de la IA (resumen) | Escribió la celda solicitada; en la primera versión cometió el error de calcular el MSE de entrenamiento con Dropout activo, lo cual fue corregido en conjunto tras nuestra revisión. |
| Qué se aceptó sin cambios | La implementación de las cuatro configuraciones y el graficado de curvas. |
| Qué se modificó o rechazó | Se corrigió el cálculo del MSE de entrenamiento (forzando modo evaluación) y el equipo decidió descartar la interpretación de la “brecha”. |
| Cómo se verificó | Al revisar que el MSE de entrenamiento fuera mayor que el de validación sin sentido físico, se detectó el fallo en el código y se volvió a ejecutar. |
| Resultado de la verificación | Tabla corregida; la brecha no es una medida útil aquí (el periodo de validación es más calmado). |
| Dónde quedó en el proyecto | Cuaderno, celda 1.9; informe Fase 1, sección 3. |
| Riesgos o limitaciones | Ver auditoría A-2. |

### E-5 · Fase 2 · Procesamiento Sentinel-1

| Campo | Contenido |
|---|---|
| N.º de entrada | E-5 |
| Fecha | nov. 2026 |
| Fase y tarea | Fase 2 · Procesamiento Sentinel-1 |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Implementar y depurar el pipeline de procesamiento de escenas Sentinel-1 diseñado por el equipo. |
| Instrucción dada (resumen) | Se le especificó el flujo metodológico y las funciones requeridas (calibración Sigma0, ruido térmico, malla de 10 m, distancia al cauce y las 20 variables SAR) solicitando apoyo en la codificación por lotes reanudable y corrección de errores de ejecución. |
| Respuesta de la IA (resumen) | Ayudó a codificar y depurar las celdas del catálogo OData, el cruce con IDEAM, el acceso a los COG en S3 y la consolidación de la tabla multimodal. |
| Qué se aceptó sin cambios | La implementación técnica de las funciones de extracción y los resúmenes por distancia al cauce. |
| Qué se modificó o rechazó | El equipo fijó las órbitas 142 y 48 y excluyó una escena con error de lectura (2020-09-13). |
| Cómo se verificó | Se compararon conteos de escenas (275 procesadas, 271 utilizables) y se inspeccionaron imágenes y histogramas. |
| Resultado de la verificación | Conteos consistentes; las imágenes muestran el cauce y el relieve esperados. |
| Dónde quedó en el proyecto | Cuaderno, celdas 2.1 a 2.8. |
| Riesgos o limitaciones | No se alcanzaron 500 escenas. |

### E-6 · Fase 2 · Espacio en Drive (2.16)

| Campo | Contenido |
|---|---|
| N.º de entrada | E-6 |
| Fecha | nov. 2026 |
| Fase y tarea | Fase 2 · Espacio en Drive (2.16) |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Resolver un problema de almacenamiento en Drive durante la ejecución del pipeline. |
| Instrucción dada (resumen) | Se consultó cómo optimizar el espacio en disco porque el Drive se llenaba con los archivos temporales. |
| Respuesta de la IA (resumen) | Sugirió borrar los GeoTIFF intermedios asumiendo que ya estaban los recortes, y posteriormente ayudó a recodificar la celda 2.16 cuando se detectó el error de dependencia. |
| Qué se aceptó sin cambios | Se ejecutó la limpieza inicial de archivos intermedios sugerida. |
| Qué se modificó o rechazó | Tras fallar una celda posterior, se reescribió la celda 2.16 en versión incremental para eliminar la dependencia de los archivos borrados. |
| Cómo se verificó | Una celda posterior falló al no encontrar los archivos; tras la refactorización del código, se ejecutó de punta a punta. |
| Resultado de la verificación | Falla detectada al ejecutar; reescritura incremental probada con éxito. |
| Dónde quedó en el proyecto | Cuaderno, celda 2.16. |
| Riesgos o limitaciones | Ver auditoría A-3. |

### E-7 · Fase 2 · Horizontes, robustez y controles

| Campo | Contenido |
|---|---|
| N.º de entrada | E-7 |
| Fecha | nov. 2026 |
| Fase y tarea | Fase 2 · Horizontes, robustez y controles |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Programar y depurar la batería de pruebas de robustez y controles diseñada por el equipo. |
| Instrucción dada (resumen) | Se le instruyó el diseño de nuestros controles experimentales y funciones de prueba: ensayar horizontes (+12 a +48 h), barajar el SAR, usar variable de reloj, SAR de la escena anterior, validación por bloques, red profunda y control por órbita. |
| Respuesta de la IA (resumen) | Tradujo a código nuestras especificaciones de prueba (celdas 2.14 a 2.23) implementando el bootstrap por bloques y las 10 semillas, además de corregir errores de dimensiones en los tensores. |
| Qué se aceptó sin cambios | La codificación de los lazos de control y la validación por bloques. |
| Qué se modificó o rechazó | El equipo decidió fijar el horizonte +24 h tras explorar, lo declaró explícitamente como hallazgo exploratorio y reportó +12 h y +48 h sin aporte. |
| Cómo se verificó | Se auditó el código para asegurar que todos los controles (SAR barajado, reloj, órbita) se entrenaran exactamente bajo el mismo protocolo. |
| Resultado de la verificación | El modelo con SAR gana en 5/5 bloques a +24 y +36 h; los controles no reproducen la mejora. |
| Dónde quedó en el proyecto | Cuaderno, celdas 2.14 a 2.23; informe Fase 2, sección 2. |
| Riesgos o limitaciones | Riesgo de selección *post hoc*; una estación; asociación, no causalidad. |

### E-8 · Fase 2 · Lecturas y variables del cuaderno

| Campo | Contenido |
|---|---|
| N.º de entrada | E-8 |
| Fecha | nov. 2026 |
| Fase y tarea | Fase 2 · Lecturas y variables del cuaderno |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Depurar nombres de variables en el cuaderno y dar formato limpio a los bloques de salida. |
| Instrucción dada (resumen) | Se pidió revisar errores de colisión de variables y estructurar el cuaderno final con salidas limpias y bloques de lectura. |
| Respuesta de la IA (resumen) | Ayudó a limpiar el código del cuaderno y redactó borradores de los textos de lectura a partir de nuestras interpretaciones. |
| Qué se aceptó sin cambios | La estructura visual de las secciones. |
| Qué se modificó o rechazó | El equipo corrigió cifras escritas a mano por la IA en los textos y depuró una variable (`etiquetas`) que estaba siendo sobrescrita por otra celda. |
| Cómo se verificó | Se compararon los textos con las salidas reales celda por celda y se rastreó el alcance de las variables. |
| Resultado de la verificación | Discrepancias y errores de variables corregidos. |
| Dónde quedó en el proyecto | Cuaderno final (todas las lecturas coinciden con las salidas). |
| Riesgos o limitaciones | Ver auditoría A-4. |

### E-9 · Fase 2 · Ramas A, B y C

| Campo | Contenido |
|---|---|
| N.º de entrada | E-9 |
| Fecha | nov. 2026 |
| Fase y tarea | Fase 2 · Ramas A, B y C |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Codificar y depurar los modelos de las tres ramas arquitectónicas definidas por el equipo para el Módulo 2. |
| Instrucción dada (resumen) | Se le especificaron los modelos a construir y las funciones de evaluación: rama de CNN preentrenadas (extracción, ajuste fino y Grad-CAM), modelos recurrentes (RNN/LSTM/GRU) y arquitectura de fusión tardía con ablación. |
| Respuesta de la IA (resumen) | Codificó las celdas 2.24 a 2.27 según nuestras indicaciones; en la rama A ayudó a corregir un cuello de botella donde el código corría en CPU (40–50 min) pasando los tensores a GPU. |
| Qué se aceptó sin cambios | La estructura en código de las arquitecturas y las funciones de ablación. |
| Qué se modificó o rechazó | El equipo configuró el entorno de ejecución en GPU T4, depuró el dispositivo de cómputo y decidió reportar los resultados negativos o no concluyentes con total rigor. |
| Cómo se verificó | Se compararon los MAE con referencias “cambio = 0” y mediana, y se validó mediante bootstrap por escena. |
| Resultado de la verificación | Rama A sin evidencia; Rama B no supera la persistencia; Rama C no concluyente. |
| Dónde quedó en el proyecto | Cuaderno, celdas 2.24 a 2.27; informe Fase 2, secciones 3 a 5. |
| Riesgos o limitaciones | Pocas imágenes (271); Rama B con 32 unidades ocultas. |

### E-10 · Fase 3 · Pipelines, aumento y GPU

| Campo | Contenido |
|---|---|
| N.º de entrada | E-10 |
| Fecha | 2026-11-22 |
| Fase y tarea | Fase 3 · Pipelines, aumento y GPU |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Codificar y depurar las funciones de optimización de hardware, pipelines de datos y aumento definidas por el equipo. |
| Instrucción dada (resumen) | Se le indicó cómo adaptar nuestro problema de tres clases para implementar pipelines en PyTorch/TensorFlow, aumento de datos con Mixup, precisión mixta (AMP) y pruebas de límite de memoria (OOM). |
| Respuesta de la IA (resumen) | Escribió y depuró las celdas 3.2 a 3.6 implementando las funciones de carga, entrenamiento con AMP y medición de tiempos en GPU. |
| Qué se aceptó sin cambios | La implementación técnica de los pipelines y los cronómetros de cómputo. |
| Qué se modificó o rechazó | El equipo evaluó el impacto y decidió mantener la configuración A (sin aumento) al comprobar que no había mejora demostrable. |
| Cómo se verificó | Se ejecutó en Colab con GPU T4 y se auditaron los tiempos reales frente a los tiempos aislados de cómputo. |
| Resultado de la verificación | Aceleración de 1,28× real y 1,97–2,09× aislando cómputo; OOM con lote 1024 en float32. |
| Dónde quedó en el proyecto | Cuaderno Fase 3, celdas 3.2 a 3.6. |
| Riesgos o limitaciones | Con 41 imágenes en validación/prueba las diferencias son ruido. |

### E-11 · Fase 3 · Carpetas de imágenes

| Campo | Contenido |
|---|---|
| N.º de entrada | E-11 |
| Fecha | 2026-11-22 |
| Fase y tarea | Fase 3 · Carpetas de imágenes |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Implementar la función de exportación de PNG por clase y partición para alimentar los pipelines. |
| Instrucción dada (resumen) | Se le instruyó escribir la función de la celda 3.2 para organizar las escenas en carpetas `train/val/test` por clases. |
| Respuesta de la IA (resumen) | Programó la función nombrando cada PNG solo con la fecha del ancla IDEAM; esto provocó un error de sobrescritura en escenas del mismo día (154 en vez de 189 imágenes de entrenamiento). |
| Qué se aceptó sin cambios | — |
| Qué se modificó o rechazó | El equipo detectó la discrepancia, corrigió la función para asignar un identificador único por escena, añadió una aserción de conteo y reejecutó toda la Fase 3. |
| Cómo se verificó | El conteo del resumen no coincidía con el conteo de archivos leídos en la celda 3.3. |
| Resultado de la verificación | Después de la corrección: 189 / 41 / 41 imágenes y verificación exitosa por conjunto. |
| Dónde quedó en el proyecto | Cuaderno Fase 3, celda 3.2 y nota de auditoría. |
| Riesgos o limitaciones | Ver auditoría A-1 (falla principal). |

### E-12 · Fase 3 · ONNX, INT8, Keras y ruta de despliegue

| Campo | Contenido |
|---|---|
| N.º de entrada | E-12 |
| Fecha | 2026-11-22 |
| Fase y tarea | Fase 3 · ONNX, INT8, Keras y ruta de despliegue |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Codificar y depurar las funciones de exportación ONNX, cuantización INT8 y benchmarking de latencia diseñadas por el equipo. |
| Instrucción dada (resumen) | Se le indicaron los formatos de exportación (ONNX, INT8 estática y réplica en Keras) y las restricciones metodológicas (latencia medida en CPU de Colab y ausencia de ejecución en LiteRT) para implementar el código de las tareas 5 y 6. |
| Respuesta de la IA (resumen) | Codificó y depuró las celdas 3.7 a 3.9 para la exportación, cuantización y comparación numérica contra el modelo original `.pth`. |
| Qué se aceptó sin cambios | La implementación técnica de las celdas 3.7 a 3.9. |
| Qué se modificó o rechazó | El equipo definió y mantuvo la conclusión técnica de no desplegar el modelo de imagen como sistema de alerta operativa. |
| Cómo se verificó | Se comparó la salida ONNX frente a PyTorch para lotes 1, 4, 8, 16 y se midió la latencia en CPU. |
| Resultado de la verificación | Diferencia máxima ≤ 2 × 10⁻⁶; INT8 cambia ~5 % de las predicciones. |
| Dónde quedó en el proyecto | Cuaderno Fase 3 e informe Fase 3. |
| Riesgos o limitaciones | LiteRT sin ejecutar; latencia medida en CPU de Colab, no en dispositivo final. |

### E-13 · Fases 1, 2 y 3 · Informes, bitácora y README

| Campo | Contenido |
|---|---|
| N.º de entrada | E-13 |
| Fecha | 2026-11-22 |
| Fase y tarea | Fases 1, 2 y 3 · Informes, bitácora y README |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Claude (Anthropic), asistente de chat/agente; la versión exacta de modelo puede haber variado durante las sesiones |
| Objetivo de la consulta | Estructurar y dar formato a los informes (Word), la bitácora, el README y la guía de GitHub. |
| Instrucción dada (resumen) | Se pidió asistir en el formateo y redacción de los documentos finales integrando las figuras de los cuadernos y nuestros resultados reales. |
| Respuesta de la IA (resumen) | Ayudó a consolidar los documentos desde las salidas de los cuadernos y a codificar las gráficas adicionales (hallazgo principal, latencia). |
| Qué se aceptó sin cambios | El esquema general de organización de los informes. |
| Qué se modificó o rechazó | Los integrantes revisaron y ajustaron la redacción técnica, la declaración del uso de IA y las firmas antes de entregar. |
| Cómo se verificó | Todas las cifras de los informes se auditaron una a una contra las salidas reales de los cuadernos. |
| Resultado de la verificación | Las cifras coinciden con las salidas. |
| Dónde quedó en el proyecto | Entrega final. |
| Riesgos o limitaciones | Los documentos son responsabilidad de los dos integrantes. |

### E-14 · Fase 1 · Enlaces de fuentes

| Campo | Contenido |
|---|---|
| N.º de entrada | E-14 |
| Fecha | 2026-11 |
| Fase y tarea | Fase 1 · Enlaces de fuentes |
| Integrantes presentes | Ambos (sesión conjunta) |
| Herramienta y modelo | Herramienta de IA distinta de Claude (se infiere por el parámetro utm_source=chatgpt.com de los enlaces) |
| Objetivo de la consulta | Ubicar los enlaces directos a las fuentes de datos seleccionadas por el equipo. |
| Instrucción dada (resumen) | El equipo buscó y trajo los enlaces de IDEAM, Copernicus y HydroRIVERS. |
| Respuesta de la IA (resumen) | Entregó enlaces (con parámetro de seguimiento de la herramienta de origen). |
| Qué se aceptó sin cambios | Los enlaces como punto de partida. |
| Qué se modificó o rechazó | Se limpiaron los parámetros de seguimiento y se verificaron las licencias directamente en los sitios oficiales de las fuentes. |
| Cómo se verificó | Se abrieron las páginas oficiales de cada fuente. |
| Resultado de la verificación | Licencias y enlaces confirmados el 2026-11-22. |
| Dónde quedó en el proyecto | Propuesta de Datos (sección 3) y referencias. |
| Riesgos o limitaciones | Se declara para transparencia. |

## 3. Auditoría de fallas de la IA (ficha de 10 campos)

### A-1 · relacionada con E-11

| Campo | Contenido |
|---|---|
| N.º de auditoría | A-1 |
| Entrada relacionada | E-11 |
| Qué produjo la IA | La función de la celda 3.2 de la Fase 3 que guarda un PNG por escena. |
| Qué estaba mal (falla) | Los archivos se nombraban solo con la fecha del ancla IDEAM; escenas distintas con la misma fecha se sobrescribían, de modo que quedaban 154 imágenes de entrenamiento en vez de 189. |
| Cómo se detectó | Al comparar el resumen de la celda 3.2 con el número de archivos que leyó la 3.3. |
| Impacto potencial | Todos los resultados de la Fase 3 (aumento, GPU, INT8) habrían sido con un conjunto incompleto y con posibles fugas entre particiones. |
| Corrección aplicada | Se corrigió la función para nombrar un archivo por escena (etiqueta única) y se añadió una verificación de que el número de PNG en disco coincide con el de escenas de cada conjunto; se volvió a ejecutar toda la Fase 3. |
| Verificación de la corrección | 189 / 41 / 41 imágenes; la verificación pasa; todas las celdas se ejecutaron de nuevo. |
| Lección y control permanente | Contar archivos contra filas siempre; no dar por buenos nombres de archivo derivados de una fecha. |
| Quién detectó y corrigió | Los dos integrantes, con apoyo de la IA para refactorizar el código. |

### A-2 · relacionada con E-4

| Campo | Contenido |
|---|---|
| N.º de auditoría | A-2 |
| Entrada relacionada | E-4 |
| Qué produjo la IA | El código del experimento de regularización (1.9) solicitado por el equipo. |
| Qué estaba mal (falla) | El MSE de entrenamiento se calculó con Dropout activo y se interpretó una “brecha” sin sentido. |
| Cómo se detectó | Al revisar que el MSE de entrenamiento fuera mayor que el de validación en todas las configuraciones. |
| Impacto potencial | Conclusiones equivocadas sobre sobreajuste. |
| Corrección aplicada | Se corrigió el código para recalcular en modo evaluación (`model.eval()`) y se dejó de usar la brecha como medida; la evidencia es el deterioro de la validación. |
| Verificación de la corrección | Tabla corregida y vuelta a ejecutar. |
| Lección y control permanente | Evaluar siempre el entrenamiento en modo de evaluación (eval). |
| Quién detectó y corrigió | Los dos integrantes, con apoyo de la IA para corregir la celda. |

### A-3 · relacionada con E-6

| Campo | Contenido |
|---|---|
| N.º de auditoría | A-3 |
| Entrada relacionada | E-6 |
| Qué produjo la IA | La indicación de borrar archivos intermedios (GeoTIFF) para liberar Drive. |
| Qué estaba mal (falla) | Se afirmó que era seguro borrarlos; una celda posterior (2.16) los necesitaba y falló. |
| Cómo se detectó | Al ejecutar la celda 2.16 después del borrado. |
| Impacto potencial | Pérdida de archivos y de tiempo de procesamiento. |
| Corrección aplicada | Se reescribió la 2.16 en versión incremental que no depende de los archivos borrados. |
| Verificación de la corrección | La celda se ejecutó completa (275 escenas con fracción de agua). |
| Lección y control permanente | No borrar nada sin revisar qué celdas lo leen. |
| Quién detectó y corrigió | Los dos integrantes, con apoyo de la IA para reescribir la celda. |

### A-4 · relacionada con E-8

| Campo | Contenido |
|---|---|
| N.º de auditoría | A-4 |
| Entrada relacionada | E-8 |
| Qué produjo la IA | Textos de lectura y variables del cuaderno. |
| Qué estaba mal (falla) | Había cifras escritas a mano en los textos que no coincidían con las salidas recalculadas (por ejemplo, un valor fijo de 0,727 y un conteo de “33 imágenes”) y una variable llamada `etiquetas` reutilizada por otra celda. |
| Cómo se detectó | Al comparar los textos con las salidas reales celda por celda. |
| Impacto potencial | Informar cifras que el código no producía. |
| Corrección aplicada | Se reemplazaron por valores calculados o se corrigieron los textos y se renombró el uso de la variable en la celda que la sobrescribía. |
| Verificación de la corrección | Las lecturas finales coinciden con las salidas. |
| Lección y control permanente | Las cifras de los textos se leen de las salidas, no de la memoria de la IA. |
| Quién detectó y corrigió | Los dos integrantes, con apoyo de la IA para depurar las referencias. |

## 4. Declaración final

Declaramos que la información de esta bitácora es veraz, que las decisiones metodológicas y de modelado corresponden a nuestra autoría, y que revisamos el contenido de los informes y los cuadernos que entregamos.

*Tomás Rendón Bustamante* · 2026-11-22   |   *Juan Sebastián Gamba Aguirre* · 2026-11-22
