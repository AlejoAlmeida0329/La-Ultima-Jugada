# Skill: product-photographer

> Cómo brifear, ejecutar y validar la fotografía de producto para mantener consistencia de catálogo.

---

## Cuándo activar este skill

- Brifear sesión fotográfica con fotógrafo freelance
- Revisar fotos antes de subir al catálogo
- Definir shotlist para una colección nueva
- Establecer guidelines de edición y post
- Auditar calidad del catálogo existente

## Contexto necesario

Cargar siempre junto:
- `02_BRAND.md` (paleta, tratamiento visual)
- `06_CATALOGO.md` (tipos de media: hero, gallery, detail, lifestyle)

---

## Principios duros

1. **Catálogo consistente vale más que catálogo perfecto.** Mejor 50 SKUs con la misma estética que 10 con producción de revista y 40 mediocres.
2. **Fondo neutro: Tinta `#0E0E0E` o Tiza `#F5F2EC`.** Nunca blanco puro, nunca crema cálido, nunca gris azulado.
3. **Iluminación dura controlada, no difusa.** Las sombras son parte de la estética.
4. **Producto antes que styling.** El cliente compra la camiseta, no la pose.
5. **Mismo setup para toda una colección.** Lo que cambia es el producto, no el lighting.

## Shotlist mínimo por SKU

**Total: 6–10 imágenes por producto.**

### Obligatorias (6)
1. **Hero — Frente flat lay** (fondo Tiza, camiseta extendida, ángulo cenital)
2. **Gallery — Espalda flat lay**
3. **Gallery — En modelo de frente** (busto)
4. **Gallery — En modelo de espalda**
5. **Detail — Escudo en close-up**
6. **Detail — Logo de manga / pecho**

### Recomendadas (2–4)
7. Detail — Textura de tela (close-up con luz lateral)
8. Detail — Etiqueta interior con talla
9. Gallery — En modelo de costado
10. Lifestyle — En contexto real (cancha, calle, gimnasio)

## Especificaciones técnicas

### Cámara y formato
- Mínimo: full frame, 24MP
- Formato: RAW + JPEG
- Aspect ratio entrega: 4:5 vertical (para mobile-first) + 1:1 cuadrada (para social)
- Resolución final: 2000px lado largo mínimo

### Lighting setup recomendado
- Flat lay: 2 luces a 45° + difusor
- Modelo: 1 luz principal + 1 fill suave, sin softbox masivo
- Detail: luz lateral dura para revelar textura

### Backdrop
- Fondo Tinta: papel seamless o tela mate negra
- Fondo Tiza: papel seamless en off-white deportivo
- Nunca: blanco puro 100%, beige cálido, gris azulado

### Post-producción
- Balance de blancos neutro (no cálido, no frío)
- Negros profundos pero con detalle preservado
- Saturación natural, sin pump artificial
- Grano sutil aceptable
- Sin filtros tipo Instagram
- Limpiar pelusas, hilos sueltos, arrugas mayores
- Mantener arrugas naturales pequeñas (no parecer maniquí de showroom barato)

## Lifestyle — guidelines específicas

Cuando hagamos lifestyle (no obligatorio, pero suma):

- **Locaciones:** cancha de barrio real, gimnasio sin filtro, calle, escaleras de estadio, parque
- **NO:** estudio sobreproducido, locaciones premium turísticas, casas modernas tipo Airbnb
- **Modelos:** gente real (puede ser amigos, gente del gym, contactos). Diversidad real, no de catálogo.
- **Pose:** actitud, foco, intensidad. NO sonrisas comerciales, NO poses tipo Vogue.
- **Vestuario complementario:** jean negro, sweatpants neutros, tenis blancos básicos. La camiseta es protagonista.

## Naming de archivos (importante para el admin)

Formato: `{sku}_{tipo}_{numero}.jpg`

Ejemplos:
- `LUJ-TRI2526-LOCALH-L_hero_01.jpg`
- `LUJ-TRI2526-LOCALH-L_gallery_02.jpg`
- `LUJ-TRI2526-LOCALH-L_detail_01.jpg`

Esto facilita el upload masivo al admin.

## Alt text (importante para SEO y accesibilidad)

Patrón: **[Tipo de foto] - [Nombre producto] - [Detalle]**

Ejemplos:
- "Camiseta tricolor 25/26 local hombre, frente"
- "Camiseta tricolor 25/26 local hombre, escudo bordado en detalle"
- "Camiseta tricolor 25/26 local hombre, en modelo de espalda"

**Importante:** sin marcas registradas en alt text (ver `legal-disclosure` skill).

## Cuidado con derechos de imagen del modelo

- Contrato de cesión de derechos por sesión
- Permiso explícito para uso comercial digital
- Plazo de uso (recomendado: 2 años renovables)
- Sin reconocimiento facial extremo (mejor si no se ve la cara completa en hero shots, solo busto o parcial)

## Checklist por SKU antes de publicar

- [ ] Hero shot presente y editado
- [ ] Mínimo 3 fotos de galería (frente, espalda, en modelo)
- [ ] Mínimo 2 fotos de detalle (escudo + logo, o etiqueta + textura)
- [ ] Todas las fotos con mismo backdrop y lighting
- [ ] Alt text descriptivo y sin marcas
- [ ] Nombres de archivo siguen convención
- [ ] Resolución 2000px lado largo mínimo
- [ ] Subidas a Cloudinary, no a Supabase Storage directo
- [ ] Orden de las imágenes en admin: hero primero, luego gallery, luego detail

## Cuando contrates fotógrafo freelance

Brief mínimo a entregar:
1. Este documento
2. `02_BRAND.md`
3. Lista de SKUs con cantidad de fotos por cada uno
4. Referencias visuales (3–5 ejemplos de marcas que te gustan: Aimé Leon Dore, Patta, Stüssy, Adsum — austeras, deportivas, editoriales)
5. Costo y plazo acordado

Pedile prueba de 1 SKU completo antes de pagar la sesión completa. Si no calza con el brief, pivotás antes.
