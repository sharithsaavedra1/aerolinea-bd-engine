# Docker

Esta carpeta contiene la definición de infraestructura mínima para levantar PostgreSQL 15 y ejecutar Liquibase de forma controlada.

## Servicios definidos

- `postgres`: motor PostgreSQL 15.
- `liquibase`: contenedor para aplicar changelogs del proyecto.

## Uso

```bash
cd docker
docker compose up -d
```

Verificar estado:

```bash
docker compose ps
```

Ejecutar migraciones:

```bash
docker compose run --rm liquibase update
```

Reconstrucción total:

```bash
docker compose down -v
docker compose up -d
docker compose run --rm liquibase update
```

## Evidencia sugerida

- Captura del contenedor PostgreSQL en estado `running`.
- Captura de ejecución satisfactoria de Liquibase.
- Registro en `seguimientos.md` del repositorio documental.
