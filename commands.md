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