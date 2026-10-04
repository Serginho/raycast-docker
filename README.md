# raycast-docker

Copia local y versionada de la extensión **Docker** para Raycast.

## Origen

- Repositorio: https://github.com/raycast/extensions
- Ruta: `extensions/docker/`
- Commit: `29c078c4a74d44d4ea11fc1704ca143254663775`
- Licencia: MIT (autor original: priithaamer y colaboradores)

## Revisión de seguridad (2026-10-04)

Se ha revisado el código fuente completo, el `package-lock.json`, las imágenes y las
dependencias fork de npm. No se ha encontrado malware ni comportamiento peligroso.

- `src/`: solo habla con el daemon de Docker (socket local, `DOCKER_HOST` o el contexto
  actual de Docker CLI). Sin `eval`, sin `child_process`, sin peticiones de red a terceros,
  sin telemetría. Lee `~/.docker/config.json` y `~/.docker/contexts/` para resolver el contexto.
- `package-lock.json`: 256 paquetes, todos de `registry.npmjs.org` con hash de integridad.
  Ninguna versión afectada por los ataques de supply-chain de 2025 (chalk/debug, etc.).
  Único install script: `esbuild` (dev, oficial).
- `@priithaamer/dockerode@3.3.1-priithaamer.1` y `@priithaamer/docker-modem@3.0.3`:
  comparados con `dockerode@3.3.1` y `docker-modem@3.0.3` originales. Solo cambian el
  nombre del paquete, eliminan el transporte SSH (`ssh2`) y añaden tipos `.d.ts`.
- `assets/` y `metadata/`: PNG válidos, sin datos tras el bloque `IEND`.

## Instalación

```bash
npm ci
npm run dev   # importa la extensión en Raycast
```
