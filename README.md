# Notas y Apuntes del lenguaje de programación R

## Aspectos Generales

R es un lenguaje de software libre desarrollado por GNU como alternativa a S-plus. Se complementa con C, C++, python y perl. Comparable en ciertos asepctos con Octave y Matlab.
R Console es una interfaz de comandos, R Commander es una interfaz gráfica interactiva libre opcional, y R Studio es un editor gráfico con herramientas  pero R se integra con Emacs, Vim, VS, etc.
Incluso es posible utilizar Jupyter en configuración con R.

Para instalar paquetes de R se utiliza el siguiente comando en la consola de R:

```r
> install.packages("<nombre>")
```

El R Studio puede hallarse como `rstudio-desktop-bin` en el AUR.

El formato de archivo es *.RData*, *.rdata* o *.r* .

Para nuestro caso se instalará `fBasics` y `Rcmdr` .

### Datos

R trabaja con un concepto de espacio conocido como Workspace, que representa un "root" donde se encuentra un projecto. Así, a partir de la definición de este workspace se pueden trabajar con script, y cargar y guardar datos. Los comandos utilizados son:

```r
#Para definir el Workspace
> setwd("/home/USER/Workspace")

#Para salvar el entorno
> save.image("/home/USER/Workspace/proyecto.rdata")

#Para salvar el entorno
> load("/home/USER/Workspace/proyecto.rdata")
```

Asimismo, pueden importarse datasets de otros archivos tales como ASCII en txt:

```r
#Para asignar el dataset a una variable
> variable <- read.delim("/home/USER/Workspace/dataset.txt", dec="<separador>")
#donde el separador puede ser "," , " " , "    ", etc.

#Para visualizar el dataset
> View(variable)
```

Para otros formatos como OCTAVE, SAS, SPSS... es necesario instalar la líbrería `foreign`, la cual se carga y se utiliza de la siguiente manera:

```r
#Para cargar la libreria
> library("foreign")

#Para leer el fichero
> read.<formato>("/home/USER/Workspace/dataset.<formato>")
```

Dentro de la función read es podible establecer parámetros de conversión que pueden resultar importantes dependiendo del caso.

#### Práctica

A modo de práctica es posible importar datasets que existen dentro de r de la siguiente manera:

```r
> data(<nombre_del_dataset>)
> identity(<nombre_del_dataset>)
> force(<nombre_del_dataset>)
```

## Números, operaciones y funciones

R puede utilizar números enteros, reales o complejos y cada uno puede aplicarse a una función.

| Suma | Resta | Mult. | Div. | Poten.    | Prod. Matrices |
| ---- | ----- | ----- | ---- | --------- | -------------- |
| x+y  | x-y   | x*y   | x/y  | x**y  x^y | A%*%B          |

## Funciones

| Significado Matemático        | Código                 |
| ----------------------------- | ---------------------- |
| Signo de *x*                  | `> sign(x)`            |
| Máximo entre *x* y *y*        | `> max(x,y)`           |
| Mínimo entre *x* y *y*        | `> min(x,y)`           |
| Factorial de *x*              | `> factorial(x)`       |
| Combinatorio *n* sobre *k*    | `> choose(n,k)`        |
| pi ( $\pi$ )                  | `> pi`                 |
| *e*                           | `> exp(1)`             |
| Infito ( $\infin$)            | `> inf`                |
| Indeterminado ( $0\over0$)    | `> NaN`                |
| N/A                           | `> NA`                 |
| Objeto Nulo                   | `> NULL`               |
| Seno y arcoseno               | `> sen(x)  asen(x)`    |
| Coseno y arcocoseno           | `> cos(x)  acos(x)`    |
| Tangente y arcotangente       | `> tan(x)  atan(x)`    |
| Trigonométricas hiperbólicas  | `> senh(x) cosh(x)...` |
| Exponencial base *e* ($e^x$)  | `> exp(x)`             |
| Logaritmo natural ( $ln(x)$ ) | `> log(x)`             |
| Logaritmo base 10             | `> log10(x)`           |
| Logaritmo base 2              | `> log2(x)`            |
| Raíz cuadrada ($\sqrt{x}$)    | `> sqrt(x)`            |
| Valor absoluto                | `> abs(x)`             |
| Redondeo Normal               | `> round(x)`           |
| Redondeo hacia Arriba         | `> ceiling(x)`         |
| Redondeo hacia Abajo          | `> floor(x)`           |
| Redondeo a *n* decimales      | `> round(x,n)`         |
| Elimina el decimal            | `> trunc(x)`           |

## Tipos de Variables

### Simples

```r
x = 3
```

### Vectores

```r
V = c(v1, v2, v3, ..., vn)
```

#### Funciones aplicables en vectores

| Función                                          | Significado                                                 |
| ------------------------------------------------ | ----------------------------------------------------------- |
| `a:b`                                            | Números secuenciales de a hasta b                           |
| `seq(a,b,by=n)`                                  | Números de a hasta b con separación n                       |
| `rep(x,n)`                                       | Repite x unas n veces                                       |
| `list(objeto1=c(a,b), objeto2="texto", objeto3)` | Crea una lista con los objetos dados                        |
| `V[n]`                                           | Valor enésimo de V                                          |
| `V[-n]`                                          | Todos los valores de V excepto el enésimo                   |
| `V[-(a:b)]`                                      | Todos los valores de V excepto los comprendidos entre a y b |
| `V[c(a,b,c)]`                                    | Devuelve los valores en las posiciones a, b y c.            |
| `V[x>a & x<b]`                                   | Devuelve los valores que sean mayores a *a* y menores a *b* |

### Matrices

Las matrices pueden entenderse como un vector de vectores, y se definen de la manera:

```r
M = matrix( c(1,2,3,4,5,6), nrow=2, ncol=3, byrow=TRUE) 

>M
     [,1] [,2] [,3]
[1,]   1    2    3
[2,]   4    5    6
```

```r
M = matrix( c(1,2,3,4,5,6), nrow=2, ncol=3) 

>M
     [,1] [,2] [,3]
[1,]   1    3    5
[2,]   2    4    6
```

Para añadir títulos a las Filas y Columnas se establece por uso de *dimnames*:

```r
dimnames=list( c( "Fila1", "Fila2"), c( "Columna1", "Columna2", "Columna3"))
```

```r
M = matrix( c(1,2,3,4,5,6), nrow=2, ncol=3, byrow=TRUE, dimnames=list( c( "Fila1", "Fila2"), c( "Columna1", "Columna2", "Columna3"))) 

>M
          Columna1     Columna2     Columna3
Fila1            1            2            3
Fila2            4            5            6
```

#### Confección de Matrices

| Función                                 | Significado                                                                                                        |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `rbind( vector1, vector2, vector3)`     | Define la matriz a partir de los vectores *o matrices* del input como filas.                                       |
| `cbind( vector1, vector2, vector3)`     | Define la matriz a partir de los vectores *o matrices* del input como columnas.                                    |
| `array(vector, dim=c(filas, columnas))` | Define la matriz de (filas, columnas) con los elementos del vector ordenados por columna. Es similar a `matrix()`. |



#### Selección

| Función                                             | Output                                                           |
| --------------------------------------------------- | ---------------------------------------------------------------- |
| `A[ fila, columna]`                                 | El elemento en la fila y columna indicadas.                      |
| `A[fila,]`                                          | Fila indicada                                                    |
| `A[,columna]`                                       | Columna indicada                                                 |
| `A[ a:b, c:d]`                                      | Submatriz de las filas a:b y columnas c:d                        |
| `A[ c( filaN, filaM, filaK), c( colG, colH, colJ)]` | Submatriz con las filas y columnas específicamente seleccionadas |



### Operadores Lógicos y Relacionales

| Operador     | Función                                   |
| ------------ | ----------------------------------------- |
| `A==B`       | Es igual a                                |
| `<`  ,  `<=` | Menor, Menor o igual                      |
| `>` , `>=`   | Mayor, Mayor o igual                      |
| `A!=B`       | `NOT` / Distinto de, Negación             |
| `A&B`        | `AND` / Y, Intersección lógica            |
| `A\|B`       | `OR` / Disyunción                         |
| `xor(A,B)`   | `XOR` / Disyunción Exclusiva              |
| `any(A,B,C)` | `TRUE`si *cualquier variable* es `TRUE`   |
| `all(A,B,C)` | `TRUE`si *todas las variables* son `TRUE` |
