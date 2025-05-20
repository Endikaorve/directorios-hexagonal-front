# Estructura de Carpetas para Arquitectura Hexagonal

## Organización General

```
/src
├── /core
│   ├── /shared
│   │   ├── /domain
│   │   ├── /services
│   │   └── /infrastructure
│   │
│   ├── /pokemon
│   │   ├── /domain
│   │   │   ├── /__tests__
│   │   │   │   └── Pokemon.test.ts
│   │   │   ├── Pokemon.ts
│   │   │   └── PokemonRepository.ts
│   │   │
│   │   ├── /services
│   │   │   ├── /__tests__
│   │   │   │   └── pokemonService.test.ts
│   │   │   └── pokemonService.ts
│   │   │
│   │   └── /infrastructure
│   │       ├── /api
│   │       │   ├── /__tests__
│   │       │   │   └── apiPokemonRepository.test.ts
│   │       │   └── apiPokemonRepository.ts
│   │       └── /file
│   │           ├── /__tests__
│   │           │   └── filePokemonRepository.test.ts
│   │           └── filePokemonRepository.ts
│   │
│   └── /trainer
│       ├── /domain
│       │   ├── /__tests__
│       │   │   └── Trainer.test.ts
│       │   ├── Trainer.ts
│       │   └── TrainerRepository.ts
│       │
│       ├── /services
│       │   ├── /__tests__
│       │   │   └── trainerService.test.ts
│       │   └── trainerService.ts
│       │
│       └── /infrastructure
│           ├── /api
│           │   ├── /__tests__
│           │   │   └── apiTrainerRepository.test.ts
│           │   └── apiTrainerRepository.ts
│           └── /file
│               ├── /__tests__
│               │   └── fileTrainerRepository.test.ts
│               └── fileTrainerRepository.ts
│
└── /ui
    ├── /pages
    ├── /components
    ├── /hooks
    └── /...
```

## Detalles de los componentes

### Contexto Pokemon

- **Domain**:

  - `Pokemon.ts`
  - `PokemonRepository.ts`
  - `/__tests__/Pokemon.test.ts`: Tests unitarios para la entidad Pokemon

- **Services**:

  - `pokemonService.ts`
    - Creación de Pokemon
    - Búsqueda de Pokemon
    - Evolución de Pokemon
  - `/__tests__/pokemonService.test.ts`: Tests unitarios para el servicio de Pokemon

- **Infrastructure**:
  - `/api/apiPokemonRepository.ts`
    - `/__tests__/apiPokemonRepository.test.ts`: Tests para el repositorio de API
  - `/file/filePokemonRepository.ts`
    - `/__tests__/filePokemonRepository.test.ts`: Tests para el repositorio de archivos

### Contexto Trainer

- **Domain**:

  - `Trainer.ts`
  - `TrainerRepository.ts`
  - `/__tests__/Trainer.test.ts`: Tests unitarios para la entidad Trainer

- **Services**:

  - `trainerService.ts`
    - Creación de Trainer
    - Gestión de equipo Pokemon
    - Autenticación de Trainer
  - `/__tests__/trainerService.test.ts`: Tests unitarios para el servicio de Trainer

- **Infrastructure**:
  - `/api/apiTrainerRepository.ts`
    - `/__tests__/apiTrainerRepository.test.ts`: Tests para el repositorio de API
  - `/file/fileTrainerRepository.ts`
    - `/__tests__/fileTrainerRepository.test.ts`: Tests para el repositorio de archivos

### Shared

- **Domain**:

  - Interfaces y tipos compartidos entre contextos
  - Excepciones base
  - Tipos genéricos

- **Services**:

  - Servicios de utilidad compartidos
  - Buses de eventos
  - Mediadores para la comunicación entre contextos

- **Infrastructure**:
  - Implementaciones compartidas
  - Configuraciones comunes
  - Herramientas de logging y monitoreo

## Comunicación entre contextos

Para la comunicación entre los contextos Pokemon y Trainer, se recomienda:

1. Eventos de dominio para comunicación asíncrona
2. Servicios dedicados para consultas entre contextos
3. DTOs para transferir datos entre límites contextuales

## Consideraciones generales

- Cada contexto mantiene su independencia
- La capa de dominio no tiene dependencias externas
- Las interfaces (puertos) se definen en el dominio
- Los adaptadores se implementan en la capa de infraestructura
- La capa de servicios orquesta los casos de uso y actúa como intermediaria entre dominio e infraestructura
- Inyección de dependencias para conectar las capas
