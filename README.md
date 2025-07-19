# Análisis de Flujos Clínicos y Estancias Hospitalarias con Python y Plotly

Este cuaderno de Google Colab realiza un análisis detallado de datos de hospitalización, centrándose en la visualización de flujos clínicos utilizando gráficos Sankey y en el análisis estadístico de las estancias hospitalarias, particularmente para Grupos Relacionados por Diagnóstico (GRD) específicos como la colecistectomía laparoscópica.

## Contenido

1.  **Carga y Preparación de Datos**: Se carga un archivo CSV que contiene datos de hospitalización y se realiza una limpieza inicial, incluyendo la estandarización de nombres de servicios.
2.  **Análisis Exploratorio Básico**: Se revisan las columnas del DataFrame y se obtienen conteos de valores para variables clave como `TIPO_ACTIVIDAD`, `TIPO_INGRESO`, `SERVICIOINGRESO`, traslados entre servicios (`SERVICIOTRASLADOx`), `SERVICIOALTA` y `TIPOALTA`.
3.  **Transformación de Datos para Sankey**: Se prepara una lista de movimientos entre servicios y tipos de ingreso/alta, calculando el número de pacientes y la estancia promedio para cada transición.
4.  **Visualización con Gráficos Sankey**:
    *   Se genera un gráfico Sankey básico para visualizar el flujo general de pacientes para un GRD específico (en este caso, 'PH COLECISTECTECTOMÍA LAPAROSCÓPICA W/CC').
    *   Se crea un segundo gráfico Sankey mejorado que colorea los flujos (enlaces) según la estancia promedio asociada a esa transición, permitiendo identificar visualmente los puntos del proceso con estancias más prolongadas.
5.  **Análisis Estadístico de Estancias**:
    *   Se calculan estadísticas descriptivas globales de la estancia hospitalaria para todo el conjunto de datos.
    *   Se obtienen estadísticas de estancia hospitalaria (promedio, mediana, min, max) por GRD seleccionado, comparando las diferencias entre procedimientos con y sin complicaciones ("W/CC").
    *   Se calculan estadísticas de estancia promedio, mediana, mínima y máxima para cada *flujo* específico (transición de un servicio a otro), tanto a nivel global como desagregado por GRD.

## Requisitos

*   Google Colaboratory o un entorno Jupyter Notebook con Python instalado.
*   Librerías: `pandas`, `plotly.express`, `plotly.graph_objects`.
*   Archivo de datos CSV llamado `df_hospital.csv` en el entorno de ejecución.

## Uso

1.  Abre el cuaderno en Google Colab.
2.  Asegúrate de que el archivo `df_hospital.csv` esté disponible en el entorno (puedes subirlo o montando Google Drive si está allí).
3.  Ejecuta las celdas secuencialmente.
4.  Los resultados de los conteos de valores, las estadísticas de estancia y los gráficos Sankey se mostrarán en la salida de las celdas.

## Archivos Necesarios

*   `df_hospital.csv`: Archivo CSV que contiene los datos brutos de hospitalización.

## Análisis Clave y Observaciones

El análisis se centra en comparar el flujo y la estancia de pacientes para la colecistectomía laparoscópica con ("W/CC") y sin complicaciones/comorbilidades.

*   **Impacto de "W/CC"**: Se observa consistentemente que los pacientes con "W/CC" tienen estancias hospitalarias promedio y medianas significativamente más largas en comparación con aquellos sin complicaciones.
*   **Identificación de Cuellos de Botella Potenciales**:
    *   Los gráficos Sankey, especialmente el coloreado por estancia promedio, visualizan los flujos con mayor volumen o estancias más prolongadas.
    *   Los flujos que involucran admisiones a través de **URGENCIA** o traslados desde/hacia unidades de **cuidados críticos (UTI/UCI)** a menudo presentan estancias promedio elevadas, particularmente en el grupo "W/CC" y al pasar al servicio de **MEDICINA**.
    *   Las transiciones de alto volumen, como **CIRUGÍA 2 -> DEALTA**, son cruciales para monitorear la eficiencia del alta.

Estos hallazgos permiten identificar áreas específicas dentro del proceso asistencial que podrían beneficiarse de una optimización para reducir la estancia y mejorar la eficiencia.

---
