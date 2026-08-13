# STABILITY — Guía de Estilo Visual (basada en Instagram @stability.ar)

## Identidad de marca
Marca de entrenamiento físico (Córdoba, Argentina). Tono: motivacional, serio, orientado a resultados reales ("El progreso no se improvisa"). Estética gym/fitness oscura y agresiva, no minimalista/pastel.

## Paleta de colores
- Azul marino oscuro (base/fondo principal): #1a2340 aprox (navy oscuro, casi negro azulado)
- Negro profundo (fondos de posteos y overlays): #0a0e1a aprox
- Rojo acento (energía, CTA, palabras clave): #d62f2f aprox (rojo intenso, no pastel)
- Azul acento secundario (íconos, callouts, líneas): #3b6fd6 aprox (azul eléctrico/medio)
- Blanco (texto principal sobre fondos oscuros): #ffffff
- Gris claro (texto secundario): #d0d0d0 aprox

Uso típico: fondo oscuro (navy/negro) + texto blanco en mayúsculas + UNA palabra o línea resaltada en rojo o azul para dar énfasis.

## Tipografía
- Titulares: sans-serif bold/heavy, todo en MAYÚSCULAS, muy compacto (letter-spacing negativo), tamaños grandes tipo "poster". Ejemplos vistos: "AHORA EN TU MANO", "LEVANTAR PESO", "TIPOS DE PERSONAS ENTRENANDO".
- Texto de apoyo: peso regular/medium, blanco o gris claro, tamaño bastante menor que el título.
- Wordmark "STABILITY": tipografía condensada/bold en mayúsculas, con el subtítulo "ENTRENAMIENTO" en versión pequeña debajo (letter-spacing amplio, tipo etiqueta).

## Logo
- Círculo blanco de fondo.
- Ícono de engranaje (gear) en azul marino oscuro.
- Flecha/trazo curvo en rojo cruzando el engranaje (sensación de movimiento/progreso).
- Se usa como foto de perfil y como marca de agua en las piezas gráficas.

## Iconografía (Historias Destacadas)
- Círculos con fondo azul marino oscuro casi negro.
- Íconos lineales (outline), trazo fino, en blanco/celeste claro: bíceps, cerebro con mancuerna, celular, barra con discos.
- Pequeño detalle de acento rojo (trazo corto) en la esquina superior de cada ícono circular.
- Estilo consistente: minimalista, técnico, "fitness app" más que "gimnasio de barrio".

## Estilo de las piezas gráficas (posts)
- Fondo: foto real de entrenamiento (gimnasio, pesas, ladrillo a la vista) oscurecida con overlay negro/navy para dar contraste al texto.
- Efecto de luz/gradiente rojo diagonal en varias piezas (sensación de energía/movimiento).
- Texto grande en mayúsculas ocupando gran parte del espacio, alineado a la izquierda.
- Callouts/anotaciones: círculos y flechas en azul eléctrico o rojo señalando partes del cuerpo o puntos de interés en la foto.
- Etiquetas pequeñas tipo pill/caption ("DESLIZA PARA VER", "PLANES") en rojo con texto blanco, esquina inferior.
- Fotos con personas reales entrenando (no stock genérico), ropa negra/oscura, ambiente de gimnasio real.

## Botones / CTAs (inferido del estilo general)
- Botón primario: fondo rojo o azul sólido, texto blanco, bold, mayúsculas o texto corto directo ("Comenzá ahora").
- Bordes rectos o levemente redondeados (no pill completo), consistente con la estética "gym poster" más que "app suave".

## Layout / sensación general
- Alto contraste, fondos oscuros predominantes.
- Fotografía real como protagonista, texto superpuesto grande.
- Un solo color de acento por pieza (rojo O azul), no ambos mezclados en el mismo texto.
- Nada de ilustraciones planas ni pastel — todo es fotográfico, crudo, "de gimnasio".

## Instrucciones para Claude
Al construir la landing page:
1. Usar fondo oscuro (navy/negro) como base del hero, con foto de entrenamiento real de fondo (o placeholder oscuro si no hay foto).
2. Titulares grandes en mayúsculas, bold, con una palabra clave resaltada en rojo.
3. Mantener paleta acotada: navy/negro + blanco + rojo como acento principal + azul como acento secundario (para íconos/detalles).
4. Reservar el círculo blanco con el logo (engranaje azul + flecha roja) para el header/nav.
5. Para íconos de features, usar estilo lineal fino sobre fondo oscuro circular, como en las historias destacadas.
6. Botones CTA sólidos (rojo o azul), texto blanco, bold, sin gradientes suaves ni pastel.

## PENDIENTE: Rediseñar la landing como Historias de Instagram

Objetivo: que navegar la landing se sienta exactamente como ver Historias de Instagram, para hacerla más fácil de "leer" y llegar mejor al usuario. Deben usarse **exactamente los mismos estilos visuales y de interacción que las Historias de Instagram reales** (no una versión libremente inspirada).

Cada sección actual de la landing (hero, sobre nosotros, planes, etc.) pasa a ser una "story"/slide dentro de este visor.

### Estilo visual (idéntico a IG Stories)
- Barra de progreso segmentada arriba de la pantalla, un segmento por slide/sección, que se va rellenando con el tiempo (o instantáneamente si el usuario navega manualmente).
- Header superior tipo story: foto de perfil circular (logo de Stability) + nombre de usuario ("stability.ar") + tiempo transcurrido, igual que en Instagram.
- Contenido a pantalla completa por slide (imagen/video de fondo + texto superpuesto), transición entre slides igual a IG (deslizamiento/fade rápido).
- Barra inferior tipo IG: campo de texto "Enviar mensaje" + ícono de corazón (like) + ícono de enviar/compartir (avioncito de papel), en la misma disposición que Instagram.

### Navegación (idéntica a IG Stories)
- Tocar/click en el **lado derecho** de la pantalla → avanza a la siguiente sección/slide.
- Tocar/click en el **lado izquierdo** de la pantalla → retrocede a la sección/slide anterior.
- Mantener presionado (long press) → pausa el avance automático, igual que Instagram.
- Swipe hacia abajo (mobile) → opcional, para cerrar/salir del modo historia si se implementa.

### Interacciones específicas
1. **Tap en el perfil** (foto/nombre arriba) → abre en pestaña nueva el perfil real de Instagram del gimnasio: `https://instagram.com/stability.ar`.
2. **Campo "Enviar mensaje" (responder la historia)** → al escribir/enviar, redirige a WhatsApp con mensaje directo prellenado usando el link `https://wa.me/5493512240889` (número: 3512 24-0889, con código de país 54 9 para Argentina). Se puede prellenar un texto tipo "Hola! Vi la historia de Stability y quiero más info".
3. **Botón de enviar (avioncito)** → dispara el share nativo del navegador (Web Share API) para compartir el link de la propia landing; si el navegador no soporta Web Share API, hacer fallback a copiar el link al portapapeles con confirmación visual.
4. **Corazón (like)** → toggle visual tipo IG (animación de "like", corazón se rellena de rojo/rebote), solo de interfaz, sin necesidad de persistencia en backend.

### Requisito técnico clave
Por detrás, la landing debe seguir funcionando como una **página web normal**: HTML/CSS/JS reales, contenido indexable por buscadores, sin depender de ningún SDK ni embed oficial de Instagram — únicamente se imita el estilo visual y el patrón de interacción de las Historias.
