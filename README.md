# sprint7-final-project-telecom

**Objetivo**

Analizar el perfil de los usuarios y sus patrones de uso de llamadas y mensajes para identificar segmentos de clientes, revisar la calidad de los datos y proponer oportunidades comerciales para ConnectaTel.

**Datasets utilizados**

El notebook utiliza tres archivos CSV:

- users_latam.csv: información del perfil de usuarios, como edad, ciudad, plan y fecha de registro.
- usage.csv: registros de uso, incluyendo tipo de interacción, fecha, duración y longitud.
- plans.csv: información de los planes disponibles.
  
En el entorno original del proyecto, los archivos se cargan desde /datasets/. Para ejecutar el notebook fuera de ese entorno, ajusta las rutas de pd.read_csv() a la ubicación donde guardaste los CSV.

**Etapas del análisis**

1. Importación de librerías y carga de los datasets.
2. Exploración de dimensiones, tipos de datos, valores ausentes y estadísticas descriptivas.
3. Identificación y tratamiento de problemas de calidad, incluidos valores centinela (-999), valores ? y fechas fuera del periodo de análisis.
4. Agregación del uso por usuario y unión con la información del perfil.
5. Análisis exploratorio mediante estadísticas descriptivas y gráficos.
6. Detección de valores extremos mediante diagramas de caja y el método del rango intercuartílico (IQR).
7. Creación de segmentos por edad y nivel de uso, tablas de distribución y tablas cruzadas de edad × uso y edad × uso × plan.
8. Elaboración de conclusiones ejecutivas y recomendaciones comerciales.
9. Documentación y publicación del notebook y este README en GitHub.
    
**Segmentación utilizada**

- Joven: menor de 30 años.
- Adulto: de 30 a 59 años.
- Adulto Mayor: 60 años o más.
- Bajo uso: menos de 5 llamadas y menos de 5 mensajes.
- Uso medio: no cumple la condición de bajo uso y registra menos de 10 llamadas y menos de 10 mensajes.
- Alto uso: los demás casos según las reglas definidas en el notebook.

Las tablas cruzadas muestran los conteos y porcentajes por grupo. El segmento de alto uso con plan Premium se plantea como una hipótesis para evaluar, no como una conclusión definitiva de rentabilidad: para comprobarla se necesitan ingresos, costos, permanencia y cancelaciones.

**Hallazgos de calidad de datos documentados**

-En users, la columna city presenta 565 valores nulos (14,12 % de los 4.000 usuarios). Además, se identificaron 96 registros con el valor ? (2,4 % de los usuarios). Estos valores de reemplazo se convierten en nulos y los registros de los usuarios se conservan.

-En users, la columna age contenía 55 valores centinela (-999), equivalentes al 1,375 % de los 4.000 usuarios.

-Se encontraron 40 fechas de registro correspondientes a 2026 (1 %), que se marcaron como ausentes por estar fuera del periodo de análisis.

-En usage, 50 de los 40.000 registros tenían la fecha date ausente (0,125 %).

-Las columnas duration y length presentaban 22.076 (55,19 %) y 17.896 (44,74 %) valores ausentes, respectivamente. Estos valores deben interpretarse según el tipo de interacción, ya que la duración corresponde a las llamadas y la longitud a los mensajes de texto.

**Cómo ejecutar el notebook**

1. Descarga o clona este repositorio.
2. Asegúrate de tener Python y Jupyter Notebook, o abre el archivo en Google Colab.
3. Instala las librerías necesarias si no están disponibles:
  ```pip install pandas numpy matplotlib seaborn```
6. Coloca los tres CSV en la ubicación correspondiente y actualiza las rutas de carga si es necesario.
7. Ejecuta las celdas en orden, desde el principio hasta los pasos 7 y 8.
8. Revisa las tablas generadas: distribución de edad, distribución de uso, tabla cruzada edad × uso y tabla edad × uso × plan.

**Reproducibilidad y limitaciones**

Los conteos y porcentajes de segmentación se calculan directamente a partir de user_profile al ejecutar el notebook. Los resultados dependen de los CSV utilizados y de los pasos de limpieza previos. La identificación de un segmento como “más valioso” requiere datos financieros adicionales; el volumen de uso por sí solo no demuestra rentabilidad.
