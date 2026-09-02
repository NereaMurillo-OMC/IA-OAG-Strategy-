# Conectar la encuesta a tu Google Sheet

No puedo entrar en tu Drive, así que la hoja la creas tú una vez y la encuesta le escribe sola a partir de ahí.

## 1. Crea la hoja
En tu Drive personal, hoja nueva. En la fila 1 pon estas cabeceras:

`fecha | equipo | interes | casos | t1 | t2 | t3 | t4 | necesidades`

## 2. Pega el script
En la hoja: **Extensiones → Apps Script**. Borra lo que haya, pega esto y guarda:

```js
function doPost(e) {
  var hoja = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
  var d = JSON.parse(e.postData.contents);
  hoja.appendRow([d.fecha, d.equipo, d.interes, d.casos, d.t1, d.t2, d.t3, d.t4, d.necesidades]);
  return ContentService.createTextOutput("ok");
}
```

## 3. Publica el Web App
**Implementar → Nueva implementación → Aplicación web**
- Ejecutar como: **yo mismo**
- Quién tiene acceso: **cualquier usuario**

Acepta los permisos y copia la URL que acaba en `/exec`.

## 4. Pega la URL en la encuesta
Tweaks de `Encuesta.dc.html` → **URL del Web App de Google Sheets**.

A partir de ahí, cada envío añade una fila a tu hoja. La copia local del navegador y la descarga en CSV (modo administrador) siguen funcionando como respaldo por si un envío falla.
