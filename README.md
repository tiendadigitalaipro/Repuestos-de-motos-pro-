# 🏍️ Repuestos de Motos Pro

**App profesional para ventas e inventarios de repuestos de motos** — Dashboard, POS, inventario, clientes, ventas y reportes.

> Desarrollado por **A2K Digital Studio**

---

## 🚀 Despliegue

- **URL en producción:** [https://tiendadigitalaipro.github.io/Repuestos-de-motos-pro-/](https://tiendadigitalaipro.github.io/Repuestos-de-motos-pro-/)
- **Hosting:** GitHub Pages
- **Arquitectura:** 100% client-side (sin backend, sin Firebase)

---

## 📦 Archivos del Proyecto

| Archivo | Descripción |
|---|---|
| `index.html` | Punto de entrada — redirige a la app principal |
| `repuestos-motos-pro.html` | App principal (~1957 líneas) |
| `admin-licencias.html` | Panel de administración de licencias |
| `ESTRUCTURA.md` | Mapa detallado de archivos y secciones |
| `MANTENIMIENTO.md` | Guía rápida de modificaciones comunes |

---

## ✨ Funcionalidades

| Módulo | Descripción |
|---|---|
| **Dashboard** | Resumen general con gráfico canvas |
| **POS** | Punto de venta con búsqueda y cobro |
| **Inventario** | Control de stock y productos |
| **Clientes** | Base de datos de clientes |
| **Ventas** | Historial de ventas |
| **Caja** | Apertura/cierre de caja |
| **Reportes** | Estadísticas y reportes |
| **Marcas/Modelos** | Gestión de 29 marcas de motos |
| **Config** | Configuración general |

### Características Especiales

- 🎨 **Gráficos Canvas** — Sin librerías externas, renderizado nativo
- 💰 **Pago mixto** — Soporte para pago parcial en múltiples métodos
- 📤 **Export/Import** de datos en formato JSON
- 📐 **Polyfill personalizado** para `roundRect` (compatibilidad navegadores)

---

## 💰 Métodos de Pago

Se soportan **8 métodos de pago** con moneda dual (**$ / Bs**) y **pago mixto**:

- Efectivo $, Efectivo Bs, Pago Móvil, Transferencia, Punto de Venta, Zelle, Tarjeta Débito, Tarjeta Crédito

---

## 🔐 Sistema de Licencias (IRON LOCK)

| Parámetro | Valor |
|---|---|
| **Salt** | `RMPMOTOS2026` |
| **Admin Password** | `RMP2026ADMIN` |
| **Master Codes** | `RMP-PRO-DEMO-2024`, `RMP-PRO-A2K-2026`, `RMP-PRO-MAST-2026` |
| **Prefijo localStorage** | `rmp_` |

---

## 📊 Datos por Defecto

- **62 productos** precargados (líneas 1837–1937)
- **29 marcas de motos** en la base de datos (líneas 753–786)
- **3 clientes** de ejemplo
- **10 categorías** de productos

---

## 🛠️ Stack Técnico

- HTML5 + CSS3 + JavaScript vanilla
- Canvas API nativo para gráficos
- localStorage para persistencia de datos
- Polyfill propio para `roundRect`
- Sin dependencias externas
- Compatible con dispositivos móviles y escritorio
