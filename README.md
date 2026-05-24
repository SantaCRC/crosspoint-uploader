CrossPoint Uploader
===================

Simple WebSocket file uploader (front-end demo).

[![pages-build-deployment](https://github.com/SantaCRC/crosspoint-uploader/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/SantaCRC/crosspoint-uploader/actions/workflows/pages/pages-build-deployment)

Resumen
- Interfaz: `crosspoint-uploader.html` (HTML + vanilla JS + Tailwind).
- Protocolo: envía `START:<filename>:<size>:<path>` por WebSocket, luego frames binarios con progreso y mensajes `PROGRESS`/`DONE`.
- Creación de carpetas: antes de `START` el cliente intenta crear carpetas en el dispositivo con `POST /mkdir` (form-urlencoded: `name`, `path`). Si el POST falla por CORS/red, el cliente continúa en modo "best-effort".
- Rendimiento: chunks por defecto `1024` bytes con `8ms` de pausa para estabilidad.


Notas
- El cliente validará que el nombre no contenga `:` antes de enviar `START`.
- Si el dispositivo destino no expone `/mkdir`, la subida aún se intenta (fallback)