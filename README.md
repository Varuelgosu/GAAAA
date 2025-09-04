# 8. Modificadores de color y estilos temáticos

En esta parte vamos a ver dos cosas muy importantes de Bootstrap:

1. **Colores:** cómo aplicar fácilmente colores a texto, fondos, bordes y componentes usando las utilidades que ya vienen con Bootstrap.  
2. **Estilos temáticos:** cómo funcionan los modos light/dark y cómo se puede cambiar los colores base de todo el proyecto usando variables de Bootstrap.

[![imagen10](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fyctov28ajeuwfmkpgq19.png "imagen10")](http://https://dev.to/ijash/customizing-bootstrap-5-color-theme-in-create-react-app-48d7 "imagen10")

---

## A) Colores

### 1. ¿Qué son los colores en Bootstrap?
Bootstrap trae una paleta de colores lista para usar en clases. Los principales:

- `primary` (azul por defecto)
- `secondary` (gris)
- `success` (verde)
- `danger` (rojo)
- `warning` (amarillo)
- `info` (celeste)
- `light` (fondo claro)
- `dark` (fondo oscuro)

Con esto puedo dar estilo rápidamente sin escribir CSS.

---

### 2. Colores en texto
Para cambiar el color del texto uso `.text-*`. Ejemplo:

```html
<p class="text-primary">Texto primario</p>
<p class="text-success">Texto de éxito</p>
<p class="text-danger">Texto de peligro</p>
<p class="text-muted">Texto con menos énfasis</p>
```
![imagen11](fotos/imagen11.png)

##### Aquí cada línea toma el color automáticamente según la clase usada.
##### .text-muted es especial, porque sirve para darle menos importancia visual al texto.

---

### 3. Colores de fondo

Bootstrap también permite cambiar el color de los fondos de forma muy rápida con las clases `.bg-*`.  
Estas se combinan con clases de texto (`.text-*`) para asegurar que el contraste sea correcto.

### Ejemplo:

```html
<div class="bg-primary text-white p-2 rounded">Fondo azul con texto blanco</div>
<div class="bg-warning text-dark p-2 rounded">Fondo amarillo con texto oscuro</div>
<div class="text-bg-success p-2 rounded">Fondo verde con contraste automático</div>
```
![imagen12](fotos/imagen12.png)

##### Notamos que .text-bg-* ajusta automáticamente el color del texto para que siempre sea legible.

---

## 4. Bordes y sombras

Bootstrap incluye utilidades para bordes y sombras que facilitan la personalización visual de tus elementos:

```html
<div class="border border-success p-3 mb-2 rounded">
  Caja con borde verde y esquinas redondeadas
</div>
<div class="border border-danger p-3 mb-2 shadow-sm">
  Caja con borde rojo y sombra pequeña
</div>
<div class="border border-primary p-3 shadow-lg">
  Caja con borde azul y sombra grande
</div>
```
![imagen13](fotos/imagen13.png)

- ✅ `.border-*` aplica color al borde.
- ✅ `.shadow-*` (`sm`, normal, `lg`) agrega distintos niveles de sombra.

---

## 5. Colores en componentes

Bootstrap permite aplicar colores directamente a componentes como botones, alertas y badges:

```html
<button class="btn btn-primary">Botón primario</button>
<button class="btn btn-outline-danger">Botón outline danger</button>

<div class="alert alert-warning mt-3">Alerta de advertencia</div>
<div class="alert alert-success">Alerta de éxito</div>

<span class="badge text-bg-info">Etiqueta info</span>
<span class="badge text-bg-dark">Etiqueta dark</span>
```
![imagen14](fotos/imagen14.png)

👉 Esto permite construir interfaces rápidas con un estilo consistente.

---

## B) Estilos temáticos

### 1. ¿Qué es un estilo temático?

Bootstrap usa variables CSS personalizadas (`--bs-*`) para manejar los colores principales del framework.
Estas variables controlan el color base de botones, fondos, textos y componentes.

👉 Si cambio una sola variable, ¡todo el tema se actualiza!

---

### 2. Variables más comunes

Algunas de las más usadas son:

- `--bs-primary`: color principal
- `--bs-secondary`: color secundario
- `--bs-body-bg`: color de fondo del body
- `--bs-body-color`: color de texto del body
- `--bs-border-color`: color de los bordes

---

### 3. Personalizar variables en CSS

Puedes sobrescribir las variables en tu archivo CSS o dentro de un `<style>`:

```html
<style>
  :root {
    --bs-primary: #e91e63;  /* rosa */
    --bs-body-bg: #f9f9f9;  /* amarillo */
    --bs-body-color: #212121; /* texto oscuro */
  }
</style>
```
![imagen15](fotos/imagen15.png)

![imagen16](fotos/imagen16.png)

👉 A partir de aquí, cualquier elemento con `btn-primary`, `text-primary` o `bg-primary` se pintará con el nuevo color.

---

### 4. Modo Light y Dark

Bootstrap permite aplicar un tema claro u oscuro usando `data-bs-theme`.

**Ejemplo global:**
```html
<html data-bs-theme="dark">
  <body class="p-3">
    <button class="btn btn-primary">Botón en dark mode</button>
  </body>
</html>
```
![imagen17](fotos/imagen17.png)

**Ejemplo por secciones:**
```html
<div data-bs-theme="light" class="p-3">
  Sección en modo claro
</div>

<div data-bs-theme="dark" class="p-3 mt-2">
  Sección en modo oscuro
</div>
```
![imagen18](fotos/imagen18.png)

👉 Con estos dos ejemplos puedes ver la diferencia entre aplicar el tema a toda la página o solo a secciones específicas.

---

### 5. Crear un tema propio

Puedes definir un tema especial con `data-bs-theme` y variables personalizadas:

```html
<style>
  [data-bs-theme="sunset"] {
    --bs-primary: #ff7043;  /* naranja atardecer */
    --bs-body-bg: #fff3e0; /* fondo cálido */
    --bs-body-color: #3e2723; /* texto marrón oscuro */
  }
</style>

<div data-bs-theme="sunset" class="p-3">
  <button class="btn btn-primary">Botón con tema Sunset</button>
</div>
```
![imagen19](fotos/imagen19.png)
---

### 6. Cambiar colores dinámicamente con JavaScript

También puedes manipular las variables con JS:

```html
<script>
  const root = document.documentElement;

  function cambiarPrimario(color) {
    root.style.setProperty('--bs-primary', color);
  }

  // Ejemplo: cambiarPrimario('#4caf50'); -> lo vuelve verde
</script>
```
![imagen20](fotos/imagen20.png)
👉 Esto es útil si quieres que el usuario pueda elegir el color principal desde un “selector de color”.

---

# 9. Diseño responsivo avanzado con media queries

En esta sección se explica cómo funciona el diseño responsivo en **Bootstrap** y cómo aprovechar las **media queries** para adaptar el sitio a diferentes tamaños de pantalla.

La idea es entender primero los **breakpoints de Bootstrap**, luego ver ejemplos de uso con utilidades, y finalmente aprender cómo crear **media queries personalizadas** para casos avanzados.

---

## A) Introducción al diseño responsivo

El **diseño responsivo** significa que una página web se ve bien en **móviles, tablets y computadoras**, ajustándose automáticamente.

Bootstrap tiene un sistema de **grid** y clases utilitarias basadas en **media queries** que facilitan este trabajo.

---

## B) Breakpoints en Bootstrap

Bootstrap define puntos de corte (*breakpoints*) que corresponden a los tamaños más comunes de pantallas:

| Tamaño              | Prefijo      | Valor mínimo |
|---------------------|--------------|--------------|
| Extra pequeño       | (sin prefijo)| <576px       |
| Pequeño             | `sm`         | ≥576px       |
| Mediano             | `md`         | ≥768px       |
| Grande              | `lg`         | ≥992px       |
| Extra grande        | `xl`         | ≥1200px      |
| Extra extra grande  | `xxl`        | ≥1400px      |

![imagen21](fotos/imagen21.png)

👉 Con estos breakpoints, Bootstrap cambia el diseño según el ancho de la pantalla.

---

## C) Ejemplo básico de grid responsivo

Usamos los breakpoints para organizar el contenido:

```html
<div class="container text-center">
  <div class="row">
    <div class="col-12 col-md-6 col-lg-4 bg-primary text-white p-3">Columna 1</div>
    <div class="col-12 col-md-6 col-lg-4 bg-success text-white p-3">Columna 2</div>
    <div class="col-12 col-md-12 col-lg-4 bg-warning text-dark p-3">Columna 3</div>
  </div>
</div>
```

**Explicación:**

- En pantallas pequeñas (`col-12`): cada columna ocupa todo el ancho (una debajo de otra).
- En pantallas medianas (`col-md-6`): aparecen dos columnas por fila.
- En pantallas grandes (`col-lg-4`): aparecen tres columnas en la misma fila.

![imagen23](fotos/imagen23.png)
![imagen24](fotos/imagen24.png)
![imagen22](fotos/imagen22.png)
✅ Esto demuestra cómo el layout cambia automáticamente con media queries.

---

## D) Clases utilitarias responsivas

Bootstrap tiene muchas utilidades que funcionan con los prefijos de breakpoint.

### 1. Mostrar/ocultar elementos

```html
<p class="d-none d-md-block">Este texto solo aparece en pantallas medianas en adelante.</p>
<p class="d-block d-md-none">Este texto solo aparece en pantallas pequeñas.</p>
```
![imagen26](fotos/imagen26.png)

![imagen25](fotos/imagen25.png)

👉 Esto se usa mucho para mostrar distintos menús en móvil y escritorio.

### 2. Alineación de texto

```html
<p class="text-center text-md-start">
  Este texto está centrado en móviles pero alineado a la izquierda en pantallas medianas y grandes.
</p>
```
![imagen29](fotos/imagen29.png)

![imagen30](fotos/imagen30.png)

---

### 3. Espaciado (padding y margin)

```html
<div class="p-2 p-md-5 bg-light border">
  Caja con poco padding en móvil, pero con mucho padding en pantallas medianas en adelante.
</div>
```
![imagen27](fotos/imagen27.png)

![imagen28](fotos/imagen28.png)

---

## E) Media queries personalizadas

A veces necesitamos escribir nuestras propias reglas en CSS para casos específicos:

```html
<style>
  /* Para pantallas menores a 768px */
  @media (max-width: 767px) {
    body {
      background-color: #f8bbd0; /* rosado */
    }
  }

  /* Para pantallas grandes (≥992px) */
  @media (min-width: 992px) {
    body {
      background-color: #bbdefb; /* celeste */
    }
  }
</style>
```

👉 Con esto, el fondo de la página cambia de color según el tamaño de pantalla.

![imagen31](fotos/imagen31.png)

![imagen32](fotos/imagen32.png)

![imagen33](fotos/imagen33.png)

---

# 10. Integración con JavaScript (Tooltips, Dropdowns, Carousels)

En esta última parte se explica cómo **Bootstrap integra JavaScript** en algunos de sus componentes más comunes: **Tooltips, Dropdowns y Carousels**.

Estos componentes necesitan **Bootstrap JS** para funcionar. Recuerda incluir este script al final del `<body>`:

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

---

## A) Tooltips

### 1. ¿Qué es un tooltip?

Un tooltip es un pequeño cuadro de texto que aparece cuando pasas el mouse sobre un elemento. Sirve para mostrar información adicional de forma discreta.

### 2. Ejemplo básico

```html
<button type="button" class="btn btn-primary" data-bs-toggle="tooltip" data-bs-title="Este es un tooltip">
  Pasa el mouse aquí
</button>
```
![imagen34](fotos/imagen34.png)

![imagen35](fotos/imagen35.png)

![imagen36](fotos/imagen36.png)

### 3. Inicialización con JavaScript

Bootstrap requiere activar los tooltips con JavaScript:

```html
<script>
  const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
  const tooltipList = [...tooltipTriggerList].map(el => new bootstrap.Tooltip(el));
</script>
```

✅ Ahora, cada vez que pases el cursor sobre el botón, verás el tooltip.

---

## B) Dropdowns

### 1. ¿Qué es un dropdown?

Un dropdown es un menú desplegable que aparece al hacer clic en un botón. Es útil para mostrar opciones adicionales sin ocupar mucho espacio.

### 2. Ejemplo básico

```html
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" data-bs-toggle="dropdown">
    Menú desplegable
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#">Opción 1</a></li>
    <li><a class="dropdown-item" href="#">Opción 2</a></li>
    <li><a class="dropdown-item" href="#">Opción 3</a></li>
  </ul>
</div>
```
![imagen37](fotos/imagen37.png)

![imagen38](fotos/imagen38.png)

![imagen39](fotos/imagen39.png)

👉 No necesitas código adicional en JS, Bootstrap lo activa automáticamente gracias al `data-bs-toggle="dropdown"`.

---

## C) Carousels

### 1. ¿Qué es un carousel?

Un carousel es un slider que muestra varias imágenes o contenido en pase automático o con controles de navegación.

### 2. Ejemplo básico

```html
<div id="demoCarousel" class="carousel slide" data-bs-ride="carousel">
  
  <!-- Indicadores -->
  <div class="carousel-indicators">
    <button type="button" data-bs-target="#demoCarousel" data-bs-slide-to="0" class="active"></button>
    <button type="button" data-bs-target="#demoCarousel" data-bs-slide-to="1"></button>
    <button type="button" data-bs-target="#demoCarousel" data-bs-slide-to="2"></button>
  </div>

  <!-- Imágenes -->
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img src="https://picsum.photos/800/300?random=1" class="d-block w-100" alt="Imagen 1">
    </div>
    <div class="carousel-item">
      <img src="https://picsum.photos/800/300?random=2" class="d-block w-100" alt="Imagen 2">
    </div>
    <div class="carousel-item">
      <img src="https://picsum.photos/800/300?random=3" class="d-block w-100" alt="Imagen 3">
    </div>
  </div>

  <!-- Controles -->
  <button class="carousel-control-prev" type="button" data-bs-target="#demoCarousel" data-bs-slide="prev">
    <span class="carousel-control-prev-icon"></span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#demoCarousel" data-bs-slide="next">
    <span class="carousel-control-next-icon"></span>
  </button>
</div>
```
![imagen40](fotos/imagen40.png)

![imagen41](fotos/imagen41.png)

👉 Este ejemplo crea un carrusel con indicadores, cuatro imágenes y controles de navegación.
