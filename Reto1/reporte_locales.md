# 📊 Exploración Dataset: Locales

## Información general

- **Registros:** 151,162
- **Columnas:** 48

## Columnas

| columna                   | tipo    |
|:--------------------------|:--------|
| id_local                  | int64   |
| id_distrito_local         | int64   |
| desc_distrito_local       | str     |
| id_barrio_local           | int64   |
| desc_barrio_local         | str     |
| cod_barrio_local          | int64   |
| id_seccion_censal_local   | int64   |
| desc_seccion_censal_local | int64   |
| coordenada_x_local        | float64 |
| coordenada_y_local        | float64 |
| id_tipo_acceso_local      | int64   |
| desc_tipo_acceso_local    | str     |
| id_situacion_local        | int64   |
| desc_situacion_local      | str     |
| id_vial_edificio          | int64   |
| clase_vial_edificio       | str     |
| desc_vial_edificio        | str     |
| id_ndp_edificio           | int64   |
| id_clase_ndp_edificio     | int64   |
| nom_edificio              | str     |
| num_edificio              | int64   |
| cal_edificio              | str     |
| secuencial_local_PC       | int64   |
| id_vial_acceso            | int64   |
| clase_vial_acceso         | str     |
| desc_vial_acceso          | str     |
| id_ndp_acceso             | int64   |
| id_clase_ndp_acceso       | int64   |
| nom_acceso                | str     |
| num_acceso                | int64   |
| cal_acceso                | str     |
| id_agrupacion             | int64   |
| nombre_agrupacion         | str     |
| id_tipo_agrup             | int64   |
| desc_tipo_agrup           | str     |
| id_planta_agrupado        | str     |
| id_local_agrupado         | str     |
| rotulo                    | str     |
| cod_postal                | str     |
| hora_apertura1            | str     |
| hora_cierre2              | str     |
| fx_carga                  | str     |
| fx_datos_ini              | str     |
| fx_datos_fin              | str     |
| hora_cierre1              | str     |
| hora_apertura2            | str     |
| coordenada_x_agrupacion   | float64 |
| coordenada_y_agrupacion   | float64 |

## Valores nulos

| columna                   |   nulos |
|:--------------------------|--------:|
| hora_apertura2            |  150350 |
| hora_cierre2              |  150300 |
| hora_cierre1              |  144851 |
| hora_apertura1            |  142366 |
| coordenada_x_agrupacion   |  136661 |
| coordenada_y_agrupacion   |  136661 |
| id_local                  |       0 |
| id_distrito_local         |       0 |
| coordenada_x_local        |       0 |
| coordenada_y_local        |       0 |
| desc_distrito_local       |       0 |
| id_barrio_local           |       0 |
| desc_barrio_local         |       0 |
| cod_barrio_local          |       0 |
| id_seccion_censal_local   |       0 |
| desc_seccion_censal_local |       0 |
| clase_vial_edificio       |       0 |
| id_vial_edificio          |       0 |
| desc_situacion_local      |       0 |
| id_situacion_local        |       0 |
| desc_tipo_acceso_local    |       0 |
| id_tipo_acceso_local      |       0 |
| desc_vial_edificio        |       0 |
| id_ndp_edificio           |       0 |
| clase_vial_acceso         |       0 |
| desc_vial_acceso          |       0 |
| id_clase_ndp_edificio     |       0 |
| nom_edificio              |       0 |
| num_edificio              |       0 |
| cal_edificio              |       0 |
| secuencial_local_PC       |       0 |
| id_vial_acceso            |       0 |
| id_agrupacion             |       0 |
| cal_acceso                |       0 |
| num_acceso                |       0 |
| nom_acceso                |       0 |
| id_clase_ndp_acceso       |       0 |
| id_ndp_acceso             |       0 |
| desc_tipo_agrup           |       0 |
| nombre_agrupacion         |       0 |
| cod_postal                |       0 |
| rotulo                    |       0 |
| id_local_agrupado         |       0 |
| id_planta_agrupado        |       0 |
| id_tipo_agrup             |       0 |
| fx_datos_fin              |       0 |
| fx_carga                  |       0 |
| fx_datos_ini              |       0 |

## Registros duplicados

- **Duplicados:** 0

## Primeras filas (head)

|   id_local |   id_distrito_local | desc_distrito_local   |   id_barrio_local | desc_barrio_local   |   cod_barrio_local |   id_seccion_censal_local |   desc_seccion_censal_local |   coordenada_x_local |   coordenada_y_local |   id_tipo_acceso_local | desc_tipo_acceso_local   |   id_situacion_local | desc_situacion_local   |   id_vial_edificio | clase_vial_edificio   | desc_vial_edificio                |   id_ndp_edificio |   id_clase_ndp_edificio | nom_edificio   |   num_edificio | cal_edificio   |   secuencial_local_PC |   id_vial_acceso | clase_vial_acceso   | desc_vial_acceso                  |   id_ndp_acceso |   id_clase_ndp_acceso | nom_acceso   |   num_acceso | cal_acceso   |   id_agrupacion | nombre_agrupacion   |   id_tipo_agrup | desc_tipo_agrup   | id_planta_agrupado   | id_local_agrupado   | rotulo               |   cod_postal | hora_apertura1   | hora_cierre2   | fx_carga            | fx_datos_ini   | fx_datos_fin   |   hora_cierre1 |   hora_apertura2 |   coordenada_x_agrupacion |   coordenada_y_agrupacion |
|-----------:|--------------------:|:----------------------|------------------:|:--------------------|-------------------:|--------------------------:|----------------------------:|---------------------:|---------------------:|-----------------------:|:-------------------------|---------------------:|:-----------------------|-------------------:|:----------------------|:----------------------------------|------------------:|------------------------:|:---------------|---------------:|:---------------|----------------------:|-----------------:|:--------------------|:----------------------------------|----------------:|----------------------:|:-------------|-------------:|:-------------|----------------:|:--------------------|----------------:|:------------------|:---------------------|:--------------------|:---------------------|-------------:|:-----------------|:---------------|:--------------------|:---------------|:---------------|---------------:|-----------------:|--------------------------:|--------------------------:|
|   20000596 |                   2 | ARGANZUELA            |               203 | CHOPERA             |                  3 |                      2043 |                          43 |               440789 |          4.47186e+06 |                      1 | Puerta Calle             |                    1 | Abierto                |             744250 | CALLE                 | TOMAS BORRAS                      |          11008969 |                       1 | NUM            |             12 |                |                    20 |           744250 | CALLE               | TOMAS BORRAS                      |        11008969 |                     1 | NUM          |           12 |              |              -1 | SIN AGRUPACION      |              -1 | SIN AGRUPACION    | PB                   | D1                  | LA CAÑA              |        28045 | 09:00            | 22:00          | 2023-12-08T07:01:00 | 2023-12-01     | 2023-12-01     |            nan |              nan |                       nan |                       nan |
|   20000605 |                   2 | ARGANZUELA            |               201 | IMPERIAL            |                  1 |                      2107 |                         107 |               439317 |          4.47254e+06 |                      1 | Puerta Calle             |                    1 | Abierto                |             597700 | GLORIETA              | PIRAMIDES                         |          11008222 |                       1 | NUM            |              6 |                |                    20 |           597700 | GLORIETA            | PIRAMIDES                         |        11008222 |                     1 | NUM          |            6 |              |              -1 | SIN AGRUPACION      |              -1 | SIN AGRUPACION    | PB                   | 01                  | CAFETERIA PIRAMIDES  |        28005 | nan              | nan            | 2023-12-08T07:01:00 | 2023-12-01     | 2023-12-01     |            nan |              nan |                       nan |                       nan |
|   20000669 |                   2 | ARGANZUELA            |               202 | ACACIAS             |                  2 |                      2096 |                          96 |               439771 |          4.47241e+06 |                      1 | Puerta Calle             |                    1 | Abierto                |             501150 | CALLE                 | MELILLA                           |          20123782 |                       1 | NUM            |             39 |                |                    50 |           501150 | CALLE               | MELILLA                           |        20123782 |                     1 | NUM          |           39 |              |              -1 | SIN AGRUPACION      |              -1 | SIN AGRUPACION    | PB                   | M1                  | BAR MELILLA          |        28005 | nan              | nan            | 2023-12-08T07:01:00 | 2023-12-01     | 2023-12-01     |            nan |              nan |                       nan |                       nan |
|   20000709 |                   2 | ARGANZUELA            |               202 | ACACIAS             |                  2 |                      2029 |                          29 |               440356 |          4.47228e+06 |                      1 | Puerta Calle             |                    1 | Abierto                |             274600 | PASEO                 | ESPERANZA                         |          11008673 |                       1 | NUM            |             45 |                |                    10 |           274600 | PASEO               | ESPERANZA                         |        11008673 |                     1 | NUM          |           45 |              |              -1 | SIN AGRUPACION      |              -1 | SIN AGRUPACION    | PB                   | IZ                  | SUPERMERCADOS SIMPLY |        28005 | nan              | nan            | 2023-12-08T07:01:00 | 2023-12-01     | 2023-12-01     |            nan |              nan |                       nan |                       nan |
|   20000721 |                   2 | ARGANZUELA            |               201 | IMPERIAL            |                  1 |                      2089 |                          89 |               439313 |          4.47287e+06 |                      1 | Puerta Calle             |                    1 | Abierto                |                917 | PASEO                 | JUAN ANTONIO VALLEJO-NAJERA BOTAS |          20106307 |                       1 | NUM            |             54 |                |                    40 |              917 | PASEO               | JUAN ANTONIO VALLEJO-NAJERA BOTAS |        20106307 |                     1 | NUM          |           54 |              |              -1 | SIN AGRUPACION      |              -1 | SIN AGRUPACION    | PB                   | C                   | ARROCERIA IMPERIAL   |        28005 | nan              | nan            | 2023-12-08T07:01:00 | 2023-12-01     | 2023-12-01     |            nan |              nan |                       nan |                       nan |

## Estadísticas numéricas

|       |         id_local |   id_distrito_local |   id_barrio_local |   cod_barrio_local |   id_seccion_censal_local |   desc_seccion_censal_local |   coordenada_x_local |   coordenada_y_local |   id_tipo_acceso_local |   id_situacion_local |   id_vial_edificio |   id_ndp_edificio |   id_clase_ndp_edificio |   num_edificio |   secuencial_local_PC |   id_vial_acceso |    id_ndp_acceso |   id_clase_ndp_acceso |   num_acceso |    id_agrupacion |   id_tipo_agrup |   coordenada_x_agrupacion |   coordenada_y_agrupacion |
|:------|-----------------:|--------------------:|------------------:|-------------------:|--------------------------:|----------------------------:|---------------------:|---------------------:|-----------------------:|---------------------:|-------------------:|------------------:|------------------------:|---------------:|----------------------:|-----------------:|-----------------:|----------------------:|-------------:|-----------------:|----------------:|--------------------------:|--------------------------:|
| count | 151162           |        151162       |        151162     |       151162       |                  151162   |                 151162      |               151162 |     151162           |           151162       |         151162       |   151162           |  151162           |                  151162 |    151162      |           151162      | 151162           | 151162           |                151162 |  151162      | 151162           |   151162        |                     14501 |           14501           |
| mean  |      2.65509e+08 |             9.93966 |           997.419 |            3.45292 |                   10011.1 |                     71.4084 |               399837 |          4.04971e+06 |                1.09698 |              2.28749 |        5.56624e+06 |       1.40338e+07 |                       1 |        42.4499 |               22.6905 |      5.61568e+06 |      1.47366e+07 |                     1 |      42.169  |      9.49711e+06 |       -0.224084 |                    393973 |               3.98494e+06 |
| std   |      5.01671e+07 |             5.62518 |           562.402 |            1.86267 |                    5627   |                     48.5326 |               129535 |          1.31157e+06 |                1.48613 |              2.00324 |        1.97007e+07 |       6.15574e+06 |                       0 |        94.4034 |               65.0502 |      1.97999e+07 |      6.69412e+06 |                     0 |      94.4053 |      2.91552e+07 |        2.92838  |                    138115 |               1.39651e+06 |
| min   |      1e+07       |             1       |           101     |            1       |                    1001   |                      1      |                    0 |          0           |                0       |              1       |      127           |       1.1e+07     |                       1 |         1      |                0      |    127           |      1.1e+07     |                     1 |       1      |     -1           |       -1        |                         0 |               0           |
| 25%   |      2.70484e+08 |             5       |           505     |            2       |                    5085   |                     32      |               439093 |          4.47075e+06 |                1       |              1       |   230600           |       1.10306e+07 |                       1 |         8      |               10      | 224400           |      1.10342e+07 |                     1 |       8      |     -1           |       -1        |                    438974 |               4.46925e+06 |
| 50%   |      2.80038e+08 |            10       |          1004     |            3       |                   10137   |                     65      |               440759 |          4.47364e+06 |                1       |              1       |   433500           |       1.10782e+07 |                       1 |        20      |               10      | 432200           |      1.1086e+07  |                     1 |      20      |     -1           |       -1        |                    441297 |               4.47322e+06 |
| 75%   |      2.85011e+08 |            15       |          1501     |            5       |                   15041   |                    104      |               443692 |          4.4767e+06  |                1       |              4       |   653500           |       1.11336e+07 |                       1 |        47      |               20      | 651100           |      2.00095e+07 |                     1 |      46      |     -1           |       -1        |                    444450 |               4.47731e+06 |
| max   |      3.00022e+08 |            21       |          2105     |            9       |                   21034   |                    222      |               454737 |          4.4955e+06  |               12       |             10       |        8.89531e+07 |       3.10718e+07 |                       1 |      5090      |             9010      |      8.89531e+07 |      3.10718e+07 |                     1 |    5090      |      9.90007e+07 |       17        |                    452668 |               4.48855e+06 |

## Estadísticas categóricas

|        | desc_distrito_local   | desc_barrio_local   | desc_tipo_acceso_local   | desc_situacion_local   | clase_vial_edificio   | desc_vial_edificio   | nom_edificio   | cal_edificio   | clase_vial_acceso   | desc_vial_acceso   | nom_acceso   | cal_acceso   | nombre_agrupacion   | desc_tipo_agrup   | id_planta_agrupado   | id_local_agrupado   | rotulo        |   cod_postal | hora_apertura1   | hora_cierre2   | fx_carga            | fx_datos_ini   | fx_datos_fin   | hora_cierre1   | hora_apertura2   |
|:-------|:----------------------|:--------------------|:-------------------------|:-----------------------|:----------------------|:---------------------|:---------------|:---------------|:--------------------|:-------------------|:-------------|:-------------|:--------------------|:------------------|:---------------------|:--------------------|:--------------|-------------:|:-----------------|:---------------|:--------------------|:---------------|:---------------|:---------------|:-----------------|
| count  | 151162                | 151162              | 151162                   | 151162                 | 151162                | 151162               | 151162         | 151162         | 151162              | 151162             | 151162       | 151162       | 151162              | 151162            | 151162               | 151162              | 151162        |       151162 | 8796             | 862            | 151162              | 151162         | 151162         | 6311           | 812              |
| unique | 21                    | 131                 | 3                        | 7                      | 25                    | 6161                 | 2              | 30             | 25                  | 6303               | 2            | 31           | 417                 | 12                | 21                   | 3468                | 80142         |           55 | 63               | 34             | 2                   | 1              | 1              | 56             | 37               |
| top    | CENTRO                | SAN ANDRES          | Puerta Calle             | Abierto                | CALLE                 | ALCALA               | NUM            |                | CALLE               | ALCALA             | NUM          |              | SIN AGRUPACION      | SIN AGRUPACION    | PB                   |                     | SIN ACTIVIDAD |        28017 | 08:00            | 02:00          | 2023-12-08T07:01:00 | 2023-12-01     | 2023-12-01     | 02:00          | 10:00            |
| freq   | 13440                 | 4092                | 134010                   | 99664                  | 125753                | 1431                 | 151087         | 142931         | 125646              | 1375               | 151083       | 142870       | 136661              | 136661            | 143646               | 60717               | 39418         |         5824 | 1977             | 461            | 101262              | 151162         | 151162         | 3063           | 435              |
