# 🔧 MANTENIMIENTO — Repuestos de Motos Pro

Guía rápida para modificaciones comunes. Todas las ediciones se realizan en `repuestos-motos-pro.html` salvo indicación contraria.

---

## 🎨 Cambiar Colores

**Archivo:** `repuestos-motos-pro.html` → **Línea 11** (CSS Variables)

```css
:root {
  --primary: # ...;   /* Color principal — cambiar aquí */
  --bg: # ...;        /* Fondo general */
  --text: # ...;      /* Color de texto */
  /* ... más variables */
}
```

> Modifica los valores para personalizar la paleta visual completa de la app.

---

## 💱 Cambiar Tasa de Cambio

**Opción 1 — Desde la app:** Ir a **Config** → Tasa de cambio.

**Opción 2 — Valor por defecto en código:**
`repuestos-motos-pro.html` → **Línea 709**

```javascript
const DEFAULT_CFG = {
  tasa: 50.00,  // 1 USD = 50 Bs — cambiar aquí
  nombre: 'Repuestos de Motos Pro',
  // ...
};
```

---

## 📦 Agregar Productos

**Opción 1 — Desde la app:** Módulo **Inventario** → Agregar producto.

**Opción 2 — En código (datos por defecto):**
`repuestos-motos-pro.html` → **Líneas 1837–1937**

```javascript
{
  id: 63,
  nombre: 'Nombre del Producto',
  marca: 'Honda',
  categoria: 'Filtros',
  precio: 15.00,
  stock: 10,
  codigo: 'FLT-001'
}
```

La función `renderInventario()` se encarga de mostrar los productos en la interfaz.

---

## 🏍️ Agregar Marcas de Motos

**Archivo:** `repuestos-motos-pro.html` → **Arreglo `MARCAS_MOTOS`** → **Líneas 753–786**

```javascript
const MARCAS_MOTOS = [
  'Honda', 'Yamaha', 'Kawasaki', 'Suzuki',
  // ... agregar nueva marca:
  'NuevaMarca',
  'OtraMarca',
];
```

---

## 🔑 Cambiar Contraseña de Admin

**Valor por defecto en código:**
`repuestos-motos-pro.html` → **Línea 709** (dentro de `DEFAULT_CFG`)

```javascript
adminPass: 'RMP2026ADMIN'  // Cambiar aquí
```

> ⚠️ Solo aplica si no hay configuración guardada en localStorage.

---

## 🔐 Cambiar Salt del Sistema de Licencias

**Archivo:** `repuestos-motos-pro.html` → **Línea 792**

```javascript
const SALT = 'RMPMOTOS2026';  // Cambiar aquí
```

> ⚠️ **Importante:** Cambiar el salt invalidará todas las licencias activas existentes.

---

## 📤 Exportar / Importar Datos

**Archivo:** `repuestos-motos-pro.html` → **Líneas 1801–1836**

### Exportar

La función de export genera un archivo JSON con todos los datos almacenados en localStorage.

### Importar

Permite cargar un archivo JSON previamente exportado para restaurar datos.

```javascript
// La exportación incluye:
// - Productos, Clientes, Ventas, Caja, Configuración
```

> Se accede desde **Config** → Exportar/Importar datos.

---

## 🔄 Resetear Todos los Datos

**Opción 1 — Desde la app:** Ir a **Config** → Resetear datos.

**Opción 2 — En código:**
`repuestos-motos-pro.html` → **Línea 1792** (función de reset)

**Opción 3 — Consola del navegador** (F12 → Console):

```javascript
localStorage.clear();
location.reload();
```

---

## 📊 Gráfico Canvas Personalizado

**Archivo:** `repuestos-motos-pro.html` → **Línea 1696** (función `drawChart()`)

La app utiliza la **Canvas API nativa** para renderizar gráficos, sin dependencias externas.

```javascript
function drawChart(canvas, data, options) {
  // Renderizado personalizado con Canvas 2D
  // Incluye polyfill para roundRect (líneas 787-789)
}
```

### Polyfill roundRect

Si el navegador no soporta `roundRect` nativo, la app incluye un polyfill personalizado en **líneas 787–789**.

---

## 💰 Pago Mixto

**Archivo:** `repuestos-motos-pro.html` → **Línea 1203** (función `selMetodo()`)

La función `selMetodo()` gestiona la selección de métodos de pago y soporta **pago mixto** (combinar múltiples métodos en una sola venta):

```javascript
function selMetodo(metodo) {
  // Gestiona la selección del método de pago
  // Soporta combinaciones de métodos
  // Actualiza el total pendiente automáticamente
}
```

---

## 📋 Resumen Rápido de Líneas Clave

| Tarea | Línea |
|---|---|
| Variables CSS | 11 |
| DB helper | 702–707 |
| Config por defecto (tasa, nombre, admin) | 709 |
| Categorías de productos | 734 |
| Métodos de pago | 737–746 |
| Marcas de motos | 753–786 |
| Polyfill roundRect | 787–789 |
| Salt de licencias | 792 |
| Sistema de licencias IRON LOCK | 790–989 |
| Pago mixto `selMetodo()` | 1203 |
| Gráfico canvas `drawChart()` | 1696 |
| Reset de datos | 1792 |
| Export/Import | 1801–1836 |
| Datos de ejemplo (62 productos) | 1837–1937 |
