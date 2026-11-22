**Propuesta de Datos — Fase 1 · Proyecto Centinela**

**Centinela: alerta de ascenso del nivel del río Cauca en La Virginia (Risaralda) con la serie del IDEAM y radar Sentinel-1**

**Integrantes:** Tomás Rendón Bustamante · Juan Sebastián Gamba Aguirre \| **Fecha:** 2026-11-22 \| **Versión:** v1 (aprobada por el docente el 2026-11-18), con las evidencias de los anexos

**1. Problema, cliente y objetivo binario**

Las crecidas del río Cauca en La Virginia pueden inundar viviendas y vías ribereñas. El cliente (hipotético, ejercicio de clase) es la oficina municipal de gestión del riesgo, que necesita anticipar ascensos bruscos para avisar con horas de antelación. **Objetivo binario:** ¿el nivel dentro de 12 h superará al actual en más de 4 cm? (sí / no). El umbral de 4 cm lo supera el 24.6 % de los ejemplos de entrenamiento.

**2. Dos modalidades**

**Imagen:** radar de apertura sintética Sentinel-1 (satélite; polarizaciones VV y VH) sobre el cauce. **Serie temporal:** nivel del río medido por el sensor de la estación La Virginia – AUT. (26177030) del IDEAM. Son instrumentos distintos con mediciones físicamente independientes (un satélite que observa la superficie y un sensor *in situ*).

**3. Fuentes**

| **Modalidad** | **Productor, conjunto y enlace**                                                                                                                      | **Licencia (verificada en)**                                                       | **Datos de personas** |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|-----------------------|
| Serie         | IDEAM. *Niveles horarios en cuerpos de agua continentales de Colombia*, estación 26177030, registros «Definitivo» 2020-2025 (enlace en la sección 8). | CC BY-SA 4.0 (ficha del conjunto en datos.gov.co, 2026-11-22)                      | No                    |
| Imagen        | ESA / Copernicus Data Space Ecosystem. Sentinel-1 IW GRDH (COG), órbitas 142 y 48 (sección 8).                                                        | Libre y abierta (dataspace.copernicus.eu/terms-and-conditions, 2026-11-22)         | No                    |
| Auxiliar      | HydroSHEDS. HydroRIVERS v1.0 (cauce principal). https://www.hydrosheds.org/products/hydrorivers                                                       | Libre, uso científico, educativo y comercial (HydroSHEDS TechDoc v1.4, 2026-11-22) | No                    |

**4. Por qué no es un reto resuelto**

No se usa Kaggle ni conjuntos preprocesados. La serie llega cruda: 136 301 registros desde 1972, de los que solo el 8.6 % son «Definitivo» (el resto, preliminar o en revisión), con frecuencia de 12 h y horaria en 2025. Las imágenes exigen procesamiento propio desde productos COG (calibración Sigma0, ruido térmico, reproyección, distancia al cauce). No se partió de réplicas.

**5. Plan de la Fase 1**

**Modalidad aplanada:** la serie, como tabla de 11 predictores (nivel actual y rezagos) para un MLP en PyTorch. **Fase 2:** rama temporal (GRU) y rama de imagen (CNN sobre Sigma0 VV/VH por distancia al cauce) con fusión. **Clave de alineación (agregada):** fecha-hora del ancla IDEAM (última observación anterior a la adquisición Sentinel-1, ≤ 12 h). **Prueba de acoplamiento:** Anexo A, diez filas reales.

**6. Línea base comprometida**

Clase mayoritaria («no sube», 75.4 % del entrenamiento) y regla de persistencia (nivel futuro = nivel actual). Como escalar crudo: el nivel actual con umbral elegido en validación.

**7. Riesgos éticos y protección de datos**

| **Riesgo**                    | **Daño para el cliente**                 | **Mitigación**                                          |
|-------------------------------|------------------------------------------|---------------------------------------------------------|
| Falso negativo (no avisar)    | Personas y bienes sin aviso a tiempo     | Priorizar sensibilidad; apoya, no reemplaza, al técnico |
| Falso positivo (falsa alerta) | Fatiga de alertas y pérdida de confianza | Umbral elegido en validación; reportar falsos positivos |
| Cambio de régimen del río     | Rendimiento menor que el medido          | Partición cronológica; declarar limitaciones            |
| Datos personales (Ley 1581)   | No aplica: sin personas identificables   | Checklist del Anexo C por fuente                        |

**8. Referencias (APA 7)**

Instituto de Hidrología, Meteorología y Estudios Ambientales. (s. f.). *Niveles horarios en cuerpos de agua continentales de Colombia* \[Conjunto de datos\]. Portal de Datos Abiertos de Colombia. https://www.datos.gov.co/Ambiente-y-Desarrollo-Sostenible/Niveles-Horarios-en-Cuerpos-de-Agua-Continentales-/ig79-2jr9

Agencia Espacial Europea. (s. f.). *Sentinel-1* \[Conjunto de datos\]. Copernicus Data Space Ecosystem. https://dataspace.copernicus.eu

Lehner, B., & Grill, G. (2013). Global river hydrography and network routing: Baseline data and new approaches to study the world's large river systems. *Hydrological Processes, 27*(15), 2171-2186. https://doi.org/10.1002/hyp.9740

**Anexo A. Prueba de acoplamiento (diez filas reales)**

La clave de alineación es la fecha-hora del ancla IDEAM (hora local de Colombia). Cada escena Sentinel-1 (etiqueta en UTC) se une con la última observación IDEAM anterior, a ≤ 12 h. Las filas se tomaron a intervalos regulares de la tabla ordenada por fecha. En la última columna se comprobó que el nivel coincide con el del CSV crudo del IDEAM.

| **N.º** | **Clave: fecha-hora del ancla IDEAM** | **Imagen: escena Sentinel-1** | **VV medio del recorte (dB)** | **Serie: nivel en el ancla (cm)** | **Coincide con el CSV crudo** |
|---------|---------------------------------------|-------------------------------|-------------------------------|-----------------------------------|-------------------------------|
| 1       | 2020-01-04 18:00                      | 20200104T232135               | -10.65                        | 310                               | sí                            |
| 2       | 2020-05-03 18:00                      | 20200504T105107               | -9.53                         | 170                               | sí                            |
| 3       | 2020-10-06 18:00                      | 20201006T232143               | -10.58                        | 122                               | sí                            |
| 4       | 2021-02-15 18:00                      | 20210216T105111               | -9.80                         | 210                               | sí                            |
| 5       | 2021-07-27 18:00                      | 20210728T105046               | -8.98                         | 300                               | sí                            |
| 6       | 2021-12-12 18:00                      | 20211212T232148               | -10.01                        | 332                               | sí                            |
| 7       | 2022-11-25 18:00                      | 20221126T105136               | -9.27                         | 440                               | sí                            |
| 8       | 2023-12-02 18:00                      | 20231203T105141               | -10.02                        | 133                               | sí                            |
| 9       | 2024-12-08 18:00                      | 20241209T105136               | -9.70                         | 144                               | sí                            |
| 10      | 2025-12-28 05:00                      | 20251228T105124               | -9.64                         | 271                               | sí                            |

**Código que produjo la tabla** (Colab; lee archivos del Drive del proyecto):

indice = pd.read_csv(CARPETA_BASE + '/Fase_3/centinela_recortes_indice.csv').sort_values('fecha_hora_ideam')

posiciones = np.linspace(0, len(indice) - 1, 10).round().astype(int) \# 10 filas a intervalos regulares

for i in posiciones:

r = indice.iloc\[i\]

chip = np.load(f"{CARPETA_BASE}/Fase_3/chips/{r\['etiqueta'\]}.npy").astype('float32')

\# clave = r\['fecha_hora_ideam'\] \| imagen = r\['etiqueta'\] \| VV medio = chip\[0\].mean() \| nivel = r\['valorObservado'\]

\# verificación: el nivel debe coincidir con el CSV crudo en esa misma fecha-hora (crudo\['fechaObservacion'\])

**Anexo B. Evidencias del test de procedencia**

| **Comprobación**                         | **Evidencia**                                                                                                                                                                                                                                                                                                                                                                                                                            |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1\. Cadena de procedencia                | Serie: IDEAM, conjunto *Niveles horarios en cuerpos de agua continentales de Colombia* (enlace en la sección 3), archivo **0026177030-NIVEL_H.csv**, 5 214 434 bytes, registros hasta 2026-11-14 06:00 (fecha de corte). **SHA-256: 35b92d2d8f701f2c59ed370003c3d0f101883735dff06af68354375cc69cfd25**. Imágenes: catálogo OData y almacenamiento S3 de Copernicus Data Space (acceso con claves personales, no incluidas en el código). |
| 2\. Descarga trazable                    | Todos los datos se obtuvieron directamente de las fuentes primarias (portal de datos abiertos del IDEAM, Copernicus Data Space y HydroSHEDS). No se usó Kaggle como fuente de datos.                                                                                                                                                                                                                                                     |
| 3\. Búsqueda de espejos en Kaggle        | Declaración del equipo (2026-11-22): no se usó ningún conjunto ni espejo de Kaggle; los datos se descargaron de las fuentes primarias.                                                                                                                                                                                                                                                                                                   |
| 4\. Huella de crudeza (antes de limpiar) | 136 301 filas; rango 1972-01-01 a 2026-11-14; columnas: fechaObservacion, valorObservado, nivelAprobacion. Aprobación: Preliminar 102 733 (75.4 %), En revisión 21 784 (16.0 %), **Definitivo 11 784 (8.6 %)**. Sin faltantes ni fechas duplicadas; valorObservado entre 0 y 730 cm (mediana 237). La frecuencia cambia (≈12 h hasta 2024, horaria en 2025). Se modelan solo los registros definitivos.                                  |
| 5\. Contraste con el espejo              | No aplica: no se utilizó ningún espejo.                                                                                                                                                                                                                                                                                                                                                                                                  |

**Anexo C. Checklist de protección de datos (Ley 1581 de 2012)**

Resultado para las tres fuentes: **sin datos de personas**. La estación, las imágenes de radar y la red hidrográfica no identifican ni se refieren a personas naturales.

| **Bloque**                     | **Respuesta (aplica igual a serie IDEAM, Sentinel-1 y HydroRIVERS)**                                                                                                                              |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| A. Datos personales            | No. Son mediciones físicas (nivel del río, retrodispersión de radar, trazado del cauce).                                                                                                          |
| B. Datos sensibles             | No.                                                                                                                                                                                               |
| C. Menores de edad             | No.                                                                                                                                                                                               |
| D. Base legal                  | No aplica: no hay tratamiento de datos personales. Los datos son abiertos y públicos.                                                                                                             |
| E. Finalidad                   | Académica (ejercicio de clase de Deep Learning); sin cliente real.                                                                                                                                |
| F. Anonimización               | No aplica; los datos no se refieren a personas.                                                                                                                                                   |
| G. Licencia                    | IDEAM: CC BY-SA 4.0. Copernicus: política libre y abierta. HydroRIVERS: libre para uso científico, educativo y comercial.                                                                         |
| H. Transferencia internacional | Copernicus y HydroSHEDS se alojan fuera del país; al no haber datos personales no hay transferencia de ellos.                                                                                     |
| I. Minimización                | Solo se usan fecha, nivel y estado de aprobación (serie) y VV/VH (radar); no se recolecta nada más.                                                                                               |
| J. Publicación del repositorio | Repositorio público sin datos crudos; contiene código, cuadernos con sus salidas y las instrucciones para descargar los datos de las fuentes primarias. Las salidas no muestran datos personales. |

**Declaración.** Declaramos que la información anterior es veraz y que en la Fase 1 no se usa ninguna persona identificable.

| **Firma**                              | **Firma**                                   |
|----------------------------------------|---------------------------------------------|
| *Tomás Rendón Bustamante* · 2026-11-22 | *Juan Sebastián Gamba Aguirre* · 2026-11-22 |
