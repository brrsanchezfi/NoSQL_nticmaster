# Uso de Bases de Datos NoSQL

## Actividad Práctica – Reto 1: Exploración Inicial de los Datos

**Alumno:** *Roberto Sanchez Figueroa*  
**Fecha:** *19/02/2026*  
**Asignatura:** Bases de Datos NoSQL

---

## Índice

1. Introducción
2. Revisión inicial de los ficheros
   2.1 Comprensión del contexto de los datos
   2.2 Exploración inicial con Python (pandas)
3. Revisión de campos y calidad de los datos
   3.1 Tipos de datos
   3.2 Valores nulos y duplicados
4. Relaciones entre ficheros
   4.1 Relaciones identificadas
   4.2 Alternativas de modelado en MongoDB
5. Conclusiones

---

## 1. Introducción

Este documento presenta la solucion a la tarea propuesta para el curso de bases NoAQL exploración inicial de los datos proporcionados para la actividad práctica de Bases de Datos NoSQL. El objetivo principal es comprender la estructura, calidad y posibles relaciones entre los ficheros antes de su carga en MongoDB.

La exploración se realiza utilizando Python y la librería **pandas**, permitiendo un análisis preliminar sin necesidad de llevar a cabo una limpieza exhaustiva de los datos.

---

## 2. Reto 1

### 2.1 Revisión inicial de los ficheros

#### 2.1.1 Comprensión del contexto de los datos

Para la revisión inicial se analizó la documentación técnica proporcionada junto con los conjuntos de datos del Ayuntamiento de Madrid, correspondiente a los metadatos del Censo de Locales y Actividades, incluyendo información sobre locales, licencias asociadas y terrazas de hostelería. Esta documentación permitió identificar el origen administrativo de la información, su finalidad estadística y los campos clave de relación entre ficheros, especialmente el identificador id_local, que posibilita el cruce entre distintos datasets. Asimismo, se verificaron las recomendaciones sobre codificación **UTF-8** y la estructura de los archivos, con el fin de garantizar una correcta lectura e interpretación de los datos.

Posteriormente, se realizó una exploración preliminar a partir de los archivos en formato **JSON** utilizando herramientas de análisis de datos en Python. En esta fase se comprobó la estructura de los documentos, los tipos de datos, la consistencia de los campos. Todos los archivos fueron cargados mediante una función genérica de lectura en Python, usando la codificación adecuada:

```python
   def cargar_json(ruta) -> pd.DataFrame:
      with open(ruta, "r", encoding="utf-8") as f:
         data = json.load(f)
      return data
```
---


### 2.2 Revisión de campos y calidad de los datos

#### 2.2.1 Exploración inicial con Python (pandas)

Para comprobar la estructura, el contenido y la calidad general de los
datos, se desarrolló un script de exploración en Python utilizando la
librería **pandas**, que permitió analizar de forma homogénea los tres
datasets en formato JSON. Este script automatizo la generación de
información descriptiva para la fase inicial de análisis,
incluyendo dimensiones del dataset, columnas disponibles, tipos de
datos, valores nulos, registros duplicados, muestras de datos (`head`) y
estadísticas descriptivas (`describe`). 

El proceso genera reportes en formato Markdown.

A continuación un fragmento representativo del script utilizado:

```python

   def explorar_dataset(nombre, data, output_md=True):
      """
      Explora un dataset JSON y muestra información básica
      """
      print(f"\n{'='*60}")
      print(f"DATASET: {nombre}")
      print(f"{'='*60}")

      df = pd.json_normalize(data)

      print("\nShape:", df.shape)
      print("\nColumnas:")
      print(df.columns.tolist())

      print("\nTipos de datos:")
      print(df.dtypes)

      print("\nValores nulos:")
      print(df.isnull().sum())

      print("\nDuplicados:", df.duplicated().sum())

      print("\nHead:")
      print(df.head())

      print("\nDescribe:")
      print(df.describe(include="all"))

      # Exportar a Markdown
      if output_md:
         report = f"""
         # Exploración Dataset: {nombre}

         ## Shape
         {df.shape}

         ## Columnas
         {df.columns.tolist()}

         ## Tipos de datos
         {df.dtypes.to_frame("tipo").to_markdown()}

         ## Valores nulos
         {df.isnull().sum().to_frame("nulos").to_markdown()}

         ## Primeras filas
         {df.head().to_markdown(index=False)}

         ## Estadísticas
         {df.describe(include="all").to_markdown()}
         """

         output_file = Path(f"reporte_{nombre}.md")
         output_file.write_text(report, encoding="utf-8")

         print(f"\nReporte Markdown generado: {output_file}")

   return df
```

Mediante esta herramienta se obtuvieron los siguientes elementos de
exploración para cada dataset:

-   Shape (dimensiones)
-   Columnas
-   Tipos de datos
-   Valores nulos
-   Registros duplicados
-   Primeras filas (head)
-   Estadísticas descriptivas (describe)
-   Reporte automático en Markdown

Los informes completos generados durante esta fase pueden consultarse en
las siguientes rutas:

-   Ver detalles en [Exploración de locales](/Reto1/reporte_locales.md)
-   Ver detalles en [Exploración de licencias](/Reto1/reporte_licencias.md)
-   Ver detalles en [Exploración de Terrazas](/Reto1/reporte_terrazas.md)

<p align="center">
  <img src="Reto1/img/ref_informes_exploracion.png" alt="SS informe automatico"
       width="700"
       style="border:1px solid #ddd; border-radius:8px;
              padding:6px; box-shadow:0 2px 6px rgba(0,0,0,0.15);">
</p>

---

### 2.3 Relaciones entre ficheros

Durante el análisis exploratorio se identificaron posibles relaciones entre los tres conjuntos de datos analizados: **locales**, **licencias** y **terrazas**.  
Dado lo que pudo inferir en la lectura de la documentacion de esto ficheros se tomo como conjetura que `id_local` puede servir con clave de referencia para todos los ficheros, por lo que se realizó una verificación empírica mediante análisis de columnas y cruces de información.


#### 2.3.1 Identificación de campos comunes

Se compararon los nombres de columnas entre los datasets para detectar posibles claves compartidas:

```python
columnas_comunes = (
    set(df_locales.columns)
    & set(df_licencias.columns)
    & set(df_terrazas.columns)
)

print(columnas_comunes)
```

El resultado mostró múltiples campos en común, destacando especialmente:

- `id_local`
- `id_ndp_edificio`
- `id_distrito_local`
- `id_barrio_local`
- Coordenadas geográficas
- Información de situación y acceso del local

Entre todos ellos, el campo **id_local** se identifica como el principal candidato para establecer relaciones entre los ficheros, ya que actúa como identificador único del local dentro del censo.

#### 2.3.2 Verificación de relaciones mediante cruces

Para validar la relación, se comprobó cuántos registros de un dataset existen en los otros:

```python
df_locales["id_local"].isin(df_licencias["id_local"]).sum()
df_locales["id_local"].isin(df_terrazas["id_local"]).sum()
```

Resultados obtenidos:

- Coincidencias entre **locales y licencias**: 74.139 registros
- Coincidencias entre **locales y terrazas**: 6.767 registros

Posteriormente, se realizó un cruce directo entre locales y licencias:

```python
df_merge = df_locales.merge(df_licencias, on="id_local", how="inner")
print(df_merge.shape)
```

Resultado:

```
(150829, 96)
```

**Detalle importante**

El resultado:

```
df_merge.shape = (150829, 96)
```

significa:

El dataset de licencias tiene **150.829 filas**  
Todas encontraron **match en locales**  

Esto constituye una **evidencia muy fuerte de referencia** entre ambos datasets, confirmando que el campo `id_local` permitiria establecer relaciones consistentes entre la información de locales y sus licencias asociadas.

#### 2.3.3 Conclusión sobre las relaciones

Se concluye que:

- Existe una relación clara entre los tres ficheros mediante el campo **id_local**.
- El dataset de **licencias** depende directamente del dataset de **locales**.
- El dataset de **terrazas** contiene un subconjunto de locales que disponen de terraza.
- La relación puede modelarse correctamente mediante un esquema relacional.

<p align="center">
  <img src="Reto1/img/modelo_relacional.png" alt="Diagrama relacional"
       width="700"
       style="border:1px solid #ddd; border-radius:8px;
              padding:6px; box-shadow:0 2px 6px rgba(0,0,0,0.15);">
</p>

#### 2.3.4 Estrategia en caso de integración

En caso de necesitar integración:

- se debe usar `id_local` como clave primaria.
- Mantener documentos separados (locales, licencias, terrazas).

---

## 5. Conclusiones

