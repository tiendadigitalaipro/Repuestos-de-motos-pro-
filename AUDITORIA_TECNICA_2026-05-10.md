# Auditoría técnica profunda — Repuestos de Motos Pro

Fecha: 2026-05-10  
Alcance: revisión de código estático en `repuestos-motos-pro.html`, `admin-licencias.html`, `index.html` y documentación técnica.

## Resumen ejecutivo (estado actual)

**Riesgo general:** ALTO en seguridad/licenciamiento y MEDIO en integridad de datos financieros.  
**Causa principal:** arquitectura 100% cliente con secretos, lógica de seguridad y datos críticos en el navegador/localStorage.

---

## Hallazgos críticos (lo que hoy puede fallar o ser vulnerado)

1. **Licencias y claves expuestas en frontend (riesgo crítico).**  
   El `salt`, códigos master y password admin están hardcodeados en cliente, visibles para cualquier usuario con DevTools. Esto permite ingeniería inversa de generación/validación de licencias.

2. **Algoritmo de hash no criptográfico para licencias y passwords (riesgo crítico).**  
   Se usa función hash casera basada en `Math.imul` (no resistente a colisiones ni ataques de fuerza bruta). No hay firma criptográfica real.

3. **No existe validación de licencia contra servidor (riesgo crítico).**  
   Toda validación ocurre localmente. Si el usuario manipula localStorage o funciones JS en runtime, puede forzar estados de licencia.

4. **Bloqueo por dispositivo débil y suplantable (riesgo alto).**  
   Device ID basado en `userAgent`, idioma, plataforma, resolución y hardwareConcurrency; puede cambiar por navegador/OS o ser emulado.

5. **Datos de negocio y ventas en localStorage sin cifrado ni integridad (riesgo alto).**  
   Inventario, caja, ventas y configuración se pueden editar manualmente desde DevTools. No hay auditoría inmutable ni checksum firmado.

6. **Autenticación administrativa sin rate-limit ni MFA (riesgo alto).**  
   En panel admin no hay límite de intentos, bloqueo temporal ni segundo factor.

7. **Export/Import JSON sin controles de esquema/versionado/firma (riesgo alto).**  
   Posible inyección de datos corruptos, valores negativos, estructuras inválidas o desalineadas con versiones futuras.

8. **Lógica financiera en `float` JavaScript (riesgo medio-alto).**  
   Cálculos monetarios con `parseFloat` y operaciones decimales pueden acumular errores de redondeo.

9. **Sin bitácora/auditoría antifraude de movimientos sensibles (riesgo medio-alto).**  
   No hay trazabilidad robusta de quién cambia tasa, elimina ventas, resetea datos o modifica caja.

10. **Sin respaldo automático remoto ni recuperación ante desastre (riesgo alto negocio).**  
    Pérdida de navegador/perfil/dispositivo implica posible pérdida total de datos si no se exportó manualmente.

---

## Lo que NO está funcionando al nivel “modo dios”

- La **seguridad de licencias** no es invulnerable: está en cliente y puede ser manipulada.
- La **protección anti-clonado** de licencia/dispositivo no es fuerte contra atacantes técnicos.
- La **garantía “no perder ni un centavo”** no puede cumplirse con almacenamiento local sin respaldo transaccional.
- La **exactitud matemática contable** no está blindada (falta motor decimal/entero-centavos + reglas de redondeo consistentes).
- La **operación multi-terminal real** no está centralizada, por lo que no hay consistencia global ni resolución de conflictos.

---

## Mejoras necesarias para convertirla en “modo dios” (roadmap recomendado)

### Fase 1 — Blindaje crítico (urgente)
1. Migrar licenciamiento a **backend** con firma asimétrica (ej. Ed25519/JWT firmado) y validación online/offline controlada.
2. Eliminar secretos del frontend (salt, master codes, admin default).
3. Reemplazar hash casero por criptografía estándar (Argon2id/bcrypt para passwords; firmas digitales para licencias).
4. Implementar telemetría de licencias: activación, revocación, límites por dispositivo, detección de duplicidad.

### Fase 2 — Integridad financiera
1. Manejar montos en **centavos enteros** (no float) y definir política de redondeo única.
2. Motor de validación de transacciones (no negativos, stock no inconsistente, cierre de caja cuadrado).
3. Libro mayor/event sourcing: cada operación inmutable con hash encadenado y usuario/fecha.

### Fase 3 — Continuidad operativa
1. Backend de persistencia (PostgreSQL) + backups automáticos + restauración probada.
2. Sincronización multi-terminal, control de concurrencia y resolución de conflictos.
3. Alertas de salud (errores, desfases de caja, intentos de fraude/licencia).

### Fase 4 — Gobierno y seguridad avanzada
1. RBAC (roles), 2FA para admin, rate-limit y bloqueo por intentos.
2. Auditoría exportable firmada y reportes fiscales consistentes.
3. CI con pruebas unitarias/integración/e2e sobre flujos POS/licencias/caja.

---

## Observaciones técnicas puntuales detectadas en código

- Existe hardcode de `_SIGN_SALT` y `MASTER_LICS` en app principal.
- Existe hardcode de `SIGN_SALT` y `ADMIN_PW_DEFAULT` en panel admin.
- Persistencia crítica en localStorage bajo prefijo `rmp_`.
- Hash usado para password/licencia no es criptográfico.

---

## Conclusión

El sistema actual es funcional como app local/offline básica, pero **no** cumple estándares de seguridad e integridad para escenarios donde “el cliente no pierda ni un centavo” ante fraude, manipulación o fallos de dispositivo.  

Quedo a la espera de tu orden para pasar a la **fase de corrección** con un plan de implementación por prioridades (rápido, mediano y enterprise).
