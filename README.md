# Instrucciones para el uso del Analizador de Puertos 443

## Descripción General
El Analizador de Puertos 443 es una herramienta desarrollada en Python que verifica la accesibilidad del puerto 443 en una lista de dominios provistos en un archivo CSV. Este programa utiliza librerías estándar de Python y herramientas de línea de comandos como curl y nmap para obtener información sobre el estado del puerto en los dominios especificados.

El objetivo principal de esta herramienta es automatizar la verificación del estado del puerto 443 en múltiples dominios, lo que resulta crucial para sitios web y servicios que requieren conexiones seguras mediante HTTPS. Este análisis es fundamental para identificar posibles problemas de seguridad o configuración en los servidores web.

Al ejecutar el programa, se lee el archivo CSV de entrada que contiene una lista de dominios a verificar. Para cada dominio, se realiza una serie de comprobaciones utilizando curl y nmap, obteniendo información sobre el estado del puerto 443. Los resultados de estas verificaciones se registran en un nuevo archivo CSV de salida para un seguimiento y análisis más detallado. Solo se hace un escaneo de puertos con nmap en el caso de que el puerto 443 este cerrado.

El programa también cuenta con la capacidad de notificar por correo electrónico a los responsables de los dominios cuyo puerto 443 se encuentre cerrado.

## Estructura del Archivo de Entrada
  - Nombre del archivo CSV de entrada: `dominios.csv`
  - Columna de interés: Columna E (0-indexed) que contiene los dominios a verificar.

## Estructura del Archivo de Salida
  - Nombre del archivo CSV de salida: `resultados_puertos.csv`
  - Campos del archivo de salida:
  - Dominio: Nombre del dominio verificado.
  - Puerto_443_abierto: Estado del puerto 443 (SI/NO/SI-ERROR-NRO/SI-REDIRECCION).
    - SI:Puerto 443 Abierto.
    - NO:Puerto 443 Cerrado.
    - SI-ERROR-NRO:Puerto 443 Abierto pero el host devolvio algun error asociado.
    - SI-REDIRECCION:Puerto 443 Abierto pero hubo una redirreccion de http a https.
  - Otros_puertos_abiertos: Listado de otros puertos abiertos o estado del host.
  - Correo Enviado: Estado del envío del correo (si aplica).
    
## Configuración por Defecto
  - **Archivo CSV de Entrada:** `dominios.csv`
  - **Columna a Extraer dominios del Archivo CSV:** Columna E (0-indexed)
  - **Fila para Iniciar la Extracción:** Fila 2 (La primera es el titulo).
  - **Archivo de Resultados:** `resultados_puertos.csv`
  - **Servidor SMTP:** `smtp.gmail.com`
  - **Puerto SMTP:** 587
  - **Dirección de Correo Electrónico del Usuario SMTP:** (Valor vacío)
  - **Contraseña del Usuario SMTP:** (Valor vacío)
  
## Modificaciones Necesarias
Para adaptar el programa a archivos diferentes, considera actualizar las siguientes variables en el código:
### Variables a Modificar
  - `archivo_csv`: Nombre del archivo CSV de entrada. (Linea de codigo 16).
  - `columna_a_extraer`: Índice de la columna que contiene los dominios en el archivo CSV. (Linea de codigo 17).
  - `fila_a_iniciar`: Número de fila para comenzar a extraer información. (Linea de codigo 18).
  - `archivo_resultado`: Nombre o ruta del archivo CSV de salida. (Linea de codigo 21).
  - `servidor_smtp`: Nombre del servidor SMTP utilizado para enviar correos.  (Linea de codigo 24).
  - `puerto_smtp`: Puerto del servidor SMTP. (Linea de codigo 25).
  - `usuario_smtp`: Nombre de usuario del correo electrónico. (Linea de codigo 26).
  - `contraseña_smtp`: Contraseña del correo electrónico. (Linea de codigo 27).
  
- **Función `obtener_correo_para_domain`**:
  - `columna_dominio`: Obtiene el dominio correspondiente en la columna E. Modificar de ser necesario. (Linea de codigo 30).
  - `columna_correo`: Retorna el correo correspondiente al dominio en la columna A. Modificar de ser necesario. (Linea de codigo 31).
  
- **Función `enviar_correo`**:
  - Modificar `asunto` y `mensaje` si se cambian los datos del mensaje a enviar. (Lineas 203 y 204 de codigo).
  - Actualizar la información del servidor SMTP si hay cambios en la configuración.
 
## Procedimiento de Ejecución
1. Asegúrate de tener el archivo de entrada con el nombre `dominios.csv` si no se modifico la configuracion original.
2. Asegurarse que el archivo de entrada `dominios.csv` tenga los permisos de ejecucion necesarios. (sudo chmod +x dominios.csv).
3. Ejecuta el script de python con el siguiente comando : sudo python3 port443.py 
4. Verifica los resultados en el archivo `resultados_puertos.csv`.


---
-Autor: Ezequiel Matias Landaeta
-Fecha de Creación: 7/12/2023
