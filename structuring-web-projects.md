# Guía de Organización de Proyectos Web

## Estructura Básica Recomendada

```
mi-proyecto/
│
├── index.html
├── README.md
│
├── css/
│   ├── main.css
│   ├── reset.css
│   └── components/
│       ├── header.css
│       ├── footer.css
│       └── buttons.css
│
├── js/
│   ├── main.js
│   ├── utils.js
│   └── components/
│       ├── modal.js
│       ├── slider.js
│       └── form-validation.js
│
├── assets/
│   ├── images/
│   │   ├── logo.png
│   │   ├── icons/
│   │   └── backgrounds/
│   │
│   ├── fonts/
│   │   └── custom-font.woff2
│   │
│   └── videos/
│       └── intro.mp4
│
└── pages/
    ├── about.html
    ├── contact.html
    └── services.html
```

## Descripción de Carpetas

### **Raíz del Proyecto**
- **index.html**: Página principal de entrada
- **README.md**: Documentación del proyecto (descripción, instrucciones, créditos)

### **css/** - Estilos
Contiene todos los archivos CSS organizados por propósito:
- **main.css**: Estilos principales y globales
- **reset.css** o **normalize.css**: Reset de estilos por defecto del navegador
- **components/**: Estilos específicos para componentes reutilizables

### **js/** - JavaScript
Agrupa toda la lógica y funcionalidad:
- **main.js**: Punto de entrada principal del JavaScript
- **utils.js**: Funciones auxiliares y utilidades
- **components/**: Scripts para componentes específicos (modales, sliders, etc.)

### **assets/** - Recursos Multimedia
Almacena todos los archivos estáticos:
- **images/**: Imágenes del sitio, organizadas por tipo o sección
- **fonts/**: Tipografías personalizadas
- **videos/**: Archivos de video
- **docs/**: PDFs u otros documentos descargables

### **pages/** - Páginas Adicionales
Páginas HTML secundarias del sitio (sobre nosotros, contacto, etc.)

## Convenciones de Nomenclatura

### Archivos y Carpetas
- Usa **minúsculas** y **guiones** para separar palabras: `about-us.html`, `hero-section.css`
- Sé **descriptivo** pero **conciso**: `user-profile.js` en lugar de `up.js`
- Evita caracteres especiales y espacios

### Código
**HTML:**
- IDs: `camelCase` → `id="mainNavigation"`
- Clases: `kebab-case` → `class="btn-primary"`

**CSS:**
- Clases: `kebab-case` → `.header-container`
- Variables CSS: `--color-primary`, `--spacing-large`

**JavaScript:**
- Variables y funciones: `camelCase` → `userName`, `getUserData()`
- Constantes: `UPPER_SNAKE_CASE` → `MAX_RETRY_ATTEMPTS`
- Clases: `PascalCase` → `UserProfile`

## Buenas Prácticas Adicionales

### Modularización
Divide tu código en archivos pequeños y específicos en lugar de tener archivos gigantes. Es mejor tener `header.js`, `footer.js` y `navigation.js` que un solo archivo de 1000 líneas.

### Versionado
Si usas Git, incluye un archivo `.gitignore` para excluir:
```
node_modules/
.env
.DS_Store
*.log
```

### Documentación
Comenta secciones importantes del código y mantén actualizado el README con:
- Descripción del proyecto
- Cómo instalar/ejecutar
- Estructura del proyecto
- Tecnologías utilizadas

### Optimización de Assets
- Comprime imágenes antes de subirlas
- Usa formatos modernos (WebP para imágenes, WOFF2 para fuentes)
- Considera usar un CDN para librerías externas

## Estructura para Proyectos Grandes

Para proyectos más complejos, considera esta estructura expandida:

```
mi-proyecto/
│
├── src/
│   ├── css/
│   ├── js/
│   └── assets/
│
├── dist/              # Archivos compilados/optimizados
│
├── docs/              # Documentación del proyecto
│
├── tests/             # Pruebas unitarias
│
└── config/            # Archivos de configuración
```

## Herramientas Recomendadas

- **Live Server**: Para desarrollo local con recarga automática
- **Prettier**: Formateo automático de código
- **ESLint**: Linting para JavaScript
- **Git**: Control de versiones

## Ejemplo de Importación en HTML

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Proyecto</title>
    
    <!-- CSS -->
    <link rel="stylesheet" href="css/reset.css">
    <link rel="stylesheet" href="css/main.css">
    <link rel="stylesheet" href="css/components/header.css">
</head>
<body>
    <!-- Contenido -->
    
    <!-- JavaScript al final del body -->
    <script src="js/utils.js"></script>
    <script src="js/components/modal.js"></script>
    <script src="js/main.js"></script>
</body>
</html>
```

## Recuerda

La organización es una inversión de tiempo inicial que te ahorrará muchas horas de búsqueda y confusión a largo plazo. Encuentra la estructura que mejor funcione para tu proyecto y mantén la consistencia.