---
id: Conceptos básicos
Categoría: Redes
tags:
  - redes
  - tcp
  - udp
  - ip
  - mac
  - puertos
  - OSI
  - Segmentation
  - Subnetting
  - networkTools
---
# **IP**
---
Una **dirección IP** (Protocolo de Internet) es un identificador único asignado a cada dispositivo conectado a una red, como internet. Su función principal es permitir la localización y comunicación de dispositivos dentro de una red, ya sea pública o privada.


### **Direcciones IPv4**

#### **Estructura de una dirección IPv4**

**IPv4** consta de 32 bits, que se representan en formato decimal como cuatro octetos separados por puntos (por ejemplo: `192.168.1.1`). Cada octeto tiene 8 bits y el valor de cada uno puede ir de **0 a 255**.

##### **División de la dirección IPv4:**
###### 1. **Dirección de red**:
- Representa la parte de la dirección que identifica la red a la que pertenece el dispositivo.
  
###### 2. **Dirección de host**:
- Representa la parte de la dirección que identifica el dispositivo (host) dentro de esa red.


#### **Clases de Direcciones IPv4**

| **Clase** | **Rango de Direcciones**    | **Máscara de Subred** | **Uso Principal**                              |
| --------- | --------------------------- | --------------------- | ---------------------------------------------- |
| A         | 1.0.0.0 a 127.255.255.255   | 255.0.0.0 (/8)        | Redes grandes (grandes empresas, ISPs)         |
| B         | 128.0.0.0 a 191.255.255.255 | 255.255.0.0 (/16)     | Redes medianas (universidades, empresas)       |
| C         | 192.0.0.0 a 223.255.255.255 | 255.255.255.0 (/24)   | Redes pequeñas (oficinas, hogares)             |
| D         | 224.0.0.0 a 239.255.255.255 | N/A                   | Multicast (transmisión a múltiples receptores) |
| E         | 240.0.0.0 a 255.255.255.255 | N/A                   | Reservado para uso futuro o investigación      |

##### Notas importantes:

- Las clases A, B y C son las que se utilizan para asignar direcciones a redes y dispositivos.

- Las clases D y E son utilizadas para propósitos especiales, como multicast y reservas para investigación.

- Las direcciones de las clases A, B y C son **las más comunes** en las redes privadas y públicas.


#### **Direcciones IPv4 privadas**
---
Además de las clases, hay rangos de direcciones IP privadas que se utilizan dentro de redes locales (LAN) y no son enrutables en internet. Estas direcciones están definidas para evitar la saturación del espacio de direcciones públicas.

| **Clase** | **Tipo** | **Rango de Direcciones**      |
| --------- | -------- | ----------------------------- |
| A         | Privada  | 10.0.0.0 a 10.255.255.255     |
| B         | Privada  | 172.16.0.0 a 172.31.255.255   |
| C         | Privada  | 192.168.0.0 a 192.168.255.255 |

> 📌  Estas direcciones son útiles para redes internas y se utilizan junto con un proceso llamado **NAT (Network Address Translation)** para comunicarse con la red pública de internet.


#### **Máscara de subred**:

La máscara de subred es la que determina cuántos bits corresponden a la parte de la red y cuántos a la parte del host. 


> [!EJEMPLOS] Ejemplo
> Si tenemos la dirección IP `192.168.1.1` y la máscara `255.255.255.0`:
>- **Red**: `192.168.1.0`
>- **Host**: `0.0.0.1` (en este caso el host específico dentro de esa red).

###### **Formato de la máscara de subred**:

Ejemplo de representación de una máscara de subred **255.255.255.0** en formato **decimal**, **binario** y **CIDR**:

| **Formato**  | **Representación**                             |
|--------------|-----------------------------------------------|
| **Decimal**  | `255.255.255.0`                               |
| **Binario**  | `11111111.11111111.11111111.00000000`         |
| **CIDR**     | `/24`                                         |

####### **CIDR (Classless Inter-Domain Routing)**

CIDR permite definir subredes de forma más flexible, sin depender de las clases A, B y C.

- Se expresa en formato **IP/prefijo**.
- **Ejemplo:** `192.168.1.1/24` → Equivale a la máscara `255.255.255.0`.
- Permite **un uso más eficiente de las direcciones IP**, evitando desperdicios.

###### **Conversión de máscara de red a binario:**

| CIDR | Máscara decimal | Máscara binaria                     |
| ---- | --------------- | ----------------------------------- |
| /24  | 255.255.255.0   | 11111111.11111111.11111111.00000000 |
| /25  | 255.255.255.128 | 11111111.11111111.11111111.10000000 |
| /26  | 255.255.255.192 | 11111111.11111111.11111111.11000000 |


### **Direcciones IPv6**
---
#### **Estructura de una dirección IPv6**

Una dirección IPv6 tiene 128 bits, que se representan en 8 bloques de 4 dígitos hexadecimales, separados por dos puntos (:). Por ejemplo:

```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

#### **Tipos de direcciones IPv6**

| **Tipo de Dirección IPv6**  | **Rango**                 | **Uso**                                    | **Ejemplo**                   |
|-----------------------------|---------------------------|--------------------------------------------|-------------------------------|
| **Unicast Global**           | 2000::/3                  | Dirección pública (enrutable en Internet)  | 2001:0db8::/32                |
| **Local Link (Link-local)**  | FE80::/10                 | Solo válida en la red local                | FE80::/64                     |
| **Multicast**                | FF00::/8                  | Para envío de paquetes a múltiples dispositivos | FF02::1 (todos los dispositivos en una red local) |
| **Unique Local Address (ULA)** | FC00::/7                  | Dirección privada para redes internas      | FC00::/8                      |
| **Anycast**                  | Usando direcciones Unicast| Direcciones asignadas a varios dispositivos | Varia según la implementación |

#### **Prefijos en IPv6**

En IPv6, las direcciones se dividen en bloques de prefijos, y la **longitud del prefijo** se utiliza para identificar cuántos bits se utilizan para la parte de red de la dirección, similar a cómo funcionan las máscaras de subred en IPv4. Los prefijos comunes son:

- **/64**: Usado para redes locales, ya que la parte de la dirección de red es de 64 bits.
- **/48**: Usado para asignaciones a organizaciones o entidades grandes.
- **/128**: Dirección única (usada para un solo dispositivo).

#### **Dirección de IPv6 "Cero" o "Cero comprimida"**

IPv6 permite comprimir direcciones de ceros usando la notación `::`. Por ejemplo:

- Dirección completa: `2001:0db8:0000:0000:0000:0000:0000:0001`
- Dirección comprimida: `2001:db8::1`


## **Diferencias claves entre IPv4 e IPv6**
---

| **Diferencia**                      | **IPv4**                               | **IPv6**                                  |
|-------------------------------------|----------------------------------------|-------------------------------------------|
| **Tamaño de la dirección**          | 32 bits                                | 128 bits                                 |
| **Formato**                          | Notación decimal (ej. 192.168.1.1)     | Notación hexadecimal (ej. 2001:db8::1)    |
| **NAT (Network Address Translation)**| Requiere NAT debido al espacio limitado de direcciones | No necesita NAT, cada dispositivo tiene una dirección pública única |
| **Configuración automática**        | No soporta autoconfiguración (requiere DHCP) | Soporta autoconfiguración (sin necesidad de servidor DHCP) |


## **Obtener la dirección IP local**

#### 1. Usando `hostname -I`

```shell
hostname -I
192.168.1.100
```

#### 2. Usando `ip a` o `ip addr`

```shell
ip a

3: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    inet 192.168.1.100/24 brd 192.168.1.255 scope global dynamic enp0s3
       valid_lft 86007sec preferred_lft

```

#### 2. Usando `ifconfig`

```shell
ifconfig

enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.100  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::a00:27ff:fe96:88c7  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:96:88:c7  txqueuelen 1000  (Ethernet)
        RX packets 120412  bytes 15825430 (15.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 73216  bytes 10564376 (10.5 MB)
        TX errors 0  dropped 0  overruns 0  carrier 0  collisions 0

```


# **MAC**
---
Una dirección **MAC (Media Access Control)** es una identificación única asignada a dispositivos de red. Se usa en la **capa 2** del modelo OSI y tiene **48 bits** (6 bytes), representados en formato hexadecimal de **12 dígitos**.

### **Componentes de la dirección MAC:**

- **Primeros 6 dígitos** (Ejemplo: `00:40:96`) → **OUI (Organizationally Unique Identifier)**, identifica al fabricante.

- **Últimos 6 dígitos** → Identifican el **controlador de interfaz de red**.

### **Cambiar la dirección MAC:**

```shell
sudo ifconfig {{interfaz}} down
sudo macchanger -m {{nueva_mac}} {{interfaz}}
sudo ifconfig {{interfaz}} up
```

### **Identificar el fabricante de una NIC usando la MAC**

`macchanger`
```shell
macchanger -m E0:B6:55:51:92:25
```

```shell
macchanger -l | grep E0:B6:55
```

`ieee-data` List.
```shell
grep -i "E0-B6-55" /usr/share/ieee-data/oui.txt
```


# **Modelo OSI**
---
El **modelo OSI (Open Systems Interconnection)** es un marco conceptual utilizado para entender cómo los diferentes protocolos de red interactúan entre sí. 

## **Las 7 capas del modelo OSI:**

| Número de Capa | Capa            | Descripción                                                | PDU (Protocol Data Unit) | Ejemplos                   |
| -------------- | --------------- | ---------------------------------------------------------- | ------------------------ | -------------------------- |
| 1              | Física          | Transmite datos en señales eléctricas o inalámbricas.      | Bits                     | Ethernet, Wi-Fi, Bluetooth |
| 2              | Enlace de Datos | Maneja la comunicación entre dispositivos en la misma red. | Tramas (Frames)          | MAC, ARP, PPP              |
| 3              | Red             | Encargada del direccionamiento y enrutamiento de paquetes. | Paquetes                 | IP, ICMP, RIP, OSPF        |
| 4              | Transporte      | Asegura la entrega de datos entre dispositivos.            | Segmentos                | TCP, UDP                   |
| 5              | Sesión          | Establece, gestiona y finaliza sesiones de comunicación.   | Datos de sesión          | NetBIOS, RPC               |
| 6              | Presentación    | Formatea, cifra y comprime los datos.                      | Datos formateados        | SSL/TLS, JPEG, ASCII       |
| 7              | Aplicación      | Permite la interacción del usuario con la red.             | Datos de aplicación      | HTTP, FTP, SMTP, DNS       |

# **UDP vs TCP**
---
### **TCP (Transmission Control Protocol)**

TCP es un **protocolo orientado a conexión** utilizado para transmitir datos de manera confiable a través de una red. Asegura que los datos lleguen en orden y sin pérdidas, mediante un proceso de verificación y corrección de errores. TCP establece una conexión entre el emisor y el receptor a través del **Three-Way Handshake**, y garantiza la entrega de los datos en el mismo orden en que se enviaron. 

#### **Three-Way Handshake (TCP)**
El proceso de tres pasos para establecer una conexión segura:

##### **Conexión exitosa**

| Paso           | Descripción                                       | Acción                                                                                                                                    |
| -------------- | ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **1. SYN**     | El cliente inicia la conexión.                    | El cliente envía un paquete **SYN** al servidor.                                                                                          |
| **2. SYN-ACK** | El servidor responde con una confirmación.        | El servidor responde con un paquete **SYN-ACK** (confirma el recibo del SYN y también indica que está listo para establecer la conexión). |
| **3. ACK**     | El cliente confirma la recepción de la respuesta. | El cliente envía un paquete **ACK** para confirmar que la conexión está establecida.                                                      |

##### **Conexión rechazada**

| Paso       | Descripción                             | Acción                                                                                                                                                     |
| ---------- | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. SYN** | El cliente intenta iniciar la conexión. | El cliente envía un paquete **SYN** al servidor.                                                                                                           |
| **2. RST** | El servidor rechaza la conexión.        | En lugar de responder con un **SYN-ACK**, el servidor responde con un paquete **RST** (Reset) para indicar que no está dispuesto a establecer la conexión. |
| **3. -**   | La conexión no se establece.            | La conexión no se establece debido al **RST**.                                                                                                             |

##### **Conexión rechazada por el Cliente**

| Paso           | Descripción                                | Acción                                                                                                                      |
| -------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| **1. SYN**     | El cliente intenta iniciar la conexión.    | El cliente envía un paquete **SYN** al servidor.                                                                            |
| **2. SYN-ACK** | El servidor responde con una confirmación. | El servidor responde con un paquete **SYN-ACK** para confirmar el recibo del SYN y estar listo para establecer la conexión. |
| **3. RST**     | El cliente rechaza la conexión.            | En lugar de enviar el paquete **ACK** de confirmación, el cliente envía un paquete **RST** al servidor.                     |
| **4. -**       | La conexión no se establece.               | Esto a veces se realiza para no dejar rastro en los logs de ciertos firewalls u otros sistemas de monitoreo.                |


### **UDP (User Datagram Protocol)**
---
UDP es un **protocolo sin conexión**, lo que significa que no establece una conexión previa antes de transmitir datos. No garantiza la entrega ni el orden de los datos, lo que lo hace más rápido pero menos confiable que TCP. 


### **Diferencias clave entre TCP y UDP:**
---

| Característica  | **TCP**                                     | **UDP**                                                |
| --------------- | ------------------------------------------- | ------------------------------------------------------ |
| **Orientación** | Orientado a conexión                        | Sin conexión                                           |
| **Fiabilidad**  | Garantiza la entrega confiable de datos     | No garantiza la entrega ni el orden de los datos       |
| **Velocidad**   | Más lento debido a la sobrecarga de control | Más rápido debido a la falta de control y verificación |
| **Uso típico**  | Transferencia de archivos, navegación web   | Streaming de video, juegos en línea, VoIP              |


### **Puertos comunes de TCP y UDP (0 a 65,535).**
---
#### **Puertos TCP comunes:**

| Puerto     | Servicio | Descripción                                |
| ---------- | -------- | ------------------------------------------ |
| `21`       | FTP      | Transferencia de archivos.                 |
| `22`       | SSH      | Acceso remoto seguro.                      |
| `23`       | Telnet   | Conexión remota sin cifrado.               |
| `25`       | SMTP     | Envío de correos electrónicos.             |
| `53`       | DNS      | Resolución de nombres de dominio.          |
| `80`       | HTTP     | Transferencia web.                         |
| `443`      | HTTPS    | Transferencia web segura (SSL/TLS).        |
| `110`      | POP3     | Recepción de correos electrónicos.         |
| `139, 445` | SMB      | Compartición de archivos en redes Windows. |
| `143`      | IMAP     | Acceso a correos electrónicos.             |

#### **Puertos UDP comunes:**

| Puerto  | Servicio | Descripción                       |
| ------- | -------- | --------------------------------- |
| `53`    | DNS      | Resolución de nombres de dominio. |
| `67/68` | DHCP     | Asignación de direcciones IP.     |
| `69`    | TFTP     | Transferencia simple de archivos. |
| `123`   | NTP      | Sincronización horaria.           |
| `161`   | SNMP     | Administración de red.            |

# **Network Segmentation, Subnetting y CIDR**
---
## **Segmentación de Red**

Dividir una red en segmentos **lógicos o físicos** usando **firewalls, VLANs o listas de control de acceso (ACLs)**. Esto mejora la **seguridad, rendimiento y administración**, ya que se puede controlar el tráfico entre segmentos y reducir la propagación de amenazas.

## **Subnetting**

Es el proceso de dividir una red IP en subredes más pequeñas mediante una **máscara de red**, lo que permite **una mejor gestión de direcciones y segmentación del tráfico**.

- **Ejemplo de máscara de red:**
    - `255.255.255.0` → Indica que los **primeros 3 octetos (24 bits)** identifican la red, mientras que el **último octeto (8 bits)** define los hosts disponibles en la subred.


> [!NOTE] Aclaración 
>   - **Segmentación** → Control de tráfico y seguridad.  
>   - **Subnetting** → Organización y uso eficiente de IPs.


# **Tools CLI para el cálculo de subredes:**
---
### `bc` 
Es una calculadora CLI avanzada para realizar cálculos matemáticos.

```shell
echo "obase=2; 192" | bc    # Binario: 11000000
echo "obase=8; 192" | bc    # Octal: 300
echo "obase=16; 192" | bc   # Hexadecimal: C0
echo "ibase=2; 11000000" | bc  # Binario a Decimal: 192
echo "ibase=8; 300" | bc    # Octal a Decimal: 192
echo "ibase=16; C0" | bc    # Hexadecimal a Decimal: 192
```

Ejecutar un comando dentro de otro usando `$()` anidada con `echo`

```shell
echo "$(echo "obase=2; 192" | bc)".168.111.42
```

📌 **Notas:**

- `obase` define la base del resultado.
- `ibase` define la base de entrada.
- Para conversiones cruzadas (ej. binario a hexadecimal), primero debes convertir a decimal.

### `ipcalc`
---
```shell
ipcalc 192.168.1.0/24
Address:   192.168.1.0          11000000.10101000.00000001. 00000000
Netmask:   255.255.255.0 = 24   11111111.11111111.11111111. 00000000
Wildcard:  0.0.0.255            00000000.00000000.00000000. 11111111
=>
Network:   192.168.1.0/24       11000000.10101000.00000001. 00000000
HostMin:   192.168.1.1          11000000.10101000.00000001. 00000001
HostMax:   192.168.1.254        11000000.10101000.00000001. 11111110
Broadcast: 192.168.1.255        11000000.10101000.00000001. 11111111
Hosts/Net: 254                   Class C, Private Internet

```

### `sipcalc`
---
```shell
sipcalc 192.168.1.0/24
-[ipv4 : 192.168.1.0/24] - 0

[CIDR]
Host address		- 192.168.1.0
Host address (decimal)	- 3232235776
Host address (hex)	- C0A80100
Network address		- 192.168.1.0
Network mask		- 255.255.255.0
Network mask (bits)	- 24
Network mask (hex)	- FFFFFF00
Broadcast address	- 192.168.1.255
Cisco wildcard		- 0.0.0.255
Addresses in network	- 256
Network range		- 192.168.1.0 - 192.168.1.255
Usable range		- 192.168.1.1 - 192.168.1.254

-
```
