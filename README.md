#  Simulador de Capas del Modelo OSI

Aplicación de escritorio desarrollada con **Python + Tkinter** que visualiza en tiempo real el proceso de transmisión de datos a través de las **7 capas del Modelo OSI**, simulando el flujo completo entre un Emisor y un Receptor con métricas de teoría de colas (M/M/1).

> Proyecto académico — Universidad Estatal de Milagro (UNEMI), Facultad de Ciencias e Ingeniería · 2026

---

##  Características principales

- **Visualización animada** capa por capa (C7 → C1 en el Emisor, C1 → C7 en el Receptor)
- **Codificación Base64** simulada en la Capa de Presentación (C6) y decodificación automática en el receptor
- **Métricas M/M/1** (tiempo de espera en cola `Wq`) generadas aleatoriamente por capa
- **PDUs** correctos por capa: Datos, Datos cifrados, SPDU, Segmento, Paquete, Trama, Bits
- **Canal físico** con indicador animado entre emisor y receptor
- **Barra de progreso** con estado en tiempo real
- **Consolas independientes** para Emisor (verde) y Receptor (azul)
- **Tema claro / oscuro** intercambiable con un solo botón
- **Botón RESET** para limpiar y reutilizar la simulación

---

##  Arquitectura — Capas OSI simuladas

| Capa | Nombre        | Abrev. | PDU generada     |
|------|---------------|--------|------------------|
| 7    | Aplicación    | APL    | Datos            |
| 6    | Presentación  | PRE    | Datos cifrados   |
| 5    | Sesión        | SES    | SPDU             |
| 4    | Transporte    | TRA    | Segmento         |
| 3    | Red           | RED    | Paquete          |
| 2    | Enlace        | ENL    | Trama            |
| 1    | Física        | FIS    | Bits             |

> **Nota técnica:** El Emisor procesa las capas de C7 a C1 (encapsulación). El Receptor las procesa de C1 a C7 (desencapsulación).

---

##  Requisitos

- **Python 3.8** o superior
- **Tkinter** (incluido por defecto en la mayoría de instalaciones de Python)

### Verificar instalación de Tkinter

```bash
python -m tkinter
```

Si se abre una ventana de prueba, Tkinter está disponible.

### Instalación de Tkinter (si no está disponible)

**Ubuntu / Debian:**
```bash
sudo apt-get install python3-tk
```

**Fedora / RHEL:**
```bash
sudo dnf install python3-tkinter
```

**Windows / macOS:** Tkinter viene incluido con el instalador oficial de Python desde [python.org](https://www.python.org).

---

## Ejecución

```bash
python Simulador_de_capas_modelo_OSI.py
```

---

##  Cómo usar el simulador

1. **Escribe un mensaje** en el campo de texto (ej: `Hola Mundo`).
2. Haz clic en **ENVIAR**.
3. Observa cómo cada capa del **Emisor** se activa secuencialmente (amarillo → verde).
4. El mensaje cruza el **canal físico** (flecha central).
5. Las capas del **Receptor** se activan en orden inverso hasta reconstruir el mensaje original.
6. Al finalizar, la consola del receptor muestra `TRANSMISIÓN EXITOSA` con el mensaje recuperado.
7. Usa **RESET** para limpiar la simulación y enviar un nuevo mensaje.
8. Usa **TEMA** para alternar entre modo oscuro y modo claro.

---

## Estructura del proyecto

```
Simulador_de_capas_modelo_OSI.py   # Archivo principal — toda la lógica y UI
README.md                           # Este archivo
```

---

##  Detalles técnicos

### Codificación en Capa de Presentación
La Capa 6 (Presentación) aplica codificación **Base64** al mensaje del usuario durante la encapsulación, y la Capa 6 del receptor realiza la decodificación inversa, devolviendo el mensaje original.

### Modelo de colas M/M/1
Cada capa genera un tiempo de espera `Wq` mediante distribución exponencial (`expovariate`) en el Emisor y distribución uniforme en el Receptor, simulando latencia de procesamiento en cada nivel de la pila.

### Encabezados y trailers
- El **Emisor** agrega un *header* aleatorio (`H<capa>_<número>`) en cada capa.
- El **Receptor** agrega un *trailer* aleatorio (`T<capa>_<número>`) al desencapsular.

### Animación
La interfaz usa `root.after()` con retardos de 180 ms por paso y 900 ms en el canal para crear la animación sin bloquear el hilo principal de Tkinter.

---

##  Temas visuales

| Tema   | Fondo        | Consola Emisor | Consola Receptor |
|--------|-------------|----------------|-----------------|
| Oscuro | `#121212`   | Verde `#10b981`| Azul `#38bdf8`  |
| Claro  | `#f8fafc`   | Verde `#059669`| Azul `#0284c7`  |

---

##  Conceptos aplicados

- Modelo de referencia OSI (ISO/IEC 7498-1)
- Encapsulación y desencapsulación de datos
- Unidades de datos de protocolo (PDU)
- Teoría de colas: modelo M/M/1
- Codificación Base64 (RFC 4648)
- Programación orientada a objetos en Python
- Interfaces gráficas con Tkinter

---

##  Autor

Desarrollado como proyecto académico para la asignatura de **Ccomunicación de datos** — UNEMI 2026.

---

## Licencia

Uso académico. Libre para modificar y distribuir con fines educativos.
