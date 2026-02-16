
# Consulta A

## Pipeline utilizado

```json
[
  {
    "$group": {
      "_id": {
        "distrito": "$local.desc_distrito_local",
        "barrio": "$local.desc_barrio_local"
      },
      "total_locales": {
        "$sum": 1
      },
      "total_terrazas": {
        "$sum": {
          "$size": "$terrazas"
        }
      }
    }
  },
  {
    "$sort": {
      "_id.distrito": 1,
      "_id.barrio": 1
    }
  }
]
```

## Métricas

- Tiempo de ejecución: **0.3650 segundos**
- Total de documentos devueltos: **131**

## Ejemplo de resultados

```json
[
  {
    "_id": {
      "distrito": "ARGANZUELA          ",
      "barrio": "ACACIAS             "
    },
    "total_locales": 1236,
    "total_terrazas": 97
  },
  {
    "_id": {
      "distrito": "ARGANZUELA          ",
      "barrio": "ATOCHA              "
    },
    "total_locales": 246,
    "total_terrazas": 6
  },
  {
    "_id": {
      "distrito": "ARGANZUELA          ",
      "barrio": "CHOPERA             "
    },
    "total_locales": 878,
    "total_terrazas": 50
  },
  {
    "_id": {
      "distrito": "ARGANZUELA          ",
      "barrio": "DELICIAS            "
    },
    "total_locales": 862,
    "total_terrazas": 71
  },
  {
    "_id": {
      "distrito": "ARGANZUELA          ",
      "barrio": "IMPERIAL            "
    },
    "total_locales": 826,
    "total_terrazas": 61
  }
]
```

---

# Consulta B

## Pipeline utilizado

```json
[
  {
    "$unwind": "$licencias"
  },
  {
    "$group": {
      "_id": "$licencias.desc_tipo_licencia",
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

## Métricas

- Tiempo de ejecución: **0.3849 segundos**
- Total de documentos devueltos: **5**

## Ejemplo de resultados

```json
[
  {
    "_id": "Transmisión de licencia Urbanística",
    "total": 57028
  },
  {
    "_id": "Declaración Responsable",
    "total": 51249
  },
  {
    "_id": "Licencia Urbanística",
    "total": 30783
  },
  {
    "_id": "Licencia recogida en el trabajo de campo",
    "total": 5956
  },
  {
    "_id": "Licencia de Funcionamiento",
    "total": 5813
  }
]
```

---

# Consulta C

## Pipeline utilizado

```json
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

## Métricas

- Tiempo de ejecución: **1.2462 segundos**
- Total de documentos devueltos: **45509**

## Ejemplo de resultados

```json
[
  {
    "_id": 20000596,
    "local": {
      "desc_distrito_local": "ARGANZUELA          ",
      "desc_barrio_local": "CHOPERA             "
    },
    "licencias": {
      "desc_tipo_situacion_licencia": "En tramitación"
    }
  },
  {
    "_id": 20000709,
    "local": {
      "desc_distrito_local": "ARGANZUELA          ",
      "desc_barrio_local": "ACACIAS             "
    },
    "licencias": {
      "desc_tipo_situacion_licencia": "En tramitación"
    }
  },
  {
    "_id": 20000709,
    "local": {
      "desc_distrito_local": "ARGANZUELA          ",
      "desc_barrio_local": "ACACIAS             "
    },
    "licencias": {
      "desc_tipo_situacion_licencia": "En tramitación"
    }
  },
  {
    "_id": 20000729,
    "local": {
      "desc_distrito_local": "ARGANZUELA          ",
      "desc_barrio_local": "DELICIAS            "
    },
    "licencias": {
      "desc_tipo_situacion_licencia": "En tramitación"
    }
  },
  {
    "_id": 20000729,
    "local": {
      "desc_distrito_local": "ARGANZUELA          ",
      "desc_barrio_local": "DELICIAS            "
    },
    "licencias": {
      "desc_tipo_situacion_licencia": "En tramitación"
    }
  }
]
```

---

# Consulta D

## Pipeline utilizado

```json
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

## Métricas

- Tiempo de ejecución: **4.4132 segundos**
- Total de documentos devueltos: **169559**

## Ejemplo de resultados

```json
[
  {
    "_id": {
      "id_local": 280032650,
      "id_seccion": "Q",
      "desc_seccion": "ACTIVIDADES SANITARIAS Y DE SERVICIOS SOCIALES",
      "id_division": "88",
      "desc_division": "ACTIVIDADES DE SERVICIOS SOCIALES SIN ALOJAMIENTO",
      "id_epigrafe": "889002",
      "desc_epigrafe": "OTROS ACTIVIDADES DE SERVICIOS SOCIALES (LABORES DE ASESORAMIENTO Y ORIENTACION) SIN ALOJAMIENTO N.C.O.P."
    },
    "total": 1
  },
  {
    "_id": {
      "id_local": 280071694,
      "id_seccion": "S",
      "desc_seccion": "OTROS SERVICIOS",
      "id_division": "96",
      "desc_division": "OTROS SERVICIOS PERSONALES",
      "id_epigrafe": "960201",
      "desc_epigrafe": "SERVICIO DE PELUQUERIA"
    },
    "total": 1
  },
  {
    "_id": {
      "id_local": 280061898,
      "id_seccion": "P",
      "desc_seccion": "EDUCACIÓN",
      "id_division": "85",
      "desc_division": "EDUCACIÓN",
      "id_epigrafe": "852001",
      "desc_epigrafe": "CENTRO DE INFANTIL Y PRIMARIA PUBLICO"
    },
    "total": 1
  },
  {
    "_id": {
      "id_local": 285026926,
      "id_seccion": "-1",
      "desc_seccion": "VALOR NULO EN ORIGEN",
      "id_division": "-1",
      "desc_division": "VALOR NULO EN ORIGEN",
      "id_epigrafe": "-1",
      "desc_epigrafe": "VALOR NULO EN ORIGEN"
    },
    "total": 1
  },
  {
    "_id": {
      "id_local": 70002362,
      "id_seccion": "G",
      "desc_seccion": "COMERCIO AL POR MAYOR Y AL POR MENOR; REPARACIÓN DE VEHÍCULOS DE MOTOR Y MOTOCICLETAS",
      "id_division": "47",
      "desc_division": "COMERCIO AL POR MENOR, EXCEPTO DE VEHÍCULOS DE MOTOR Y MOTOCICLETAS",
      "id_epigrafe": "472911",
      "desc_epigrafe": "OTRO COMERCIO AL POR MENOR DE PRODUCTOS ALIMENTICIOS (PERECEDEROS Y NO PERECEDEROS) CON VENDEDOR N.C.O.P."
    },
    "total": 1
  }
]
```

---

# Consulta E

## Pipeline utilizado

```json
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

## Métricas

- Tiempo de ejecución: **0.6180 segundos**
- Total de documentos devueltos: **131**

## Ejemplo de resultados

```json
[
  {
    "actividad_mas_frecuente": "VALOR NULO EN ORIGEN",
    "total": 555,
    "distrito": "CARABANCHEL         ",
    "barrio": "PUERTA BONITA       "
  },
  {
    "actividad_mas_frecuente": "VALOR NULO EN ORIGEN",
    "total": 490,
    "distrito": "CARABANCHEL         ",
    "barrio": "COMILLAS            "
  },
  {
    "actividad_mas_frecuente": "VALOR NULO EN ORIGEN",
    "total": 675,
    "distrito": "PUENTE DE VALLECAS  ",
    "barrio": "ENTREVIAS           "
  },
  {
    "actividad_mas_frecuente": "COMERCIO AL POR MAYOR Y AL POR MENOR; REPARACIÓN DE VEHÍCULOS DE MOTOR Y MOTOCICLETAS",
    "total": 263,
    "distrito": "CHAMBERI            ",
    "barrio": "VALLEHERMOSO        "
  },
  {
    "actividad_mas_frecuente": "COMERCIO AL POR MAYOR Y AL POR MENOR; REPARACIÓN DE VEHÍCULOS DE MOTOR Y MOTOCICLETAS",
    "total": 151,
    "distrito": "BARAJAS             ",
    "barrio": "CASCO H.BARAJAS     "
  }
]
```

---
