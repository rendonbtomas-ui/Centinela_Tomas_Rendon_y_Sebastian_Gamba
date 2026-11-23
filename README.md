
# Proyecto Centinela — nivel del río Cauca en La Virginia con serie del IDEAM y radar Sentinel-1

Ejercicio de clase de **Profundización I: Deep Learning** (Maestría en Ciencia de Datos, Universidad Santo Tomás).
Autores: *Tomás Rendón Bustamante* y *Juan Sebastián Gamba Aguirre*. Fecha: 2026-11-22.

> Es un ejercicio académico. El cliente (una oficina municipal de gestión del riesgo de La Virginia, Risaralda) es hipotético. **Ningún modelo de este repositorio debe usarse como sistema de alerta.**

## Qué se hizo

Se predice el nivel del río Cauca en la estación **La Virginia – AUT. (26177030)** del IDEAM combinando dos modalidades: la serie de nivel (IDEAM) e imágenes de radar **Sentinel-1** resumidas a lo largo del cauce (HydroRIVERS).

| Fase | Contenido | Cuaderno |
|---|---|---|
| 1 | Línea base con MLP en PyTorch (V1/V2), persistencia, MLP binario, experimento de regularización | `notebooks/Centinela_Fase1_Fase2_FINAL.ipynb` (secciones 1.x) |
| 2 | Procesamiento de 275 escenas Sentinel-1; el radar frente a la serie sola a +12/+24/+36/+48 h con validación por bloques y controles; Ramas A (CNN preentrenadas + Grad-CAM), B (RNN/LSTM/GRU) y C (fusión tardía) | mismo cuaderno (secciones 2.x) |
| 3 | Pipelines PyTorch/TensorFlow, aumento y Mixup, GPU con precisión mixta, ONNX, cuantización INT8, modelo Keras, ruta de despliegue | `notebooks/Centinela_Fase3_FINAL.ipynb` |

## Resultados principales

- **+24 h y +36 h:** con validación por bloques (136 escenas de prueba) el modelo con radar baja el error medio de 13,70 a 11,54 cm (+24 h) y de 21,02 a 17,78 cm (+36 h), gana en 5 de 5 bloques y supera a los controles (radar barajado, reloj, órbita). A +12 h no hay efecto y a +48 h es inconcluso. El horizonte +24 h se fijó *después* de explorar otros horizontes.
- Las redes recurrentes **no superan** a la persistencia; las CNN sobre imágenes solas no superan las referencias; la fusión tardía es **no concluyente** (40 escenas de prueba).
- Fase 3: la cadena técnica funciona (ONNX con diferencia ≤ 2 × 10⁻⁶; INT8 de 44,8 a 11,3 MB y de 35,3 a 23,8 ms en CPU), pero el modelo de imagen **no supera** a la clase mayoritaria (0 de 11 aciertos en “sube”).
- Limitaciones: 271 escenas utilizables (no 500), una estación, asociación estadística (no causalidad), latencia medida en CPU de Colab (no en una tablet) y conversión a LiteRT sin ejecutar.

## Documentos (carpeta `docs/`)

Propuesta de Datos (Fase 1), Informe Fases 1 y 2, Informe Fase 3 y Bitácora de IA y auditoría (con su declaración de uso de IA).

## Datos: este repositorio **no** incluye datos

No se suben datos crudos ni derivados (CSV, `.npz`, imágenes, GeoTIFF). Se descargan de las fuentes primarias:

| Fuente | Qué se usa | Licencia |
|---|---|---|
| IDEAM, [Niveles horarios en cuerpos de agua continentales de Colombia](https://www.datos.gov.co/Ambiente-y-Desarrollo-Sostenible/Niveles-Horarios-en-Cuerpos-de-Agua-Continentales-/ig79-2jr9) | Archivo de la estación 26177030 (`0026177030-NIVEL_H.csv`); solo registros «Definitivo» 2020–2025 | CC BY-SA 4.0 (fuente: [IDEAM](https://www.ideam.gov.co/)) |
| [Copernicus Data Space Ecosystem](https://dataspace.copernicus.eu) | Sentinel-1 IW GRDH (COG), órbitas relativas 142 (descendente) y 48 (ascendente) | Libre y abierta ([términos](https://dataspace.copernicus.eu/terms-and-conditions)) |
| [HydroRIVERS v1.0](https://www.hydrosheds.org/products/hydrorivers) (Lehner y Grill, 2013) | Cauce principal para la distancia al río | Libre para uso científico, educativo y comercial |

Los resultados derivados de la serie del IDEAM mantienen la atribución al IDEAM y la licencia CC BY-SA 4.0. Los datos no contienen información de personas (Ley 1581 de 2012).

## Cómo reproducirlo (Google Colab)

1. **Cuenta y claves.** Cree una cuenta gratuita en Copernicus Data Space y genere sus claves de acceso S3 (Access Key y Secret Key). **No las escriba en el cuaderno**: guárdelas en los *Secretos* de Colab con los nombres `COPERNICUS_ACCESS_KEY` y `COPERNICUS_SECRET_KEY`, o el cuaderno las pide con `getpass`.
2. **Datos.** Descargue el CSV del IDEAM y el archivo `HydroRIVERS_v10_sa.gdb.zip` (HydroSHEDS, Sudamérica). El cuaderno le pide subirlos cuando los necesita.
3. **Drive.** Ejecute con la cuenta de Drive donde quiera guardar resultados: el cuaderno crea la carpeta `MyDrive/Centinela/` (con `Fase_2/` y `Fase_3/`) para escenas procesadas, recortes y pesos.
4. **Fase 1 y 2.** Abra `Centinela_Fase1_Fase2_FINAL.ipynb` en Colab y ejecute las celdas **de arriba hacia abajo** (la parte de la Fase 1 solo necesita el CSV). El procesamiento Sentinel-1 (2.7) es reanudable y tarda horas. Las celdas 2.26 y 2.27 requieren **GPU (T4)**; la 2.25 debe ejecutarse antes.
5. **Fase 3.** Abra `Centinela_Fase3_FINAL.ipynb` con **GPU T4**; lee los recortes que dejó la celda 2.24a en `Fase_3/` y ejecute de arriba hacia abajo.
6. Los cuadernos que se entregan ya traen las **salidas** de una ejecución completa; por eso no hace falta repetir el procesamiento para revisarlos.

### Reproducir sin los datos originales

El repositorio no incluye datos; quien no pueda descargarlos solo puede leer los cuadernos con sus salidas. Para ejecutarlos desde cero hay que seguir los pasos de arriba. Una versión que corra sola sin descargas exigiría publicar los datos derivados (tablas de 20 valores por escena y recortes de 224 × 224), lo que se puede hacer respetando CC BY-SA 4.0 y la atribución al IDEAM, pero no se incluyó en esta entrega.

## Estructura del repositorio

```
README.md
notebooks/   Centinela_Fase1_Fase2_FINAL.ipynb · Centinela_Fase3_FINAL.ipynb
docs/        Propuesta de Datos · Informe Fases 1 y 2 · Informe Fase 3 · Bitácora de IA y auditoría
```

## Uso de IA

Se usó IA generativa (Claude y, para ubicar enlaces, otra herramienta) como asistente. La declaración completa, las entradas y las fallas de la IA que se detectaron están en la Bitácora de IA y auditoría.

## Referencias

Lehner, B., & Grill, G. (2013). Global river hydrography and network routing: Baseline data and new approaches to study the world's large river systems. *Hydrological Processes, 27*(15), 2171–2186. https://doi.org/10.1002/hyp.9740
