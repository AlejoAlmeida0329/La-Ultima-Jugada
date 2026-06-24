# Skill: brand-designer

> Cómo aplicar la identidad visual de La Última Jugada en cualquier output gráfico o UI.

---

## Cuándo activar este skill

- Diseñar pantallas o componentes UI
- Crear mockups de páginas
- Construir piezas gráficas (banners, social, packaging)
- Definir hero sections, cards, layouts
- Generar SVGs ilustrativos o iconografía
- Revisar cualquier output visual antes de publicar

## Contexto necesario

Cargar siempre junto:
- `02_BRAND.md` (paleta, tipografía, sistema gráfico)
- `03_VOICE.md` (si la pieza lleva texto)

---

## Reglas duras

1. **Paleta dominante = Tinta + Tiza + Rojo cancha.** Los tricolores nacionales (amarillo `#FCD116`, azul `#003893`, rojo `#CE1126`) aparecen **solo cuando hay producto de selección visible en la misma pieza**.
2. **Tipografía:** PP Neue Machina (display) + Inter (texto). Sin fuentes decorativas, sin itálicas decorativas.
3. **Esquinas:** 0px o 2px máximo. Nunca pill shapes, nunca radius > 4px.
4. **Sin gradientes dorados.** Sin glow effects. Sin "metalic" feel.
5. **Sin emojis decorativos** en UI comercial.
6. **CTAs en MAYÚSCULAS**, tracking 0%, peso bold.
7. **Mobile-first.** Diseñá primero a 360px, después escalá.
8. **Espaciados generosos verticales.** Usar múltiplos de 8px (8, 16, 24, 32, 48, 64, 96).

## Patrones visuales

### Grid y layout
- Asimétrico, deportivo, no "elegante centrado"
- Numerales grandes (3-dígitos en display) como elemento gráfico
- Líneas finas (1px Gris cemento) como separadores
- Sin cajas con sombra. Si necesitás separación, usá línea o color de fondo.

### Botones
- Primary: fondo Tinta, texto Tiza, sin borde, esquina 2px, padding 16/24
- Secondary: fondo Tiza, texto Tinta, borde 1px Tinta
- Destructive: fondo Rojo cancha, texto Tiza
- Disabled: fondo Gris cemento al 30%, texto Gris cemento

### Inputs
- Borde 1px Gris cemento
- Focus: borde 2px Tinta
- Error: borde 2px Rojo cancha + texto de error abajo
- Sin labels flotantes. Label arriba, fijo.

### Cards
- Fondo Tiza
- Sin sombra, sin border-radius (o 2px)
- Imagen ocupa 100% del ancho de la card
- Texto abajo con padding consistente

### Tipografía aplicada
- Hero: PP Neue Machina, 96–128px, mayúsculas, tracking -2%
- H1: PP Neue Machina, 48–64px
- H2: PP Neue Machina, 32–40px
- H3: Inter Bold, 24px
- Body: Inter Regular, 16px, line-height 1.5
- Caption: Inter Regular, 13px, color Gris cemento

## Lo que NUNCA hacés

- Gradientes dorados o brillantes
- Texturas tipo carbono, fibra, metálico
- Drop shadows pronunciadas
- Border radius tipo pill
- Iconos con relleno de color brillante
- Stock photos
- Banderas grandes ondeantes
- Mariposas, trenes, vegetación ornamental
- Frases en inglés decorativas

## Checklist antes de entregar

- [ ] ¿La pieza tiene <5% de área en tricolores si no hay producto de selección visible?
- [ ] ¿Funciona en móvil 360px?
- [ ] ¿Las tipografías son las correctas?
- [ ] ¿CTAs en mayúsculas?
- [ ] ¿Esquinas a 0 o 2px?
- [ ] ¿Hay algún gradiente dorado? → eliminar
- [ ] ¿Hay stock photos? → reemplazar
- [ ] ¿Pasa el test "esto no parece flyer de WhatsApp"?

## Cuando no estés seguro

Aplicá la regla del "más austero gana". En la duda, eliminá elementos, no agregués. La marca vive del contraste, no del adorno.
