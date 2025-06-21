# myapp-segura

Este repositorio contiene la infraestructura y configuración DevSecOps para los proyectos **backend-devsecops** y **frontend-devsecops**.

---

## 🚦 Estado del Pipeline CodeQL

[![Pipeline DevSecOps](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml/badge.svg)](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml)

El pipeline principal ejecuta pruebas, análisis de seguridad y despliegue continuo para ambos proyectos.

---

## 🔎 Análisis de Calidad y Seguridad (SonarCloud)

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

## 📋 ¿Cómo funciona?

- Cada push o pull request ejecuta el pipeline de CI/CD.
- Se instalan dependencias, se ejecutan pruebas y se realiza el análisis de calidad y seguridad con SonarCloud.
- Los resultados son visibles en los badges de arriba y en los enlaces directos a SonarCloud.

---

## 📊 Enlaces rápidos

- [Pipeline DevSecOps](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml)
- [SonarCloud Backend](https://sonarcloud.io/project/overview?id=navia20_backend-devsecops)
- [SonarCloud Frontend](https://sonarcloud.io/project/overview?id=navia20_frontend-devsecops)