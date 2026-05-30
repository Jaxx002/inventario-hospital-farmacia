# Inventario Farmacéutico — Hospital de la Mujer

Sistema de control de inventario para el área de farmacia hospitalaria. Aplicación web de un solo archivo, sin servidor ni base de datos externa: corre directamente en el navegador con almacenamiento local (IndexedDB).

---

## Capturas de pantalla

> _Puedes agregar imágenes aquí con `![descripción](ruta-a-imagen.png)` una vez que captures la interfaz._

---

## Características

- **Panel de control** — métricas en tiempo real: total de medicamentos, stock bajo mínimo, movimientos del día, alertas activas.
- **Almacén** — catálogo completo con búsqueda por clave/nombre/lote, filtros por categoría y estado de stock, barras de nivel visual.
- **Entradas / Salidas / Ajustes** — registro de movimientos con número de lote, fecha de caducidad, área destino y responsable.
- **Bitácora** — historial completo de transacciones con filtros por tipo.
- **Reportes Excel** — 5 plantillas descargables directamente desde el navegador (SheetJS):
  - Stock actual completo
  - Escasos y agotados
  - Próximos a caducar (≤ 90 días)
  - Bitácora de movimientos
  - Consumo por área · últimos 30 días
- **Gestión de áreas** — alta y baja de servicios/departamentos del hospital.
- **Modo compacto** — densidad de tabla ajustable (cómodo / compacto).
- **100 % offline** — todos los datos se guardan en IndexedDB del navegador; no requiere conexión a internet después de la primera carga de los CDN.

---

## Tecnologías

| Capa | Tecnología |
|------|-----------|
| UI | React 18 (CDN, sin build) |
| Estilos | CSS variables + estilos en línea |
| Base de datos | IndexedDB vía [Dexie.js](https://dexie.org/) |
| Exportación | [SheetJS (xlsx)](https://sheetjs.com/) |
| Transpilación JSX | Babel Standalone (CDN) |
| Tipografías | Google Fonts — Geist, Instrument Serif, JetBrains Mono |

No hay `package.json`, bundler ni proceso de build. Todo cabe en un único archivo HTML.

---

## Instalación y uso

1. **Descarga o clona el repositorio:**
   ```bash
   git clone https://github.com/<tu-usuario>/inventario-hospital-farmacia.git
   ```

2. **Abre el archivo en el navegador:**
   ```
   inventario Hospital_farmacia/Panel Inventario.html
   ```
   — o arrastra el archivo directamente a Chrome, Edge o Firefox.

3. Listo. No necesitas instalar nada más.

> **Nota:** Se recomienda usar **Google Chrome** o **Microsoft Edge** para mejor compatibilidad con IndexedDB y la descarga de archivos Excel.

---

## Estructura del archivo principal

`Panel Inventario.html` está organizado en secciones claramente delimitadas:

```
§1  Base de datos (Dexie / IndexedDB)
§2  Componentes UI compartidos (iconos SVG, badges, botones, modal, toast)
§3  Pantalla Panel (dashboard)
§4  Pantalla Almacén (catálogo y tabla)
§5  Pantalla Movimientos (bitácora)
§6  Pantalla Reportes
§7  Generación de Excel (SheetJS)
§8  Shell de la app (sidebar, topbar, estado global)
§9  Modales (Entrada, Salida, Detalle, Gestión de meds, Gestión de áreas)
§10 Bootstrap (ReactDOM.render)
```

---

## Modelo de datos

```
medicamentos  — sku (PK), nombre, presentacion, categoria, ubicacion,
                stock, minimo, lote, caducidad

movimientos   — id (auto), tipo, sku, cantidad, area, usuario,
                timestamp, nota

areas         — id (auto), nombre (unique)

config        — clave, valor  (p. ej. "initialized": true)
```

---

## Limitaciones conocidas

- Los datos viven **solo en el navegador** donde se registraron. Si se borra el almacenamiento del navegador, se pierden.
- No tiene autenticación de usuario; cualquier persona que abra el archivo tiene acceso total.
- No es multi-usuario en tiempo real.

---

## Posibles mejoras futuras

- Autenticación y roles (farmacéutico / jefe de farmacia / auditor)
- Sincronización en la nube (Firebase / Supabase) para respaldo
- Exportación a PDF
- Notificaciones de caducidad próxima por correo

---

## Licencia

Distribuido bajo la licencia [MIT](LICENSE).

---

## Autor

Desarrollado para el área de Farmacia — Hospital de la Mujer.  
Mantenido por [@juega](https://github.com/juega).
