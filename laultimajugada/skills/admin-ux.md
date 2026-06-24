# Skill: admin-ux

> Cómo diseñar las pantallas del admin para que las pueda usar una persona no técnica sin documentación.

---

## Cuándo activar este skill

- Diseñar cualquier pantalla del admin (`/admin/*`)
- Construir formularios de creación/edición de productos
- Diseñar tablas de listado (productos, órdenes, clientes)
- Definir flujos de bulk action
- Resolver UX de upload de imágenes
- Diseñar dashboards de métricas

## Contexto necesario

Cargar siempre junto:
- `01_PRD.md` (user stories del admin, sitemap admin)
- `06_CATALOGO.md` (estructura de datos)
- `brand-designer.md` (paleta y tipografía del admin son las mismas que la tienda)

---

## Principios duros

1. **Usable por no técnicos.** Catalina (persona de catálogo) no sabe SQL, no entiende slugs, no tiene que ver IDs.
2. **Acción destructiva = confirmación + explicación.** Eliminar, archivar, despublicar siempre piden confirmación con consecuencia clara.
3. **Preview antes de publicar.** Cambios visuales tienen vista previa de cómo se verá en tienda.
4. **Sin jerga técnica.** "Borrador" no "draft", "Publicado" no "active", "Sin stock" no "stock_quantity = 0".
5. **Tareas comunes deben tomar menos de 5 minutos.** Crear un producto con variantes y subir fotos = 5 min.
6. **Errores específicos y accionables.** No "Error al guardar". Sí "Falta el precio. Sin precio no se puede publicar."

## Patrones por pantalla

### Login
- Email + contraseña
- Magic link como opción preferida (Supabase Auth)
- Sin "registrarse" — los usuarios del admin se crean por invitación

### Dashboard
- 4–6 métricas clave del día / semana / mes
- Lista corta: "Órdenes que necesitan atención"
- Lista corta: "Productos con bajo stock"
- Acceso directo a tareas comunes

Métricas a mostrar:
- Ventas hoy / semana / mes (monto + #órdenes)
- Conversion rate
- AOV
- Órdenes pendientes de despacho
- Variantes con stock < 3

### Lista de productos
- Tabla con: thumbnail, name, subtitle, precio, stock total, estado, acciones
- Filtros: estado, colección, categoría
- Búsqueda: por name, SKU, slug
- Sort: name, fecha de creación, precio, stock
- Acciones por fila: editar, duplicar, archivar
- Acciones bulk: archivar, marcar como destacado, eliminar (con confirmación)
- Botón principal arriba: **+ NUEVO PRODUCTO**

### Crear / editar producto
Layout en columnas (en desktop):

**Columna izquierda (principal):**
1. Sección "Información"
   - Nombre
   - Subtítulo
   - Descripción corta (textarea)
   - Descripción larga (rich text)
2. Sección "Imágenes"
   - Drag & drop multi-upload
   - Reorden por arrastre
   - Asignar tipo (hero / gallery / detail / lifestyle)
   - Editar alt text por imagen
3. Sección "Variantes"
   - Lista de tallas con stock por talla
   - Botón "+ Agregar talla"
   - Bulk: aplicar mismo stock a todas

**Columna derecha (meta):**
1. Estado: Borrador / Publicado / Archivado
2. Precio + precio tachado opcional
3. Colección (dropdown)
4. Categorías (multi-select con tags)
5. Atributos (key-value editable)
6. SEO: meta title, meta description (con contador de caracteres)
7. Acciones: GUARDAR / GUARDAR Y PUBLICAR / VER VISTA PREVIA

### Upload de imágenes
- Drag & drop area grande
- Click para seleccionar archivos
- Preview inmediato (thumbnail) antes de subir
- Progress bar por imagen
- Si una imagen falla: mostrar error específico ("Archivo muy grande", "Formato no soportado")
- Reorden por arrastre con feedback visual claro

### Vista previa
- Botón "Ver vista previa" abre nueva pestaña con el producto renderizado como se verá en tienda
- Aunque sea borrador, la vista previa funciona

### Lista de órdenes
- Tabla con: número, fecha, cliente, total, estado, acciones
- Filtros: estado, rango de fechas
- Búsqueda: por número de orden, email del cliente
- Acciones por fila: ver detalle, marcar como despachada, cancelar
- Estados con color: pendiente (gris), pagada (azul), despachada (amarillo), entregada (verde), cancelada (rojo)

### Detalle de orden
- Info del cliente
- Productos (con thumbnails)
- Resumen de pagos
- Dirección de envío
- Historial de cambios de estado
- Acciones: cambiar estado, descargar factura, agregar nota interna
- Notas internas: solo visibles para admin, no para cliente

### Inventario
- Tabla de variantes con: SKU, producto, talla, stock actual, alerta de bajo stock
- Bulk edit: seleccionar varias y ajustar stock
- Vista de "Bajo stock" preconfigurada (variantes con < 3 unidades)

### Configuración
- Datos de la tienda (nombre, contacto)
- Política de envío (costo, tiempos)
- Pagos (toggles para métodos activos)
- Cupones (lista + crear nuevo)
- Políticas legales (rich text editor con guardado)

## Confirmaciones para acciones destructivas

| Acción | Confirmación |
|---|---|
| Archivar producto | "Vas a archivar este producto. No se verá en la tienda pero se preserva el historial de órdenes. ¿Continuar?" |
| Eliminar producto (solo si nunca se vendió) | "Eliminación permanente. No se puede deshacer. ¿Continuar?" |
| Cancelar orden | "Vas a cancelar la orden #{ID}. Esto inicia el reembolso al cliente. ¿Continuar?" |
| Cambiar precio en producto publicado | "Este cambio se ve en la tienda inmediatamente. ¿Continuar?" |

## Errores claros (no genéricos)

| Genérico ❌ | Específico ✅ |
|---|---|
| "Error al guardar" | "Falta el precio. Sin precio no se puede publicar." |
| "Operación fallida" | "No se pudo subir la imagen. Pesa más de 5MB." |
| "Campo inválido" | "El SKU ya existe en otro producto. Usá uno diferente." |

## Feedback visual

- Acción exitosa: toast verde corto, "Producto guardado" / "Orden actualizada"
- Acción con warning: toast amarillo, "Guardado, pero el producto está sin stock"
- Acción fallida: toast rojo + mantener el form con los datos (no perder lo que el usuario escribió)
- Loading: estado claro en botones ("GUARDANDO..." disabled), no spinners flotantes

## Checklist antes de entregar una pantalla del admin

- [ ] ¿Una persona no técnica puede usarla sin docs?
- [ ] ¿Las acciones destructivas piden confirmación?
- [ ] ¿Hay vista previa para cambios visuales?
- [ ] ¿Los errores son específicos y accionables?
- [ ] ¿Funciona en tablet (1024px) además de desktop?
- [ ] ¿Sin jerga técnica (slug, draft, active)?
- [ ] ¿Los botones primarios son claros y únicos por pantalla?
- [ ] ¿Hay undo o confirmación para acciones que cambian el estado público?

## Mobile en admin

H1: el admin no necesita ser mobile-first. Se asume desktop o tablet horizontal (1024px+). Las pantallas del admin pueden tener feature parity reducido en móvil.

H3+: si la persona de catálogo necesita gestionar desde el celular (subir fotos desde el shooting), priorizar mobile para "crear producto" y "subir imagen".
