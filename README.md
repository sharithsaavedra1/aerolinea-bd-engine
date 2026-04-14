# airline-db-engine

Repositorio técnico para la estabilización, versionamiento y despliegue del modelo de base de datos PostgreSQL entregado como insumo base.
## enlace del repositorio de documentacion 
https://github.com/sharithsaavedra1/aerolinea-docs-arquitectura 
## enlace del trello https://github.com/sharithsaavedra1/aerolinea-docs-arquitectura

## Propósito

Este repositorio implementa la ruta técnica definida en la prueba:

- Contenerización de PostgreSQL 15.
- Integración de Liquibase.
- Organización del DDL por dominios funcionales.
- Preparación de scripts de datos de prueba.
- Base operativa para continuar el trabajo desescolarizado.

## Estructura

```text
airline-db-engine/
├── modelo_postgresql.sql
├── README.md
├── docker/
│   ├── docker-compose.yml
│   └── README.md
├── liquibase/
│   ├── changelog-master.xml
│   └── changelogs/
│       ├── 001-geography-reference.xml
│       ├── 002-airline.xml
│       ├── 003-identity.xml
│       ├── 004-security.xml
│       ├── 005-customer-loyalty.xml
│       ├── 006-airport.xml
│       ├── 007-aircraft.xml
│       ├── 008-flight-operations.xml
│       ├── 009-sales-reservation-ticketing.xml
│       ├── 010-boarding.xml
│       ├── 011-payment.xml
│       └── 012-billing.xml
└── data/
    ├── README.md
    ├── 001-plan-carga.md
    └── 002-sample-seed.sql
```

## Criterio técnico aplicado

El modelo original no se rehace desde cero. Se conserva como referencia base y se propone su migración gradual hacia Liquibase, respetando la organización por dominios funcionales observada en el script entregado.

## Dominios contemplados

- Geografía y datos de referencia
- Aerolínea
- Identidad
- Seguridad
- Clientes y fidelización
- Aeropuerto
- Aeronaves
- Operaciones de vuelo
- Ventas, reservas y tiquetería
- Abordaje
- Pagos
- Facturación

## Ramas sugeridas

- `develop`: integración de trabajo activo.
- `qa`: validación funcional y técnica.
- `main`: versión estable de entrega.

## Flujo sugerido

1. Levantar PostgreSQL con Docker Compose.
2. Ejecutar Liquibase contra la base vacía.
3. Aplicar los changelogs por dominio funcional.
4. Cargar datos de prueba en orden de dependencias.
5. Validar reconstrucción desde cero con `down -v` y nuevo `up`.
6. Promover cambios desde `develop` a `qa` y luego a `main`.

## Comandos base

```bash
cd docker
docker compose up -d

docker compose run --rm liquibase update

docker compose exec postgres psql -U postgres -d airline_db -f /workspace/data/002-sample-seed.sql
```

## Nota

Los archivos XML de Liquibase incluidos en este repositorio dejan preparada la segmentación por dominio exigida por la prueba. La conversión detallada y completa del DDL puede continuarse de manera incremental durante la fase desescolarizada, manteniendo coherencia con el modelo original.
