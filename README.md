# PI_DataAnalitics



# ETL (Extract, Transform, Load) README

## Descripción
Este proyecto realiza un proceso de ETL (Extract, Transform, Load) sobre datos de homicidios almacenados en un archivo Excel. El objetivo es analizar y transformar la información para facilitar su exploración y visualización.

## Librerías utilizadas
El proyecto utiliza las siguientes librerías de Python:
- pandas
- openpyxl

## Ruta de los datos
Los datos se encuentran en el archivo `homicidios.xlsx` en la carpeta `data`.

## Extracción y Lectura de Datos
Se extraen los datos del archivo Excel utilizando pandas y openpyxl, y se carga la información en un DataFrame.

```python
import pandas as pd
import openpyxl

# Ruta para la lectura de los datos
path = "data/homicidios.xlsx"

# Lectura de los datos y transformación en un DataFrame
df = pd.read_excel(path, engine="openpyxl", sheet_name="HECHOS")
```

## Exploración de Datos (EDA)
Se realizan algunas exploraciones iniciales de los datos, como la cantidad de valores únicos en la columna 'ID', la cantidad de fechas únicas y la identificación de la cantidad de accidentes anuales.

```python
# Cantidad de valores únicos en la columna 'ID'
df['ID'].nunique()

# Cantidad de fechas únicas
df['FECHA'].nunique()

# Cantidad de accidentes anuales
print(df.groupby("AAAA").ID.nunique())
```

Además, se presenta un análisis más detallado de la distribución de accidentes por año y tipo de víctima y acusado.

## Fecha del Primer y Último Accidente
Se revisa la fecha del primer y último accidente en el conjunto de datos.

```python
# Fecha del primer accidente
Fecha_primer_accidente = df['FECHA'].min()
print(Fecha_primer_accidente)

# Fecha del último accidente
Fecha_ultimo_accidente = df['FECHA'].max()
print(Fecha_ultimo_accidente)
```

## Almacenamiento de Datos Transformados
Finalmente, se almacenan los datos transformados en archivos JSON para su posterior uso.

```python
# Almacenamiento de los DataFrames transformados en archivos JSON
df.to_json('./Data/clean/HECHOS.json')
df1.to_json('./Data/clean/VICTIMA.json')
df2.to_json('./Data/clean/ACUSADO.json')
```

## Archivos Resultantes
- `HECHOS.json`: Contiene el DataFrame completo.
- `VICTIMA.json`: Contiene el DataFrame con información sobre las víctimas.
- `ACUSADO.json`: Contiene el DataFrame con información sobre los acusados.