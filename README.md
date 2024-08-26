# Hash Analysis

Bienvenidos a la guía básica de análisis de Hash realizada gracias al [curso](https://www.coursera.org/learn/detection-and-response) de Google de Ciberseguridad 

Mas cosas a tener en cuenta cuando analizamos incidentes

###  **Detección y Análisis (Detection and Analysis)**

- **Indicadores de Compromiso (Indicators of Compromise - IoCs)**: Los IoCs son evidencia observable que sugiere la posibilidad de un incidente de seguridad. Ayudan a identificar quién y qué estuvo involucrado en un ataque después de que ha ocurrido, mientras que los Indicadores de Ataque (IoAs) se enfocan en encontrar el cómo y por qué de un ataque en tiempo real. La **Pirámide del Dolor** es un concepto que clasifica los IoCs en niveles de dificultad para los atacantes cuando se bloquean. Los niveles incluyen valores hash, direcciones IP, nombres de dominio, artefactos de red y host, herramientas, y tácticas, técnicas y procedimientos (TTPs), siendo los TTPs los más difíciles de detectar.
- **Proceso de Triage**: El triage es el proceso de priorizar incidentes según su urgencia. Consta de tres pasos: recibir y evaluar las alertas, asignar prioridades según el impacto y la recuperabilidad, y finalmente, analizar y recopilar información sobre el incidente para tomar decisiones informadas. Este proceso permite a los equipos de seguridad responder de manera efectiva y eficiente a las alertas de seguridad, asignando los recursos necesarios para abordar los problemas más críticos primero.

###  **Actividad Post-Incidente (Post-incident Activity)**

- **Revisión Post-incidente (Post-incident Review)**: Después de contener, erradicar y recuperarse de un incidente, la fase de actividad post-incidente se centra en aprender de lo ocurrido para mejorar la respuesta en el futuro. Las **lecciones aprendidas** se discuten en reuniones que involucran a todas las partes implicadas, con el objetivo de identificar errores, brechas en los procesos y posibles mejoras. Estas reuniones generan **recomendaciones** que pueden incluir la actualización de procedimientos o la implementación de nuevas herramientas de seguridad.
- **Informe Final**: Durante esta fase también se elabora un informe final que documenta todo lo ocurrido durante el incidente, incluyendo un resumen ejecutivo, una cronología detallada, un análisis de las acciones tomadas y una lista de recomendaciones para prevenir futuros incidentes similares. Este informe es clave para la transparencia y la mejora continua en la gestión de incidentes.





## Actividad de Análisis

**SHA256 file hash:** 54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b

Vamos a utilizar la herramienta de análisis de virus total para identificar los indicadores de peligro (Indicators of Compromise) e introducirlos en la plantilla de Pirámide del Dolor

------

### Paso 1: Introducimos el hash en [VirusTotal](https://www.virustotal.com/gui/home/upload)



<img align="center" src="/img/1ºimagenn.PNG"  />

------

### Paso 2: Analisis del informe de VirusTotal



**Detección:** Esta pestaña muestra una lista de proveedores de seguridad y sus veredictos sobre un artefacto, como si es malicioso, sospechoso o inseguro. Observa cuántos proveedores han marcado este hash como malicioso.

<img align="center" src="/img/2ºimagenn.PNG"  />

**Detalles:** Aquí se ofrece información adicional, incluyendo hashes relacionados como MD5 y SHA-1.

<img align="center" src="/img/3ºimagenn.PNG"  />

**Relaciones:** Esta pestaña contiene datos sobre las conexiones de red del malware con URLs, dominios y direcciones IP, indicando cuántos proveedores han marcado estas conexiones como maliciosas.

<img align="center" src="/img/4ºimagenn.PNG"  />

**Comportamiento:** Muestra información sobre la actividad observada del malware al ejecutarlo en un entorno aislado, detallando acciones en el registro, sistema de archivos, procesos, y las tácticas y técnicas empleadas.

<img align="center" src="/img/5ºimagenn.PNG"  />

------

### Paso 3: Determinar si es malcioso

Podemos determinar si es malicioso de la siguiente manera:

En la primera pagina podemos ver que distintos proveedores de seguridad lo identifican como malicioso, concretamente mas de 50 proveedores

En la puntuación de la comunidad se puede observar una puntuación negativa, otro indicativo de que puede ser malicioso. 

------

### Paso 4: Identificacion de indicadores de compromiso en la Piramide

- **Hash value:**  Otro hash para identificar a este archivo malicioso es el que podemos ver dentro de la pestaña **detalles** en MD5 O SHA-1

  Luego estos dos hash tambien identifican a este archivo:

  ***MD5 287d612e29b71c90aa54947313810a25***

   ***SHA-1 8f35a9e70dbec8f1904991773f394cd4f9a07f5e***

- **IP address**: Podemos encontrar las IPs contactadas en la seccion de **Relaciones**

<img align="center" src="/img/6ºimagenn.PNG"  />

- **Domain name:** Podemos encontrarlo en la parte de detalles filtrando por detecciones

  <img align="center" src="/img/7ºimagenn.PNG"  />

  Ademas si seguimos buscando encontramos los siguientes dominios agectados: misecure.com / org.misecure.com / res.public.onecdn.static.microsoft ...

  

- **Network artifact/host artifact:** Nos dirijimos a la parte de comportamiento y bajamos a la seccion de Network Communication para entender el comportamiento en las redes despues de ejecutar el archivo

  <img align="center" src="/img/8ºimagenn.PNG"  />

  Como podemos ver hay diferentes HTTP Request

- **Tools:** No podemos determinar ninguna herramienta en concreto pero segun la pestaña de detalles el archivo captura la entrada introducida por los usuarios <img align="center" src="/img/9ºimagenn.PNG"  />

- **Tactics, techniques, and procedures (TTPs):** Esto lo podemos encontrar en la parte inferior de la pestaña Behavior

  <img align="center" src="/img/10ºimagenn.PNG"  />
  
  

