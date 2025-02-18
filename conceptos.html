---
id: Cálculo de Subredes y Hosts
Categoría: Redes
tags:
  - redes
  - Subnetting
  - networkHosts
---
## 1. Cálculo de subredes y hosts
---
### **1.1. Determinar el número de subredes**

- **Bits prestados**:  

  Al hacer subnetting, se "toman" bits del campo de hosts para crear subredes. Si se toman **`n`** bits adicionales, el número de subredes posibles es:  

```
Número de subredes = 2^n
```

### **1.2. Determinar el número de hosts por subred**

 #### **Cálculo de hosts**:  

  Si se tienen **`h`** bits disponibles para hosts, el número total de direcciones en una subred es:  

```
Total de direcciones = 2^h
```
  
#### **Hosts útiles**:  

Se deben restar 2 direcciones especiales: la dirección de red y la de broadcast. El cálculo de hosts útiles sería:
  
```
Hosts útiles = 2^h - 2
```



## 2. Ejemplo práctico de subredes
---
### **Ejemplo 1: Dividir una red /24 en 4 subredes**

#### 1. **Datos iniciales**:

   - Red original: `192.168.1.0/24`
   - Bits disponibles para hosts en /24: `32 - 24 = 8` bits.

#### 2. **Determinar Bits para subredes**:

   - Para crear **4 subredes** se requiere:
```
2^n >= 4  ⇒  n = 2
```

   - Nueva máscara de subred:  
```
/24 + 2 = /26
```

#### 3. **Calcular hosts por subred**:

   - Bits para hosts en la nueva máscara:  
```
32 - 26 = 6 bits
```

   - Hosts útiles por subred:  
```
2^6 - 2 = 64 - 2 = 62
```

#### 4. **Conversión de la máscara**:

   - Máscara de subred `/26` en formato decimal:  
```
255.255.255.192
```

### **Ejemplo 2: Determinar tamaño de subred con VLSM (Variable length subnet masking)**

**Requisito**: Crear una subred que soporte al menos **30 hosts**.

#### 1. **Determinar el número de bits necesarios**:

   - Necesitamos encontrar el menor número **`h`** tal que:
```
2^h - 2 >= 30
```

   - Probamos con valores de **`h`**:
    - Para **h = 5**: `2^5 - 2 = 32 - 2 = 30` → Cumple el requisito.

#### 2. **Definir la máscara de subred**:

   - Bits para hosts: **h = 5**  
   - Máscara de subred:  
```
32 - 5 = 27  bits para la red → Notación: /27
```

   - **Hosts útiles en /27**:  
     - 30 direcciones útiles (de 32 direcciones totales).


## 3. Rango de direcciones en una subred
---

| **Elemento**               | **Descripción**                                                                     | **Ejemplo (Decimal)**                                        | **Ejemplo (Binario)**                                                         |
| -------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------- |
| **Dirección de Red**       | Primera dirección de la subred, donde todos los bits de host son 0.                 | `192.168.1.0` (para subred `192.168.1.0/24`)                 | `11000000.10101000.00000001.00000000`                                         |
| **Dirección de Broadcast** | Última dirección de la subred, donde todos los bits de host son 1.                  | `192.168.1.255` (para subred `192.168.1.0/24`)               | `11000000.10101000.00000001.11111111`                                         |
| **Rango de Hosts Útiles**  | Rango de direcciones entre la dirección de red y la de broadcast, excluyendo ambas. | `192.168.1.1 - 192.168.1.254` (para subred `192.168.1.0/24`) | `11000000.10101000.00000001.00000001` - `11000000.10101000.00000001.11111110` |
