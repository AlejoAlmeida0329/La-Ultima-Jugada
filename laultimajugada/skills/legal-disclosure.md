# Skill: legal-disclosure

> Cómo aplicar las reglas legales de naming, disclosure y disclaimer en cualquier output público sin volverse abogado.

---

## Cuándo activar este skill

- Nombrar productos o colecciones nuevas
- Escribir descripciones de producto
- Redactar meta tags (title, description) para SEO
- Definir alt text de imágenes
- Crear copy de marketing / campañas / redes
- Auditar el sitio existente antes de publicar
- Revisar piezas gráficas que vayan a ser públicas

## Contexto necesario

Cargar siempre junto:
- `05_LEGAL.md` (marco completo y disclaimer crítico)
- `03_VOICE.md` (si la pieza lleva copy)

---

## Disclaimer crítico

**Este skill no sustituye asesoría legal.** Aplicalo como filtro operativo de día a día, pero la revisión legal profesional antes del primer pago sigue siendo obligatoria. Si una situación específica te genera duda y no encaja en estos patrones, **escalá al abogado, no improvisés**.

---

## Términos prohibidos — bloqueo automático

Estos términos NUNCA aparecen en producto, marketing, meta tags, alt text o nombres de archivo:

### Marcas registradas
- Adidas (y variantes: ADIDAS, adidas, Addidas)
- FCF
- Federación Colombiana de Fútbol
- FIFA
- World Cup / Copa Mundo / Copa del Mundo
- Nike, Puma, otros (cuando aplique a producto)

### Términos que implican oficialidad
- "original"
- "originales"
- "oficial"
- "oficiales"
- "auténtica"
- "auténticas"
- "auténtico"
- "auténticos"
- "licenciada"
- "licenciado"
- "verdadera"
- "genuina"

**Regla:** si una de estas palabras aparece en una pieza pública, frená y reescribí.

## Términos requeridos

### En descripción de producto
Toda descripción debe contener al menos una vez:
> "Réplica premium calidad 1:1"

### En disclaimer del PDP
Visible en el detalle del producto (no en footer únicamente):
> "Réplica premium calidad 1:1. Producto no oficial, no licenciado."

### En footer del sitio
Link permanente a `/replicas` (política de réplicas).

## Patrones de naming aprobados

### Productos
✅ Correcto:
- "Tricolor 25/26 — Local Hombre"
- "Tricolor 25/26 — Local Mujer"
- "Macondo — Edición Especial"
- "Centenario — 100 Años"
- "Café — Visitante 25/26"

❌ Incorrecto:
- "Camiseta Adidas Colombia 25/26"
- "Camiseta Oficial Selección 25/26"
- "Jersey Auténtica FCF"
- "Réplica de Camiseta Adidas Colombia" (incluso con "réplica" delante, el problema es nombrar la marca)

### Colecciones
✅ Correcto:
- "Tricolor 25/26"
- "Macondo"
- "Centenario"
- "Retro Cafetero"

❌ Incorrecto:
- "Colección Adidas Colombia"
- "Equipación Oficial 25/26"

### Imágenes (alt text + filename)
✅ Correcto:
- alt: "Camiseta tricolor 25/26 local hombre, frente"
- file: `LUJ-TRI2526-LOCALH-L_hero_01.jpg`

❌ Incorrecto:
- alt: "Camiseta Adidas Colombia frente"
- file: `adidas-colombia-2526.jpg`

## Patrones de copy aprobados

### Mencionar el equipo sin nombrar marca registrada
✅ "Camiseta estilo selección Colombia"
✅ "Estilo selección nacional"
✅ "Estilo equipo de Colombia"
❌ "Camiseta de la selección Colombia oficial"

### Hablar de la temporada
✅ "Local 25/26"
✅ "Visitante temporada 25/26"
❌ "Equipación oficial temporada 25/26"

### Mencionar característica técnica
✅ "Tela poliéster reciclado transpirable"
✅ "Escudo bordado"
❌ "Tecnología Climacool" (es marca registrada de Adidas)
❌ "Aeroready" (también marca registrada)

Si necesitás referirte a la tecnología de transpiración, usá descripción genérica: "tela transpirable", "tejido ligero", "ventilación mejorada".

## Meta tags — auditoría obligatoria

Antes de publicar un producto, revisar que no contengan términos prohibidos:

- `meta_title`
- `meta_description`
- `meta_keywords` (si se usa)
- `og:title`, `og:description`
- `twitter:title`, `twitter:description`
- Schema.org JSON-LD del producto

### Ejemplo de meta correcta

```html
<title>Tricolor 25/26 — Local Hombre | La Última Jugada</title>
<meta name="description" content="Camiseta estilo selección Colombia local 25/26. Réplica premium calidad 1:1. Envío nacional $12.000.">
```

### Ejemplo de meta incorrecta (no usar)

```html
<title>Camiseta Adidas Colombia 2025 Oficial FCF</title>
<meta name="description" content="Compra la camiseta oficial Adidas de la Selección Colombia FCF 25/26 al mejor precio.">
```

## Marketing pago — reglas adicionales

Cuando se haga pauta en Google / Meta:

- ❌ Sin keywords pagas que contengan marcas registradas
- ❌ Sin uso de logos de terceros en piezas gráficas
- ❌ Sin uso del escudo FCF separado del producto físico
- ❌ Sin imágenes de jugadores reales (Vinotinto, James, Falcao, etc.)
- ❌ Sin imágenes oficiales de partidos / estadios identificables

Permitido en pauta:
- ✅ Foto del producto (la camiseta misma) en fondo neutro
- ✅ Lifestyle propio con modelos no famosos
- ✅ Keywords genéricas: "camiseta selección colombia", "camiseta tricolor", "ropa deportiva colombia"

## Redes sociales — reglas

- Sin tag a cuentas oficiales (@adidascolombia, @fcfseleccioncol) en posts comerciales
- Sin uso del hashtag #SeleccionColombia, #VamosMiColombia en contexto de venta (pueden usarse en contexto editorial/cultural neutro)
- Sin reposteo de contenido oficial

## Protocolo si encontrás algo dudoso

1. Frená la publicación.
2. Anotalo en un doc de "casos dudosos" para revisar con abogado.
3. Reescribilo en versión segura mientras se resuelve.
4. Si el abogado dice OK, lo desbloqueás. Si dice no, lo dejás bloqueado.

**Costo de equivocarse versus costo de revisar:** revisar una pieza con abogado es ~$150k COP. Recibir una demanda o un C&D es exponencialmente más costoso. La revisión paga.

## Checklist antes de publicar cualquier pieza pública

- [ ] ¿Contiene alguna palabra de la lista prohibida? → reemplazar
- [ ] Si es producto: ¿incluye "réplica premium calidad 1:1" en la descripción?
- [ ] ¿Los meta tags están limpios de marcas?
- [ ] ¿El alt text de imágenes está limpio?
- [ ] ¿El nombre de archivo está limpio?
- [ ] Si es marketing pago: ¿la keyword/audiencia está limpia?
- [ ] ¿El footer del sitio mantiene visible la política de réplicas?

## El test final

Si un abogado de Adidas o FCF mirara esta pieza, ¿podría argumentar que estás usando su marca registrada o haciéndote pasar por producto oficial?

- Si la respuesta es claramente NO → publicá.
- Si la respuesta es "tal vez" → reescribí.
- Si la respuesta es claramente SÍ → no publiqués y revisá con abogado.
