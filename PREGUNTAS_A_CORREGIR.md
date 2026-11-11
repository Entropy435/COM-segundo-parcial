# Informe de Auditoría: Preguntas a Corregir en el Cuestionario Web

**Fecha del informe:** 7 de noviembre de 2026  
**Materia:** Comunicaciones (COM) - Segundo Parcial  
**Origen de la auditoría:** Contrastación de las 19 capturas de pantalla de la carpeta `C:\Users\andyt\Desktop\fotos com` (donde lo seleccionado en el Google Forms original es la clave oficial de la cátedra con puntaje 1/1 y los comentarios en rosa reflejan las respuestas actuales en nuestra aplicación web).  
**Archivo afectado en el código:** `scratch/verified_all_questions.json`

---

## 1. Resumen General del Diagnóstico

El análisis comparativo identificó **14 preguntas con discrepancias** entre lo que el examen oficial de Google Forms califica como correcto y lo que actualmente califica nuestra aplicación web.

Las causas de estos desfasajes se clasifican en cuatro categorías claras:
1. **Inversión de orden en Grillas / Diagramas (5 casos):** El profesor numeró los elementos en el dibujo de abajo hacia arriba o de izquierda a derecha, mientras que en la web se asumió el orden inverso.
2. **Criterio de Cátedra vs. Rigor Técnico (5 casos):** En ciertos temas de redes (Módem Dial-Up en capas 1 y 2, señal ADSL sobre cobre como analógica, perturbación de ruido en el diagrama de ojo, o cierre por EMI en vertical), las diapositivas de la cátedra manejan definiciones particulares que contradicen la bibliografía general de ingeniería. Para el examen, la clave evaluadora automática de la cátedra es la que otorga el puntaje.
3. **Trampas Visuales en Esquemas (1 caso):** El profesor insertó un componente extraño (**CMTS**, exclusivo de cable coaxial) dentro del esquema de una red ADSL. La pregunta es Falsa debido a ese bloque intruso.
4. **Omisiones en Selección Múltiple y Tipos Numéricos (3 casos):** Falta marcar una casilla correcta que sí estaba en el Forms ("conmutación de paquetes") y discrepancias de decimales/redondeo (`221,9` vs `221`).

---

## 2. Tabla Comparativa Rápida (14 Preguntas)

| # | ID | Sección | Bloque | Tema Principal | Respuesta Actual en la Web (Errónea) | Respuesta Oficial en Google Forms (Correcta) | Tipo de Causa |
|:--:|:--:|:--:|:---|:---|:---|:---|:---|
| **1** | **#78** | Teórico | Bloque 1: OSI y TCP/IP | Grilla PDUs TCP/IP | Invertido (1=Mensaje ... 5=Señales) | **1=Señales, 2=Tramas, 3=Paquetes, 4=Segmentos, 5=Mensaje** | Inversión Grilla |
| **2** | **#11** | Teórico | Bloque 3: xDSL y FTTx | Celdas ATM en la milla ADSL | Falso | **Verdadero** | Criterio Cátedra |
| **3** | **#12** | Teórico | Bloque 3: xDSL y FTTx | Transmisión DSLAM - ATU-R es digital | Verdadero | **Falso** (en cobre es señal analógica DMT) | Criterio Cátedra |
| **4** | **#16** | Teórico | Bloque 3: xDSL y FTTx | Afirmaciones ADSL (Multi) | 4 opciones marcadas | **5 opciones marcadas** (sumar *Conmutación de paquetes*) | Omisión Casilla |
| **5** | **#18** | Teórico | Bloque 3: xDSL y FTTx | Diagrama ADSL 1 a 7 | Invertido (1 a 3 en Abonado) | **1 a 3 en Central (1=DSLAM, 2=Splitter, 3=Central)** | Inversión Grilla |
| **6** | **#80** | Teórico | Bloque 3: xDSL y FTTx | Afirmaciones xDSLx Col 1-3 | Col 1 = Abonado, Col 2 = Plantel | **Col 1 = Plantel exterior, Col 2 = Abonado** | Cruce de Columnas |
| **7** | **#81** | Teórico | Bloque 3: xDSL y FTTx | Siglas FTTx 1 a 4 | 1=FTTN, 2=FTTC, 3=FTTB, 4=FTTH | **1=FTTC, 2=FTTB, 3=FTTN, 4=FTTH** | Orden Diagrama |
| **8** | **#91** | Teórico | Bloque 3: xDSL y FTTx | Diagrama ADSL con CMTS | Verdadero | **Falso** (tiene incrustado un bloque CMTS de CATV) | Pregunta Trampa |
| **9** | **#106**| Teórico | Bloque 3: xDSL y FTTx | Capas OSI de Módem Dial-Up | Capas Física | **Capas Física y de Enlace de Datos** | Criterio Cátedra |
| **10**| **#14** | Teórico | Bloque 4: HFC y DOCSIS | Diagrama CATV 1 a 7 | Mapeo teórico invertido | **1=Splitter, 2=Cable Módem, 3=ISP, 4=Coaxil, 5=CMTS...** | Grilla Scrambled |
| **11**| **#82** | Teórico | Bloque 6: Cableado y Medios| Estándares IEEE 802 | Marca e2 en 802.11b, g, n | **Solo 802.11 base es e2; b, g, n son No corresponde** | Criterio Cátedra |
| **12**| **#2**  | Práctico| Bloque 5: Perturbaciones | Diagrama de Ojo (Perturbación) | Jitter | **Ruido** (cruces por cero limpios; dispersión vertical) | Corrección Errónea |
| **13**| **#53** | Práctico| Bloque 5: Perturbaciones | Tasa Video PPV 1280x720 | 221 | **221,9** (clave oficial del Forms) | Typo Cátedra |
| **14**| **#205**| Práctico| Bloque 5: Perturbaciones | Cierre ojo con EMI | Horizontal y Vertical | **Vertical** (acopla ruido en amplitud/tensión) | Criterio Cátedra |

---

## 3. Ficha Detallada Pregunta por Pregunta

---

### PREGUNTA 1: ID #78 (Teórico - Bloque 1)
- **Enunciado:** *"Indique la estructura de las unidades de datos en cada capa del modelo TCP/IP"*
- **Tipo:** Grilla (`grid`)
- **Filas:** `['Segmentos', 'Paquetes', 'Mensaje', 'Tramas', 'Señales']`
- **Columnas:** `['espacio 1', 'espacio 2', 'espacio 3', 'espacio 4', 'espacio 5']`
- **Respuesta actual en la web:** `correct = [1, 2, 0, 3, 4]`  
  *(Segmentos: espacio 2, Paquetes: espacio 3, Mensaje: espacio 1, Tramas: espacio 4, Señales: espacio 5)*
- **Respuesta oficial en Google Forms:**  
  En el diagrama del examen, los números están puestos de abajo hacia arriba:
  - `espacio 1` = Capa Física (**Señales**)
  - `espacio 2` = Capa de Enlace (**Tramas**)
  - `espacio 3` = Capa de Red (**Paquetes**)
  - `espacio 4` = Capa de Transporte (**Segmentos**)
  - `espacio 5` = Capa de Aplicación (**Mensaje**)
- **Por qué está mal:** La web asumió el orden top-down (de capa superior a inferior), pero el dibujo del examen numera desde el fondo (1 en router/señales) hasta la cima (5 en correos).
- **Acción de corrección:** Cambiar `correct` a `[3, 2, 4, 1, 0]`.

---

### PREGUNTA 2: ID #11 (Teórico - Bloque 3)
- **Enunciado:** *"La transmisión a través de celdas ATM forma parte del tipo de transmisión que se utiliza en la milla en la tecnología de acceso a internet ADSL"*
- **Tipo:** Verdadero / Falso (`tf`)
- **Respuesta actual en la web:** `correct = 1` (**Falso**)
- **Respuesta oficial en Google Forms:** `correct = 0` (**Verdadero**, puntaje 1/1 ✓)
- **Por qué está mal:** Desde el punto de vista físico estricto, la última milla sobre el cobre usa DMT (modulación discreta), y ATM corre por encima como protocolo de enlace y transporte hacia el DSLAM/BRAS. Sin embargo, para la cátedra, la arquitectura clásica de acceso ADSL está basada en celdas ATM (IP sobre ATM sobre ADSL), por lo que en el examen lo califican como Verdadero.
- **Acción de corrección:** Cambiar `correct` a `0` (**Verdadero**).

---

### PREGUNTA 3: ID #12 (Teórico - Bloque 3)
- **Enunciado:** *"La transmisión entre el DSLAM y el ATU-R es digital"*
- **Tipo:** Verdadero / Falso (`tf`)
- **Respuesta actual en la web:** `correct = 0` (**Verdadero**)
- **Respuesta oficial en Google Forms:** `correct = 1` (**Falso**, puntaje 1/1 ✓)
- **Por qué está mal:** Aunque transporta datos digitales (bits), la señal física que viaja por el bucle de abonado de cobre entre el módem del usuario (ATU-R) y el concentrador de la central (DSLAM / ATU-C) es una **señal analógica modulada** mediante DMT (Discrete Multi-Tone con múltiples subportadoras analógicas en banda ancha). Para la cátedra, esa transmisión es analógica, por ende la afirmación de que es digital es Falsa.
- **Acción de corrección:** Cambiar `correct` a `1` (**Falso**).

---

### PREGUNTA 4: ID #16 (Teórico - Bloque 3)
- **Enunciado:** *"Indique cuáles de las siguientes afirmaciones son verdaderas respecto del acceso a internet por ADSL: Seleccione una o más de una"*
- **Tipo:** Selección Múltiple (`multi`)
- **Respuesta actual en la web:** `correct = [0, 4, 6, 9]` (4 casillas)
- **Respuesta oficial en Google Forms:** Requiere **5 casillas obligatorias**:
  1. `[0]` *"El acceso hasta el abonado se implementa sobre el mismo plantel exterior utilizado para brindar servicio al abonado telefónico."*
  2. `[4]` *"Este tipo de acceso a Internet tiene una tarifa plana, esto es independiente de la cantidad de MBytes consumidos por mes."*
  3. `[6]` *"El elemento que permite este tipo de acceso se denomina DSLAM y se encuentra en la central telefónica."*
  4. `[7]` *"Acceso a Internet por ADSL se implementa en Redes de Conmutación de paquetes"* (**¡FALTABA ESTA!**)
  5. `[9]` *"Este tipo de acceso a Internet permite tasas de transferencia de hasta 20 Mb/s."*
- **Por qué está mal:** La explicación del sitio ya mencionaba la conmutación de paquetes, pero el arreglo de índices en el JSON omitió el índice `7`. El alumno que rinde en Google Forms pierde el punto si no tilda las 5.
- **Acción de corrección:** Cambiar `correct` a `[0, 4, 6, 7, 9]`.

---

### PREGUNTA 5: ID #18 (Teórico - Bloque 3)
- **Enunciado:** *"De acuerdo a la siguiente figura, seleccione los elementos que se corresponden con los números indicados"*
- **Tipo:** Grilla (`grid`)
- **Filas:** `['Central telefonica', 'BRAS', 'Bucle de abonado', 'Instalaciones de abonado', 'ATM', 'Splitter (lado central)', 'OLT', 'Splitter ( lado abonado)', 'DSLAM ( ATU -C)', 'Modem (ATU-R)']`
- **Columnas:** `['1', '2', '3', '4', '5', '6', '7', 'No corresponde']`
- **Respuesta actual en la web:** `correct = [6, 7, 3, 0, 7, 5, 7, 1, 4, 2]`  
  *(Había invertido la figura poniendo 1 a 3 en el abonado y 5 a 7 en la central).*
- **Respuesta oficial en Google Forms:**  
  En el diagrama oficial del examen:
  - Lado Central (izquierda): `1` = **DSLAM (ATU-C)**, `2` = **Splitter (lado central)**, `3` = **Central telefónica (POTS Switch)**.
  - Al medio: `4` = **Bucle de abonado (Cross Box / par telefónico)**.
  - Lado Abonado (derecha): `5` = **Instalaciones de abonado**, `6` = **Splitter (lado abonado)**, `7` = **Modem (ATU-R)**.
  - Sobrantes: **BRAS**, **ATM** y **OLT** van a `No corresponde`.
- **Acción de corrección:** Cambiar `correct` a `[2, 7, 3, 4, 7, 1, 7, 5, 0, 6]`.

---

### PREGUNTA 6: ID #80 (Teórico - Bloque 3)
- **Enunciado:** *"Seleccione la opcion correcta para las siguientes afirmaciones"*
- **Tipo:** Grilla (`grid`)
- **Filas:**
  - `0`: *Utiliza TDMA para acceder a los ATU-C*
  - `1`: *Se encuentra en las instalaciones del abonado al servicio*
  - `2`: *Utiliza el plantel exterior destinado al servicio telefonico*
- **Columnas:** `['Columna 1', 'Columna 2', 'Columna 3']`  
  *(Donde la imagen define: 1 = La conexión entre ATU-R y ATU-C; 2 = El Modem-Router; 3 = El DSLAM)*
- **Respuesta actual en la web:** `correct = [2, 0, 1]`
- **Respuesta oficial en Google Forms:**
  - *Se encuentra en las instalaciones del abonado* -> **Columna 2** (El Modem-Router).
  - *Utiliza el plantel exterior destinado al servicio telefónico* -> **Columna 1** (La conexión entre ATU-R y ATU-C).
  - *Utiliza TDMA...* -> **Columna 3** (o no corresponde).
- **Acción de corrección:** Cambiar `correct` a `[2, 1, 0]`.

---

### PREGUNTA 7: ID #81 (Teórico - Bloque 3)
- **Enunciado:** *"Seleccione las siglas que identifican cada tipo de red de acceso de banda ancha implementada con cableado mixto (fibra-cobre)"*
- **Tipo:** Grilla (`grid`)
- **Filas:** `['FTTH', 'FTTN', 'FTTB', 'FTTC']`
- **Columnas:** `['espacio 1', 'espacio 2', 'espacio 3', 'espacio 4']`
- **Respuesta actual en la web:** `correct = [3, 0, 2, 1]`  
  *(FTTH=4, FTTN=1, FTTB=3, FTTC=2)*
- **Respuesta oficial en Google Forms:**  
  En el diagrama del docente, los números indican:
  - `espacio 1` = **FTTC** (gabinete / acera)
  - `espacio 2` = **FTTB** (edificio / fábrica)
  - `espacio 3` = **FTTN** (nodo)
  - `espacio 4` = **FTTH** (hogar)
  Por ende, para las filas `['FTTH', 'FTTN', 'FTTB', 'FTTC']`:
  - FTTH -> `espacio 4` (índice 3)
  - FTTN -> `espacio 3` (índice 2)
  - FTTB -> `espacio 2` (índice 1)
  - FTTC -> `espacio 1` (índice 0)
- **Acción de corrección:** Cambiar `correct` a `[3, 2, 1, 0]`.

---

### PREGUNTA 8: ID #91 (Teórico - Bloque 3)
- **Enunciado:** *"Un usuario realiza una transmision de datos utilizando la tecnologia de acceso a internet ADSL, a una velocidad de 0.96 Mbps. La relacion S/N del canal es de 37 dB, ¿el diagrama que se muestra a continuacion representa la tecnologia completa de la red ADSL utilizada?"*
- **Tipo:** Verdadero / Falso (`tf`)
- **Respuesta actual en la web:** `correct = 0` (**Verdadero**)
- **Respuesta oficial en Google Forms:** `correct = 1` (**Falso**, puntaje 1/1 ✓)
- **Por qué está mal:** Es una **pregunta trampa visual**. El esquema muestra `PC -> CPE -> DSLAM -> CMTS -> BRIP`. El dispositivo **CMTS (Cable Modem Termination System)** pertenece exclusivamente a redes de cable coaxial / CATV (DOCSIS), jamás a ADSL. Al incluir ese bloque erróneo, la respuesta correcta es **Falso**.
- **Acción de corrección:** Cambiar `correct` a `1` (**Falso**).

---

### PREGUNTA 9: ID #106 (Teórico - Bloque 3)
- **Enunciado:** *"¿En qué capas del Modelo OSI operan un Modem Dial Up?"*
- **Tipo:** Opción Única (`single`)
- **Opciones:** `['Capas Física y de Enlace de Datos', 'Ninguna correcta', 'Capas Física', 'Capas de Red y de Enlace de Datos', 'Capas Física y de Red']`
- **Respuesta actual en la web:** `correct = 2` (**Capas Física**)
- **Respuesta oficial en Google Forms:** `correct = 0` (**Capas Física y de Enlace de Datos**, puntaje 1/1 ✓)
- **Por qué está mal:** Teóricamente un módem tradicional es un equipo de Capa 1 (DCE / modulación). Sin embargo, el apunte de la cátedra sostiene que los módems Dial-Up implementan protocolos de entramado, control de flujo y detección/corrección de errores (normas V.42 / LAPM), por lo que operan en **Capa Física y de Enlace de Datos**.
- **Acción de corrección:** Cambiar `correct` a `0` (**Capas Física y de Enlace de Datos**).

---

### PREGUNTA 10: ID #14 (Teórico - Bloque 4)
- **Enunciado:** *"De acuerdo a la siguiente figura, seleccione los elementos que se corresponde con los números indicado"*
- **Tipo:** Grilla (`grid`)
- **Filas:** `['ISP', 'Splitter de coaxil', 'CMTS', 'Instalaciones de abonado', 'Cable Modem', 'Cabecera de CATV', 'Cable de distribucion (Coaxil)']`
- **Columnas:** `['1', '2', '3', '4', '5', '6', '7']`
- **Respuesta actual en la web:** `correct = [0, 4, 1, 6, 5, 2, 3]`
- **Respuesta oficial en Google Forms:**  
  La plantilla de respuestas del formulario original tiene asignado:
  - Splitter de coaxil -> **1**
  - Cable Modem -> **2** (o 7)
  - ISP -> **3**
  - Cable de distribucion (Coaxil) -> **4**
  - CMTS -> **5**
  - Instalaciones de abonado -> **6**
  - Cabecera de CATV -> **3** / 7
- **Por qué está mal:** El formulario original tiene las columnas asignadas con un orden desordenado respecto al recorrido físico del diagrama.
- **Acción de corrección:** Sincronizar el array con la clave de puntos del Google Forms original.

---

### PREGUNTA 11: ID #82 (Teórico - Bloque 6)
- **Enunciado:** *"Seleccione las opciones correctas"*  
  *(e1 = Estándar para redes LAN con cableado de cobre; e2 = Estándar para redes LAN inalámbricas; e3 = Estándar para redes PAN inalámbricas)*
- **Tipo:** Grilla (`grid`)
- **Filas:** `['IEEE 802.11', 'IEE 802.11n', 'IEE 802.11g', 'IEE 802.11b', 'IEEE 802.3', 'IEE 802.11', 'IEEE 802.15']`
- **Columnas:** `['e1', 'e2', 'e3', 'no corresponde']`
- **Respuesta actual en la web:** `correct = [3, 1, 1, 1, 0, 1, 2]`  
  *(Marcaba e2 para 802.11b, g, n y mandaba el genérico a no corresponde).*
- **Respuesta oficial en Google Forms:**
  - `IEEE 802.3` -> **e1** (Ethernet cobre)
  - `IEEE 802.11` (nombre base) -> **e2** (WLAN inalámbrica)
  - `IEEE 802.15` -> **e3** (PAN inalámbrica / Bluetooth)
  - `IEE 802.11n` -> **no corresponde**
  - `IEE 802.11g` -> **no corresponde**
  - `IEE 802.11b` -> **no corresponde**
  - `IEE 802.11` (duplicado) -> **no corresponde**
- **Por qué está mal:** La cátedra exige asociar a `e2` únicamente la norma madre `IEEE 802.11`. Considera que las enmiendas específicas (b, g, n) no corresponden a la definición general.
- **Acción de corrección:** Cambiar `correct` a `[1, 3, 3, 3, 0, 3, 2]`.

---

### PREGUNTA 12: ID #2 (Práctico - Bloque 5)
- **Enunciado:** *"Observe la figura adjunta e indique la presencia o no, de algunas de las siguientes perturbaciones"*
- **Tipo:** Opción Única (`single`)
- **Opciones:** `['ISI', 'Atenuacion', 'Ruido', 'Ninguna', 'Jitter']`
- **Respuesta actual en la web:** `correct = 4` (**Jitter**)
- **Respuesta oficial en Google Forms:** `correct = 2` (**Ruido**, puntaje 1/1 ✓)
- **Por qué está mal:** En el oscilograma del diagrama de ojo se observa que los cruces por cero en el eje horizontal ($t/T = 1$) son nítidos y convergen en un único punto (no hay ensanchamiento horizontal/temporal de fase). En cambio, los niveles lógicos superiores ($+1$) e inferiores ($-1$) presentan un notable engrosamiento y dispersión vertical (amplitud). Por lo tanto, la perturbación visible es **Ruido**.
- **Acción de corrección:** Cambiar `correct` a `2` (**Ruido**).

---

### PREGUNTA 13: ID #53 (Práctico - Bloque 5)
- **Enunciado:** *"Una compañía de comunicaciones desea realizar un estudio de requerimientos de una red de comunicación que transmita películas de video bajo la modalidad de paga por ver (PPV)... (1280 x 720 pixeles, 1024 niveles de brillo, 24 fotogramas/s sin compresión)..."*
- **Tipo:** Opción Única (`single`)
- **Opciones:** `['221,9', '221', '225', '230', 'ninguna es correcta']`
- **Respuesta actual en la web:** `correct = 1` (**221**)
- **Respuesta oficial en Google Forms:** `correct = 0` (**221,9**, puntaje 1/1 ✓)
- **Por qué está mal:** El cálculo numérico estricto da:  
  $$1280 \times 720 \times \log_2(1024) \times 24 = 921.600 \times 10 \times 24 = 221.184.000\text{ bps} \approx 221,18\text{ Mb/s}$$  
  En el sitio web se eligió 221 por redondeo al entero más cercano. Sin embargo, en la clave del Google Forms el docente cargó como correcta la opción **221,9**. Si el alumno marca 221 en el parcial, el sistema le descuenta el punto.
- **Acción de corrección:** Cambiar `correct` a `0` (**221,9**).

---

### PREGUNTA 14: ID #205 (Práctico - Bloque 5)
- **Enunciado:** *"El diagrama de ojo de una señal con EMI se cierra en forma:"*
- **Tipo:** Opción Única (`single`)
- **Opciones:** `['Horizontal', 'Horizontal y Vertical', 'Vertical', 'No tiene variación']`
- **Respuesta actual en la web:** `correct = 1` (**Horizontal y Vertical**)
- **Respuesta oficial en Google Forms:** `correct = 2` (**Vertical**, puntaje 1/1 ✓)
- **Por qué está mal:** La teoría específica de la cátedra indica: *"La interferencia electromagnética (EMI) acopla ruido en amplitud/tensión en el canal, reduciendo el margen de ruido y cerrando la apertura del diagrama de ojo en sentido vertical"*.
- **Acción de corrección:** Cambiar `correct` a `2` (**Vertical**).

---

## 4. Instrucciones para la Ejecución de las Correcciones

Para aplicar estas correcciones al sistema:
1. Actualizar el archivo `scratch/verified_all_questions.json` modificando los campos `correct` y enriqueciendo las `explanation` de las 14 preguntas listadas.
2. Ejecutar el generador estático:
   ```bash
   python scratch/build_html_generator.py
   ```
3. Ejecutar el script de despliegue a producción:
   ```bash
   python scratch/fast_deploy.py "Sincronizadas 14 preguntas con la clave oficial de Google Forms"
   ```
