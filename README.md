# Heroes Backend

Backend API en NestJS para gestionar un catálogo de héroes y villanos con búsqueda avanzada, paginación y resumen del dashboard.

## Tecnologías

- NestJS
- TypeScript
- Express
- class-validator
- class-transformer

## Requisitos

- Node.js 18+
- npm

## Instalación

```bash
npm install
```

## Ejecutar la aplicación

```bash
# modo desarrollo
npm run start

# modo watch
npm run start:dev

# modo producción
npm run start:prod
```

La API corre por defecto en:

- http://localhost:3000/api

## Scripts disponibles

```bash
npm run build
npm run start
npm run start:dev
npm run start:debug
npm run test
npm run test:watch
npm run test:cov
npm run lint
```

## Endpoints

Todos los endpoints están prefijados con `/api`.

### Heroes

#### Obtener todos los héroes

```http
GET /api/heroes?limit=6&offset=0&category=all
```

Parámetros opcionales:

- `limit`: número máximo de registros por página
- `offset`: desplazamiento
- `category`: filtro por categoría (`all`, `Hero`, `Villain`)

Respuesta:

```json
{
  "total": 12,
  "pages": 2,
  "heroes": []
}
```

#### Crear héroe

```http
POST /api/heroes
```

Body ejemplo:

```json
{
  "name": "Spider-Man",
  "slug": "spider-man",
  "alias": "Peter Parker",
  "powers": ["Wall-crawling", "Spider-sense"],
  "description": "A young hero with amazing agility.",
  "strength": 85,
  "intelligence": 80,
  "speed": 90,
  "durability": 75,
  "team": "Avengers",
  "image": "https://example.com/spider-man.png",
  "firstAppearance": "Amazing Fantasy #15",
  "status": "Alive",
  "category": "Hero",
  "universe": "Marvel"
}
```

#### Obtener un héroe por id o slug

```http
GET /api/heroes/:id
```

#### Actualizar héroe

```http
PATCH /api/heroes/:id
```

#### Eliminar héroe

```http
DELETE /api/heroes/:id
```

#### Resumen del dashboard

```http
GET /api/heroes/summary
```

Respuesta ejemplo:

```json
{
  "totalHeroes": 10,
  "strongestHero": {
    "name": "Superman"
  },
  "smartestHero": {
    "name": "Batman"
  },
  "heroCount": 6,
  "villainCount": 4
}
```

#### Búsqueda avanzada

```http
GET /api/heroes/search?name=batman&category=hero&strength=80
```

Parámetros opcionales:

- `name`
- `team`
- `category`
- `universe`
- `status`
- `strength`

Devuelve una lista filtrada de héroes.

## Estructura del proyecto

```bash
src/
├── app.module.ts
├── main.ts
├── common/
│   └── dto/
│       └── pagination.dto.ts
├── data/
│   └── heroes.data.ts
├── heroes/
│   ├── dto/
│   │   ├── advande-search.dto.ts
│   │   ├── create-hero.dto.ts
│   │   └── update-hero.dto.ts
│   ├── entities/
│   │   └── hero.entity.ts
│   ├── heroes.controller.ts
│   ├── heroes.module.ts
│   └── heroes.service.ts
└── public/
    └── index.html
```

## Notas

- La validación global está activa con `ValidationPipe`.
- CORS está habilitado para facilitar integración con frontend.
- Los datos se mantienen en memoria durante la ejecución del servidor.

## Autor

Proyecto de backend para consumo desde un frontend de héroes.
