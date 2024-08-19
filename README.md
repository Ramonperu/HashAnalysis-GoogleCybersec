# WireShark & TcpDump

Bienvenidos a la guia basica de WireShark y TcpDump realizada gracias al [curso](https://www.coursera.org/learn/detection-and-response) de Google de Ciberseguridad 

## **Wireshark**

Wireshark es una herramienta gráfica de análisis de protocolos de red que permite capturar y analizar tráfico de red en tiempo real. Es utilizada por profesionales de la red **para diagnosticar problemas, analizar flujos de datos, y entender el funcionamiento de diferentes protocolos**.

<img align="center" src="/img/1ºimagenn.PNG"  />

### **Uso de Filtros en Wireshark**

Wireshark ofrece dos tipos principales de filtros: **filtros de captura** y **filtros de visualización**. Estos filtros son esenciales para manejar grandes volúmenes de datos, permitiendo enfocar el análisis en el tráfico relevante.



1. **Filtros de Captura:** Los filtros de captura se aplican antes de iniciar la captura de tráfico, limitando los datos que se almacenan. Wireshark utiliza la sintaxis de los Filtros de Paquetes Berkeley (BPF) para definir estos filtros.

   Ejemplos comunes:

   - Capturar tráfico de una IP específica:

     ```
     host 192.168.1.1
     ```

   - Capturar tráfico TCP en un puerto específico:

     ```
     tcp port 80
     ```

   - Capturar solo tráfico ICMP (ping):

     ```
     icmp
     ```

   - Capturar tráfico entre dos hosts específicos:

     ```
     host 192.168.1.1 and host 192.168.1.2
     ```

2. **Filtros de Visualización:** Los filtros de visualización se aplican a los datos ya capturados, permitiendo filtrar la visualización en la interfaz gráfica sin afectar la captura en sí. Estos filtros son más flexibles y utilizan una sintaxis específica de Wireshark.

   Ejemplos comunes:

   - Filtrar por dirección IP de origen o destino:

     ```
     ip.addr == 192.168.1.1
     ```

   - Filtrar tráfico HTTP:

     ```
     http
     ```

   - Filtrar por puerto TCP específico:

     ```
     tcp.port == 443
     ```

   - Filtrar paquetes que contienen un string específico en el contenido:

     ```
     frame contains "password"
     ```

   - Filtrar por dirección MAC:

     ```
     eth.addr == 00:11:22:33:44:55
     ```

   - Filtrar tráfico de un protocolo específico, como DNS:

     ```
     dns
     ```

3. **Uso avanzado de filtros:**

   - Combinación de filtros:

      Se pueden combinar múltiples condiciones usando operadores lógicos como and, or, y not.

     ```
     ip.src == 192.168.1.1 and tcp.port == 80
     ```

   - Seguimiento de flujos TCP:

      Para analizar el flujo completo de una sesión TCP:

     - Selecciona un paquete en la ventana de captura.
     - Clic derecho y selecciona "Follow" > "TCP Stream". Esto mostrará la conversación completa en una ventana separada.

## **Tcpdump**

tcpdump es una herramienta de línea de comandos que permite capturar y analizar paquetes de red en tiempo real. Es muy utilizada en entornos de servidor y en situaciones donde se necesita una herramienta ligera y poderosa para capturar tráfico sin necesidad de una interfaz gráfica.

### **Comandos y Uso Básico de tcpdump**

tcpdump tiene una amplia variedad de opciones y parámetros que permiten capturar y analizar tráfico de red de manera muy detallada. A continuación se detallan algunos de los comandos más básicos y su uso.

1. **Iniciar captura en una interfaz específica:**

   ```
   tcpdump -i eth0
   ```

   Este comando captura tráfico en la interfaz `eth0`. Se puede reemplazar `eth0` con la interfaz de red que desees monitorear.

2. **Mostrar la lista de interfaces disponibles:**

   ```
   tcpdump -D
   ```

   Muestra las interfaces de red disponibles en el sistema.

3. **Capturar tráfico de un host específico:**

   ```
   tcpdump host 192.168.1.1
   ```

   Captura todo el tráfico proveniente o destinado a la IP `192.168.1.1`.

4. **Filtrar tráfico por puerto:**

   ```
   tcpdump port 80
   ```

   Captura tráfico en el puerto `80` (normalmente HTTP). Puedes especificar otros puertos según sea necesario.

5. **Guardar la captura en un archivo:**

   ```
   tcpdump -w capture.pcap
   ```

   Este comando guarda la captura en un archivo llamado `capture.pcap`, que puede ser analizado posteriormente con tcpdump o Wireshark.

6. **Leer un archivo de captura:**

   ```
   tcpdump -r capture.pcap
   ```

   Lee y analiza el contenido de un archivo de captura `capture.pcap`.

7. **Mostrar más detalles de los paquetes capturados:**

   ```
   tcpdump -v
   ```

   Usa la opción `-v` (verbose) para obtener más detalles sobre cada paquete capturado. Puedes usar `-vv` para aún más detalles.

8. **Capturar solo el comienzo de cada paquete:**

   ```
   tcpdump -s 64
   ```

   Captura solo los primeros 64 bytes de cada paquete, lo que es útil si solo necesitas las cabeceras y quieres ahorrar espacio en el archivo de captura.

9. **Combinar filtros:**

   - Capturar tráfico HTTP desde un host específico:

     ```
     tcpdump tcp port 80 and host 192.168.1.1
     ```

   - Capturar tráfico TCP excepto de un puerto específico:

     ```
     tcpdump tcp and not port 22
     ```

10. **Mostrar tráfico en formato legible (conversión de nombres de dominio y puertos):**

    ```
    tcpdump -n
    ```

    La opción `-n` evita la resolución de nombres de host y puertos, mostrando las direcciones IP y números de puerto en lugar de nombres de dominio o servicios.

## **Similitudes y Diferencias entre Wireshark y tcpdump**

**Similitudes:**

- Ambos son poderosos analizadores de tráfico de red y pueden capturar y analizar paquetes.
- Usan el formato `.pcap` para almacenar capturas, lo que permite intercambiar archivos entre ambas herramientas.
- Soportan filtros para seleccionar tráfico específico, aunque Wireshark tiene una interfaz más amigable para construir y aplicar filtros.

**Diferencias:**

- Interfaz de Usuario:
  - Wireshark tiene una GUI intuitiva, lo que facilita el análisis visual y la navegación por los datos.
  - tcpdump es una herramienta de línea de comandos, más adecuada para entornos sin GUI o donde se requiere una herramienta ligera.
- Recursos:
  - Wireshark es más pesado en términos de consumo de CPU y memoria, especialmente en capturas grandes.
  - tcpdump es mucho más eficiente y puede ejecutarse en sistemas con recursos limitados.
- Funcionalidad Adicional:
  - Wireshark ofrece herramientas adicionales como gráficos de tiempo, análisis estadístico, y decodificación avanzada de protocolos.
  - tcpdump se centra en la captura y análisis básico, siendo ideal para scripts y automatización.

