# Comandos Linux

## wc

Muestra la cantidad de *lineas* - *palabras* - *caracteres*, con las banderas:

1. `-l`
2. `-w`
3. `-m`

## sort

Ordena elementos

1. `-r` orden inverso
2. `-n` criterio numerico
3. `-k num` donde `num` es el numero de columna
4. `-t sep` donde `sep` es el separador, por default es el espacio, donde se especifica en tre comillas
5. `-f` Ignora mayusculas y minusculas

## uniq

No muestra las lineas repetidas **que sean contiguas** 

1. `-c` muestra el numero de repeticiones
2. `-d` muestra solo las repetidas
3. `-u` muestra solo las **no** repetidas

## expand 

Converte tabuladores a espacios:

```bash
expand -t num 
```

Donde `num` es el numero de espacios por tabulador

## fmt

Sirve para limitar la cantidad de caracteres a lo ancho:

`-w num` donde `num` es el maximo de caracteres a lo ancho

## cut

Separa/corta columnas en partes

```bash
cut -d del -f cols fichero
cut -c caracteres fichero
```

* `del` es el **simbolo** delimitador
* `cols` son las columnas
  * `-f 1`, `-f 3`
  * `-f 1,3`
  * `-f 1-3`, `-f 1,3-5`
  * `-c a-b` donde `a` y `b` son columnas, en general `a` $<$ `b`

## split

Sirve para dividir un fichero en ficheros mas pequeños

```bash
split -l lineas fichero [prefijo]
split -b tamaño fichero [prefijo]
```

Se generaran archivos con el formato:

* `xaa`
* `xab`
* `xac`
* $\vdots$
* Los que sean necesarios

Se puede cambiar la `x` por el `[prefijo]`.

La bandera `-b` sirve para especificar el tamaño, como `1M`, es decir 1 megabyte.

## join / paste*

Sirven para unir ficheros con un campo en comun, **DEBEN ESTAR ORDENADOS**

```bash
join [opciones] f1 f2 ...
```

Opciones:

* `-t` delimitador (por defecto espacios y tabs)
* `-1 campo fichero1`
* `-2 campo fichero2`

con **paste** simplemente junta las columnas usando el delimitador con `-t` 

## grep

Busca uno o varios **patrones** en ficheros

```bash
grep [opciones] patron fichero(s)
```

Ejemplo:

```bash
grep : fichero
```

Buscara las lineas donde se encuentre el simbolo `:`

Opciones:

* `-i` para no distiguir mayusculas y minusculas
* `-c` cuenta el numero de coincidencias
* `-e` para buscar mas patrones, ejemplo:
  * `grep -e An -e : -e , fichero`
* `-v` muestra las no coincidencias
* `-A num` muestra las `num` lineas a continuacion de los resultados
* `-B num`  igual que el anterior, pero ahora muestra las `num` anteriores
* `-r` o `-R` para buscar dentro de directorios, ya que de manera estandar no busca dentro de directorios
*  `-H` para mostrar el nombre del fichero y `-h` para omitirlo

# Expresiones regulares

Sirve para buscar de una forma mas *compleja* la informacion que necesitamos.

* `^` ($\leftarrow$ Acento circunflejo):
  * `^s` busca los elementos que empiecen con `s`
* `s$` busca los elementos que terminen con `s`
* `^...$` busca los elementos de 3 caracteres (pero de toda la linea)
* `^[AM]` Frases que empiecen por la letra `A` o la letra `M`
* `^[A-M]` De `A` a `M` minuscula
* `^[^AM]` / `^[^A-M]`Los nombres que no empiecen con A o M 

<u>**Los siguientes comandos solo funcionan con `grep`**</u>

Usando `grep -E [comandos]`

* `?` Cero o una vez: `[1-9]?` 

## egref / fgrep

Es igual que

```bash
grep -E # Habilita expresiones regulares
grep -F # Desabilita expresiones regulares, TODAS
```

## sed

Sirve para modificar o borrar el contenido de un fichero.

```bash
sed [opciones] 'expresion' ficheros
```

* `-i` aplica los cambios al fichero original <b style="color:red"> CUIDADO </b>, mejor usar `-i[ext]` donde `[ext]` es la extension del archivo original. Es decir, si se aplica `-i.orig` a un fichero `file.txt` esto quiere decir que los cambios se aplicaran a `file.txt` y el original se guardara como seguridad en `file.txt.orig`. 
* `-E` se habilitan las expresiones regulares



### Sustitucion

```bash
sed 's/patron/remplazo/mod' ficheros
```

Donde `mod` puede ser `g` (busca todas las coincidencias) `-i` no distingue mayusculas de minusculas.

### Borrado

```bash
sed 'patron/d' ficheros
```

### Ejemplos practicos:

Para eliminar los espacios en blanco:

```bash
sed '/^$/d' ficheros
grep -v ^$ fichero 
```

