# Verificador-Puerto-443
# Instrucciones para el uso del Analizador de Puertos 443

## Descripción General
El Analizador de Puertos 443 es un programa que verifica la disponibilidad del puerto 443 en una lista de dominios proporcionados en un archivo CSV.

## Estructura del Archivo de Entrada
- Nombre del archivo CSV de entrada: `dominios.csv`
- Columna de interés: Columna E (0-indexed) que contiene los dominios a verificar.

## Estructura del Archivo de Salida
- Nombre del archivo CSV de salida: `resultados_puertos.csv`
- Campos del archivo de salida:
  - Dominio: Nombre del dominio verificado.
  - Puerto_443_abierto: Estado del puerto 443 (SI/NO/ERROR/...)
  - Otros_puertos_abiertos: Listado de otros puertos abiertos o estado del host.
  - Correo Enviado: Estado del envío del correo (si aplica).

## Modificaciones Necesarias
Para adaptar el programa a archivos diferentes, considera actualizar las siguientes variables en el código:
- `archivo_csv`: Nombre o ruta del archivo CSV de entrada. (Linea de codigo 82).
- `columna_a_extraer`: Índice de la columna que contiene los dominios. (Linea de codigo 83).
- `fila_a_iniciar`: Índice de la fila que contiene el primer dominio(la primer fila es el titulo). (Linea de codigo 84).
- `archivo_resultado`: Nombre o ruta del archivo CSV de salida. (Linea de codigo 88).

## Procedimiento de Ejecución
1. Asegúrate de tener el archivo de entrada con el nombre `dominios.csv` si no modificaste la configuracion original.
2. Ejecuta el código del programa python con el siguiente comando : sudo python3 port443.py 
3. Verifica los resultados en el archivo `resultados_puertos.csv`.

## Referencias Técnicas
- Documentación adicional sobre el uso de Python con archivos CSV.
- Referencias a herramientas como `smtplib` o `subprocess` si se requiere.

---
Autor: Ezequiel Matias Landaeta
Fecha de Creación: 6/12/2023
