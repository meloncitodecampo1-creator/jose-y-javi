# Registro de Cambios y Colaboración (Pico 4 WebXR)

Este documento recopila la evolución del proyecto, los pasos técnicos dados y la comunicación entre el usuario y la IA Antigravity.

---

## 📅 2026-02-01 | Sesión Inicial: Planificación e Implementación Base

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen de la Conversación
1.  **Solicitud**: El usuario desea crear una aplicación WebXR para Pico 4 con A-Frame, incluyendo passthrough (cámara), seguimiento de mandos y una escena blanca con una caja central.
2.  **Planificación**: Se generó un plan de implementación y una guía de configuración para VS Code.
3.  **Implementación**: Se creó el archivo `index.html` con toda la lógica necesaria.
4.  **Solicitud de Git**: El usuario pidió añadir todos los archivos al repositorio en el commit inicial.
5.  **Solicitud de Seguimiento**: El usuario pidió este archivo de log para centralizar la información de los cambios y quién los hace.

#### 🛠️ Pasos Técnicos Realizados
1.  **Análisis de Requisitos**: Investigación de las capacidades de A-Frame 1.5.0 para Pico 4 (Passthrough mediante fondo transparente en modo AR).
2.  **Creación de Documentación**: 
    *   `setup_instructions.md`: Guía para Live Server e IPs.
3.  **Desarrollo de Software**:
    *   `index.html`: Boilerplate de A-Frame con entidades `pico-controls`, `laser-controls` y lógica de cambio de visibilidad para AR/VR.
4.  **Gestión de Repositorio**:
    *   `git init` en el directorio del proyecto.
    *   `git add .` (Añadiendo `index.html`, `setup_instructions.md` y archivos de soporte).
    *   `git commit -m "Initial commit: Pico 4 WebXR project setup with passthrough and controllers"`
5.  **Creación del Log**: Se inicializó este archivo (`LOG_CAMBIOS.md`).

6. **Servidor Local**: Se ha detectado la IP local (`192.168.18.79`) y se ha lanzado un servidor en el puerto 5500 accesible para las Pico 4.

---

## 📅 2026-02-01 | Sesión: Lanzamiento de Servidor

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Lanzar el archivo en un servidor local para conectar las Pico 4.
- **Acción**: Identificación de IP local y ejecución de `http-server`.

---

## 📅 2026-02-01 | Sesión: Mejora de Interfaz (Botones XR)

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Añadir un botón para entrar en VR/AR ya que el predeterminado de A-Frame no funcionaba correctamente o no era accesible.
- **Acción**: 
    *   Se añadió un contenedor `custom-ui` con estilos CSS.
    *   Se implementaron dos botones: "Entrar en VR" y "Entrar en AR (Passthrough)".
    *   Se añadieron funciones JavaScript para llamar a `sceneEl.enterVR()`.
    *   Se desactivó `xr-mode-ui` integrado de A-Frame para evitar duplicidad.

---

## 📅 2026-02-01 | Sesión: Resolución de Problemas de WebXR e HTTPS

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Problema**: El modo VR/AR no se activaba al pulsar los botones en las Pico 4.
- **Causa**: WebXR requiere un "Secure Context" (HTTPS) para funcionar en redes locales.
- **Acción**: 
    *   Se identificó la necesidad de configurar `chrome://flags` en las gafas o usar un túnel HTTPS (ngrok).
    *   Se prepararon instrucciones de portabilidad para replicar el entorno en otros equipos.

---

## 🚀 Instrucciones para Ejecución en Otro Equipo

Para que este proyecto funcione en un nuevo ordenador y sea visible en las Pico 4, sigue estos pasos:

### 1. Requisitos Previos
*   Instalar **Node.js** (incluye `npm`).
*   Tener el código del proyecto en una carpeta.

### 2. Lanzar el Servidor
En una terminal dentro de la carpeta del proyecto, ejecuta:
```bash
npx http-server -p 5500 -a 0.0.0.0
```
*(Si hay errores de permisos en Windows, usa el script de Node.js rápido que creamos en la sesión anterior).*

### 3. Configuración de Red e IP
1.  Averigua la IP local del nuevo PC (ej: `ipconfig` en Windows).
2.  Asegúrate de que las Pico 4 estén en la misma red Wi-Fi.

### 4. Habilitar WebXR (Crucial)
Como el servidor es `http` (no seguro), debes habilitar la excepción en las Pico 4:
1.  En el navegador de las gafas, entra en: `chrome://flags`.
2.  Busca **"Insecure origins treated as secure"**.
3.  Añade la dirección del PC: `http://[IP-DEL-PC]:5500`.
4.  Cambia a **"Enabled"** y reinicia el navegador.

---

## 📅 2026-02-01 | Sesión: Configuración de Entorno Profesionall (Node, Ngrok, HTTPS)

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Instalar Node.js, Python e implementar seguridad HTTPS para las Pico 4.
- **Acción**: 
    *   Se verificó la instalación de **Python 3.14.2**.
    *   Se instaló **Node.js LTS (v24.13.0)** mediante `winget`.
    *   Se instaló **Ngrok** mediante `winget`.
    *   Se inició un servidor local usando Python en el puerto 5500.
    *   Se configuró un túnel HTTPS (localtunnel/ngrok) para permitir el acceso seguro desde las Pico 4 sin necesidad de modificar flags de seguridad.

---

## 🚀 Direcciones de Acceso (Pico Browser)

1.  **Directo (HTTP)**: `http://192.168.18.22:5500` (Requiere `chrome://flags` si no hay HTTPS).
2.  **Seguro (HTTPS)**: `https://fast-wombats-see.loca.lt`
    *   **IMPORTANTE**: Asegúrate de escribir `https://` (con la 's') al principio. Si entras solo con `http://`, las Pico 4 bloquearán el modo VR por seguridad.
    *   **Password**: `217.29.105.27` (si te la vuelve a pedir).

---

## 📅 2026-02-01 | Sesión: Implementación de Manos y Hand Tracking

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Mostrar modelos de manos en lugar de solo los rayos de los mandos.
- **Acción**: 
    *   Se actualizaron las entidades de control para incluir `hand-controls`.
    *   Se configuró el estilo `highPoly` para obtener modelos de manos detallados.
    *   Se añadió soporte para `hand-tracking-controls`, permitiendo que las manos se muevan incluso sin mandos (si las Pico 4 tienen activado el seguimiento de manos).

---

## 📅 2026-02-01 | Sesión: Física e Interacción de Objetos

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Crear una mesa con objetos que el jugador pueda agarrar con las manos.
- **Acción**: 
    *   Se integraron las librerías `aframe-extras` y `super-hands` para habilitar colisiones y físicas.
    *   Se diseñó una **mesa** con materiales de madera (visual).
    *   Se crearon tres objetos interactuables: una **esfera roja**, un **cubo azul** y un **cilindro amarillo**.
    *   Se configuraron los controladores con `sphere-collider` y `super-hands` para permitir el agarre (squeeze/grab).

---

## 📅 2026-02-01 | Sesión: Locomoción y Diseño de Habitación

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Permitir el movimiento por la escena usando el joystick izquierdo y crear una habitación con paredes color marrón claro.
- **Acción**: 
    *   Se implementó un **rig de cámara** con el componente `movement-controls`.
    *   Se configuró el **joystick izquierdo** del mando Pico para permitir el movimiento suave.
    *   Se diseñó una habitación con **paredes color Tan (#DEB887)** y suelo marrón claro.
    *   Se ajustó la lógica de visibilidad para que tanto la mesa como las nuevas paredes se oculten al entrar en modo AR (Passthrough).

---

## 📅 2026-02-01 | Sesión: Física Aplicada y Lanzamientos

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Añadir gravedad a los objetos y la mesa, permitir golpearlos y lanzarlos al soltar el gatillo.
- **Acción**: 
    *   Se implementó el sistema de físicas **Cannon.js**.
    *   Se activó `dynamic-body` en la esfera, cubo y cilindro, permitiendo que caigan y rueden.
    *   Se configuró el suelo, paredes y mesa como `static-body` para servir de obstáculos físicos.
    *   Se añadieron colisiones físicas a las manos para poder **golpear** los objetos.
    *   Se configuró el lanzamiento con inercia: al soltar el gatillo mientras se mueve la mano, el objeto sale disparado con la velocidad del movimiento.

---

## 📅 2026-02-01 | Sesión: Resolución de Errores de Seguridad (CSP)

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Problema**: El navegador de las Pico 4 bloqueaba la ejecución de scripts debido a políticas de seguridad (CSP), impidiendo que la escena pasara de los "puntos de carga".
- **Acción**: 
    *   Se implementó una etiqueta `<meta>` de **Content-Security-Policy** específica.
    *   Se concedieron permisos para `'unsafe-eval'` y `'unsafe-inline'`, necesarios para que A-Frame y sus componentes de interacción funcionen correctamente.
    *   Se autorizaron los dominios de confianza para scripts y conexiones de red.

---

## 📅 2026-02-01 | Sesión: Certificado HTTPS Local (mkcert)

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Problema**: Los túneles públicos (localtunnel) daban problemas de CSP y carga lenta.
- **Acción**: 
    *   Se instaló **mkcert** y se generó un certificado SSL local para la IP del PC.
    *   Se inició un servidor HTTPS local seguro en el puerto 5500.
    *   Esto permite una conexión directa, rápida y segura entre las Pico 4 y el PC.

---

## 🚀 Direcciones de Acceso (Pico Browser)

1.  **Seguro Local (HTTPS)**: `https://192.168.18.22:5500`

---

## 📅 2026-02-01 | Sesión: Limpieza Profunda y Restauración de Carga

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Problema**: El navegador de las Pico 4 se quedaba bloqueado en "puntos de carga" infinitos al usar HTTPS local o túneles.
- **Acción**: 
    *   **Reescritura Total**: Se ha reescrito el `index.html` desde cero eliminando cualquier código redundante o pesado.
    *   **Eliminación de CSP**: Se ha retirado la etiqueta de seguridad CSP que podía estar causando bloqueos en el navegador de las gafas.
    *   **Optimización de Librerías**: Se han mantenido solo las versiones más estables de A-Frame y Super-Hands.
    *   **Físicas en Pausa**: Se ha desactivado temporalmente el motor de físicas Cannon.js por ser el sospechoso principal de los cuelgues en el procesador de las Pico 4.

---

## 🚀 Dirección de Acceso Recomendada
**`https://192.168.18.22:5500`**
*   **Nota**: Refresca la caché del navegador de las gafas si el problema persiste.

---

## 📅 2026-02-01 | Sesión: Activación Final de Físicas y Colisiones

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Problema**: Tras la limpieza de código, los objetos y manos habían perdido sus propiedades físicas (gravedad, colisión y agarre avanzado).
- **Acción**: 
    *   **Reactivación de Motor**: Se ha vuelto a integrar `aframe-physics-system`.
    *   **Configuración de Manos**: Se han añadido cuerpos estáticos (`static-body`) a las manos para que puedan interactuar físicamente con los objetos.
    *   **Física en Objetos**: Se ha aplicado el mixin `objeto-fisico` con `dynamic-body` a la esfera, el cubo y el cilindro.
    *   **Suelo y Mesa Sólidos**: Se ha verificado que tanto el suelo como el tablero de la mesa tengan `static-body` para que los objetos no los atraviesen al caer.

---

## 🚀 Dirección de Acceso
**`https://192.168.18.22:5500`**

---

## 📅 2026-02-01 | Sesión: Refinamiento de Mesa y Controles de Gatillo

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Añadir las cuatro patas a la mesa y configurar el gatillo (trigger) como único botón de agarre y lanzamiento.
- **Acción**: 
    *   **Carpintería Virtual**: Se han añadido las dos patas faltantes a la mesa para completar un total de cuatro.
    *   **Mapeo de Controles**: Se ha configurado `super-hands` para que el agarre se active exclusivamente con el **gatillo (trigger)**.
    *   **Física de Lanzamiento**: Al soltar el gatillo mientras se realiza un movimiento, el sistema transfiere de forma natural la inercia al objeto, permitiendo lanzamientos realistas.

---

## 🚀 Dirección de Acceso
**`https://192.168.18.22:5500`**

---

## 📅 2026-02-01 | Sesión: Feedback Visual de Agarre (Brillo Verde)

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Hacer que el objeto cambie de color cuando está agarrado para saber que la interacción funciona.
- **Acción**: 
    *   **Brillo de Agarre**: Se ha configurado un sistema de **emisión de luz (brillo verde)** que se activa solo cuando el objeto está agarrado por la mano.
    *   **Mantenimiento de Color**: El objeto mantiene su color original (rojo, azul o amarillo) pero emite un resplandor verde lima cuando el gatillo lo sujeta con éxito.
    *   **Refuerzo de Colisiones**: Se han añadido esferas de colisión invisibles a las manos para asegurar que el contacto con los objetos sea más preciso y consistente.

---

## 🚀 Dirección de Acceso
**`https://192.168.18.22:5500`**

---

## 📅 2026-02-01 | Sesión: Sistema de Depuración de Mandos (Debugger)

### 👤 Usuario Git: `javibelloso`

#### 💬 Resumen
- **Solicitud**: Identificar qué botón se usa para agarrar y mostrar un debugger en pantalla que indique qué botones se están pulsando.
- **Acción**: 
    *   **Panel de Depuración**: Se ha creado un panel flotante en la esquina inferior derecha que muestra en tiempo real la mano y el botón detectado.
    *   **Identificación del Gatillo**: Se ha confirmado que el botón de agarre es el **Gatillo (Trigger)**, el botón trasero del mando.
    *   **Eventos de Mando**: Se han programado "escuchadores" para:
        *   Gatillo (Trigger)
        *   Botón lateral (Grip)
        *   Botones frontales (A/B y X/Y)
    *   **Feedback de Estado**: El debugger indica explícitamente cuando el gatillo está en estado "Agarrando" o "Lanzando".

---

## 🚀 Dirección de Acceso
**`https://192.168.18.22:5500`**

---

## 📈 Próximos Pasos Sugeridos
- [ ] Mostrar el nivel de presión del gatillo si el hardware lo permite.
- [ ] Añadir una representación visual del mando en el aire con los botones resaltados.
- [ ] Implementar un historial de los últimos 5 botones pulsados.
