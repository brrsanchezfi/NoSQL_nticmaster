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

## 2. RETO 1 – EXPLORACIÓN INICIAL DE LOS DATOS

### 2.1 Revisión inicial de los ficheros

#### 2.1.1 Comprensión del contexto de los datos

Para la revisión inicial se analizó la documentación técnica proporcionada junto con los conjuntos de datos del Ayuntamiento de Madrid, correspondiente a los metadatos del Censo de Locales y Actividades, incluyendo información sobre locales, licencias asociadas y terrazas de hostelería. Esta documentación permitió identificar el origen administrativo de la información, su finalidad estadística y los campos clave de relación entre ficheros, especialmente el identificador id_local, que posibilita el cruce entre distintos datasets. Asimismo, se verificaron las recomendaciones sobre codificación **UTF-8** y la estructura de los archivos, con el fin de garantizar una correcta lectura e interpretación de los datos.

Posteriormente, se realizó una exploración preliminar a partir de los archivos en formato **JSON** utilizando herramientas de análisis de datos en Python. En esta fase se comprobó la estructura de los documentos, los tipos de datos, la consistencia de los campos. Todos los archivos fueron cargados mediante una función genérica de lectura en Python, usando la codificación adecuada:

```python
 def cargar_json(ruta) -> pd.DataFrame:
 with open(ruta, "r", encoding="utf-8") as f:
 data = json.load(f)

 return pd.DataFrame(data)
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

- Shape (dimensiones)
- Columnas
- Tipos de datos
- Valores nulos
- Registros duplicados
- Primeras filas (head)
- Estadísticas descriptivas (describe)
- Reporte automático en Markdown

Los informes completos generados durante esta fase pueden consultarse en
las siguientes rutas:

- Ver detalles en [Exploración de locales](/Reto1/reporte_locales.md)
- Ver detalles en [Exploración de licencias](/Reto1/reporte_licencias.md)
- Ver detalles en [Exploración de Terrazas](/Reto1/reporte_terrazas.md)

<p align="center">
 <img src="Reto1/img/ref_informes_exploracion.png" alt="SS informe automatico"
 width="700"
 style="border:1px solid #ddd; border-radius:8px;
 padding:6px; box-shadow:0 2px 6px rgba(0,0,0,0.15);">
</p>

---

### 2.3 Relaciones entre ficheros

Durante el análisis exploratorio se identificaron posibles relaciones entre los tres conjuntos de datos analizados: **locales**,**Actividad Economica**,**licencias** y **terrazas**. 
Dado lo que pudo inferir en la lectura de la documentacion de esto ficheros se tomo como conjetura que `id_local` puede servir con clave de referencia para todos los ficheros, por lo que se realizó una verificación empírica mediante análisis de columnas y cruces de información.


#### 2.3.1 Identificación de campos comunes

Se compararon los nombres de columnas entre los datasets para detectar posibles claves compartidas:

```python
columnas_comunes = (
 set(df_locales.columns)
 & set(df_licencias.columns)
 & set(df_terrazas.columns)
 & set(df_actividadeconomica.columns)
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
df_locales["id_local"].isin(df_actividadeconomica["id_local"]).sum()
```

Resultados obtenidos:

- Coincidencias entre **locales y licencias**: 74.139 registros
- Coincidencias entre **locales y terrazas**: 6.767 registros
- Coincidencias entre **locales y actividadeconomica**: 169.559 registros

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
- Mantener documentos separados (locales, licencias, terrazas, actividadeconomica).

---

## 3. RETO 2 – MODELADO DE DATOS

**Nota:** La base de datos se implementará utilizando un contenedor Docker para el despliegue de MongoDB y la API de Python **PyMongo** para la carga y manipulación de los datos.


### 3.1 Diseño del modelo de datos

En el reto anterior (sección **2.3.3**) se evaluó la posibilidad de utilizar un modelo relacional; sin embargo, considerando la naturaleza de los datos, su origen en ficheros JSON y el objetivo de trabajar con una base de datos NoSQL orientada a documentos, se decidió implementar un modelo **embebido**. Este almacenara en un único documento la información principal del local junto con sus entidades relacionadas.

El diseño propuesto utiliza el campo **id_local** como identificador lógico del documento principal.

El modelo se estructura tomando como entidad raíz el **local**, dentro del cual se embeben las colecciones relacionadas de **licencias**, **terrazas** y, cuando aplica, información de **actividad económica**.

Ejemplo conceptual del documento:
```json
 {
 "id_local": 12345,

 "local": {
 "...": "atributos del local"
 },

 "licencias": [
 {
 "...": "atributos de licencia"
 }
 ],

 "terrazas": [
 {
 "...": "atributos de terraza"
 }
 ],

 "actividadeconomica": [
 {
 "...": "atributos de actividad"
 }
 ]
 }

```



#### 3.1.2 Implementación del modelo

Para la implementación se desplegó una instancia de MongoDB mediante contenedores Docker, para su revision ingresar a la siguiente ruta [docker-compose](docker-compose.yml)

Adicional en el notebook [2_modelado.ipynb](Reto2\2_modelado.ipynb) esta implementada la contruccion del modelo semantico que se propuso y la carga de los documentos en la base de datos llamada **censo_locales_db**.

<p align="center">
 <img src="Reto2/img//carga_documentos_mongodb.png" alt="Diagrama relacional"
 width="400"
 style="border:1px solid #ddd; border-radius:8px;
 padding:6px; box-shadow:0 2px 6px rgba(0,0,0,0.15);">
</p>


### 3.2 Uso del modelo mediante consultas

#### 3.2.1 Diseno y ejecucion de consultas en MongoDB

a. El Total de locales y terrazas por distrito y barrio: construye una consulta que
permita obtener el total de locales y terrazas agrupados por cada distrito y
barrio. 

```python
   {
      "$group": {
         "_id": {
               "distrito": "$local.desc_distrito_local",
               "barrio": "$local.desc_barrio_local"
         },
         "total_locales": {"$sum": 1},
         "total_terrazas": {"$sum": {"$size": "$terrazas"}}
      }
   },
   {
      "$sort": {
         "_id.distrito": 1,
         "_id.barrio": 1
      }
   }
```

b. Tipos de licencias y cantidad de licencias por cada tipo: crea una consulta para contar cuántas licencias hay de cada tipo en los datos. 

```python
   [
      {"$unwind": "$licencias"},
      {
         "$group": {
               "_id": "$licencias.desc_tipo_licencia",
               "total": {"$sum": 1} # $count
         }
      },
      {"$sort": {"total": -1}}
   ]
```

c. Listado de locales y terrazas con licencias “En trámite”: diseña una consulta
que filtre y devuelva un listado detallado de locales y terrazas cuyo estado de
licencia sea “En trámite”. 

```python
   [
   {
      "$unwind": "$licencias"
   },
   {
      "$match": {
         "licencias.desc_tipo_situacion_licencia": {
         "$regex": "En tramitación",
         "$options": "i"
         }
      }
   },
   {
      "$project": {
         "id_local": 1,
         "licencias.desc_tipo_situacion_licencia": 1,
         "local.desc_distrito_local": 1,
         "local.desc_barrio_local": 1
      }
   }
   ]
```

d. Consulta por sección, división y epígrafe de la actividad comercial: crea una consulta para clasificar locales y terrazas según los campos sección, división y
epígrafe. 

```python
   [
   {
      "$unwind": "$actividadeconomica"
   },
   {
      "$group": {
         "_id": {
         "id_local": "$local.id_local",
         "id_seccion": "$actividadeconomica.id_seccion",
         "desc_seccion": "$actividadeconomica.desc_seccion",
         "id_division": "$actividadeconomica.id_division",
         "desc_division": "$actividadeconomica.desc_division",
         "id_epigrafe": "$actividadeconomica.id_epigrafe",
         "desc_epigrafe": "$actividadeconomica.desc_epigrafe"
         },
         "total": {
         "$sum": 1
         }
      }
   },
   {
      "$sort": {
         "total": -1
      }
   }
   ]
```

e. Actividad económica más frecuente por barrio y distrito: diseña una consulta que identifique cuál es la actividad económica predominante en cada barrio y distrito. 

```python
   [
   {
      "$unwind": "$actividadeconomica"
   },
   {
      "$group": {
         "_id": {
         "distrito": "$local.desc_distrito_local",
         "barrio": "$local.desc_barrio_local",
         "actividad": "$actividadeconomica.desc_seccion"
         },
         "total": {
         "$sum": 1
         }
      }
   },
   {
      "$sort": {
         "total": -1
      }
   },
   {
      "$group": {
         "_id": {
         "distrito": "$_id.distrito",
         "barrio": "$_id.barrio"
         },
         "actividad_mas_frecuente": {
         "$first": "$_id.actividad"
         },
         "total": {
         "$first": "$total"
         }
      }
   },
   {
      "$project": {
         "_id": 0,
         "distrito": "$_id.distrito",
         "barrio": "$_id.barrio",
         "actividad_mas_frecuente": 1,
         "total": 1
      }
   }
   ]
```

f. Actualización de horarios de apertura y cierre de ciertos locales: modifica los horarios de apertura y cierre de un conjunto seleccionado de locales según un criterio que tú determines.
 
```python

   ## condicion arbitraria, se modifican la fecha del distrito "ARGANZUA"

   filtro = {
      "local.desc_distrito_local": {
                  "$regex": "ARGANZUELA",
                  "$options": "i"
               }
   }

   cantidad = collection.count_documents(filtro)

   print("Documentos que se modificarían:", cantidad)

```

Resultado:
```Documentos que se modificarían: 5933```

```python
   update = {
      "$set": {
         "local.horario_apertura": "08:00",
         "local.horario_cierre": "22:00"
      }
   }

   resultado_f = collection.update_many(filtro, update)

   print("Documentos modificados:", resultado_f.modified_count)

```
Resultado:
```Documentos modificados: 5933```
---





## 5. Conclusiones

