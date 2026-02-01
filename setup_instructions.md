# Configuración del IDE para WebXR (Pico 4)

Para trabajar de manera eficiente en este proyecto de Realidad Virtual, te recomiendo instalar y configurar lo siguiente en tu VS Code (Antigravity):

## 1. Extensiones Recomendadas

*   **Live Server (Ritwick Dey)**: Esta es la herramienta más importante. Permite lanzar un servidor local con un clic. Necesitarás esto para que tus gafas Pico 4 puedan acceder a la web que estás programando.
*   **GLTF Tools**: Útil si decides importar modelos 3D más adelante, ya que permite previsualizarlos dentro de VS Code.
*   **A-Frame Snippets**: Opcional, pero ayuda a escribir código de A-Frame más rápido.

## 2. Configuración de Red para Pico 4

Para que las gafas vean tu trabajo:
1.  Asegúrate de que tu PC y las Pico 4 estén en la **misma red Wi-Fi**.
2.  Inicia **Live Server** en VS Code (botón "Go Live" en la barra inferior).
3.  Anota la IP de tu ordenador (en Windows: abre terminal y escribe `ipconfig`, busca "IPv4 Address", suele ser algo como `192.168.1.XX`).
4.  En el navegador de las Pico 4, escribe: `http://TU_IP:5500`.

## 3. Navegador en Pico 4

*   Usa el **Pico Browser** integrado.
*   Si tienes problemas de seguridad (HTTPS), puedes entrar en `chrome://flags` dentro del navegador de las gafas y buscar "unsafely-treat-insecure-origin-as-secure", añadiendo tu IP y puerto.

---

Una vez tengas esto, estaremos listos para crear el archivo `index.html`.
