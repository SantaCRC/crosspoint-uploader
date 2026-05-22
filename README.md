CrossPoint Uploader
===================

Simple WebSocket file uploader (front-end demo).

Resumen
- Interfaz: `crosspoint-uploader.html` (HTML + vanilla JS + Tailwind).
- Protocolo: envía `START:<filename>:<size>:<path>` por WebSocket, luego frames binarios con progreso y mensajes `PROGRESS`/`DONE`.
- Creación de carpetas: antes de `START` el cliente intenta crear carpetas en el dispositivo con `POST /mkdir` (form-urlencoded: `name`, `path`). Si el POST falla por CORS/red, el cliente continúa en modo "best-effort".
- Rendimiento: chunks por defecto `1024` bytes con `8ms` de pausa para estabilidad.

Cómo usar (local)
1. Servir los ficheros desde un servidor HTTP para evitar restricciones de origen (recomendado):

```bash
cd /ruta/al/proyecto
python3 -m http.server 8080
# luego abrir http://localhost:8080/crosspoint-uploader.html
```

2. Ajustar `WebSocket URL` y `Target path` en la UI.
3. Seleccionar un archivo y pulsar *Upload file*.

Notas
- El cliente validará que el nombre no contenga `:` antes de enviar `START`.
- Si el dispositivo destino no expone `/mkdir`, la subida aún se intenta (fallback).
- Para pruebas automatizadas o CLI existe `validate_ws_upload.sh` (si está presente) — úsalo en el host que pueda abrir WebSocket al dispositivo.

Autor
- SantaCRC

License
- MIT (usa y modifica libremente).