# Guía Completa de Atajos de Teclado

## Atajos para Windows/Linux | macOS

La mayoría de estos atajos funcionan en **Visual Studio Code**, **Windsurf** y **Cursor**, ya que Windsurf y Cursor están basados en VS Code.

---

## 🎯 EDICIÓN MULTI-CURSOR (El que buscas)

### Seleccionar y editar múltiples líneas simultáneamente

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Alt + Click` | `Option + Click` | Añade un cursor en cada posición donde hagas click |
| `Ctrl + Alt + ↑/↓` | `Cmd + Option + ↑/↓` | Añade cursor arriba/abajo de la línea actual |
| `Ctrl + D` | `Cmd + D` | Selecciona la siguiente coincidencia de la palabra actual |
| `Ctrl + Shift + L` | `Cmd + Shift + L` | Selecciona TODAS las coincidencias de la palabra actual |
| `Alt + Shift + I` | `Option + Shift + I` | Añade cursores al final de cada línea seleccionada |
| `Ctrl + U` | `Cmd + U` | Deshace la última operación de cursor |

**Ejemplo práctico:**
```
Tienes estas líneas:
const nombre = "Juan"
const apellido = "Pérez"
const edad = 25

1. Selecciona las tres líneas
2. Presiona Alt + Shift + I
3. Ahora puedes escribir al final de todas a la vez (por ejemplo, añadir punto y coma)
```

---

## ✂️ EDICIÓN BÁSICA

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Ctrl + X` | `Cmd + X` | Cortar línea (sin seleccionar) |
| `Ctrl + C` | `Cmd + C` | Copiar línea (sin seleccionar) |
| `Ctrl + V` | `Cmd + V` | Pegar |
| `Ctrl + Z` | `Cmd + Z` | Deshacer |
| `Ctrl + Y` | `Cmd + Shift + Z` | Rehacer |
| `Ctrl + Shift + K` | `Cmd + Shift + K` | Eliminar línea completa |
| `Alt + ↑/↓` | `Option + ↑/↓` | Mover línea arriba/abajo |
| `Shift + Alt + ↑/↓` | `Shift + Option + ↑/↓` | Copiar línea arriba/abajo |
| `Ctrl + /` | `Cmd + /` | Comentar/descomentar línea |
| `Shift + Alt + A` | `Shift + Option + A` | Comentario de bloque /* */ |
| `Ctrl + ]` | `Cmd + ]` | Indentar línea |
| `Ctrl + [` | `Cmd + [` | Des-indentar línea |

---

## 🔍 BÚSQUEDA Y REEMPLAZO

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Ctrl + F` | `Cmd + F` | Buscar en archivo actual |
| `Ctrl + H` | `Cmd + Option + F` | Buscar y reemplazar |
| `Ctrl + Shift + F` | `Cmd + Shift + F` | Buscar en todos los archivos |
| `Ctrl + Shift + H` | `Cmd + Shift + H` | Reemplazar en todos los archivos |
| `F3` | `Cmd + G` | Ir a siguiente coincidencia |
| `Shift + F3` | `Cmd + Shift + G` | Ir a anterior coincidencia |
| `Alt + Enter` | `Option + Enter` | Seleccionar todas las coincidencias |

---

## 📂 NAVEGACIÓN DE ARCHIVOS

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Ctrl + P` | `Cmd + P` | Búsqueda rápida de archivos |
| `Ctrl + Tab` | `Ctrl + Tab` | Cambiar entre archivos abiertos |
| `Ctrl + W` | `Cmd + W` | Cerrar archivo actual |
| `Ctrl + Shift + T` | `Cmd + Shift + T` | Reabrir archivo cerrado |
| `Ctrl + K Ctrl + W` | `Cmd + K Cmd + W` | Cerrar todos los archivos |
| `Ctrl + \` | `Cmd + \` | Dividir editor |
| `Ctrl + 1/2/3` | `Cmd + 1/2/3` | Enfocar grupo de editor 1, 2 o 3 |
| `Ctrl + B` | `Cmd + B` | Mostrar/ocultar barra lateral |

---

## 🎬 NAVEGACIÓN EN EL CÓDIGO

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Ctrl + G` | `Cmd + G` | Ir a línea específica |
| `Ctrl + Shift + O` | `Cmd + Shift + O` | Ir a símbolo (función, clase, etc.) |
| `Ctrl + T` | `Cmd + T` | Buscar símbolo en todo el proyecto |
| `F12` | `F12` | Ir a definición |
| `Alt + F12` | `Option + F12` | Ver definición (peek) |
| `Ctrl + K F12` | `Cmd + K F12` | Abrir definición al lado |
| `Shift + F12` | `Shift + F12` | Ver referencias |
| `Ctrl + Shift + \` | `Cmd + Shift + \` | Ir a paréntesis/corchete coincidente |
| `Ctrl + Home` | `Cmd + ↑` | Ir al inicio del archivo |
| `Ctrl + End` | `Cmd + ↓` | Ir al final del archivo |

---

## ✏️ SELECCIÓN DE TEXTO

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Shift + ←/→` | `Shift + ←/→` | Seleccionar carácter a carácter |
| `Ctrl + Shift + ←/→` | `Option + Shift + ←/→` | Seleccionar palabra a palabra |
| `Shift + ↑/↓` | `Shift + ↑/↓` | Seleccionar línea arriba/abajo |
| `Ctrl + Shift + Home` | `Cmd + Shift + ↑` | Seleccionar hasta el inicio |
| `Ctrl + Shift + End` | `Cmd + Shift + ↓` | Seleccionar hasta el final |
| `Ctrl + A` | `Cmd + A` | Seleccionar todo |
| `Shift + Alt + →` | `Ctrl + Shift + →` | Expandir selección |
| `Shift + Alt + ←` | `Ctrl + Shift + ←` | Contraer selección |
| `Ctrl + L` | `Cmd + L` | Seleccionar línea completa |

---

## 🖥️ TERMINAL INTEGRADA

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `` Ctrl + ` `` | `` Cmd + ` `` | Mostrar/ocultar terminal |
| `` Ctrl + Shift + ` `` | `` Ctrl + Shift + ` `` | Crear nueva terminal |
| `Ctrl + Shift + 5` | `Cmd + Shift + 5` | Dividir terminal |

---

## 🐛 DEPURACIÓN

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `F5` | `F5` | Iniciar/continuar depuración |
| `Shift + F5` | `Shift + F5` | Detener depuración |
| `F9` | `F9` | Alternar punto de interrupción |
| `F10` | `F10` | Pasar sobre (step over) |
| `F11` | `F11` | Entrar en (step into) |
| `Shift + F11` | `Shift + F11` | Salir de (step out) |

---

## 🎨 INTERFAZ Y VISTAS

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Ctrl + Shift + P` | `Cmd + Shift + P` | Paleta de comandos |
| `Ctrl + Shift + N` | `Cmd + Shift + N` | Nueva ventana |
| `Ctrl + Shift + W` | `Cmd + Shift + W` | Cerrar ventana |
| `Ctrl + K Z` | `Cmd + K Z` | Modo Zen (sin distracciones) |
| `Ctrl + =` | `Cmd + =` | Aumentar zoom |
| `Ctrl + -` | `Cmd + -` | Disminuir zoom |
| `Ctrl + Shift + E` | `Cmd + Shift + E` | Mostrar explorador |
| `Ctrl + Shift + F` | `Cmd + Shift + F` | Mostrar búsqueda |
| `Ctrl + Shift + G` | `Cmd + Shift + G` | Mostrar control de código fuente |
| `Ctrl + Shift + D` | `Cmd + Shift + D` | Mostrar depuración |
| `Ctrl + Shift + X` | `Cmd + Shift + X` | Mostrar extensiones |

---

## 🔧 REFACTORIZACIÓN

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `F2` | `F2` | Renombrar símbolo |
| `Ctrl + .` | `Cmd + .` | Acciones rápidas (Quick Fix) |
| `Shift + Alt + F` | `Shift + Option + F` | Formatear documento |
| `Ctrl + K Ctrl + F` | `Cmd + K Cmd + F` | Formatear selección |

---

## 📝 SNIPPETS Y AUTOCOMPLETADO

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Ctrl + Space` | `Ctrl + Space` | Activar sugerencias |
| `Ctrl + Shift + Space` | `Cmd + Shift + Space` | Información de parámetros |
| `Tab` | `Tab` | Aceptar sugerencia/expandir snippet |
| `Ctrl + I` | `Cmd + I` | Activar IA inline (Cursor) |

---

## 🌟 ATAJOS ESPECÍFICOS DE CURSOR

Cursor añade algunos atajos específicos para IA:

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Ctrl + K` | `Cmd + K` | Abrir chat de Cursor |
| `Ctrl + L` | `Cmd + L` | Abrir chat con contexto del archivo |
| `Ctrl + I` | `Cmd + I` | Edición inline con IA |
| `Ctrl + Shift + L` | `Cmd + Shift + L` | Añadir selección al chat |

---

## 🌊 ATAJOS ESPECÍFICOS DE WINDSURF

Windsurf también incluye características de IA:

| Atajo Windows/Linux | Atajo macOS | Función |
|---------------------|-------------|---------|
| `Ctrl + L` | `Cmd + L` | Abrir panel de Cascade (IA) |
| `Ctrl + Shift + L` | `Cmd + Shift + L` | Añadir contexto al chat |
| `Ctrl + Enter` | `Cmd + Enter` | Enviar mensaje al chat de IA |

---

## 💡 TIPS Y TRUCOS

### Multi-cursor avanzado
**Seleccionar ocurrencias progresivamente:**
1. Coloca el cursor en una palabra
2. Presiona `Ctrl + D` (o `Cmd + D`) repetidamente
3. Cada vez seleccionará la siguiente ocurrencia
4. Edita todas a la vez

**Seleccionar todas las ocurrencias:**
1. Selecciona una palabra
2. Presiona `Ctrl + Shift + L` (o `Cmd + Shift + L`)
3. Se seleccionan TODAS las ocurrencias en el archivo

### Mover código rápidamente
- `Alt + ↑/↓` mueve líneas completas sin cortar/pegar
- `Shift + Alt + ↑/↓` duplica líneas instantáneamente

### Búsqueda inteligente de archivos
- `Ctrl + P` y escribe parte del nombre
- Añade `:` seguido de número de línea: `archivo.js:25`
- Añade `@` para buscar símbolos: `@nombreFuncion`

### Edición de columnas
1. Mantén `Alt + Shift` (o `Option + Shift`)
2. Arrastra con el ratón verticalmente
3. Crea una selección rectangular perfecta

### Paleta de comandos
- `Ctrl + Shift + P` (o `Cmd + Shift + P`) es tu mejor amigo
- Escribe cualquier acción que quieras hacer
- Ejemplo: "format", "theme", "preferences"

---

## 🎓 EJERCICIOS PRÁCTICOS

### Ejercicio 1: Multi-cursor básico
```javascript
const nombre = "Juan";
const apellido = "Pérez";
const edad = 25;
```
**Tarea:** Añade punto y coma al final de todas las líneas usando multi-cursor.

### Ejercicio 2: Refactorización rápida
```javascript
const userName = "admin";
console.log(userName);
alert(userName);
```
**Tarea:** Renombra `userName` a `username` en todas partes usando `F2`.

### Ejercicio 3: Edición masiva
```html
<div>Texto 1</div>
<div>Texto 2</div>
<div>Texto 3</div>
```
**Tarea:** Selecciona "Texto" en las tres líneas usando `Ctrl + D` y cámbialo por "Contenido".

---

## 📌 RECORDATORIOS

- **Los atajos son personalizables**: Ve a `Archivo > Preferencias > Atajos de teclado` (Windows/Linux) o `Code > Preferencias > Atajos de teclado` (macOS)
- **Practica los más útiles**: No necesitas memorizar todos, empieza con 5-10 que uses frecuentemente
- **Multi-cursor es el más poderoso**: Dominar esto te hará 10x más rápido
- **Usa la paleta de comandos**: Cuando no recuerdes un atajo, `Ctrl/Cmd + Shift + P` es tu salvavidas

## 🚀 LOS 10 ATAJOS ESENCIALES PARA EMPEZAR

Si solo vas a memorizar 10, que sean estos:

1. `Ctrl/Cmd + P` - Búsqueda rápida de archivos
2. `Ctrl/Cmd + Shift + P` - Paleta de comandos
3. `Ctrl/Cmd + D` - Seleccionar siguiente ocurrencia
4. `Alt/Option + ↑/↓` - Mover líneas
5. `Ctrl/Cmd + /` - Comentar/descomentar
6. `Alt/Cmd + Click` - Multi-cursor
7. `Ctrl/Cmd + F` - Buscar
8. `F2` - Renombrar símbolo
9. `` Ctrl/Cmd + ` `` - Mostrar terminal
10. `Ctrl/Cmd + B` - Ocultar/mostrar sidebar

¡Practica estos atajos y verás cómo tu productividad se dispara! 🎯