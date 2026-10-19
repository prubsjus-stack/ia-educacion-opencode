# Prompt maestro — "OpenCode aplicado a la Educación"

Copia **todo** el bloque de abajo en un chat nuevo y pégalo tal cual.

---

## BLOQUE PARA COPIAR

Quiero que construyas una **presentación HTML profesional en un solo archivo** llamada
`index.html`, en español, lista para presentar frente a una audiencia en un aula.

---

# 1. EL TEMA Y EL TONO

- Título: **OpenCode aplicado a la Educación**
- Subtítulo: *Cómo una herramienta de inteligencia artificial puede acompañar el aprendizaje de un estudiante dentro del aula, en lugar de sustituirlo.*
- Presentador: **JUSTIN MENDOZA**
- Fecha: **Lunes 19 de octubre de 2026**
- Idioma: **español de España**, con tildes y `«»` para citas. Nada de comillas rectas.
- **NO** hables de IA en general, ni de machine learning, ni de modelos, ni de arquitectura
  técnica. Habla de **OpenCode** y de lo que cambia en un aula.
- Tono: sereno, honesto, sin publicidad, sin emojis, sin humor payaso.
- Público: estudiantes y docentes de una carrera técnica.
- Concepto central que debe repetirse: **OpenCode no reemplaza al estudiante: lo acompaña.**

---

# 2. REGLAS TÉCNICAS INNEGOCIABLES

1. **Un solo archivo `index.html`**, autónomo. Nada de carpetas, builds, npm ni frameworks.
2. Todo el CSS en un `<style>` y todo el JS en un `<script>`.
3. Las únicas dependencias externas son las fuentes de Google Fonts.
4. No uses frameworks, no uses CDNs de JS, no uses imágenes externas.
5. Debe funcionar abriendo el archivo con doble clic (`file://`).
6. Idioma del documento: `<html lang="es">`.

### Escenario fijo
```
#viewport{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;overflow:hidden}
#stage{position:relative;width:1280px;height:720px;flex:none;transform-origin:center center}
```
`#stage` se escala por JS con `min(innerWidth/1280, innerHeight/720)`.
Cada `.slide` es `position:absolute;inset:0` dentro del stage.

### Fuentes
```html
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=Inter:wght@300;400;500;600&family=Instrument+Serif:ital@0;1&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```

### Tokens de color
```css
--ink:#06080f;   --blue:#5b8cf6;   --blue-soft:rgba(91,140,246,.13);
--amber:#f0b429; --rose:#f07171;   --green:#3ecf8e;
--text:#eef2f8;  --muted:#98a5bb;  --dim:#5f6b80;
--hair:rgba(255,255,255,.075);
--surface:rgba(255,255,255,.028); --surface2:rgba(255,255,255,.05);
--sans:'Inter','Segoe UI',sans-serif;
--display:'Plus Jakarta Sans','Inter',sans-serif;
--serif:'Instrument Serif',Georgia,serif;
--mono:'JetBrains Mono',Consolas,monospace;
```

---

# 3. SISTEMA DE VISUAL — "MINIMALISTA OSCURO"

Fondo casi negro, **un solo color de acento** (azul), tipografía grande, mucho aire,
cero cajas y cero bordes decorativos. Editorial, no "app de dashboard".

## Fondo (capas fijas, `z-index` bajo)
- Dos *glows* radiales muy difuminados (`filter:blur(130px)`, `opacity:.4`) que se desplazan
  en bucles de 26 s y 30 s: azul `#1d4ed8` arriba-izquierda, violeta `#5b21b6` abajo-derecha.
- Una rejilla de 64×64 px con `rgba(255,255,255,.026)` y máscara radial elíptica.
- Grano: SVG `feTurbulence` embebido como data URI, `opacity:.03`.
- Viñeta: `radial-gradient(ellipse at center,transparent 48%,rgba(3,5,10,.8) 100%)`.

## Tipografía
- Títulos de diapositiva: `--display`, peso 800, `letter-spacing` negativo, 40–68 px.
- Palabras resaltadas dentro del título: `<em>` en **Instrument Serif cursiva azul**.
- Texto corrido: `--sans` peso 300, 14–15 px, `line-height` 1.6.
- Etiquetas pequeñas y pies: `--mono`, mayúsculas, `letter-spacing:.2em`, 9–11 px.

## Reglas de layout que **deben** respetarse (son la causa de todos los bugs anteriores)
```css
.slide{padding:76px 96px 84px;display:none;flex-direction:column}
.slide > *{flex:0 0 auto}            /* nada se encoge ni se solapa */
.slide > .head{flex:0 0 auto}        /* el titulo NO crece */
.slide > .body{flex:1 1 auto;min-height:0;display:flex;flex-direction:column;
               justify-content:flex-start}
/* el bloque principal se estira para que la lamina ocupe los 720px completos */
.slide > .body > .grid{flex:1 1 auto;align-content:stretch;grid-auto-rows:1fr}
.slide > .body > .modes{flex:1 1 auto;grid-auto-rows:1fr}
/* las tarjetas son columnas con el texto centrado */
.slide > .body > .grid > .card{display:flex;flex-direction:column;justify-content:center}
```
- **`.foot` es `position:absolute;bottom:34px`** y lleva `padding-bottom` reservado en la
  lámina. Su fondo tapa lo que tenga detrás (`background:var(--ink)`) y lleva un degradado
  superior. El contenido **nunca** puede llegar a la banda del pie.
- `.cover` y `.end` llevan `padding-bottom:118px`.
- Cuando varias tarjetas tengan títulos de 1 y 2 líneas, iguala la altura con
  `min-height` en el `h3` para que los párrafos queden alineados.

## Pie de lámina
Una sola fuente de numeración: `<div class="foot"><span>Título corto</span><span><b>03</b> / 09</span></div>`.
**Nunca** dupliques el contador con otro elemento (ni `SEQ 01/09`, ni `pager`, ni similar).

---

# 4. INTRO CINEMATOGRÁFICA (8,9 s) — NO LA CAMBIES

Marca de cine clásica, sin cuenta regresiva (¡no pongas 8 · 7 · 6!).

Secuencia, en este orden:
1. **Fundido desde negro.**
2. **Academy leader**: anillo con dos círculos girando en sentidos opuestos, los cinco
   barridos horizontales classics y el **obturador** que se cierra en el centro,
   el **cruz** central y el texto espaciado `P I C T U R E   S T A R T`.
3. **Whip cut**: dos barras blancas que barren la pantalla en horizontal.
4. **Destello anamórfico**: destello azul + destello blanco horizontal + anillo expansivo.
5. **Marca hexagonal SVG** que se dibuja trazo a trazo (6 radios hacia el centro + hexágono
   + 6 nodos + núcleo), con línea vertical que **atraviesa** el hexágono y ligero *drift*.
6. **Bloque de título**: glow azul → `OPENCODE` (display, 800, muy espacionado) →
   filete que se dibuja → `<em>APLICADO A LA EDUCACIÓN</em>` en serif →
   `JUSTIN MENDOZA — 19 · 10 · 2026`.
7. **Cierre**: todo se contrae hacia el centro y se desvanece a negro.

Capa de texto tipo HUD en las cuatro esquinas durante la intro:
`OPEN SOURCE AGENT` (arriba-izq), `TC 00:00:00:00` (arriba-der, contador real de timecode),
`TÍTULOS · EDICIÓN 01` (abajo-izq), `LANG ES` (abajo-der), marcas de esquinas, barra de
progreso inferior y el texto `PULSA PARA SALTAR`.

Al terminar dispara el evento `intro:done`. Si el usuario **no ha cambiado de diapositiva**
(`idx === 0`), reinicia la portada con animación. Si ya se movió, no hagas nada.

---

# 5. LAS 9 DIAPOSITIVAS (texto exacto, no lo reescribas)

Cada `<section class="slide">` lleva `data-title` y `data-notes` con las notas del orador
(escritas para leerse en el escenario, en español).

---

### L1 · Portada — `class="slide cover"`
- Marca hexagonal + `O P E N C O D E` espaciado.
- H1: `OpenCode` / `<em>aplicado a la Educación</em>`
- Bajada: `Cómo una herramienta de inteligencia artificial puede acompañar el aprendizaje
  de un estudiante dentro del aula, en lugar de sustituirlo.`
- Chips: `JUSTIN MENDOZA` · `Lunes 19 de octubre de 2026`
- Pie: `Portada` / `01 / 09`
- Notas: saludo breve, enunciar el tema exacto, aclarar que no se habla de programación.
  Dura 30 segundos.

---

### L2 · El problema en el aula
- Eyebrow: `01 · El problema`
- H1: `El estudiante se queda <em>atascado</em> en tres momentos`
- Bajada: `No por falta de esfuerzo. Porque la ayuda llega siempre en el momento equivocado.`
- Tres filas numeradas:
  1. **Cuando algo no funciona y no sabe por qué** — El programa avisa un error, el alumno busca el mensaje, no lo entiende, se frustra y entrega el taller a medias.
  2. **Cuando la duda llega fuera de horario** — La tutoría ya cerró. El alumno se queda con la duda hasta el día siguiente y para entonces ya perdió el hilo.
  3. **Cuando tiene que leer código escrito por otros** — En un proyecto real el alumno lee archivos que no escribió, y ahí no hay manual que le diga qué hace cada cosa.
- Aviso: **OpenCode está pensada exactamente para estos tres casos** —
  `Y lo importante: no los resuelve haciendo la tarea por el estudiante, sino acompañándolo paso a paso.`
- Pie: `El problema en el aula` / `02 / 09`

---

### L3 · OpenCode, en una frase
- Eyebrow: `02 · La herramienta`
- H1: `OpenCode, <em>en una frase</em>`
- Bajada: `Es un programa que se conecta a una inteligencia artificial y le permite trabajar
  sobre los archivos del estudiante: leerlos, corregirlos y explicarlos.`
- Tres puntos con filete de acento superior:
  - **Gratis** — El programa no cuesta nada y se instala con un solo comando.
  - **De código abierto** — Cualquiera puede ver cómo funciona. Nadie es dueño del trabajo del alumno.
  - **Se usa donde ya se estudia** — En la terminal o dentro del editor de código. No hay que aprender otra plataforma.
- Cuatro cifras (se separan por reglas verticales): `208 k` Personas en GitHub ·
  `16 M` Usuarios cada mes · `75 +` Modelos de IA · `0 $` Costo del programa.
  **Ojo:** las cifras hacen *count-up* animado; el sufijo (`k`, `M`, `+`, `$`) va en un
  `<span>` aparte, nunca pegado al número, o se duplica al animarse.
- Pie: `La herramienta` / `03 / 09`

---

### L4 · Así se ve dentro de un aula
- Eyebrow: `04 · En la práctica`
- H1: `Así se ve <em>dentro de un aula</em>`
- **Grabación de pantalla simulada** en HTML (no vídeo): panel izquierdo con `SESSIONS`,
  la sesión `taller-inventario` activa y `practica-arrays`, `portafolio-web` debajo;
  barra de estado `main ···` · `build` · `build mode · tab to switch` · `kimi-k2 · 12.4k tokens`;
  campo de entrada `BUILD` con cursor parpadeante. Un chat se **escribe a máquina** carácter
  a carácter, con mensajes del usuario y del asistente y un indicador de "pensando".
  Botón ↻ para **reiniciar la grabación**. La reproducir automáticamente al entrar en la
  lámina y detenerla al salir (`data-video="tape"`).
- Aviso: **Lo que hizo el estudiante, no la máquina** — `Dijo qué quería, corrigió el plan,
  revisó el resultado y preguntó el porqué. Esas cuatro cosas siguen siendo trabajo del alumno.`
- Pie: `En la práctica` / `04 / 09`

---

### L5 · La tecla Tab  *(la más importante)*
- Eyebrow: `05 · El detalle clave`
- H1: `Con una tecla se evita <em>copiar sin entender</em>`
- Dos columnas con filete superior (gris la izquierda, azul la derecha):
  - **MODO PLAN** + tecla `Tab` → **Pensar primero**
    - El programa **no puede escribir archivos**. Solo muestra su propuesta en pantalla.
    - Dice qué archivos va a crear o cambiar
    - Explica por qué eligió esa solución
    - El estudiante corrige lo que no le convence
  - **MODO BUILD** + tecla `Tab` → **Ejecutar lo acordado**
    - Ahora sí escribe dentro del proyecto, siguiendo exactamente el plan que el estudiante aprobó.
    - Aplica los cambios uno por uno
    - Muestra qué archivo modificó
    - Se deshace con `/undo` si no era lo esperado
- Aviso: **La diferencia está en quién decide** — `En Modo Plan el estudiante tiene que leer
  y corregir antes de ver el resultado. La IA deja de ser «la que hace la tarea» y pasa a ser
  «la que ayuda a revisar tu propia idea».`
- Pie: `El detalle clave` / `05 / 09`

---

### L6 · Cuatro usos en educación
- Eyebrow: `06 · Aplicaciones`
- H1: `Cuatro usos <em>en educación</em>`
- Bajada: `No es una herramienta del futuro: son cuatro cosas que se pueden aplicar el próximo lunes.`
- Cuatro tarjetas con filete de acento, numeradas `01`–`04`:
  1. **Tutor personal** — El alumno practica a su ritmo, sin ocupar al profesor ni quedarse esperando turno.
  2. **Explicar errores** — Se le pasa el mensaje de error y se le pide que lo explique *antes* de darle la solución.
  3. **Ejercicios a medida** — Genera más ejercicios del mismo tipo con otros datos, justo donde el alumno se equivocó.
  4. **Revisión de la tarea** — El alumno pide una revisión crítica y detecta lo que el profesor iba a marcar.
- Aviso: **Y para el profesor** — `Con /share el alumno entrega la conversación completa.
  El docente ya no solo ve el resultado: ve cómo llegó a él.`
- Pie: `Aplicaciones` / `06 / 09`

---

### L7 · Qué cambia para quien aprende y para quien enseña
- Eyebrow: `07 · El impacto`
- H1: `Qué cambia <em>para quien aprende y para quien enseña</em>`
- Dos columnas:
  - **EL ESTUDIANTE** (filete azul)
    - Practica a su ritmo, sin esperar turno ni esperar al día siguiente
    - Pregunta lo básico sin pena, que es la duda que nunca se atreve a hacer
    - Experimenta sin miedo, porque todo se puede deshacer con `/undo`
    - Aprende a formular bien lo que quiere: la habilidad más difícil
  - **EL DOCENTE** (filete gris)
    - Deja de repetir la misma explicación por quinta vez en el taller
    - Puede darle a cada alumno ejercicios distintos, con datos distintos
    - Con `/share` revisa el proceso, no solo el resultado
    - Dedica la clase a discutir y decidir, que es lo que solo él puede hacer
- Aviso: **El estudiante no pierde, cambia de lugar** — `Pasa de copiar la respuesta a
  evaluar la respuesta. Esa es la diferencia entre entender y memorizar.`
- Pie: `El impacto` / `07 / 09`

---

### L8 · Sus límites
- Eyebrow: `08 · Los límites`
- H1: `Lo que <em>tiene que resolver uno</em>`
- Bajada: `Una herramienta que solo tiene ventajas no es creíble. Estos son los cuatro problemas reales de OpenCode.`
- Cuatro tarjetas con filete **rojo**:
  1. **Puede resolverlo todo por ti** — El mayor riesgo: el alumno entrega un proyecto funcionando que no sabe explicar.
  2. **Se equivoca con seguridad** — A veces inventa funciones que no existen y lo dice como si fuera verdad.
  3. **El programa es gratis, la IA no siempre** — Los modelos más potentes son de pago, aunque existen opciones gratuitas.
  4. **El código sale de tu computadora** — Lo que escribes se envía al servidor del modelo que estés usando.
- Aviso rojo: **Pero el problema no son los límites: es no ponerlos** — `Con cuatro reglas
  sencillas —que son las mías— los cuatro riesgos de esta diapositiva desaparecen. Las menciono al final.`
- Pie: `Los límites` / `08 / 09`

---

### L9 · Conclusión y gracias — `class="slide end"`
- Eyebrow: `09 · Conclusión`
- H1: `Aplicada a la educación, OpenCode no reemplaza al estudiante: <em>lo acompaña</em>.`
- Cuatro reglas en **2×2** (no en 4 columnas: ahí el texto se parte y queda ilegible):
  1. **Nadie entrega algo que no pueda explicar** — Si no sabe explicar cada línea, todavía no es trabajo suyo.
  2. **Empezar siempre en Modo Plan** — Pedir el resultado terminado es saltarse el aprendizaje.
  3. **Preguntar siempre el porqué** — Es la pregunta que convierte un resultado en conocimiento.
  4. **Entregar también el proceso** — Con `/share` se ve cómo llegó a su respuesta.
- Chips al pie: `Sitio: opencode.ai` · `Código abierto: github.com/anomalyco/opencode` ·
  `Gracias por su atención · ¿Preguntas?`
- Pie: `Gracias por su atención` / `09 / 09`

---

# 6. ANIMACIONES

**Regla absoluta del proyecto: una sola animación por elemento.** Nunca apiles dos
animaciones que toquen la misma propiedad en el mismo nodo, y nunca combos
`animation-direction:reverse` + `animation-fill-mode:both`.

- **Cascada de entrada** (`cascade(slide)`): recorre los hijos directos de la lámina,
  los hijos de `.slide-head` y de `.body`, y asigna `--i` incremental. CSS:
  ```css
  .slide.active > *:not(.foot):not(.hud-corner),
  .slide.active .slide-head > *,
  .slide.active .body > *{
    animation:itemIn .78s cubic-bezier(.16,1,.3,1) both;
    animation-delay:calc(90ms + var(--i,0) * 78ms);
  }
  @keyframes itemIn{from{opacity:0;transform:translateY(26px);filter:blur(4px)}
                    to{opacity:1;transform:none;filter:blur(0)}}
  ```
- **Salida**: la lámina que se va recibe `.leaving` 300 ms y luego se le quita.
- **Filetes que se dibujan**: el guion del eyebrow (`width:0 → 26px`), el acento de cada
  tarjeta (`0 → 32px`), las reglas horizontales (`scaleX(.6 → 1)`), todos con retardo
  escalonado por `--i`.
- **Count-up** de las cifras de la lámina 3.
- **Sesión de OpenCode** de la lámina 4: el chat se escribe carácter a carácter con
  temporizadores cleaned al salir de la lámina.
- Los bucles ambientales (glows, grano) se detienen con
  `@media (prefers-reduced-motion: reduce)`. **No mates las animaciones de cascada** con
  esa misma regla: el usuario con movimiento reducido debe ver el contenido igual.

---

# 7. INTERACCIÓN

| Tecla | Acción |
|---|---|
| `→` / `Espacio` / `↓` / `PageDown` | siguiente |
| `←` / `↑` / `PageUp` | anterior |
| `Home` / `End` | primera / última |
| `F` | pantalla completa |
| `O` | vista general (cuadrícula de miniaturas) |
| `N` | notas del orador |
| `B` | modo en negro (pantalla negra, Esc para volver) |
| `?` | ayuda con los atajos |
| `R` | reinicia la lámina actual |

- **Barra de progreso** superior que crece con el índice.
- **Vista general** (`#overview`): miniaturas de las 9 láminas, la actual resaltada.
- **Notas del orador**: panel con `data-notes` de la lámina activa.
- Clic en los botones `‹` `›` de la esquina inferior derecha.
- Un `#watermark` discreto arriba: `OpenCode aplicado a la Educación · v10 · 9 diapositivas`.

### Reglas de navegación que ya fallaron antes — no las repitas
- Al cambiar de lámina, **quita `.active` de todas las demás**. Nunca puede haber dos
  láminas activas a la vez.
- El contador de lámina tiene **una sola fuente**: el `.foot` de cada `<section>`.
  No generes un `#pager` en JS.
- El reinicio tras la intro solo se dispara si `idx === 0`.
- Nunca uses `flex-shrink` en hijos directos de `.slide`: produce solapamientos en vez
  de desbordes visibles.

---

# 8. VERIFICACIÓN OBLIGATORIA ANTES DE ENTREGAR

No digas que está listo sin comprobarlo. Renderiza y **mira** cada una de las 9 láminas.

Método recomendado (determinista, sin teclado): genera copias temporales de `index.html`
inyectando antes de `</head>` un `<style>` que congele las animaciones y `#intro{display:none}`
más un script que aplique la clase `snap` a la lámina N, y captura cada una con:

```
msedge.exe --headless=new --disable-gpu --hide-scrollbars \
  --virtual-time-budget=4000 --window-size=1600,900 --screenshot=salida.png copia.html
```

Lista de comprobación por lámina:
- [ ] El contenido **llena el encuadre**: nada de bandas negras de más de ~60 px
      entre el subtítulo y el bloque principal, ni medio encuadre vacío.
- [ ] Ningún elemento toca o invade la banda del pie.
- [ ] Los títulos de 1 y 2 líneas quedan alineados entre columnas.
- [ ] Solo una lámina activa.
- [ ] Un solo contador de lámina.
- [ ] CSS balanceado (mismo número de `{` y de `}`), 9 `<section>`, 9 `data-notes`.
- [ ] Cero conflictos de animación y cero combinaciones `reverse` + `both`.

---

# 9. PUBLICAR EN GITHUB (solo cuando el usuario lo pida)

1. `git init` en la carpeta del proyecto, `git add .`, `git commit -m "Presentacion: OpenCode aplicado a la Educacion"`.
2. Pregunta al usuario su **usuario o URL de repositorio** antes de crear nada.
3. `gh repo create <nombre> --public --source . --push` (o `git remote add origin` + `git push -u origin main`).
4. Activa **GitHub Pages** desde *Settings → Pages → Deploy from a branch → main / root*.
5. La presentación es un HTML estático: funciona igual en Pages que local.

---

# 10. LO QUE NO DEBES HACER

- No añadas intro, no cambies el texto de las láminas, no inventes diapositivas nuevas.
- No pongas cuenta regresiva `8 · 7 · 6` en la intro.
- No añadas boxes, sombras, bordes redondeados grandes ni iconos: es minimalista.
- No uses color distinto del azul como acento en más de una lamina a la vez
  (el rojo solo aparece en la lámina 8).
- No metas jerga técnica.
- No subas nada a GitHub sin que te lo pidan.