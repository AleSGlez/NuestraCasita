# 🏡 NuestraCasita — Plan

App para organizar la casa de Ale y Raúl: compras, quehaceres, acuerdos y calendario.
Hermana de **Nuestro Patrimonio** (finanzas). Este plan es vivo: lo vamos cambiando poco a poco.

---

## Principios

- **Simple primero.** Aprobamos poco y crecemos según lo que de verdad usemos.
- **Cada fase entrega algo usable**, no piezas sueltas.
- **No duplicar Patrimonio.** El dinero vive en Patrimonio; Casita solo le manda gastos por confirmar.
- **Pocas notificaciones**, solo las importantes.
- **Sin puntos ni rankings** entre nosotros.

---

## Decisiones tomadas

| Tema | Decisión |
|---|---|
| Stack | Igual que Patrimonio: React 18 + Vite + Tailwind + Supabase + Zustand + TanStack Query, PWA, Vercel |
| Base de datos | **Mismo proyecto de Supabase** que Patrimonio. Misma cuenta y misma `pareja_id` |
| Tablas nuevas | Prefijo `casa_` y RLS con el patrón de `pareja_id` de Patrimonio |
| Gastos | Casita crea **gastos por confirmar**; Patrimonio los confirma con su lógica existente (`aplicarEfecto`), así los saldos se actualizan bien. Campo `persona`: `p1`, `p2` o `ambos` |
| Calendario | Un solo calendario: se reutiliza `calendario_eventos` de Patrimonio (agregando hora, persona y tipo `hogar`). Sincronización con Google y Apple por enlace de suscripción `.ics` |
| Quehaceres | Nombre, frecuencia y responsable: **Ale / Raúl / turnarse / quien pueda**. Sin puntos |
| Diseño | Mismos componentes que Patrimonio, con identidad propia: **azul `#0284C7`**, ícono y nombre propios, modo oscuro |
| Conexión | Botón para abrir Patrimonio (y uno en Patrimonio para abrir Casita) |

---

## Navegación

| Inicio | Compras | Casa | Calendario | Más |
|---|---|---|---|---|
| Resumen del día y acciones rápidas | Lista del súper | Quehaceres y acuerdos | Eventos compartidos | Cosas del depa, info, notas, botón a Patrimonio |

Los módulos nuevos se agregan en **Más** sin cambiar la barra.

---

## Fases

### Fase 0 — La base 🧱
- Proyecto con el stack de Patrimonio.
- Login con la cuenta de Patrimonio; detecta `pareja_id` y quién es p1/p2.
- Estilo de Casita: azul, ícono y nombre propios, modo oscuro.
- Barra de navegación con las 5 pestañas (vacías).
- PWA instalable y deploy en Vercel.
- Botón para abrir Patrimonio.

✅ Lista cuando: la instalamos en el iPhone, entramos con nuestra cuenta y vemos la app con su estilo.

### Fase 1 — Lista de compras 🛒
- Lista compartida en tiempo real (tachar y que el otro lo vea).
- Categorías o pasillos, cantidades y notas.
- Frecuentes: agregar de un toque.
- "Cerrar compra": limpia lo comprado y guarda historial.

✅ Lista cuando: la usamos en el súper de verdad.

### Fase 2 — Quehaceres y acuerdos 🧹🤝
- Quehaceres con frecuencia y responsable (Ale / Raúl / turnarse / quien pueda).
- "Hoy te toca…" en Inicio; marcar como hecha.
- **Nuestros acuerdos:** uno propone, el otro acepta; editables, con fecha; recordatorio opcional cada 3 meses para revisarlos.
- Sugerencia para repartir: elegir tareas por turnos; las que nadie quiere van en "turnarse"; revisar al mes.

✅ Lista cuando: la primera semana nos repartimos los quehaceres con la app.

### Fase 3 — Calendario 📅
- Extender `calendario_eventos` (hora, persona, tipo `hogar`).
- Vista de calendario en Casita con eventos de casa (y opcionalmente pagos de Patrimonio).
- Enlace `.ics` privado para Google y Apple Calendar (un solo sentido; Google tarda horas en refrescar).

✅ Lista cuando: los eventos de Casita aparecen en nuestros calendarios del celular.

### Fase 4 — Conexión con Patrimonio 💰
- Al cerrar una compra: total, categoría, persona (p1/p2/ambos) y método de pago.
- Se guarda en `casa_gastos_pendientes`.
- En Patrimonio: aviso "🏠 N gastos de Casita por confirmar" → se registran con su lógica existente.
- Botón en Patrimonio para abrir Casita.

✅ Lista cuando: una compra hecha en Casita aparece bien registrada en Patrimonio.

### Fase 5 — Notificaciones 🔔
- Reutilizar el sistema de push de Patrimonio.
- Recordatorios de quehaceres y eventos; avisos importantes de la lista.

### Fase 6+ — Ideas para después ✨
Se eligen según lo que de verdad usemos:
- 🍝 Menú semanal → ingredientes a la lista de compras.
- 🪑 **Cosas del depa** (una sola lista con estado *quiero / compré / tengo*, con precio y garantía): reemplaza mudanza, wishlist e inventario del hogar.
- 🏠 **Info del depa**: contactos, WiFi, contrato, documentos y garantías.
- 🔧 Mantenimiento: tareas recurrentes con recordatorio.
- 🧴 Despensa básica con aviso de agotados.
- 📝 Notas compartidas.
- 🐶 Mascotas (pendiente: ¿tenemos o tendremos?).
- Indicador de presupuesto de Patrimonio en Inicio (ej. "Súper: $2,300 de $4,000").
- Más adelante, si hace falta: sincronización en ambos sentidos con Google Calendar, búsqueda global, galería del depa, paquetes.

---

## Pendientes por decidir
- [ ] ¿Mascota?
- [ ] Ajustar el azul cuando veamos la primera pantalla.
- [ ] Cómo nos repartimos los quehaceres (antes de la Fase 2).
