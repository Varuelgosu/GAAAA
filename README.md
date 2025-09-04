# 8. Modificadores de color y estilos temáticos

**Objetivo:** Explicar de forma clara y básica cómo funcionan los colores y los estilos temáticos en Bootstrap para que puedas entenderlos desde cero, probar los ejemplos en Visual Studio Code y luego usar el contenido en tu Word o README.

---

## Introducción (qué veremos)
Este documento está pensado para principiantes. Lo dividimos en **dos apartados**:

- **A) Colores:** clases utilitarias (`.text-*`, `.bg-*`, `.border-*`), paleta estándar y cómo probar ejemplos rápidos.
- **B) Estilos temáticos:** variables CSS del tema (`--bs-*`), modos (light/dark) y temas scoped (`data-bs-theme`), además de un ejemplo sencillo para alternar temas.

Cada sección incluye explicaciones paso a paso y ejemplos listos para pegar en VS Code.

---

## A) COLORES (explicación básica y ejemplos)

### 1. ¿Qué son los "colores" en Bootstrap?
Bootstrap trae una **paleta de colores por defecto** pensada para usarse en botones, alertas, badges, fondos y texto. Los nombres principales son:

- `primary` (primario)
- `secondary` (secundario)
- `success` (éxito)
- `danger` (peligro/error)
- `warning` (advertencia)
- `info` (información)
- `light` y `dark` (fondo/texto base)

Cada uno se puede aplicar con utilidades ya listas.

---

### 2. Utilidades de texto
Clases principales:

- `.text-primary`, `.text-secondary`, `.text-success`, `.text-danger`, `.text-warning`, `.text-info`, `.text-light`, `.text-dark`.
- `.text-body` (usa el color de texto del body)
- `.text-muted` (texto con menor énfasis)

**Ejemplo (copia-pega en HTML):**

```html
<p class="text-primary">Este texto es .text-primary</p>
<p class="text-muted">Este texto es .text-muted (menos énfasis)</p>
```

**Paso a paso para probarlo:**
1. Abre Visual Studio Code.
2. Crea un archivo `index.html`.
3. Pega el ejemplo completo que viene al final de este documento (tiene el CDN de Bootstrap).
4. Abre en navegador (Live Server o doble clic) y observa los textos.

---

### 3. Utilidades de fondo
Clases principales:

- `.bg-primary`, `.bg-secondary`, `.bg-success`, `.bg-warning`, `.bg-info`, `.bg-light`, `.bg-dark`, `.bg-body`.
- `.text-bg-*` combina fondo + texto con contraste automático (útil para badges pequeños o etiquetas).
- Opacidad: `.bg-opacity-10`, `.bg-opacity-50` o usando la variable `--bs-bg-opacity`.

**Ejemplo:**

```html
<div class="bg-primary text-white p-2 rounded">Caja con .bg-primary</div>
<div class="text-bg-warning p-2 rounded mt-2">Caja con .text-bg-warning (contraste automático)</div>
```

**Nota:** cuando usas `.bg-*` recuerda ajustar el color del texto (por ejemplo `text-white`) si la clase no lo hace automáticamente.

---

### 4. Utilidades de borde y sombra
- `.border`, `.border-0`, `.border-top`, `.border-primary` (color de borde), `.border-opacity-50`.
- `.rounded`, `.rounded-circle` (esquinas redondeadas).
- `.shadow`, `.shadow-sm`, `.shadow-lg`.

**Ejemplo:**

```html
<div class="border border-success p-3 rounded shadow-sm">Caja con borde verde y sombra</div>
```

---

### 5. Componentes que usan colores del tema
Los botones, alerts, badges y otros componentes toman sus colores de la paleta de tema:

```html
<button class="btn btn-primary">Botón primario</button>
<button class="btn btn-outline-primary">Botón outline</button>
<span class="badge text-bg-info ms-2">Info</span>
<div class="alert alert-danger mt-3">Alerta danger</div>
```

Estos componentes reflejan los cambios si modificas las variables del tema (ver sección B).

---

## B) ESTILOS TEMÁTICOS (variables, modos y temas scoped)

### 1. ¿Qué es un "estilo temático"?
Un estilo temático es la forma de definir o cambiar los colores base de Bootstrap (por ejemplo el color primario, fondo del body, color de los bordes) de forma centralizada. Bootstrap expone variables CSS (prefijadas con `--bs-`) que puedes sobrescribir sin recompilar SASS.

### 2. Variables CSS importantes (lista breve)
- `--bs-primary` → color primario (ej. `#0d6efd`)
- `--bs-primary-rgb` → valor RGB sin `rgb()` (ej. `13,110,253`) — útil si hay transparencias
- `--bs-body-bg` → fondo del documento
- `--bs-body-color` → color del texto principal
- `--bs-border-color` → color por defecto de los bordes
- `--bs-bg-opacity` → opacidad aplicada a algunas utilidades de fondo

---

### 3. Sobrescribir variables en CSS (sin SASS)
Puedes redefinir variables directamente en `:root` o en un selector específico. Ejemplo:

```html
<style>
  :root {
    --bs-primary: #1a73e8;
    --bs-primary-rgb: 26,115,232;
    --bs-body-bg: #ffffff;
    --bs-body-color: #212529;
  }

  /* Tema scoped para un contenedor */
  [data-bs-theme="mi-tema"] {
    --bs-primary: #ff6b6b;
    --bs-primary-rgb: 255,107,107;
    --bs-body-bg: #0f1724;
    --bs-body-color: #e6eef8;
  }
</style>
```

**Qué pasa:** Después de definir esto, todas las utilidades y componentes que usan `--bs-primary` o `--bs-body-bg` tomarán los nuevos valores.

---

### 4. Cambiar variables en tiempo real (JavaScript)
Si quieres permitir que el usuario cambie colores durante la ejecución (por ejemplo con un color picker), puedes hacerlo con JavaScript:

```html
<script>
  const root = document.documentElement;
  function setPrimary(hex) {
    root.style.setProperty('--bs-primary', hex);
    // convertir hex a rgb (sin librerías)
    const v = hex.replace('#','');
    const bigint = parseInt(v, 16);
    const r = (bigint >> 16) & 255;
    const g = (bigint >> 8) & 255;
    const b = bigint & 255;
    root.style.setProperty('--bs-primary-rgb', `${r}, ${g}, ${b}`);
  }

  // ejemplo de uso: setPrimary('#ff8800');
</script>
```

---

### 5. Modos de color: light / dark (`data-bs-theme`)
Bootstrap (5.3+) soporta alternar modos aplicando el atributo `data-bs-theme`.

**Ejemplos:**

```html
<!-- Modo oscuro global -->
<html data-bs-theme="dark"> ... </html>

<!-- O en un contenedor específico -->
<div data-bs-theme="dark">Contenido en modo dark</div>
```

También puedes detectar la preferencia del sistema y aplicarlo con JavaScript:

```js
if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
  document.documentElement.setAttribute('data-bs-theme','dark');
}
```

---

### 6. Theming con SASS (nota breve)
Si trabajas con un pipeline (npm, webpack, Vite...) y usas SASS, lo ideal es redefinir `$theme-colors` antes de importar `bootstrap` para generar utilidades personalizadas:

```scss
$theme-colors: (
  "primary": #0d6efd,
  "success": #198754,
  // ...
);
@import "bootstrap";
```

Esto recompila todo el CSS con tus colores. Es más potente pero requiere configuración.

---

## Ejemplo completo (archivo `index.html`) — copia y prueba en VS Code

Crea `index.html` y pega esto (incluye CDN de Bootstrap):

```html
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Demo: Colores y Temas (Bootstrap)</title>
  <!-- Bootstrap CSS (CDN) -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    :root { --bs-primary: #0d6efd; --bs-primary-rgb: 13,110,253; }
    [data-bs-theme="sunset"] {
      --bs-primary: #ff7043; --bs-primary-rgb: 255,112,67; --bs-body-bg: #fff7f2; --bs-body-color: #2b2b2b;
    }
  </style>
</head>
<body class="p-4 bg-body">
  <h1 class="text-primary">Demo: Modificadores de color</h1>

  <section class="my-3">
    <h2 class="h6">Utilidades</h2>
    <p class="text-primary">.text-primary</p>
    <div class="bg-success text-white p-2 rounded mb-2">.bg-success</div>
    <div class="border border-warning p-2 rounded">.border-warning</div>
  </section>

  <section class="my-3">
    <h2 class="h6">Componentes</h2>
    <button class="btn btn-primary">Primario</button>
    <button class="btn btn-outline-primary">Outline</button>
    <span class="badge text-bg-info ms-2">Info</span>
    <div class="alert alert-danger mt-3">Alerta danger</div>
  </section>

  <section class="my-3">
    <h2 class="h6">Tema scoped</h2>
    <div data-bs-theme="sunset" class="p-3 rounded">
      <button class="btn btn-primary">Botón (sunset)</button>
      <div class="mt-2 text-bg-warning p-2 rounded">Sub elemento con contraste automático</div>
    </div>
  </section>

  <section class="my-3">
    <h2 class="h6">Cambiar primario con JS</h2>
    <input id="colorpicker" type="color" value="#0d6efd" class="form-control form-control-color w-auto d-inline-block">
    <button id="apply" class="btn btn-sm btn-secondary ms-2">Aplicar</button>
    <button id="toggleTheme" class="btn btn-sm btn-outline-secondary ms-2">Toggle light/dark</button>
  </section>

  <!-- Bootstrap JS (CDN) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
  <script>
    const root = document.documentElement;
    const picker = document.getElementById('colorpicker');
    const apply = document.getElementById('apply');
    const toggle = document.getElementById('toggleTheme');

    apply.addEventListener('click', () => {
      const hex = picker.value;
      root.style.setProperty('--bs-primary', hex);
      const v = hex.replace('#','');
      const bigint = parseInt(v, 16);
      const r = (bigint >> 16) & 255;
      const g = (bigint >> 8) & 255;
      const b = bigint & 255;
      root.style.setProperty('--bs-primary-rgb', `${r}, ${g}, ${b}`);
    });

    toggle.addEventListener('click', () => {
      const current = root.getAttribute('data-bs-theme') || 'light';
      root.setAttribute('data-bs-theme', current === 'light' ? 'dark' : 'light');
    });
  </script>
</body>
</html>
```

**Cómo probar:**
1. Guarda `index.html` en una carpeta.
2. Abre la carpeta con Visual Studio Code.
3. Instala y usa Live Server (opcional) o abre el archivo en tu navegador.
4. Prueba cambiar el color con el color picker y alternar el tema.

---

## Errores comunes y soluciones rápidas
- **No ves cambios al cambiar `--bs-primary`:** comprueba si otra regla CSS tiene más prioridad (usa `:root` o un selector más específico). También actualiza `--bs-primary-rgb` si tu estilo usa valores RGB.
- **Mal contraste en modo dark:** define `--bs-body-bg` y `--bs-body-color` en tu tema dark.
- **Cambio no aplicado a componentes compilados con SASS:** si usas una versión compilada generada por SASS, asegúrate de que no existan estilos en línea o reglas con mayor especificidad.

---

## Ejercicios sugeridos (para practicar antes de pasar al Word)
1. Cambia `--bs-primary` y observa qué componentes se actualizan.
2. Crea un tema `data-bs-theme="mi-tema"` con colores diferentes y aplícalo a un `div`.
3. Ajusta `--bs-bg-opacity` para un bloque `.bg-primary` y observa la opacidad.
4. Implementa la detección `prefers-color-scheme` para activar dark mode automáticamente.

---

## Notas de accesibilidad y buenas prácticas
- Comprueba siempre el contraste (WCAG) cuando cambies colores.
- No uses solo color para transmitir información: agrega texto o íconos y `aria-labels` cuando aplique.
- Prefiere modificar variables (`--bs-*`) y `data-bs-theme` en lugar de cambiar muchas clases manualmente.

---

Si quieres, ahora puedo:

- Exportar este contenido a un archivo `.docx` listo para descargar (te preparo el archivo). 
- Convertirlo a `README.md` cuando estés listo.

Dime cuál prefieres y lo hago enseguida.
