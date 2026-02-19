# 📊 Exploración Dataset: Airbnb

## Información general

- **Registros:** 16,313
- **Columnas:** 13

## Columnas

| columna                      | tipo    |
|:-----------------------------|:--------|
| accommodates                 | int64   |
| amenities                    | object  |
| bedrooms                     | float64 |
| beds                         | float64 |
| country                      | str     |
| host_id                      | int64   |
| id                           | int64   |
| location                     | object  |
| name                         | str     |
| neighbourhood_group_cleansed | str     |
| number_of_reviews            | int64   |
| price                        | float64 |
| room_type                    | str     |

## Valores nulos

| columna                      |   nulos |
|:-----------------------------|--------:|
| beds                         |      32 |
| name                         |      11 |
| bedrooms                     |       5 |
| country                      |       1 |
| accommodates                 |       0 |
| amenities                    |       0 |
| host_id                      |       0 |
| id                           |       0 |
| location                     |       0 |
| neighbourhood_group_cleansed |       0 |
| number_of_reviews            |       0 |
| price                        |       0 |
| room_type                    |       0 |

## Registros duplicados

- **Duplicados:** 0

## Primeras filas (head)

|   accommodates | amenities                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |   bedrooms |   beds | country   |   host_id |    id | location                                                                    | name                                  | neighbourhood_group_cleansed   |   number_of_reviews |   price | room_type       |
|---------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------:|-------:|:----------|----------:|------:|:----------------------------------------------------------------------------|:--------------------------------------|:-------------------------------|--------------------:|--------:|:----------------|
|              2 | ['TV', 'Wireless Internet', 'Air conditioning', 'Kitchen', 'Smoking allowed', 'Elevator', 'Heating', 'Family/kid friendly', 'Hangers', 'translation missing: en.hosting_amenity_50', 'Hot water', 'Microwave', 'Coffee maker', 'Refrigerator', 'Dishes and silverware', 'Cooking basics', 'Long term stays allowed', 'Well-lit path to entrance']                                                                                                                                                                                                                       |          0 |      1 | Spain     |     71597 | 18628 | {'coordinates': [40.424715317537384, -3.6986381877058387], 'type': 'Point'} | Greta Studio Wifi Chueca en Madrid    | Centro                         |                  37 |      54 | Entire home/apt |
|              2 | ['TV', 'Cable TV', 'Wireless Internet', 'Air conditioning', 'Kitchen', 'Elevator', 'Heating', 'Washer', 'Dryer', 'Essentials', 'Hangers', 'Hair dryer', 'Iron', 'Laptop friendly workspace', 'translation missing: en.hosting_amenity_49', 'translation missing: en.hosting_amenity_50', 'Hot water', 'Bed linens', 'Extra pillows and blankets', 'Ethernet connection']                                                                                                                                                                                                |          0 |      1 | Spain     |     74966 | 19864 | {'coordinates': [40.413418179848634, -3.706838445919361], 'type': 'Point'}  | PLAZA MAYOR  (wifi, air conditioning) | Centro                         |                  56 |      65 | Entire home/apt |
|              2 | ['TV', 'Cable TV', 'Internet', 'Wireless Internet', 'Air conditioning', 'Wheelchair accessible', 'Kitchen', 'Doorman', 'Elevator', 'Buzzer/wireless intercom', 'Heating', 'Washer', 'Dryer', 'Essentials', '24-hour check-in', 'Hangers', 'Hair dryer', 'Iron', 'Laptop friendly workspace', 'Private entrance']                                                                                                                                                                                                                                                        |          0 |      1 | Spain     |     82175 | 21512 | {'coordinates': [40.42492023544748, -3.7134461317198415], 'type': 'Point'}  | Studio in Plaza de España             | Moncloa - Aravaca              |                  36 |      40 | Entire home/apt |
|              1 | ['TV', 'Internet', 'Wireless Internet', 'Air conditioning', 'Kitchen', 'Free parking on premises', 'Doorman', 'Elevator', 'Heating', 'Washer', 'First aid kit', 'Fire extinguisher', 'Essentials', 'Shampoo', 'Lock on bedroom door', 'Hangers', 'Hair dryer', 'Iron', 'Laptop friendly workspace', 'translation missing: en.hosting_amenity_49', 'translation missing: en.hosting_amenity_50', 'Hot water', 'Bed linens', 'Extra pillows and blankets', 'Pocket wifi', 'Microwave', 'Coffee maker', 'Refrigerator', 'Dishes and silverware', 'Cooking basics', 'Oven'] |          1 |      1 | Spain     |     83531 | 21853 | {'coordinates': [40.4034095295952, -3.740841968636018], 'type': 'Point'}    | Bright and airy room                  | Latina                         |                  26 |      17 | Private room    |
|             10 | ['TV', 'Internet', 'Wireless Internet', 'Air conditioning', 'Wheelchair accessible', 'Kitchen', 'Doorman', 'Elevator', 'Heating', 'Family/kid friendly', 'Washer', 'Dryer', 'Essentials', '24-hour check-in', 'Hangers', 'Hair dryer', 'Iron', 'Laptop friendly workspace']                                                                                                                                                                                                                                                                                             |          4 |      5 | Spain     |     82175 | 23021 | {'coordinates': [40.4234166657964, -3.712456247572053], 'type': 'Point'}    | Elegant Apartment in Spain Square     | Moncloa - Aravaca              |                  55 |      90 | Entire home/apt |

## Estadísticas numéricas

|       |   accommodates |     bedrooms |        beds |         host_id |              id |   number_of_reviews |      price |
|:------|---------------:|-------------:|------------:|----------------:|----------------:|--------------------:|-----------:|
| count |    16313       | 16308        | 16281       | 16313           | 16313           |          16313      | 16313      |
| mean  |        3.29817 |     1.32947  |     2.00737 |     5.51615e+07 |     1.40669e+07 |             27.6553 |    75.0693 |
| std   |        2.01121 |     0.836362 |     1.54489 |     4.93438e+07 |     6.70065e+06 |             45.7246 |   144.493  |
| min   |        1       |     0        |     0       |  5154           | 18628           |              0      |     8      |
| 25%   |        2       |     1        |     1       |     1.09695e+07 |     8.79178e+06 |              1      |    35      |
| 50%   |        3       |     1        |     2       |     3.89033e+07 |     1.58433e+07 |              9      |    59      |
| 75%   |        4       |     2        |     2       |     9.61883e+07 |     1.95532e+07 |             33      |    88      |
| max   |       16       |    10        |    44       |     1.68123e+08 |     2.27722e+07 |            488      |  9000      |

## Estadísticas categóricas

|        | amenities   | country   | location                                                                    | name                            | neighbourhood_group_cleansed   | room_type       |
|:-------|:------------|:----------|:----------------------------------------------------------------------------|:--------------------------------|:-------------------------------|:----------------|
| count  | 16313       | 16312     | 16313                                                                       | 16302                           | 16313                          | 16313           |
| unique | 14528       | 1         | 16313                                                                       | 15867                           | 21                             | 3               |
| top    | ['']        | Spain     | {'coordinates': [40.424715317537384, -3.6986381877058387], 'type': 'Point'} | Perfect room in Madrid's Center | Centro                         | Entire home/apt |
| freq   | 107         | 16312     | 1                                                                           | 12                              | 8474                           | 10338           |
