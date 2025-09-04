# 8. Modificadores de color y estilos temáticos

**Objetivo:** Explicar de forma clara y básica cómo funcionan los colores y los estilos temáticos en Bootstrap, mostrar ejemplos prácticos y aplicarlos en Visual Studio Code para entenderlos desde cero.

---

## Introducción
En esta parte vamos a ver dos cosas muy importantes de Bootstrap:

1. **Colores:** cómo aplicar fácilmente colores a texto, fondos, bordes y componentes usando las utilidades que ya vienen con Bootstrap.  
2. **Estilos temáticos:** cómo funcionan los modos light/dark y cómo puedo cambiar los colores base de todo mi proyecto usando variables de Bootstrap.

Mi idea es que primero entendamos lo básico con ejemplos sencillos, y luego probemos un ejemplo completo que podemos ejecutar en nuestro Visual Studio Code.

---

## A) Colores

### 1. ¿Qué son los colores en Bootstrap?
Bootstrap trae una paleta de colores lista para usar en clases. Los principales son:

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
