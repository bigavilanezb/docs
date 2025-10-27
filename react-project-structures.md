# Guía Completa: Estructuras de Proyectos React

## Tabla de Contenidos
1. [Proyecto Pequeño](#proyecto-pequeño)
2. [Proyecto Mediano](#proyecto-mediano)
3. [Proyecto Grande](#proyecto-grande)
4. [Proyecto Enterprise](#proyecto-enterprise)
5. [Comparativa y Criterios de Selección](#comparativa)

---

## Proyecto Pequeño
**Características**: MVP, landing pages, prototipos, portfolios personales
**Tamaño**: 5-20 componentes, 1-3 desarrolladores, <10,000 líneas de código

### Estructura Recomendada: Plana Simplificada

```
src/
├── assets/
│   ├── images/
│   │   └── logo.svg
│   └── styles/
│       └── global.css
│
├── components/
│   ├── Header.jsx
│   ├── Footer.jsx
│   ├── Button.jsx
│   ├── Card.jsx
│   └── ContactForm.jsx
│
├── pages/
│   ├── Home.jsx
│   ├── About.jsx
│   └── Contact.jsx
│
├── utils/
│   ├── constants.js
│   └── helpers.js
│
├── App.jsx
├── main.jsx
└── routes.jsx
```

### Análisis y Justificación

**Por qué funciona:**
- **Simplicidad**: Todo está a máximo 2 niveles de profundidad. Fácil de navegar.
- **Velocidad de desarrollo**: No pierdes tiempo decidiendo dónde va cada archivo.
- **Bajo overhead**: No necesitas mantener una estructura compleja para pocas funcionalidades.
- **Curva de aprendizaje**: Cualquier desarrollador nuevo entiende la estructura en minutos.

**Limitaciones:**
- Se vuelve caótica con >30 componentes
- Difícil separar responsabilidades en equipos
- No escala bien con lógica de negocio compleja

### Alternativa: Estructura por Tipo

```
src/
├── components/
│   ├── ui/              # Componentes de UI puros
│   │   ├── Button.jsx
│   │   └── Input.jsx
│   └── forms/           # Componentes de formularios
│       └── ContactForm.jsx
│
├── pages/
├── hooks/
│   └── useForm.js
├── services/
│   └── api.js
└── utils/
```

**Cuándo usar esta alternativa:**
- Cuando tienes 15-30 componentes y necesitas algo de organización
- Cuando varios componentes comparten el mismo propósito (todos son formularios, todos son modales)

**Ventaja**: Mejor organización sin complejidad adicional
**Desventaja**: Puede llevar a carpetas con un solo archivo

---

## Proyecto Mediano
**Características**: Aplicaciones SaaS básicas, dashboards, e-commerce, apps corporativas
**Tamaño**: 30-100 componentes, 3-8 desarrolladores, 10,000-50,000 líneas

### Estructura Recomendada: Feature-Based

```
src/
├── assets/
│   ├── images/
│   ├── fonts/
│   └── icons/
│
├── components/              # Solo componentes VERDADERAMENTE reutilizables
│   ├── ui/
│   │   ├── Button/
│   │   │   ├── Button.jsx
│   │   │   ├── Button.module.css
│   │   │   ├── Button.test.jsx
│   │   │   └── index.js
│   │   ├── Input/
│   │   ├── Modal/
│   │   ├── Table/
│   │   └── index.js         # Barrel export
│   │
│   └── layout/
│       ├── Header/
│       ├── Sidebar/
│       ├── Footer/
│       └── MainLayout.jsx
│
├── features/                # Organización por dominio/funcionalidad
│   ├── auth/
│   │   ├── components/      # Componentes específicos de auth
│   │   │   ├── LoginForm.jsx
│   │   │   ├── RegisterForm.jsx
│   │   │   └── PasswordReset.jsx
│   │   ├── hooks/
│   │   │   ├── useAuth.js
│   │   │   └── useLogin.js
│   │   ├── services/
│   │   │   └── authService.js
│   │   ├── utils/
│   │   │   └── tokenManager.js
│   │   └── index.js         # Exporta todo lo público
│   │
│   ├── products/
│   │   ├── components/
│   │   │   ├── ProductCard.jsx
│   │   │   ├── ProductList.jsx
│   │   │   └── ProductFilters.jsx
│   │   ├── hooks/
│   │   │   └── useProducts.js
│   │   ├── services/
│   │   │   └── productService.js
│   │   └── index.js
│   │
│   ├── cart/
│   │   ├── components/
│   │   ├── hooks/
│   │   │   └── useCart.js
│   │   ├── context/
│   │   │   └── CartContext.jsx
│   │   └── utils/
│   │       └── cartCalculations.js
│   │
│   └── users/
│       ├── components/
│       ├── hooks/
│       └── services/
│
├── pages/                   # Componentes de página que componen features
│   ├── Home/
│   │   ├── Home.jsx
│   │   └── Home.module.css
│   ├── Dashboard/
│   ├── Products/
│   │   └── ProductDetails.jsx
│   ├── Cart/
│   └── NotFound.jsx
│
├── hooks/                   # Hooks globales custom
│   ├── useLocalStorage.js
│   ├── useDebounce.js
│   ├── useMediaQuery.js
│   └── index.js
│
├── context/                 # Context providers globales
│   ├── AuthContext.jsx
│   ├── ThemeContext.jsx
│   └── index.js
│
├── services/                # Configuración API global
│   ├── api.js              # Axios/fetch configurado
│   ├── apiClient.js        # Interceptors, error handling
│   └── endpoints.js        # URLs centralizadas
│
├── utils/                   # Utilidades globales
│   ├── validators.js
│   ├── formatters.js
│   ├── constants.js
│   └── helpers.js
│
├── routes/
│   ├── AppRoutes.jsx
│   ├── PrivateRoute.jsx
│   └── routes.config.js
│
├── styles/
│   ├── global.css
│   ├── variables.css
│   └── themes/
│
├── App.jsx
└── main.jsx
```

### Análisis Profundo

**Por qué Feature-Based es ideal:**

1. **Escalabilidad Mental**: Los desarrolladores piensan en términos de funcionalidades ("voy a trabajar en el carrito"), no en términos técnicos.

2. **Colocation**: Todo lo relacionado está junto. Si eliminas una feature, borras una carpeta.

3. **Trabajo en Paralelo**: Múltiples desarrolladores pueden trabajar en diferentes features sin conflictos.

4. **Boundaries Claros**: Cada feature es como un mini-proyecto con sus propias reglas.

5. **Testing más fácil**: Los tests viven cerca del código que prueban.

### Principio de Organización en Features

```javascript
// ❌ MAL: Componente reutilizable en feature
features/
  products/
    components/
      Button.jsx          // Esto debería estar en components/ui/

// ✅ BIEN: Componente específico de dominio
features/
  products/
    components/
      AddToCartButton.jsx // Lógica específica de productos
```

### Ejemplo de Barrel Exports

```javascript
// features/auth/index.js
export { LoginForm, RegisterForm } from './components';
export { useAuth, useLogin } from './hooks';
export { authService } from './services';

// Ahora puedes importar:
// import { LoginForm, useAuth } from 'features/auth';
```

### Alternativa: Estructura por Capas

```
src/
├── presentation/        # UI Components
│   ├── components/
│   └── pages/
├── business/           # Lógica de negocio
│   ├── hooks/
│   └── services/
└── data/              # Manejo de datos
    ├── api/
    └── models/
```

**Cuándo usar:**
- Cuando tu equipo tiene roles muy definidos (frontend/backend)
- Aplicaciones con lógica de negocio muy compleja
- Cuando trabajas con arquitectura hexagonal

**Ventaja**: Separación clara de responsabilidades técnicas
**Desventaja**: Dificulta el razonamiento por funcionalidad, más navegación entre carpetas

---

## Proyecto Grande
**Características**: Plataformas complejas, múltiples módulos, muchas integraciones
**Tamaño**: 100-500 componentes, 8-20 desarrolladores, 50,000-200,000 líneas

### Estructura Recomendada: Modular Híbrida

```
src/
├── modules/                 # Módulos independientes
│   ├── auth/
│   │   ├── api/            # API específica del módulo
│   │   │   ├── endpoints.js
│   │   │   └── authApi.js
│   │   ├── components/
│   │   │   ├── forms/
│   │   │   ├── modals/
│   │   │   └── widgets/
│   │   ├── hooks/
│   │   ├── pages/          # Páginas del módulo
│   │   │   ├── Login/
│   │   │   ├── Register/
│   │   │   └── ForgotPassword/
│   │   ├── store/          # Estado local del módulo
│   │   │   ├── authSlice.js
│   │   │   └── selectors.js
│   │   ├── routes/
│   │   │   └── authRoutes.jsx
│   │   ├── types/          # TypeScript types
│   │   │   └── auth.types.ts
│   │   ├── utils/
│   │   ├── constants.js
│   │   └── index.js
│   │
│   ├── products/
│   │   ├── api/
│   │   ├── components/
│   │   │   ├── catalog/
│   │   │   ├── details/
│   │   │   └── reviews/
│   │   ├── hooks/
│   │   ├── pages/
│   │   │   ├── ProductList/
│   │   │   ├── ProductDetails/
│   │   │   └── ProductCreate/
│   │   ├── store/
│   │   └── routes/
│   │
│   ├── orders/
│   ├── payments/
│   ├── analytics/
│   └── admin/
│
├── shared/                  # Recursos compartidos entre módulos
│   ├── components/
│   │   ├── ui/
│   │   │   ├── Button/
│   │   │   ├── Input/
│   │   │   ├── DataTable/
│   │   │   ├── DatePicker/
│   │   │   └── FileUpload/
│   │   ├── layout/
│   │   │   ├── AppShell/
│   │   │   ├── Navbar/
│   │   │   ├── Sidebar/
│   │   │   └── Breadcrumbs/
│   │   └── feedback/       # Toasts, alerts, loaders
│   │
│   ├── hooks/
│   │   ├── useDebounce.js
│   │   ├── useLocalStorage.js
│   │   ├── usePagination.js
│   │   └── useInfiniteScroll.js
│   │
│   ├── utils/
│   │   ├── validators/
│   │   │   ├── emailValidator.js
│   │   │   └── formValidators.js
│   │   ├── formatters/
│   │   │   ├── dateFormatter.js
│   │   │   └── currencyFormatter.js
│   │   └── helpers/
│   │
│   ├── constants/
│   │   ├── routes.js
│   │   ├── apiEndpoints.js
│   │   └── appConfig.js
│   │
│   └── types/              # Types compartidos
│       ├── common.types.ts
│       └── api.types.ts
│
├── core/                    # Configuración central
│   ├── api/
│   │   ├── apiClient.js    # Axios configurado
│   │   ├── interceptors.js
│   │   └── errorHandler.js
│   │
│   ├── router/
│   │   ├── AppRouter.jsx
│   │   ├── ProtectedRoute.jsx
│   │   └── RouterConfig.js
│   │
│   ├── store/              # Redux/Zustand global
│   │   ├── store.js
│   │   ├── rootReducer.js
│   │   └── middleware.js
│   │
│   ├── auth/               # Autenticación central
│   │   ├── AuthProvider.jsx
│   │   └── useAuthGuard.js
│   │
│   └── config/
│       ├── env.js
│       └── featureFlags.js
│
├── layouts/                 # Layouts de página
│   ├── MainLayout.jsx
│   ├── AuthLayout.jsx
│   ├── DashboardLayout.jsx
│   └── AdminLayout.jsx
│
├── pages/                   # Páginas de alto nivel que componen módulos
│   ├── Home.jsx
│   ├── Dashboard.jsx
│   └── NotFound.jsx
│
├── assets/
│   ├── images/
│   ├── fonts/
│   ├── icons/
│   └── locales/            # i18n
│       ├── en.json
│       └── es.json
│
├── styles/
│   ├── global.css
│   ├── variables.css
│   ├── themes/
│   │   ├── light.css
│   │   └── dark.css
│   └── utilities.css
│
├── tests/                   # Tests de integración
│   ├── e2e/
│   ├── integration/
│   └── utils/
│
├── App.jsx
└── main.jsx
```

### Análisis Profundo

**Principios Arquitectónicos:**

1. **Modularidad Estricta**: Cada módulo es autónomo y podría extraerse a un paquete npm.

2. **Dependency Rule**: 
   - Módulos NO deben importar de otros módulos
   - Módulos SOLO importan de `shared/` o `core/`
   - `shared/` NO importa de módulos
   - `core/` NO importa de módulos ni shared

```javascript
// ❌ MAL: Módulos dependiendo entre sí
import { ProductCard } from 'modules/products';  // Desde modules/orders

// ✅ BIEN: Usando shared
import { ProductCard } from 'shared/components';

// ✅ BIEN: Usando APIs públicas
import { fetchProduct } from 'core/api/productApi';
```

3. **Comunicación entre Módulos**: A través de eventos o store global, nunca importaciones directas.

```javascript
// modules/orders/components/OrderCreated.jsx
import { eventBus } from 'core/events';

function OrderCreated({ orderId }) {
  useEffect(() => {
    eventBus.emit('order:created', { orderId });
  }, [orderId]);
}

// modules/analytics/hooks/useOrderAnalytics.js
eventBus.on('order:created', (data) => {
  // Actualizar analytics
});
```

### Gestión de Estado en Proyectos Grandes

**Estrategia de Estado Multinivel:**

```
Global State (Redux/Zustand)
    ├── Auth state
    ├── UI state (theme, sidebar)
    └── Cache global
    
Module State
    ├── Module-specific state
    └── Module cache
    
Component State (useState)
    └── UI local state
```

### Alternativa: Micro-Frontends

```
apps/
├── shell/                  # App principal
├── auth-app/              # Micro-app de auth
├── products-app/
└── admin-app/

packages/
├── ui-components/
├── shared-utils/
└── api-client/
```

**Cuándo usar Micro-Frontends:**
- Equipos completamente independientes
- Necesitas deployments independientes
- Diferentes tecnologías en diferentes partes
- Organización muy grande (50+ devs)

**Ventajas:**
- Máxima independencia de equipos
- Deployments independientes
- Tecnologías diversas

**Desventajas:**
- Complejidad de infraestructura
- Overhead de comunicación
- Duplicación de dependencias

---

## Proyecto Enterprise
**Características**: Sistemas críticos, alta escalabilidad, múltiples equipos
**Tamaño**: 500+ componentes, 20+ desarrolladores, 200,000+ líneas

### Estructura Recomendada: Domain-Driven Design (DDD)

```
src/
├── domains/                    # Dominios de negocio
│   ├── sales/                 # Bounded Context: Ventas
│   │   ├── modules/
│   │   │   ├── orders/
│   │   │   │   ├── application/      # Casos de uso
│   │   │   │   │   ├── commands/
│   │   │   │   │   │   └── CreateOrder.js
│   │   │   │   │   ├── queries/
│   │   │   │   │   │   └── GetOrderById.js
│   │   │   │   │   └── handlers/
│   │   │   │   ├── domain/           # Lógica de dominio
│   │   │   │   │   ├── entities/
│   │   │   │   │   │   └── Order.js
│   │   │   │   │   ├── value-objects/
│   │   │   │   │   │   └── Money.js
│   │   │   │   │   ├── aggregates/
│   │   │   │   │   └── events/
│   │   │   │   │       └── OrderCreated.js
│   │   │   │   ├── infrastructure/   # Implementación técnica
│   │   │   │   │   ├── api/
│   │   │   │   │   ├── repositories/
│   │   │   │   │   │   └── OrderRepository.js
│   │   │   │   │   └── persistence/
│   │   │   │   └── presentation/     # UI
│   │   │   │       ├── components/
│   │   │   │       ├── pages/
│   │   │   │       ├── hooks/
│   │   │   │       └── viewmodels/
│   │   │   │
│   │   │   ├── invoicing/
│   │   │   ├── shipping/
│   │   │   └── returns/
│   │   │
│   │   └── shared/               # Compartido en el dominio
│   │       ├── types/
│   │       └── utils/
│   │
│   ├── inventory/             # Bounded Context: Inventario
│   │   ├── modules/
│   │   │   ├── products/
│   │   │   ├── warehouses/
│   │   │   └── suppliers/
│   │   └── shared/
│   │
│   ├── customer-service/      # Bounded Context: Servicio al cliente
│   │   ├── modules/
│   │   │   ├── tickets/
│   │   │   ├── chat/
│   │   │   └── knowledge-base/
│   │   └── shared/
│   │
│   └── analytics/
│
├── shared-kernel/              # Compartido entre TODOS los dominios
│   ├── design-system/
│   │   ├── components/
│   │   │   ├── atoms/
│   │   │   │   ├── Button/
│   │   │   │   ├── Input/
│   │   │   │   └── Typography/
│   │   │   ├── molecules/
│   │   │   │   ├── FormField/
│   │   │   │   └── SearchBar/
│   │   │   ├── organisms/
│   │   │   │   ├── DataGrid/
│   │   │   │   └── NavigationBar/
│   │   │   └── templates/
│   │   ├── tokens/            # Design tokens
│   │   │   ├── colors.js
│   │   │   ├── spacing.js
│   │   │   └── typography.js
│   │   └── themes/
│   │
│   ├── core/
│   │   ├── api/
│   │   │   ├── client/
│   │   │   │   ├── HttpClient.js
│   │   │   │   └── GraphQLClient.js
│   │   │   ├── interceptors/
│   │   │   └── middleware/
│   │   ├── auth/
│   │   │   ├── AuthService.js
│   │   │   ├── TokenManager.js
│   │   │   └── PermissionChecker.js
│   │   ├── error-handling/
│   │   │   ├── ErrorBoundary.jsx
│   │   │   ├── ErrorLogger.js
│   │   │   └── ErrorMapper.js
│   │   ├── events/
│   │   │   ├── EventBus.js
│   │   │   └── DomainEvents.js
│   │   └── validation/
│   │       ├── schemas/
│   │       └── validators/
│   │
│   ├── utils/
│   │   ├── date/
│   │   ├── money/
│   │   ├── string/
│   │   └── array/
│   │
│   ├── hooks/
│   │   ├── usePermissions.js
│   │   ├── useFeatureFlag.js
│   │   └── useTracker.js
│   │
│   └── types/                 # TypeScript types globales
│       ├── common.types.ts
│       ├── api.types.ts
│       └── domain.types.ts
│
├── infrastructure/             # Infraestructura transversal
│   ├── routing/
│   │   ├── AppRouter.jsx
│   │   ├── domainRoutes.js
│   │   └── guards/
│   ├── state/
│   │   ├── store.js
│   │   ├── rootReducer.js
│   │   └── sagas/
│   ├── i18n/
│   │   ├── config.js
│   │   └── locales/
│   ├── monitoring/
│   │   ├── analytics.js
│   │   ├── errorTracking.js
│   │   └── performance.js
│   ├── testing/
│   │   ├── test-utils.js
│   │   ├── mocks/
│   │   └── fixtures/
│   └── config/
│       ├── env.js
│       ├── feature-flags.js
│       └── app-config.js
│
├── application/                # Orquestación de la aplicación
│   ├── layouts/
│   │   ├── MainLayout/
│   │   ├── AuthLayout/
│   │   └── DashboardLayout/
│   ├── pages/                 # Páginas que combinan dominios
│   │   ├── HomePage.jsx
│   │   └── DashboardPage.jsx
│   └── App.jsx
│
├── assets/
│   ├── images/
│   ├── fonts/
│   ├── icons/
│   └── animations/
│
└── main.jsx
```

### Análisis Profundo

**Conceptos Clave de DDD:**

1. **Bounded Contexts (Contextos Delimitados)**
   - Cada dominio tiene su propio lenguaje ubicuo
   - Los conceptos significan cosas diferentes en diferentes contextos
   - Ejemplo: "Order" en `sales` vs "Order" en `inventory`

2. **Ubiquitous Language (Lenguaje Ubicuo)**
   - El código refleja el lenguaje del negocio
   - Los nombres de clases/métodos vienen del dominio

```javascript
// ✅ Lenguaje del dominio
class Order {
  place() { }
  cancel() { }
  fulfill() { }
}

// ❌ Lenguaje técnico
class Order {
  create() { }
  delete() { }
  update() { }
}
```

3. **Capas de Arquitectura**

```
Presentation (UI)
      ↓
Application (Casos de uso)
      ↓
Domain (Lógica de negocio)
      ↓
Infrastructure (DB, API)
```

**Reglas de dependencia:**
- Presentation → Application → Domain
- Infrastructure → Domain (implementa interfaces del dominio)
- Domain NO depende de nadie

### Ejemplo Práctico de DDD

```javascript
// domains/sales/modules/orders/domain/entities/Order.js
export class Order {
  constructor(id, items, customerId, status) {
    this.id = id;
    this.items = items;
    this.customerId = customerId;
    this.status = status;
  }

  place() {
    if (this.items.length === 0) {
      throw new Error('Cannot place an order without items');
    }
    this.status = 'placed';
    this.emitEvent(new OrderPlaced(this.id));
  }

  calculateTotal() {
    return this.items.reduce((sum, item) => sum + item.price, 0);
  }
}

// domains/sales/modules/orders/application/commands/PlaceOrder.js
export class PlaceOrderHandler {
  constructor(orderRepository, eventBus) {
    this.orderRepository = orderRepository;
    this.eventBus = eventBus;
  }

  async execute(command) {
    const order = await this.orderRepository.findById(command.orderId);
    order.place();
    await this.orderRepository.save(order);
    this.eventBus.publish(order.getEvents());
  }
}

// domains/sales/modules/orders/infrastructure/repositories/OrderRepository.js
export class OrderRepository {
  async findById(id) {
    const data = await api.get(`/orders/${id}`);
    return Order.fromData(data);
  }

  async save(order) {
    await api.put(`/orders/${order.id}`, order.toData());
  }
}

// domains/sales/modules/orders/presentation/components/PlaceOrderButton.jsx
export function PlaceOrderButton({ orderId }) {
  const placeOrder = usePlaceOrder();
  
  const handleClick = async () => {
    await placeOrder.execute({ orderId });
  };

  return <Button onClick={handleClick}>Place Order</Button>;
}
```

### Comunicación entre Bounded Contexts

**1. Eventos de Dominio**
```javascript
// domains/sales/modules/orders/domain/events/OrderPlaced.js
export class OrderPlaced {
  constructor(orderId, customerId, items) {
    this.orderId = orderId;
    this.customerId = customerId;
    this.items = items;
  }
}

// domains/inventory/modules/stock/application/handlers/OrderPlacedHandler.js
eventBus.subscribe('OrderPlaced', (event) => {
  // Reducir stock cuando se crea una orden
  reduceStock(event.items);
});
```

**2. Anti-Corruption Layer (ACL)**
```javascript
// domains/sales/infrastructure/adapters/InventoryAdapter.js
export class InventoryAdapter {
  constructor(inventoryApi) {
    this.inventoryApi = inventoryApi;
  }

  async checkAvailability(productIds) {
    const response = await this.inventoryApi.checkStock(productIds);
    // Traducir del modelo de inventory al modelo de sales
    return response.map(item => ({
      productId: item.sku,
      available: item.quantity > 0
    }));
  }
}
```

### Alternativa: Clean Architecture

```
src/
├── core/
│   ├── entities/          # Entidades de negocio
│   ├── use-cases/         # Casos de uso
│   └── interfaces/        # Interfaces de repositorios
│
├── adapters/
│   ├── controllers/       # Controladores React
│   ├── presenters/        # Transformadores de datos
│   └── gateways/          # Implementación de repos
│
├── frameworks/
│   ├── ui/               # Componentes React
│   ├── api/              # Cliente HTTP
│   └── state/            # Redux/Zustand
│
└── main.jsx
```

**Diferencias con DDD:**
- Clean Architecture: Foco en capas técnicas y dependencias
- DDD: Foco en el dominio y lenguaje del negocio

**Cuándo usar Clean Architecture:**
- Aplicaciones con lógica de negocio muy compleja
- Necesitas cambiar frameworks fácilmente
- Testing extremadamente importante

### Testing en Enterprise

```
domains/
  sales/
    modules/
      orders/
        __tests__/
          unit/
            domain/
              Order.test.js
            application/
              PlaceOrder.test.js
          integration/
            OrderFlow.test.js
          e2e/
            OrderCheckout.test.js
```

**Estrategia de Testing:**
- **Unit**: Lógica de dominio pura (80% de tests)
- **Integration**: Casos de uso + repos (15%)
- **E2E**: Flujos críticos de usuario (5%)

---

## Comparativa y Criterios de Selección

### Matriz de Decisión

| Criterio | Pequeño | Mediano | Grande | Enterprise |
|----------|---------|---------|---------|------------|
| **Componentes** | 5-20 | 30-100 | 100-500 | 500+ |
| **Desarrolladores** | 1-3 | 3-8 | 8-20 | 20+ |
| **Tiempo de setup** | <1 hora | 1-3 horas | 1-2 días | 1-2 semanas |
| **Curva aprendizaje** | Muy baja | Baja | Media | Alta |
| **Mantenibilidad** | Baja | Alta | Muy alta | Extrema |
| **Escalabilidad** | Baja | Media | Alta | Muy alta |
| **Testing** | Básico | Importante | Crítico | Obligatorio |
| **TypeScript** | Opcional | Recomendado | Muy recomendado | Obligatorio |
| **Documentación** | Mínima | Necesaria | Extensa | Completa |
| **CI/CD** | Opcional | Recomendado | Obligatorio | Crítico |

### Árbol de Decisión

```
¿Cuántos desarrolladores?
├─ 1-3 personas
│  └─ ¿MVP o prototipo?
│     ├─ Sí → PEQUEÑO (Estructura Plana)
│     └─ No → ¿Crecerá rápido?
│        ├─ Sí → MEDIANO (Feature-Based)
│        └─ No → PEQUEÑO
│
├─ 3-8 personas
│  └─ ¿Múltiples funcionalidades independientes?
│     ├─ Sí → MEDIANO (Feature-Based)
│     └─ No → Evaluar complejidad del dominio
│
├─ 8-20 personas
│  └─ ¿Equipos independientes?
│     ├─ Sí → GRANDE (Modular)
│     └─ No → MEDIANO+ (Feature-Based mejorado)
│
└─ 20+ personas
   └─ ¿Dominios de negocio complejos?
      ├─ Sí → ENTERPRISE (DDD)
      └─ No → GRANDE (Modular)
```

### Señales de que Necesitas Migrar

**De Pequeño a Mediano:**
- ❌ Más de 30 componentes en una carpeta
- ❌ Difícil encontrar código relacionado
- ❌ Múltiples desarrolladores pisándose
- ❌ Archivos con más de 500 líneas

**De Mediano a Grande:**
- ❌ Features que dependen entre sí
- ❌ Builds lentos (>5 min)
- ❌ Tests que tardan >30 min
- ❌ Conflictos constantes en git
- ❌ Difícil hacer cambios sin romper cosas

**De Grande a Enterprise:**
- ❌ Lógica de negocio en componentes UI
- ❌ Equipos bloqueándose mutuamente
- ❌ Necesitas soporte multi-tenant
- ❌ Requisitos de auditoría/compliance
- ❌ Múltiples versiones de la app

---

## Patrones y Mejores Prácticas Universales

### 1. Principio de Única Responsabilidad

```javascript
// ❌ MAL: Componente haciendo demasiado
function UserProfile() {
  const [user, setUser] = useState(null);
  const [posts, setPosts] = useState([]);
  
  useEffect(() => {
    fetch('/api/user').then(res => res.json()).then(setUser);
    fetch('/api/posts').then(res => res.json()).then(setPosts);
  }, []);
  
  const handleUpdateProfile = async (data) => {
    await fetch('/api/user', { method: 'PUT', body: JSON.stringify(data) });
  };
  
  return (
    <div>
      <ProfileHeader user={user} />
      <ProfileForm user={user} onSubmit={handleUpdateProfile} />
      <PostsList posts={posts} />
    </div>
  );
}

// ✅ BIEN: Separación de responsabilidades
function UserProfile() {
  const { user } = useUser();
  const { posts } = useUserPosts(user?.id);
  const { updateProfile } = useUpdateProfile();
  
  return (
    <ProfileLayout>
      <ProfileHeader user={user} />
      <ProfileForm user={user} onSubmit={updateProfile} />
      <PostsList posts={posts} />
    </ProfileLayout>
  );
}
```

### 2. Colocation (Cercanía)

```javascript
// ✅ Todo relacionado junto
components/
  UserCard/
    UserCard.jsx
    UserCard.test.jsx
    UserCard.module.css
    UserCard.stories.jsx
    useUserCard.js        // Hook específico
    index.js

// En lugar de disperso
components/
  UserCard.jsx
tests/
  UserCard.test.jsx
styles/
  UserCard.css
hooks/
  useUserCard.js
```

### 3. Composición sobre Herencia

```javascript
// ❌ MAL: Herencia
class BaseButton extends Component {
  render() { /* ... */ }
}
class PrimaryButton extends BaseButton { }
class SecondaryButton extends BaseButton { }

// ✅ BIEN: Composición
function Button({ variant = 'primary', children, ...props }) {
  return (
    <button className={`btn btn-${variant}`} {...props}>
      {children}
    </button>
  );
}

// Uso
<Button variant="primary">Click</Button>
<Button variant="secondary">Cancel</Button>
```

### 4. Custom Hooks para Lógica Reutilizable

```javascript
// ✅ Extraer lógica compleja
function useProductFilters(products) {
  const [filters, setFilters] = useState({
    category: null,
    priceRange: [0, 1000],
    inStock: false
  });
  
  const filteredProducts = useMemo(() => {
    return products.filter(product => {
      if (filters.category && product.category !== filters.category) return false;
      if (product.price < filters.priceRange[0] || product.price > filters.priceRange[1]) return false;
      if (filters.inStock && !product.inStock) return false;
      return true;
    });
  }, [products, filters]);
  
  return { filters, setFilters, filteredProducts };
}

// Uso simple en componente
function ProductList({ products }) {
  const { filters, setFilters, filteredProducts } = useProductFilters(products);
  
  return (
    <>
      <FilterPanel filters={filters} onChange={setFilters} />
      <ProductGrid products={filteredProducts} />
    </>
  );
}
```

### 5. Atomic Design para Design Systems

```
components/
  atoms/              # Elementos básicos
    Button/
    Input/
    Label/
    Icon/
  
  molecules/          # Combinación de atoms
    FormField/        # Label + Input + ErrorMessage
    SearchBar/        # Input + Button + Icon
    Card/
  
  organisms/          # Secciones complejas
    LoginForm/        # Múltiples FormFields + Button
    ProductCard/      # Card + Image + Button
    Navigation/
  
  templates/          # Layouts de página
    DashboardTemplate/
    AuthTemplate/
  
  pages/              # Instancias de templates con datos
    Dashboard.jsx
    Login.jsx
```

### 6. Barrel Exports Inteligentes

```javascript
// components/ui/index.js
export { Button } from './Button';
export { Input } from './Input';
export { Modal } from './Modal';

// Permite importaciones limpias
import { Button, Input, Modal } from 'components/ui';

// En lugar de
import Button from 'components/ui/Button/Button';
import Input from 'components/ui/Input/Input';
import Modal from 'components/ui/Modal/Modal';
```

### 7. Configuración por Entorno

```javascript
// config/env.js
const configs = {
  development: {
    apiUrl: 'http://localhost:3000',
    debugMode: true,
    analytics: false
  },
  staging: {
    apiUrl: 'https://staging.api.com',
    debugMode: true,
    analytics: true
  },
  production: {
    apiUrl: 'https://api.com',
    debugMode: false,
    analytics: true
  }
};

export const config = configs[import.meta.env.MODE] || configs.development;

// Uso
import { config } from 'config/env';
console.log(config.apiUrl);
```

### 8. Feature Flags

```javascript
// core/config/featureFlags.js
export const features = {
  newDashboard: false,
  darkMode: true,
  betaFeatures: import.meta.env.MODE === 'development',
  paymentV2: true
};

export function isFeatureEnabled(feature) {
  return features[feature] ?? false;
}

// Uso en componentes
function Dashboard() {
  if (isFeatureEnabled('newDashboard')) {
    return <NewDashboard />;
  }
  return <LegacyDashboard />;
}
```

---

## Casos de Estudio Reales

### Caso 1: E-Commerce (Proyecto Mediano)

**Requisitos:**
- Catálogo de productos
- Carrito de compras
- Checkout
- Panel de usuario
- 5 desarrolladores

**Estructura elegida: Feature-Based**

```
src/
├── features/
│   ├── catalog/
│   │   ├── components/
│   │   │   ├── ProductGrid.jsx
│   │   │   ├── ProductCard.jsx
│   │   │   └── ProductFilters.jsx
│   │   ├── hooks/
│   │   │   ├── useProducts.js
│   │   │   └── useProductFilters.js
│   │   └── services/
│   │       └── productService.js
│   │
│   ├── cart/
│   │   ├── components/
│   │   │   ├── CartDrawer.jsx
│   │   │   └── CartItem.jsx
│   │   ├── context/
│   │   │   └── CartContext.jsx
│   │   └── hooks/
│   │       └── useCart.js
│   │
│   ├── checkout/
│   │   ├── components/
│   │   │   ├── CheckoutForm.jsx
│   │   │   └── OrderSummary.jsx
│   │   └── hooks/
│   │       └── useCheckout.js
│   │
│   └── user/
│       ├── components/
│       ├── pages/
│       └── hooks/
│
├── components/ui/        # Sistema de diseño
├── pages/               # Páginas principales
└── services/api.js      # Cliente API global
```

**Por qué funciona:**
- Features claramente delimitadas
- Equipos pueden trabajar en paralelo
- Fácil agregar nuevas features (wishlist, reviews)
- Testing por feature
- Deploy incremental posible

### Caso 2: SaaS Dashboard (Proyecto Grande)

**Requisitos:**
- Multi-tenant
- Analytics en tiempo real
- Gestión de usuarios
- Configuraciones complejas
- Integraciones con terceros
- 15 desarrolladores en 3 equipos

**Estructura elegida: Modular**

```
src/
├── modules/
│   ├── analytics/
│   │   ├── components/
│   │   ├── widgets/
│   │   ├── store/
│   │   └── api/
│   │
│   ├── users/
│   │   ├── components/
│   │   ├── permissions/
│   │   └── api/
│   │
│   ├── settings/
│   └── integrations/
│
├── shared/
│   ├── components/
│   │   ├── charts/      # Componentes de gráficos
│   │   └── tables/
│   └── hooks/
│
└── core/
    ├── auth/
    ├── router/
    └── store/
```

**Ventajas:**
- Módulos pueden desarrollarse independientemente
- Posible extraer módulos a microservicios después
- Clear ownership por equipo
- Reduces merge conflicts

### Caso 3: Plataforma Bancaria (Enterprise)

**Requisitos:**
- Múltiples productos (cuentas, préstamos, inversiones)
- Compliance estricto
- Auditoría completa
- Alta disponibilidad
- 50+ desarrolladores

**Estructura elegida: DDD**

```
src/
├── domains/
│   ├── accounts/
│   │   ├── modules/
│   │   │   ├── savings/
│   │   │   │   ├── domain/
│   │   │   │   │   ├── entities/
│   │   │   │   │   ├── value-objects/
│   │   │   │   │   └── events/
│   │   │   │   ├── application/
│   │   │   │   │   ├── commands/
│   │   │   │   │   └── queries/
│   │   │   │   ├── infrastructure/
│   │   │   │   └── presentation/
│   │   │   ├── checking/
│   │   │   └── shared/
│   │
│   ├── loans/
│   ├── investments/
│   └── compliance/
│
├── shared-kernel/
│   ├── design-system/
│   ├── core/
│   │   ├── audit/
│   │   ├── security/
│   │   └── validation/
│   └── utils/
│
└── infrastructure/
    ├── state/
    ├── routing/
    └── monitoring/
```

**Por qué DDD:**
- Lógica de negocio compleja requiere modelado profundo
- Compliance necesita separación estricta de capas
- Múltiples equipos trabajando en diferentes dominios
- Necesidad de evolucionar dominios independientemente
- Auditoría requiere trazabilidad clara

---

## Migración entre Estructuras

### De Pequeño a Mediano

**Estrategia: Refactoring Gradual**

1. **Identificar Features**
```
Antes:
components/
  LoginForm.jsx
  ProductCard.jsx
  CartItem.jsx

Después:
features/
  auth/
    components/
      LoginForm.jsx
  products/
    components/
      ProductCard.jsx
  cart/
    components/
      CartItem.jsx
```

2. **Mover Lógica a Hooks**
```javascript
// Antes: Lógica en componente
function ProductList() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(false);
  
  useEffect(() => {
    setLoading(true);
    fetch('/api/products')
      .then(res => res.json())
      .then(setProducts)
      .finally(() => setLoading(false));
  }, []);
  
  return /* JSX */;
}

// Después: Lógica en hook
function useProducts() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(false);
  
  useEffect(() => {
    setLoading(true);
    fetch('/api/products')
      .then(res => res.json())
      .then(setProducts)
      .finally(() => setLoading(false));
  }, []);
  
  return { products, loading };
}

function ProductList() {
  const { products, loading } = useProducts();
  return /* JSX */;
}
```

3. **Crear Barrel Exports**
4. **Actualizar imports gradualmente**
5. **Agregar tests para features críticas**

### De Mediano a Grande

**Estrategia: Módulos Progresivos**

1. **Identificar Bounded Contexts**
   - ¿Qué features están fuertemente acopladas?
   - ¿Qué features nunca se comunican?

2. **Crear Módulos**
```
features/auth → modules/auth
features/products + features/catalog → modules/catalog
features/cart + features/checkout → modules/orders
```

3. **Establecer APIs entre Módulos**
```javascript
// modules/orders/index.js
export { useCreateOrder } from './hooks';
export { OrderService } from './services';
// NO exportar componentes internos

// modules/catalog/components/AddToCartButton.jsx
import { useCreateOrder } from 'modules/orders';  // ✅ API pública
// NO: import { OrderForm } from 'modules/orders/components';  // ❌
```

4. **Implementar Event Bus**
5. **Migrar Estado a Store Modular**

### De Grande a Enterprise

**Estrategia: Domain Discovery**

1. **Event Storming Workshop**
   - Reunir stakeholders
   - Identificar eventos de dominio
   - Agrupar en bounded contexts

2. **Definir Ubiquitous Language**
   - Crear glosario
   - Documentar términos de dominio

3. **Extraer Entidades de Dominio**
```javascript
// Antes: Modelo anémico
const order = {
  id: 1,
  items: [],
  status: 'pending'
};

function placeOrder(order) {
  if (order.items.length === 0) throw new Error();
  order.status = 'placed';
}

// Después: Entidad rica
class Order {
  constructor(id, items) {
    this.id = id;
    this.items = items;
    this.status = 'pending';
  }
  
  place() {
    if (this.items.length === 0) {
      throw new DomainException('Cannot place empty order');
    }
    this.status = 'placed';
    this.emitEvent(new OrderPlaced(this.id));
  }
}
```

4. **Implementar Capas DDD**
5. **Migrar módulo por módulo**

---

## Herramientas y Automatización

### Linters y Formatters

```javascript
// .eslintrc.js - Reglas de estructura
module.exports = {
  rules: {
    // Prevenir imports entre features
    'no-restricted-imports': ['error', {
      patterns: [
        {
          group: ['features/*/components/*'],
          message: 'Import from feature index instead'
        }
      ]
    }],
    
    // Forzar naming conventions
    'filename-rules/match': ['error', 'kebab-case']
  }
};
```

### Scripts de Generación

```javascript
// scripts/create-feature.js
const fs = require('fs');
const path = require('path');

function createFeature(name) {
  const featurePath = path.join('src/features', name);
  
  const dirs = [
    'components',
    'hooks',
    'services',
    'utils'
  ];
  
  dirs.forEach(dir => {
    fs.mkdirSync(path.join(featurePath, dir), { recursive: true });
  });
  
  // Crear index.js
  fs.writeFileSync(
    path.join(featurePath, 'index.js'),
    `// Export public API here\n`
  );
  
  console.log(`✅ Feature '${name}' created`);
}

// Uso: node scripts/create-feature.js notifications
```

### Análisis de Dependencias

```bash
# Instalar madge
npm install -g madge

# Generar gráfico de dependencias
madge --circular --extensions js,jsx src/

# Detectar dependencias circulares
madge --circular --warning src/
```

### Bundle Analysis

```javascript
// vite.config.js
import { visualizer } from 'rollup-plugin-visualizer';

export default {
  plugins: [
    visualizer({
      open: true,
      filename: 'dist/stats.html'
    })
  ],
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          // Separar vendors
          if (id.includes('node_modules')) {
            return 'vendor';
          }
          // Separar por feature
          if (id.includes('features/auth')) {
            return 'auth';
          }
          if (id.includes('features/products')) {
            return 'products';
          }
        }
      }
    }
  }
};
```

---

## Checklist de Implementación

### Para Cualquier Proyecto

- [ ] Estructura de carpetas definida y documentada
- [ ] Convención de nombres establecida
- [ ] README.md con guía de estructura
- [ ] .editorconfig para consistencia
- [ ] ESLint con reglas de estructura
- [ ] Prettier configurado
- [ ] Pre-commit hooks (husky + lint-staged)
- [ ] Scripts de generación de código

### Proyecto Pequeño

- [ ] Estructura plana implementada
- [ ] Componentes organizados
- [ ] Utils y helpers separados
- [ ] Estilos globales configurados

### Proyecto Mediano

- [ ] Features identificadas y separadas
- [ ] Hooks extraídos y organizados
- [ ] Services/API client configurado
- [ ] Context providers organizados
- [ ] Routing estructurado
- [ ] Tests organizados por feature
- [ ] Documentación de features

### Proyecto Grande

- [ ] Módulos claramente delimitados
- [ ] API pública de cada módulo definida
- [ ] Event bus implementado
- [ ] Shared components separados
- [ ] Estado modular configurado
- [ ] Lazy loading por módulo
- [ ] Feature flags implementados
- [ ] Monorepo considerado (si aplica)

### Proyecto Enterprise

- [ ] Bounded contexts identificados
- [ ] Ubiquitous language documentado
- [ ] Capas DDD implementadas
- [ ] Domain events configurados
- [ ] Anti-corruption layers donde necesario
- [ ] Arquitectura documentada (ADRs)
- [ ] Testing strategy por capa
- [ ] Monitoring y observabilidad
- [ ] Security audit completado
- [ ] Performance budgets definidos

---

## Recursos y Referencias

### Libros Recomendados
- "Clean Architecture" - Robert C. Martin
- "Domain-Driven Design" - Eric Evans
- "Patterns of Enterprise Application Architecture" - Martin Fowler

### Herramientas
- **nx.dev** - Monorepo tools
- **Turbo** - Incremental builds
- **Storybook** - Component documentation
- **Chromatic** - Visual testing
- **Madge** - Dependency analysis

### Templates Open Source
- [Bulletproof React](https://github.com/alan2207/bulletproof-react)
- [React Enterprise Boilerplate](https://github.com/react-boilerplate/react-boilerplate)

---

## Conclusión

La estructura perfecta no existe. La mejor estructura es la que:

1. **Se adapta a tu equipo actual** - No sobre-ingeniería
2. **Puede crecer contigo** - Permite evolución
3. **Es comprensible** - Nuevos devs se onboardean rápido
4. **Facilita el trabajo** - No lo complica

**Regla de oro**: Empieza simple, refactoriza cuando duele.

**Señal de alarma**: Si pasas más tiempo decidiendo dónde poner un archivo que escribiéndolo, tu estructura es muy compleja.**