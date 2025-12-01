#!/usr/bin/env bash

# Verificar que se haya pasado un archivo
if [[ -z "$1" ]]; then
    echo "Uso: ./convert.sh archivo.lu"
    exit 1
fi

archivo_lu="$1"
archivo_c="${archivo_lu%.lu}.c"    # reemplaza .lu por .c

rm -f "$archivo_c"
cp "$archivo_lu" "$archivo_c"

contenido=$(<"$archivo_c")

echo "$contenido"

# Si hay print → agregar stdio y reemplazar
if [[ "$contenido" == *"print"* ]]; then
    sed -i '1i #include <stdio.h>' "$archivo_c"
    sed -i 's/print/printf/g' "$archivo_c"
fi

# Si hay scan → también stdio
if [[ "$contenido" == *"scan"* ]]; then
    sed -i '1i #include <stdio.h>' "$archivo_c"
    sed -i 's/scan/scanf/g' "$archivo_c"
fi

# start → main
if [[ "$contenido" == *"start"* ]]; then
    sed -i 's/start/int main(){/g' "$archivo_c"
fi

# Convertir "hola" → ("hola")
sed -i 's/printf \?"\([^"]*\)"/printf("\1")/g' "$archivo_c"

# Agregar cierre }
echo "}" >> "$archivo_c"

# Número de líneas
total=$(wc -l < "$archivo_c")
last=$((total - 1))

# Solo ejecutar sed si hay líneas suficientes
if (( last >= 3 )); then
    sed -i "3,${last} s/\([^;]\)$/\1;/" "$archivo_c"
fi

gcc -o {archivo_lu%.lu} {archivo_lu%.lu}.c
rm -rf {archivo_lu%.lu}.c
