# Simulacion-M-M-S

La base de datos proviene de https://seelab.net.technion.ac.il/data/

# Diccionario de Datos: Anonymous Bank Call-Center

A continuación se detalla la explicación de los 17 campos que componen cada registro del conjunto de datos.

### 1. Identificación del Sistema (VRU)
* **vru+line:** Código de 6 dígitos que identifica la unidad y la línea.
    * Cada llamada entra primero por una VRU (Unidad de Respuesta de Voz); existen 6 VRUs etiquetadas de AA01 a AA06.
    * Cada VRU tiene varias líneas (1-16), sumando un total de 65 líneas.

### 2. Identificación de la Llamada y el Cliente
* **call_id:** Un número de 5 dígitos asignado a cada llamada entrante. Los identificadores son únicos pero no necesariamente consecutivos debido a la asignación en diferentes VRUs.
* **customer_id:** Número de identificación del cliente (0 a 12 dígitos).
    * Es "0" si el sistema no identifica al cliente (por ejemplo, clientes potenciales).
    * Nota: Debido a un error del sistema, no se grabó el ID de los clientes que no esperaron en la cola.
* **priority:** Indica la prioridad del cliente (0, 1 o 2):
    * **0 y 1:** Clientes regulares o no identificados.
    * **2:** Clientes de alta prioridad[cite: 44]. A estos se les asigna 1.5 minutos de tiempo de espera al inicio para avanzar su posición en la cola y están exentos de una tarifa mensual.

### 3. Clasificación de la Llamada
* **type:** Código de 2 letras que describe el tipo de servicio solicitado:
    * **PS:** Actividad regular (*Peilut Shotefet*).
    * **PE:** Actividad regular en inglés (*Peilut English*).
    * **IN:** Consultas de internet (*Internet*).
    * **NE:** Actividad bursátil/acciones (*Niarot Erech*).
    * **NW:** Clientes potenciales solicitando información.
    * **TT:** Clientes a los que el banco devolvió la llamada pero fueron puestos en espera porque el agente estaba ocupado.

### 4. Tiempos de Entrada y VRU
* **date:** Fecha de la llamada en formato Año-Mes-Día (6 dígitos).
* **vru_entry:** Hora exacta (6 dígitos) en que la llamada entra al centro de llamadas (entra a la VRU).
* **vru_exit:** Hora de salida de la VRU (6 dígitos), ya sea hacia la cola de espera, directamente al servicio o por abandono.
* **vru_time:** Tiempo en segundos (1 a 3 dígitos) que la llamada pasó dentro de la VRU.

### 5. Tiempos en Cola de Espera (Queue)
* **q_start:** Hora en que la llamada se une a la cola de espera. Si el cliente abandona desde la VRU y no llega a la cola, este valor es `00:00:00`.
* **q_exit:** Hora en que la llamada sale de la cola de espera (ya sea para recibir servicio o por abandono).
* **q_time:** Tiempo total en segundos (1 a 3 dígitos) que la llamada pasó en la cola de espera.

### 6. Resultado y Servicio del Agente
* **outcome:** El resultado final de la llamada, con tres posibilidades:
    * **AGENT:** Se proporcionó servicio.
    * **HANG:** El cliente colgó.
    * **PHANTOM:** Una llamada virtual que debe ser ignorada (son escasas).
* **ser_start:** Hora en que el agente comenzó el servicio.
* **ser_exit:** Hora en que el agente terminó el servicio.
* **ser_time:** Duración del servicio en segundos.
* **server:** Nombre del agente que atendió la llamada. Si no hubo servicio, aparece como `NO_SERVER`.
