# 3 Proyectos React para Dominar el Framework

## Índice
1. [Proyecto 1: Dashboard Analítico Interactivo](#proyecto-1)
2. [Proyecto 2: Sistema de Gestión de Tareas Colaborativo](#proyecto-2)
3. [Proyecto 3: Plataforma de E-Learning](#proyecto-3)
4. [Progresión y Timeline](#progresión)

---

## Proyecto 1: Dashboard Analítico Interactivo

### 🎯 Tipo: Dinámico con Estado Complejo
**Nivel**: Intermedio | **Tiempo estimado**: 3-4 semanas

### Descripción General
Un dashboard que muestre métricas y KPIs en tiempo real con múltiples visualizaciones interactivas, filtros avanzados y capacidad de personalización.

### Funcionalidades Esenciales

#### Must-Have (MVP)
```
📊 Visualizaciones de Datos
├── Gráficos de líneas (tendencias temporales)
├── Gráficos de barras (comparativas)
├── Gráficos de dona/pie (distribuciones)
├── Cards con métricas clave (KPIs)
└── Tablas de datos interactivas

🎛️ Filtros y Controles
├── Selector de rango de fechas
├── Filtros por categorías
├── Búsqueda en tiempo real
└── Exportar datos (CSV/PDF)

📱 Responsive Design
├── Layout adaptable
├── Sidebar colapsable
└── Gráficos redimensionables

💾 Gestión de Estado
├── Filtros persistentes
├── Configuración de usuario
└── Layout personalizable
```

#### Nice-to-Have (Avanzado)
```
🔄 Actualizaciones en Tiempo Real
├── WebSocket para datos live
├── Notificaciones de cambios
└── Auto-refresh configurable

🎨 Personalización
├── Tema claro/oscuro
├── Arrastrar y soltar widgets
├── Guardar layouts personalizados
└── Múltiples dashboards

📈 Funciones Avanzadas
├── Comparación de períodos
├── Predicciones/tendencias
├── Anotaciones en gráficos
└── Alertas configurables
```

### Stack Técnico Recomendado

```javascript
// Core
React 18+ (Hooks, Suspense, Concurrent Features)
React Router v6 (Navegación)

// Visualización de Datos
Recharts o Chart.js (Gráficos)
TanStack Table v8 (Tablas complejas)

// Gestión de Estado
Zustand o Context API + useReducer

// UI/UX
Tailwind CSS (Estilos)
Framer Motion (Animaciones)
React Hot Toast (Notificaciones)

// Utilidades
date-fns (Manejo de fechas)
lodash (Manipulación de datos)
react-hook-form (Formularios de filtros)
```

### Arquitectura del Proyecto

```
src/
├── features/
│   ├── dashboard/
│   │   ├── components/
│   │   │   ├── widgets/
│   │   │   │   ├── LineChartWidget.jsx
│   │   │   │   ├── BarChartWidget.jsx
│   │   │   │   ├── KPICard.jsx
│   │   │   │   └── DataTable.jsx
│   │   │   ├── filters/
│   │   │   │   ├── DateRangePicker.jsx
│   │   │   │   ├── CategoryFilter.jsx
│   │   │   │   └── SearchBar.jsx
│   │   │   └── layout/
│   │   │       ├── DashboardGrid.jsx
│   │   │       └── WidgetContainer.jsx
│   │   ├── hooks/
│   │   │   ├── useDashboardData.js
│   │   │   ├── useFilters.js
│   │   │   └── useChartData.js
│   │   └── utils/
│   │       ├── dataTransformers.js
│   │       └── chartHelpers.js
│   │
│   └── settings/
│       └── components/
│           └── ThemeToggle.jsx
│
├── components/
│   └── ui/
│       ├── Card.jsx
│       ├── Button.jsx
│       └── Select.jsx
│
├── hooks/
│   ├── useLocalStorage.js
│   └── useDebounce.js
│
├── services/
│   └── api.js
│
└── utils/
    ├── mockData.js  // Para desarrollo
    └── constants.js
```

### Fases de Desarrollo

**Fase 1: Setup y Layout (Semana 1)**
- Configurar proyecto con Vite
- Implementar layout responsive
- Crear componentes base (Card, Button, etc.)
- Sistema de grid para widgets

**Fase 2: Visualizaciones Básicas (Semana 2)**
- Implementar gráficos con datos mock
- KPI cards con métricas
- Tabla básica de datos
- Primeros hooks personalizados

**Fase 3: Filtros y Interactividad (Semana 3)**
- Sistema de filtros completo
- Sincronización de filtros con datos
- Búsqueda y exportación
- Persistencia en localStorage

**Fase 4: Pulido y Avanzado (Semana 4)**
- Tema claro/oscuro
- Animaciones y transiciones
- Optimización de performance
- Testing básico

### 💡 Valor de Aprendizaje

#### Conceptos React que Dominarás

**Estado Complejo**
```javascript
// Aprenderás a manejar estado multinivel
const [filters, setFilters] = useState({
  dateRange: { start: null, end: null },
  categories: [],
  searchTerm: ''
});

// Actualización optimizada
const updateFilter = useCallback((key, value) => {
  setFilters(prev => ({
    ...prev,
    [key]: value
  }));
}, []);
```

**Memoización y Performance**
```javascript
// Evitar recálculos innecesarios
const filteredData = useMemo(() => {
  return rawData
    .filter(item => matchesFilters(item, filters))
    .sort(sortByDate);
}, [rawData, filters]);

// Callbacks optimizados
const handleChartClick = useCallback((data) => {
  console.log(data);
}, []);
```

**Custom Hooks Avanzados**
```javascript
// Lógica reutilizable
function useDashboardData(filters) {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  
  useEffect(() => {
    fetchData(filters).then(setData);
  }, [filters]);
  
  return { data, loading, refetch: () => fetchData(filters) };
}
```

**Composición de Componentes**
```javascript
// Componentes reutilizables y flexibles
<Widget>
  <Widget.Header>
    <Widget.Title>Sales Overview</Widget.Title>
    <Widget.Actions>
      <ExportButton />
    </Widget.Actions>
  </Widget.Header>
  <Widget.Body>
    <LineChart data={salesData} />
  </Widget.Body>
</Widget>
```

#### Habilidades Técnicas que Adquirirás

✅ **Visualización de Datos**
- Trabajar con librerías de charts
- Transformar datos para diferentes visualizaciones
- Manejar grandes volúmenes de datos

✅ **Performance Optimization**
- Virtual scrolling para tablas grandes
- Lazy loading de componentes
- Debouncing de búsquedas
- Memoización estratégica

✅ **UX Avanzada**
- Feedback visual inmediato
- Loading states inteligentes
- Transiciones suaves
- Responsive design complejo

✅ **Gestión de Estado Real**
- Estado derivado
- Estado sincronizado
- Persistencia de preferencias
- Cache de datos

#### 🚀 Valor Profesional

**Para el Portfolio**
- Demuestra capacidad de manejar datos complejos
- Muestra skills de UX/UI
- Ejemplo de código organizado y escalable

**Para Entrevistas**
- Hablar sobre optimización de renders
- Explicar decisiones de arquitectura
- Demostrar pensamiento sobre UX

**Empresas que Valoran Esto**
- Startups de analytics (Mixpanel, Amplitude)
- SaaS B2B (cualquier producto con dashboards)
- Fintech (visualización de datos financieros)
- E-commerce (analytics de ventas)

---

## Proyecto 2: Sistema de Gestión de Tareas Colaborativo

### 🎯 Tipo: Dinámico Full-Stack (Frontend + Backend Simulado)
**Nivel**: Intermedio-Avanzado | **Tiempo estimado**: 4-6 semanas

### Descripción General
Un sistema estilo Trello/Asana para gestión de proyectos con tableros Kanban, tareas, subtareas, asignaciones, comentarios y colaboración en tiempo real.

### Funcionalidades Esenciales

#### Must-Have (MVP)
```
📋 Gestión de Tableros
├── Crear/editar/eliminar tableros
├── Listas de tareas (columnas)
├── Drag & Drop entre columnas
└── Múltiples tableros por usuario

✅ Gestión de Tareas
├── Crear tareas con título/descripción
├── Asignar a usuarios
├── Etiquetas/tags coloridos
├── Fechas de vencimiento
├── Prioridades (alta, media, baja)
└── Archivar/completar tareas

👥 Colaboración
├── Comentarios en tareas
├── @menciones de usuarios
├── Adjuntar archivos
└── Historial de cambios

🔍 Búsqueda y Filtros
├── Búsqueda global
├── Filtrar por asignado
├── Filtrar por etiquetas
└── Filtrar por fecha

🎨 Personalización
├── Tema claro/oscuro
├── Fondos de tablero
└── Colores personalizados
```

#### Nice-to-Have (Avanzado)
```
🔔 Notificaciones
├── Notificaciones en tiempo real
├── Centro de notificaciones
└── Emails (simulados)

📊 Analytics
├── Velocidad del equipo
├── Tareas completadas
├── Burndown charts
└── Productividad por usuario

🤖 Automatizaciones
├── Reglas automáticas
├── Plantillas de tareas
└── Recordatorios

💬 Chat en Tiempo Real
├── Chat por tablero
├── Mensajes directos
└── Historial de chat
```

### Stack Técnico Recomendado

```javascript
// Core
React 18+ (Suspense, Transitions)
React Router v6
TypeScript (Recomendado para este proyecto)

// Drag & Drop
@dnd-kit/core (Moderno y accesible)
// o react-beautiful-dnd

// Gestión de Estado
Zustand o Redux Toolkit
TanStack Query (React Query) - Para cache y sincronización

// UI/UX
Tailwind CSS
Radix UI o Headless UI (Componentes accesibles)
Framer Motion (Animaciones)

// Formularios
React Hook Form + Zod (Validación)

// Rich Text
Tiptap o Lexical (Editor de texto enriquecido)

// Backend Simulado (Para desarrollo)
MSW (Mock Service Worker)
o JSON Server
o Supabase (Backend real simple)
```

### Arquitectura del Proyecto

```
src/
├── features/
│   ├── boards/
│   │   ├── components/
│   │   │   ├── BoardCard.jsx
│   │   │   ├── BoardList.jsx
│   │   │   ├── CreateBoardModal.jsx
│   │   │   └── BoardSettings.jsx
│   │   ├── hooks/
│   │   │   ├── useBoards.js
│   │   │   └── useBoardMutations.js
│   │   ├── api/
│   │   │   └── boardsApi.js
│   │   └── types/
│   │       └── board.types.ts
│   │
│   ├── tasks/
│   │   ├── components/
│   │   │   ├── TaskCard.jsx
│   │   │   ├── TaskModal.jsx
│   │   │   ├── TaskList.jsx
│   │   │   ├── TaskComments.jsx
│   │   │   └── TaskForm.jsx
│   │   ├── hooks/
│   │   │   ├── useTasks.js
│   │   │   ├── useTaskDrag.js
│   │   │   └── useTaskFilters.js
│   │   └── utils/
│   │       └── taskHelpers.js
│   │
│   ├── kanban/
│   │   ├── components/
│   │   │   ├── KanbanBoard.jsx
│   │   │   ├── KanbanColumn.jsx
│   │   │   └── DroppableColumn.jsx
│   │   └── hooks/
│   │       └── useKanbanDnd.js
│   │
│   ├── comments/
│   │   ├── components/
│   │   │   ├── CommentList.jsx
│   │   │   ├── CommentItem.jsx
│   │   │   └── CommentForm.jsx
│   │   └── hooks/
│   │       └── useComments.js
│   │
│   ├── notifications/
│   │   ├── components/
│   │   │   ├── NotificationCenter.jsx
│   │   │   └── NotificationItem.jsx
│   │   └── hooks/
│   │       └── useNotifications.js
│   │
│   └── users/
│       ├── components/
│       │   └── UserAvatar.jsx
│       └── hooks/
│           └── useUsers.js
│
├── components/
│   ├── ui/
│   │   ├── Modal.jsx
│   │   ├── Dropdown.jsx
│   │   ├── DatePicker.jsx
│   │   └── TagInput.jsx
│   └── layout/
│       ├── Sidebar.jsx
│       ├── Header.jsx
│       └── MainLayout.jsx
│
├── hooks/
│   ├── useLocalStorage.js
│   ├── useDebounce.js
│   ├── useKeyPress.js
│   └── useClickOutside.js
│
├── store/
│   ├── boardsStore.js
│   ├── tasksStore.js
│   └── uiStore.js
│
├── services/
│   ├── api.js
│   └── websocket.js (Para tiempo real)
│
└── utils/
    ├── dateHelpers.js
    ├── validators.js
    └── constants.js
```

### Fases de Desarrollo

**Fase 1: Core Setup (Semana 1)**
- Setup del proyecto con TypeScript
- Sistema de routing
- Layout principal y navegación
- Componentes UI base
- Mock API setup

**Fase 2: Tableros y Listas (Semana 2)**
- CRUD de tableros
- Crear/editar listas
- Vista de tablero básica
- Zustand/Redux store setup

**Fase 3: Tareas y Drag & Drop (Semanas 3-4)**
- CRUD de tareas
- Modal de detalles de tarea
- Implementar drag & drop
- Asignaciones y etiquetas
- Fechas de vencimiento

**Fase 4: Colaboración (Semana 5)**
- Sistema de comentarios
- @menciones
- Historial de cambios
- Notificaciones básicas

**Fase 5: Features Avanzadas (Semana 6)**
- Búsqueda y filtros avanzados
- Persistencia optimizada
- Optimizaciones de performance
- Testing

### 💡 Valor de Aprendizaje

#### Conceptos React que Dominarás

**Drag & Drop Complejo**
```javascript
// Manejar drag and drop con múltiples dropzones
import { DndContext, closestCenter } from '@dnd-kit/core';

function KanbanBoard() {
  const handleDragEnd = (event) => {
    const { active, over } = event;
    
    if (active.id !== over.id) {
      // Mover tarea entre columnas
      moveTask(active.id, over.id);
    }
  };
  
  return (
    <DndContext onDragEnd={handleDragEnd} collisionDetection={closestCenter}>
      {columns.map(column => (
        <DroppableColumn key={column.id} column={column}>
          {tasks.map(task => (
            <DraggableTask key={task.id} task={task} />
          ))}
        </DroppableColumn>
      ))}
    </DndContext>
  );
}
```

**Optimistic Updates**
```javascript
// Actualizar UI antes de confirmar con servidor
function useUpdateTask() {
  const queryClient = useQueryClient();
  
  return useMutation({
    mutationFn: updateTask,
    onMutate: async (newTask) => {
      // Cancelar queries en vuelo
      await queryClient.cancelQueries(['tasks']);
      
      // Snapshot del estado anterior
      const previousTasks = queryClient.getQueryData(['tasks']);
      
      // Actualizar optimísticamente
      queryClient.setQueryData(['tasks'], old => 
        old.map(t => t.id === newTask.id ? newTask : t)
      );
      
      return { previousTasks };
    },
    onError: (err, newTask, context) => {
      // Revertir en caso de error
      queryClient.setQueryData(['tasks'], context.previousTasks);
    }
  });
}
```

**Gestión de Estado Compleja**
```javascript
// Store con Zustand
import create from 'zustand';

const useTaskStore = create((set, get) => ({
  boards: [],
  currentBoard: null,
  tasks: [],
  
  // Acciones
  addTask: (task) => set(state => ({
    tasks: [...state.tasks, task]
  })),
  
  moveTask: (taskId, newColumnId) => set(state => ({
    tasks: state.tasks.map(task =>
      task.id === taskId 
        ? { ...task, columnId: newColumnId }
        : task
    )
  })),
  
  // Selectores
  getTasksByColumn: (columnId) => 
    get().tasks.filter(task => task.columnId === columnId),
  
  getTaskById: (taskId) =>
    get().tasks.find(task => task.id === taskId)
}));
```

**Portal y Modales Avanzados**
```javascript
// Modal con portal y gestión de foco
import { createPortal } from 'react-dom';
import { useEffect, useRef } from 'react';

function TaskModal({ isOpen, onClose, task }) {
  const modalRef = useRef();
  
  useEffect(() => {
    if (isOpen) {
      modalRef.current?.focus();
    }
  }, [isOpen]);
  
  useEffect(() => {
    const handleEscape = (e) => {
      if (e.key === 'Escape') onClose();
    };
    
    document.addEventListener('keydown', handleEscape);
    return () => document.removeEventListener('keydown', handleEscape);
  }, [onClose]);
  
  if (!isOpen) return null;
  
  return createPortal(
    <div className="modal-overlay" onClick={onClose}>
      <div 
        ref={modalRef}
        className="modal-content"
        onClick={e => e.stopPropagation()}
        tabIndex={-1}
      >
        <TaskDetails task={task} />
      </div>
    </div>,
    document.body
  );
}
```

#### Habilidades Técnicas que Adquirirás

✅ **Drag & Drop**
- Implementar interfaces drag and drop complejas
- Manejar múltiples dropzones
- Feedback visual durante drag
- Accesibilidad en D&D

✅ **Real-Time Features**
- WebSockets básicos
- Sincronización de estado
- Conflictos de concurrencia
- Optimistic updates

✅ **Gestión de Estado Avanzada**
- Normalización de datos
- Selectores y derivación de estado
- Cache strategies
- Estado local vs global

✅ **TypeScript en React**
- Types para props y estado
- Generics en hooks
- Type-safe APIs
- Discriminated unions

✅ **Formularios Complejos**
- Validación multi-step
- Forms dinámicos
- Error handling elegante
- UX de formularios

✅ **Accesibilidad**
- Keyboard navigation
- Screen readers
- Focus management
- ARIA attributes

#### 🚀 Valor Profesional

**Para el Portfolio**
- Proyecto complejo y profesional
- Demuestra capacidad full-stack (frontend)
- UX pulida y moderna
- Código limpio y testeado

**Para Entrevistas**
- Discutir arquitectura de estado complejo
- Explicar optimizaciones de performance
- Demostrar conocimiento de UX patterns
- Hablar sobre testing strategies

**Empresas que Valoran Esto**
- Productividad tools (Notion, Linear, Asana)
- Collaboration software (Slack, Discord)
- Project management (Jira, Monday.com)
- Cualquier SaaS colaborativo

**Skills Transferibles**
- Drag & drop → Cualquier app interactiva
- Real-time → Chat, games, collaborative editing
- Estado complejo → Cualquier app grande
- TypeScript → Requisito en muchas empresas

---

## Proyecto 3: Plataforma de E-Learning

### 🎯 Tipo: Dinámico con Multimedia
**Nivel**: Avanzado | **Tiempo estimado**: 6-8 semanas

### Descripción General
Una plataforma completa de aprendizaje online con cursos, lecciones en video, quizzes interactivos, progreso del estudiante, certificados y gamificación.

### Funcionalidades Esenciales

#### Must-Have (MVP)
```
📚 Gestión de Cursos
├── Catálogo de cursos
├── Detalles de curso (descripción, instructor, rating)
├── Estructura de módulos y lecciones
├── Inscripción a cursos
└── Mi biblioteca de cursos

🎥 Reproductor de Video
├── Video player custom
├── Controles (play, pause, velocidad)
├── Marcadores temporales
├── Notas en timestamps
├── PiP (Picture in Picture)
└── Subtítulos/captions

📝 Contenido Interactivo
├── Lecciones de texto con markdown
├── Code playground integrado
├── Quizzes de opción múltiple
├── Ejercicios prácticos
└── Recursos descargables

📊 Progreso del Estudiante
├── Tracker de progreso por curso
├── Marcar lecciones completadas
├── Historial de aprendizaje
├── Tiempo total estudiado
└── Certificados al completar

🔍 Búsqueda y Descubrimiento
├── Búsqueda de cursos
├── Filtros (categoría, nivel, duración)
├── Cursos recomendados
└── Cursos populares
```

#### Nice-to-Have (Avanzado)
```
🏆 Gamificación
├── Sistema de puntos (XP)
├── Niveles y badges
├── Streaks diarios
├── Leaderboards
└── Desafíos semanales

💬 Comunidad
├── Foro de discusión por curso
├── Q&A con instructor
├── Reseñas y ratings
└── Compartir progreso

🎓 Features de Instructor
├── Dashboard de instructor
├── Crear/editar cursos
├── Analytics de estudiantes
└── Responder preguntas

📱 Features Móviles
├── Descarga de lecciones
├── Modo offline
├── Notificaciones push
└── Widget de progreso

🤖 IA/Personalización
├── Recomendaciones personalizadas
├── Path de aprendizaje adaptativo
├── Asistente virtual
└── Resúmenes automáticos
```

### Stack Técnico Recomendado

```javascript
// Core
React 18+
React Router v6
TypeScript

// Video
React Player o Video.js
Plyr (UI bonita para videos)

// Rich Content
MDX (Markdown + JSX)
Prism.js (Syntax highlighting)
React Markdown

// Code Playground
Sandpack (de CodeSandbox)
o Monaco Editor (VS Code editor)

// Gestión de Estado
Zustand + TanStack Query
Jotai (Atoms para estado granular)

// UI/UX
Tailwind CSS
Framer Motion
Radix UI

// Formularios y Validación
React Hook Form
Zod

// Charts y Progress
Recharts
Progress bars custom

// Backend (Opciones)
Supabase (Full backend)
o Firebase
o PocketBase
o Mock API
```

### Arquitectura del Proyecto

```
src/
├── features/
│   ├── courses/
│   │   ├── components/
│   │   │   ├── catalog/
│   │   │   │   ├── CourseCard.jsx
│   │   │   │   ├── CourseGrid.jsx
│   │   │   │   ├── CourseFilters.jsx
│   │   │   │   └── SearchBar.jsx
│   │   │   ├── details/
│   │   │   │   ├── CourseHero.jsx
│   │   │   │   ├── CourseCurriculum.jsx
│   │   │   │   ├── CourseReviews.jsx
│   │   │   │   └── EnrollButton.jsx
│   │   │   └── player/
│   │   │       ├── CoursePlayer.jsx
│   │   │       ├── LessonSidebar.jsx
│   │   │       └── NavigationControls.jsx
│   │   ├── hooks/
│   │   │   ├── useCourses.js
│   │   │   ├── useCourseProgress.js
│   │   │   └── useEnrollment.js
│   │   └── api/
│   │
│   ├── lessons/
│   │   ├── components/
│   │   │   ├── VideoLesson.jsx
│   │   │   ├── TextLesson.jsx
│   │   │   ├── CodeLesson.jsx
│   │   │   └── QuizLesson.jsx
│   │   ├── video/
│   │   │   ├── VideoPlayer.jsx
│   │   │   ├── VideoControls.jsx
│   │   │   ├── VideoNotes.jsx
│   │   │   └── VideoBookmarks.jsx
│   │   └── hooks/
│   │       ├── useVideoPlayer.js
│   │       └── useVideoProgress.js
│   │
│   ├── quizzes/
│   │   ├── components/
│   │   │   ├── Quiz.jsx
│   │   │   ├── Question.jsx
│   │   │   ├── QuizResults.jsx
│   │   │   └── QuizReview.jsx
│   │   ├── types/
│   │   │   └── quiz.types.ts
│   │   └── hooks/
│   │       └── useQuiz.js
│   │
│   ├── progress/
│   │   ├── components/
│   │   │   ├── ProgressDashboard.jsx
│   │   │   ├── ProgressChart.jsx
│   │   │   ├── Achievements.jsx
│   │   │   └── Certificate.jsx
│   │   └── hooks/
│   │       └── useProgress.js
│   │
│   ├── gamification/
│   │   ├── components/
│   │   │   ├── XPBar.jsx
│   │   │   ├── BadgeDisplay.jsx
│   │   │   ├── StreakCounter.jsx
│   │   │   └── Leaderboard.jsx
│   │   └── hooks/
│   │       └── useGamification.js
│   │
│   ├── community/
│   │   ├── components/
│   │   │   ├── DiscussionForum.jsx
│   │   │   ├── QuestionThread.jsx
│   │   │   └── ReviewForm.jsx
│   │   └── hooks/
│   │
│   └── user/
│       ├── components/
│       │   ├── UserProfile.jsx
│       │   ├── MyLearning.jsx
│       │   └── Settings.jsx
│       └── hooks/
│
├── components/
│   ├── ui/
│   │   ├── Card.jsx
│   │   ├── Badge.jsx
│   │   ├── ProgressBar.jsx
│   │   └── Tabs.jsx
│   ├── layout/
│   │   ├── AppLayout.jsx
│   │   ├── CourseLayout.jsx
│   │   └── PlayerLayout.jsx
│   └── shared/
│       ├── Rating.jsx
│       ├── Avatar.jsx
│       └── Tooltip.jsx
│
├── hooks/
│   ├── useAuth.js
│   ├── useLocalStorage.js
│   ├── useMediaQuery.js
│   └── useIntersectionObserver.js
│
├── store/
│   ├── authStore.js
│   ├── progressStore.js
│   └── uiStore.js
│
├── services/
│   ├── api/
│   │   ├── courses.js
│   │   ├── progress.js
│   │   └── quizzes.js
│   └── storage/
│       └── videoStorage.js
│
└── utils/
    ├── videoHelpers.js
    ├── progressCalculators.js
    └── certificateGenerator.js
```

### Fases de Desarrollo

**Fase 1: Fundamentos (Semanas 1-2)**
- Setup del proyecto
- Sistema de autenticación
- Layout y navegación principal
- Catálogo de cursos básico
- Página de detalles de curso