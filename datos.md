# Trabajar con datos en Python

Si eres un científico trabajas con datos. Citando
a Mythbusters, *the only difference between screwing around
and science is writing it down*. Existen millones
de librerías para leer diferentes tipos de datos, desde imágenes
y ficheros de audio a formatos súper específicos como discretizados
de superficies y volúmenes (*meshes*).

En este capítulo me voy a centrar en dos formas comunes de leer datos en columnas
o matrices usando Python: las librerías `numpy` y `pandas`.

## Leer ficheros usando numpy

[numpy](https://numpy.org) es un paquete de Python para manejar vectores o arrays en una o más dimensiones. Es una de las
librerías más útiles y que más he usado.

### Múltiples columnas, separados por espacios o tabuladores

El caso más sencillo es que el fichero contenga datos numéricos en forma de una matriz `NxM`, donde `N`
es el número de filas y `M` es el número de columnas. Si los datos están separados por espacios o
tabuladores, `numpy` es la forma más fácil de hacerlo:

```python
import numpy as np

data = np.loadtxt("data01.dat")
```

Donde `data01.dat` es el fichero de datos. `data` es un objeto que contiene los datos como si fuera
una matriz. `data.shape` proporciona las dimensiones del array, en este caso 2D.

```python
col_data = data[:,0]
```
es la forma de acceder a datos por columnas, en este caso la primera columna. `numpy` permite hacer
operaciones entre columnas, por ejemplo:

```python
sum_cols = data[:,0] + data[:,1]
```

### Ignorar líneas

Muchos ficheros contienen comentarios o el nombre de las columnas. `numpy` no tiene la capacidad
de trabajar con los nombres de las columnas, con lo que lo apropiado es ignorar esas líneas:

```python
import numpy as np

data = np.loadtxt("data02.dat", skiprows=3)
```
ignora las primeras tres líneas del fichero. 

Por defecto, `numpy` ignora las líneas que comienzan con la almohadilla (`#`)

### Valores separados por comas

Si los valores están separados por comas, `numpy` permite especificar el delimitador de los campos
en el fichero:

```python
import numpy as np

data = np.loadtxt("data03.dat", delimiter=',')
```
Esto es útil para leer ficheros con datos en formato CSV,
como por ejemplo al exportar hojas de excel.

### Limitaciones

`numpy.loadtxt` tiene una serie de limitaciones:

- Un array en `numpy` no puede contener más de un tipo de variable. Por ejemplo, si la columna primera
  son enteros y el resto floats, `numpy` importa todo como float. Es posible especificar el tipo
  de dato usando el modificador `dtype`. 

- `numpy` no puede asociar nombres de columnas a los datos.

Para eso es necesario usar `pandas`.

## Leer ficheros con pandas

[pandas](https://pandas.pydata.org) es un paquete de Python que extiende la capacidad de `numpy` para trabajar con dataframes. Los
tres motivos principales son para analizar ficheros donde las columnas mezclan diferentes tipos de
variables (strings, ints, floats, etc), cuando queremos preservar los nombres de las columnas, y
cuando cada fila tiene su propio nombre o índice.

La parte de pandas que no me gusta es que tiende a asumir que la
primera columna de un fichero contiene un índice y que, como
no lo uso a menudo, 
es difícil recordar cómo acceder a las columnas por número en lugar
de por nombre.

### Datos separados por comas con títulos en las columnas

Supongamos el fichero `data01.dat`:

```csv
X,Y
0.0, 0.0
1.0, 2.0
2.0, 3.0
```

`pandas` permite acceder a los datos por columnas:

```python
import pandas as pd
data = pd.read_csv("data01.dat")
print(data['X'])
```
Sin embargo, si intentamos usar slices para acceder a la primera
columna como en numpy usando:
```python
print(data[:,0])
```
obtenemos un error. De hecho, el resultado de `data['X']` es un objeto
de tipo `Series`. 

Si consideramos ahora el siguiente fichero:
```csv
Ciudad,Ranking
Sevilla,1
Chicago,2
Madrid,3
```
y corremos el siguiente código:
```python
import pandas as pd

data = pd.read_csv("data02.dat")
print(data['Ciudad'])
print(data['Ranking'])
```
El resultado es:
```
0    Sevilla
1    Chicago
2     Madrid
Name: Ciudad, dtype: object
0    1
1    2
2    3
Name: Ranking, dtype: int64
```
La columna 'Ranking' es de tipo `int64`, mientras que 'Ciudad' es
de tipo `object`, que representa un objecto genérico en Python.
Si modificamos el fichero de manera que el Ranking de Sevilla
es `1.0`:
```
Ciudad,Ranking
Sevilla,1.0
Chicago,2
Madrid,3
```
el resultado es que la columna 'Ranking' es ahora de tipo `float64`.

Convertir el formato a un numpy array es trivial:

```python
import pandas as pd

data = pd.read_csv("data03.dat")
data_np = data["Ranking"].to_numpy()
print(data_np, type(data_np))
```
Resulta en:
```
[1. 2. 3.] <class 'numpy.ndarray'>
```
