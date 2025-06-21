# myapp-segura

Este repositorio contiene la infraestructura y configuración DevSecOps para los proyectos **backend-devsecops** y **frontend-devsecops**.

---

##  Estado del Pipeline CodeQL

[![Pipeline DevSecOps](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml/badge.svg)](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml)

El pipeline principal ejecuta pruebas, análisis de seguridad, build de imágenes Docker y despliegue continuo para ambos proyectos.

---

##  Análisis de Calidad y Seguridad (SonarCloud)

### Backend

[![SonarCloud Back-devsecops](https://github.com/navia20/backend-devsecops/actions/workflows/sonarcloud.yml/badge.svg)](https://github.com/navia20/backend-devsecops/actions/workflows/sonarcloud.yml)
[Ver análisis en SonarCloud](https://sonarcloud.io/project/overview?id=navia20_backend-devsecops)

El backend es analizado automáticamente en cada push y pull request. El análisis incluye:
- Calidad del código
- Seguridad
- Mantenibilidad
- Duplicación
- (Opcional) Cobertura de tests

---

### Frontend

[![SonarCloud Front-devsecops](https://github.com/navia20/frontend-devsecops/actions/workflows/sonarcloud.yml/badge.svg)](https://github.com/navia20/frontend-devsecops/actions/workflows/sonarcloud.yml)
[Ver análisis en SonarCloud](https://sonarcloud.io/project/overview?id=navia20_frontend-devsecops)

El frontend también es analizado automáticamente en cada push y pull request, con métricas similares a las del backend.

---

##  Build y despliegue de Docker

Ambos proyectos cuentan con un `Dockerfile` y están preparados para ser construidos y ejecutados en contenedores Docker.

- El pipeline ejecuta el build de las imágenes Docker para backend y frontend usando los archivos `Dockerfile` de cada submódulo.
- Se utiliza `docker-compose` para levantar ambos servicios de forma conjunta y facilitar pruebas de integración y despliegue local.
- Los pasos principales del pipeline incluyen:
  - Build de imágenes Docker (`docker build`)
  - Levantado de servicios con Docker Compose (`docker-compose up`)
  - Healthchecks automáticos para verificar que los servicios estén corriendo correctamente

Puedes probar localmente:
```bash
# Desde la raíz del proyecto
# Construir y levantar ambos servicios
 docker-compose up --build
```

---

##  ¿Cómo funciona?

- Cada push o pull request ejecuta el pipeline de CI/CD.
- Se instalan dependencias, se ejecutan pruebas, se realiza el análisis de calidad y seguridad con SonarCloud y se construyen las imágenes Docker.
- Los resultados son visibles en los badges de arriba y en los enlaces directos a SonarCloud.

---

##  Enlaces rápidos

- [Pipeline DevSecOps](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml)
- [SonarCloud Backend](https://sonarcloud.io/project/overview?id=navia20_backend-devsecops)
- [SonarCloud Frontend](https://sonarcloud.io/project/overview?id=navia20_frontend-devsecops)