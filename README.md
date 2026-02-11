# Uso de Bases de Datos NoSQL

## Actividad Práctica – Reto 1: Exploración Inicial de los Datos

**Alumno/a:** *Roberto Sanchez Figueroa*  
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

Este documento presenta la exploración inicial de los datos proporcionados para la actividad práctica de Bases de Datos NoSQL. El objetivo principal es comprender la estructura, calidad y posibles relaciones entre los ficheros antes de su carga en MongoDB.

La exploración se realiza utilizando Python y la librería **pandas**, permitiendo un análisis preliminar sin necesidad de llevar a cabo una limpieza exhaustiva de los datos.

---

## 2. Revisión inicial de los ficheros

### 2.1 Comprensión del contexto de los datos

Tras revisar los ficheros y su documentación asociada, se observa que los datos contienen información relacionada con *[describir brevemente el dominio de los datos: usuarios, pedidos, productos, eventos, etc.]*.

Los ficheros se presentan en formato **CSV/JSON**, lo cual resulta adecuado tanto para su análisis preliminar en Python como para su posterior carga en MongoDB. A nivel general, la estructura es coherente, aunque se detectan variaciones en algunos campos y formatos.

---

### 2.2 Exploración inicial con Python (pandas)

Para comprobar la estructura y el contenido de los datos se utilizó el siguiente script de ejemplo en Python:

```python
import pandas as pd

# Carga del fichero
df = pd.read_csv("datos_ejemplo.csv")

# Visualización de las primeras filas
print(df.head())

# Información general del DataFrame
print(df.info())

# Estadísticas básicas
print(df.describe(include="all"))
```

Este análisis permite verificar que los datos se cargan correctamente, conocer el número de registros y columnas, y obtener una visión general del contenido de cada campo.

---

## 3. Revisión de campos y calidad de los datos

### 3.1 Tipos de datos

Durante la revisión de los campos se identifican principalmente los siguientes tipos de datos:

* **Numéricos:** identificadores, cantidades, importes.
* **Texto:** nombres, descripciones, estados.
* **Fechas y horas:** timestamps de creación o actualización.

Se observa que algunos campos que representan fechas o valores numéricos están almacenados como texto, lo que podría requerir transformaciones posteriores dependiendo del uso que se haga de los datos en MongoDB.

---

### 3.2 Valores nulos y duplicados

Se realizó una comprobación básica para identificar valores nulos y registros duplicados:

```python
# Valores nulos por columna
print(df.isnull().sum())

# Número de registros duplicados
print(df.duplicated().sum())
```

A partir de la revisión de una muestra de los documentos se detectan algunos campos con valores nulos y un número reducido de duplicados. Estos aspectos se documentan para tenerlos en cuenta en fases posteriores, sin realizar una limpieza completa en esta etapa.

---

## 4. Relaciones entre ficheros

### 4.1 Relaciones identificadas

Se analizó la posible existencia de relaciones entre los distintos ficheros mediante campos comunes como identificadores únicos o claves implícitas. En algunos casos es posible establecer relaciones lógicas entre conjuntos de datos, aunque estas no siempre están normalizadas.

---

### 4.2 Alternativas de modelado en MongoDB

En los casos en los que no se ha identificado una relación clara entre ficheros, se propone:

* Almacenar los datos en **colecciones independientes** en MongoDB.
* Utilizar referencias manuales entre documentos si fuese necesario.
* Aplicar estrategias de integración futura mediante procesos ETL o agregaciones.

Este enfoque es coherente con el modelo flexible de MongoDB y su capacidad para gestionar datos no estructurados o semiestructurados.

---

## 5. Conclusiones

La exploración inicial de los datos ha permitido comprender su estructura general, identificar posibles problemas de calidad y analizar la viabilidad de relaciones entre los distintos ficheros. Esta fase resulta clave para definir un modelo de datos adecuado en MongoDB y reducir problemas en etapas posteriores del proyecto.
