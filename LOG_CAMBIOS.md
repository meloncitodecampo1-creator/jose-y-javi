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

## 📈 Próximos Pasos Sugeridos
- [ ] Implementar la capacidad de "agarrar" la caja con las manos.
- [ ] Cambiar el color de las manos dinámicamente.
- [ ] Añadir sonidos al interactuar.
