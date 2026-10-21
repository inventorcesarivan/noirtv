# NOIR IPTV — edición cine + probador M3U

Reproductor web estático con interfaz oscura inspirada en plataformas de streaming.

## Funciones
- Barra superior fija con Menú principal y categorías TV, Radio, Películas, Series y Juegos.
- Biblioteca con portadas grandes; el reproductor solo se abre al seleccionar un contenido.
- Fuentes M3U/M3U8 locales o remotas, URL directa y soporte Xtream Codes inicial.
- Fuentes guardadas localmente en el navegador.
- Probador de listas M3U: carga de archivo o URL, prueba HTTP de cada enlace, clasificación como disponible/fallido/inconcluso, cancelación, revisión y descarga de una lista depurada.
- Posibilidad de guardar los canales disponibles como una nueva fuente local.
- HLS.js y diagnóstico de errores de reproducción.

## Uso
1. Extraé el ZIP.
2. Abrí `index.html` en un navegador moderno o publicalo en un hosting estático.
3. Abrí **Menú principal** para agregar fuentes, importar una lista, administrar fuentes o abrir el probador M3U.
4. Para probar una lista, elegí un archivo `.m3u`/`.m3u8` o pegá una URL y pulsá **Analizar lista**. Al finalizar, descargá la lista limpia.

## Limitaciones importantes del probador
- El probador usa solicitudes HTTP desde el navegador. CORS, autenticación, URLs temporales, restricciones por IP, solicitudes especiales o servidores que rechazan `Range` pueden producir resultados **inconclusos**.
- Un enlace HTTP que responde no garantiza que el vídeo se reproduzca, y un error CORS no significa que el canal esté caído.
- Por seguridad, la exportación excluye únicamente enlaces marcados como fallidos; conserva los inconclusos para evitar eliminar canales que podrían funcionar. Revisá los resultados antes de usar la lista.
- Para comprobar listas masivas con fiabilidad real, hace falta un backend de análisis autorizado; una página estática no puede eludir CORS.
- La aplicación no distribuye canales ni listas. Utilizá únicamente fuentes y transmisiones para las que tengas autorización.

## Privacidad
Las fuentes se guardan en `localStorage` del navegador y no están cifradas. No guardes credenciales en equipos compartidos. No subas listas privadas ni credenciales al repositorio.

## Publicación
Se puede publicar `index.html` en Netlify o un hosting estático. HLS.js se carga desde CDN, por lo que se requiere conexión a Internet para esa biblioteca.

## Organizador de bibliotecas (nuevo)
- Desde **Menú principal → Organizador de bibliotecas** podés seleccionar varias fuentes M3U, combinarlas o exportarlas a un solo archivo.
- La combinación clasifica automáticamente en TV, Radio, Películas y Series, con subsecciones por país, idioma o temática cuando hay datos suficientes.
- Se eliminan solo URLs exactamente repetidas; las entradas con URLs distintas se conservan aunque tengan nombres parecidos.
- Las fuentes originales permanecen separadas. La combinación guardada aparece como una nueva fuente independiente.
- Después de cargar una fuente, las subsecciones aparecen como filtros debajo de las categorías principales.
- Las listas remotas necesitan que el servidor permita la lectura desde el navegador (CORS). Si una fuente no se puede leer, el organizador informa el error.
- Las bibliotecas grandes pueden superar la cuota de almacenamiento local del navegador. En esos casos, la descarga M3U es la opción más fiable; no compartas listas que incluyan URLs privadas o credenciales.


## Mejoras de conexión Xtream Codes (v2)
- Normaliza direcciones base y evita duplicar `/player_api.php` si se pegó la ruta completa.
- Muestra detalles HTTP disponibles y distingue fallos de conexión/CORS de respuestas HTTP.
- No puede saltarse CORS ni autenticación del proveedor desde una web estática. Algunos servidores requieren un backend autorizado o no exponen una API Xtream estándar.
