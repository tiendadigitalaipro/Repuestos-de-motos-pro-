# 📁 ESTRUCTURA — Repuestos de Motos Pro

Mapa completo de archivos y secciones de código.

---

## 🗂️ Archivos

| Archivo | Líneas | Descripción |
|---|---|---|
| `index.html` | — | Punto de entrada. Redirige automáticamente a `repuestos-motos-pro.html` |
| `repuestos-motos-pro.html` | ~1957 | App principal (CSS + HTML + JS en un solo archivo) |
| `admin-licencias.html` | ~330 | Panel de administración de licencias |

---

## 📐 repuestos-motos-pro.html — Mapa General

| Bloque | Líneas | Tamaño aprox. |
|---|---|---|
| **CSS** | 10–218 | ~209 líneas |
| **HTML** | ~219–700 | ~482 líneas |
| **JavaScript** | ~701–1957 | ~1257 líneas |

---

## 🎨 CSS (Líneas 10–218)

| Líneas | Sección |
|---|---|
| 1–9 | Meta tags, título |
| **11** | **Variables CSS** (colores, fuentes, spacing) |
| 12–218 | Estilos generales, componentes, tarjetas, tablas, modales |

---

## 🏗️ HTML (Líneas ~219–700)

| Sección | Módulo |
|---|---|
| Dashboard | Resumen general con gráfico canvas |
| POS | Punto de venta |
| Inventario | Control de productos y stock |
| Clientes | Base de datos de clientes |
| Ventas | Historial de ventas |
| Caja | Arqueo de caja |
| Reportes | Estadísticas |
| Marcas/Modelos | Gestión de marcas de motos |
| Config | Configuración general |
| Modales | Diálogos y formularios |

---

## ⚙️ JavaScript (Líneas ~701–1957)

| Líneas | Sección |
|---|---|
| **702–707** | **DB helper** — Función de acceso a localStorage |
| **709** | **Config por defecto** (`tasa: 50.00`, nombre del negocio, etc.) |
| 710–733 | Utilidades y funciones auxiliares |
| **734** | **Categorías de productos** (10 categorías) |
| **737–746** | **Métodos de pago** (8 métodos) |
| 747–752 | Funciones de inicialización |
| **753–786** | **Base de datos de marcas** — `MARCAS_MOTOS` (29 marcas) |
| 787–789 | Polyfill `roundRect` |
| **790–989** | **Sistema de licencias IRON LOCK** |
| 990–1200 | Lógica POS y búsqueda de productos |
| **1203** | **`selMetodo()`** — Selección de método de pago (pago mixto) |
| 1204–1400 | Carrito, checkout y procesamiento de ventas |
| 1401–1550 | Inventario y Clientes CRUD |
| 1551–1695 | Ventas, Caja y Reportes |
| **1696** | **`drawChart()`** — Gráfico canvas personalizado |
| 1697–1800 | Funciones de renderizado y eventos |
| **1801–1836** | **Export/Import de datos** (JSON) |
| **1792** | **Función de reseteo** — Borrar todos los datos |
| **1837–1937** | **Datos de ejemplo** (62 productos + 3 clientes) |
| 1938–1957 | Event listeners y configuración final |

---

## 🔧 admin-licencias.html — Mapa (~330 líneas)

| Líneas | Sección |
|---|---|
| 1–150 | HTML y estilos del panel admin |
| 151–250 | Lógica de validación y autenticación |
| 251–330 | Gestión de licencias y funciones CRUD |

---

## 🏍️ Marcas de Motos (29 marcas)

Definidas en `MARCAS_MOTOS` — **Líneas 753–786**:

Honda, Yamaha, Kawasaki, Suzuki, Bajaj, Akt, Hero, TVS, Zanella, Corven, Motomel, Gilera, Piaggio, Vespa, Kymco, Triumph, Ducati, BMW, Harley-Davidson, KTM, Husqvarna, Royal Enfield, Benelli, SYM, Hyosung, Lifan, Bashan, Zontes, Other

---

## 📦 Categorías de Productos (10 categorías)

Definidas en **Línea 734**:

Aceites, Filtros, Baterías, Llantas, Frenos, Cadena/Transmisión, Electricidad, Carrocería, Suspensión, Otros

---

## 🗄️ Claves localStorage

| Prefijo | Clave | Descripción |
|---|---|---|
| `rmp_` | `rmp_config` | Configuración general |
| `rmp_` | `rmp_productos` | Inventario de productos |
| `rmp_` | `rmp_clientes` | Base de datos de clientes |
| `rmp_` | `rmp_ventas` | Historial de ventas |
| `rmp_` | `rmp_caja` | Estado de caja |
| `rmp_` | `rmp_licencia_activa` | Estado de licencia |

> Para resetear toda la app: `localStorage.clear()` en consola del navegador.
