# 🛡️ MiApp Segura – DevSecOps Web Application

Este repositorio documenta y contiene una solución web full-stack segura, construida bajo una arquitectura desacoplada y orientada a principios de desarrollo seguro (DevSecOps). La aplicación permite la autenticación básica de usuarios y la gestión de notas personales, y está compuesta por un backend desarrollado en **NestJS** y un frontend implementado con **React + Vite + TypeScript**.

El enfoque principal del proyecto fue diseñar e integrar un pipeline de **Integración y Entrega Continua (CI/CD)**, utilizando **GitHub Actions** como plataforma de automatización. Se incorporaron controles de seguridad automatizados desde etapas tempranas del desarrollo, incluyendo análisis estático del código con **SonarCloud**, pruebas de construcción con **Docker**, validación funcional de los contenedores y publicación de artefactos.

Esta solución busca cumplir con las buenas prácticas del desarrollo moderno y seguro, asegurando que cada componente del sistema sea validado automáticamente antes de su despliegue. Todos los servicios están completamente contenerizados y orquestados mediante **Docker Compose**, permitiendo una ejecución coherente tanto en entornos locales como remotos.

Además, se utilizó un enfoque modular y reutilizable, favoreciendo la escalabilidad y la mantenibilidad de la aplicación. Las tecnologías y herramientas empleadas son 100% gratuitas y de código abierto, con el objetivo de fomentar la reproducibilidad académica, la colaboración y el aprendizaje de prácticas DevSecOps en contextos reales de desarrollo.

---

## 📌 Tabla de Contenidos

- [🎯 Objetivo General](#🎯-objetivo-general)
- [✅ Objetivos Específicos](#✅-objetivos-específicos)
- [🛠️ Tecnologías y Herramientas](#🛠️-tecnologías-y-herramientas)
- [🧱 Arquitectura del Proyecto](#🧱-arquitectura-del-proyecto)
- [🐳 Dockerización](#🐳-dockerización)
- [🛠️ Estado del Pipeline CodeQL](#🛠️-estado-del-pipeline-codeql)
- [🧪 Análisis de Calidad y Seguridad (SonarCloud)](#🧪-análisis-de-calidad-y-seguridad-sonarcloud)
  - [🔍 Backend](#🔍-backend)
  - [🎨 Frontend](#🎨-frontend)
- [🚀 Build y despliegue de Docker](#🚀-build-y-despliegue-de-docker)
- [⚙️ ¿Cómo funciona?](#⚙️-cómo-funciona)
- [🔗 Enlaces rápidos](#🔗-enlaces-rápidos)

---

## 🎯 Objetivo General

Diseñar e implementar un pipeline DevSecOps funcional para una aplicación modular web, incorporando buenas prácticas de seguridad desde el desarrollo hasta la entrega continua.

---

## ✅ Objetivos Específicos

- Construir una aplicación desacoplada con frontend y backend separados.
- Implementar contenedores Docker funcionales y orquestados.
- Automatizar la construcción, validación y análisis de seguridad con GitHub Actions.
- Integrar SonarCloud para evaluar la calidad y seguridad del código.

---

## 🛠️ Tecnologías y Herramientas

| Tipo              | Herramienta                                                            |
| ----------------- | ---------------------------------------------------------------------- |
| Backend           | [NestJS](https://nestjs.com/) + TypeORM                                |
| Frontend          | [React](https://react.dev/) + [Vite](https://vitejs.dev/) + TypeScript |
| Contenedores      | [Docker](https://www.docker.com/), Docker Compose                      |
| CI/CD             | [GitHub Actions](https://docs.github.com/actions)                      |
| Análisis estático | [SonarCloud](https://sonarcloud.io/)                                   |
| Base de Datos     | [Supabase](https://supabase.com/)                                      |

Durante el proyecto se utilizaron tecnologías modernas para construir una solución segura y automatizada. El backend fue desarrollado con NestJS y conectado a Supabase, mientras que el frontend se implementó con React, Vite y TypeScript. Ambos módulos fueron contenerizados con Docker y orquestados mediante Docker Compose. Para la automatización del flujo CI/CD se usó GitHub Actions, y el análisis de calidad del código se realizó con SonarCloud, permitiendo detectar vulnerabilidades y mantener buenas prácticas de desarrollo.

---

## 🧱 Arquitectura del Proyecto

El repositorio principal (`myapp-segura`) alberga la raíz del proyecto y los submódulos de backend y frontend, definidos en `.gitmodules`. Allí mismo reside `docker-compose.yml`, responsable de orquestar y ejecutar los Dockerfiles de ambos servicios a partir de un solo comando, lo que simplifica el arranque local y el despliegue coherente de toda la solución.

```
myapp-segura/
├── .github/workflows/
├── docker-compose.yml
├── backend-devsecops/ # Submódulo NestJS
└── frontend-devsecops/ # Submódulo React/Vite
```

En el backend se empleó `NestJS` junto con `TypeORM` para conectar de forma segura con la base de datos `Supabase`. La estructura está organizada en módulos independientes (autenticación y notas), cada uno con sus controladores, servicios, entidades y DTO s. Esta separación facilita la escalabilidad: basta agregar nuevos módulos sin modificar la lógica existente.

```text
backend-devsecops/
├── .github/
├── dist/
├── node_modules/
├── src/
│   ├── migrations/
│   ├── modules/
│   │   ├── auth/
│   │   ├── notes/
│   │   │   ├── DTOs/
│   │   │   ├── entity/
│   │   │   ├── notes.controller.ts
│   │   │   ├── notes.module.ts
│   │   │   └── notes.service.ts
│   │   └── users/
│   ├── app.controller.ts
│   ├── app.module.ts
│   └── main.ts
```

El frontend, construido con `React + Vite + TypeScript`, sigue una arquitectura modular clara: la carpeta api centraliza las llamadas al backend, assets conserva recursos estáticos y components agrupa vistas reutilizables. Archivos clave como App.tsx, main.tsx, index.css y vite-env.d.ts conforman el punto de entrada y la configuración global de tipos, favoreciendo la legibilidad y el trabajo colaborativo.

```text
frontend-devsecops/
├── public/
│   └── index.html
├── src/
│   ├── api/                     # Lógica de conexión con el backend
│   ├── assets/                  # Archivos estáticos
│   ├── components/              # Componentes reutilizables de la interfaz
│   ├── App.tsx
│   ├── App.css
│   ├── index.css
│   ├── main.tsx
│   └── vite-env.d.ts
├── Dockerfile
├── eslint.config.js
├── package.json
├── package-lock.json
├── tsconfig.json
├── vite.config.ts
```

---

## 🐳 Dockerización

Cada módulo (frontend y backend) tiene su propio `Dockerfile`. Desde el repositorio raíz, se orquesta todo mediante `docker-compose`:

```bash
# Construir y levantar la aplicación
docker-compose up --build

# Detener contenedores
docker-compose down
```

Revisar configuración en [`docker-compose.yml`](docker-compose.yml).

---

## 🛠️ Estado del Pipeline CodeQL

[![Pipeline DevSecOps](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml/badge.svg)](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml)

El pipeline principal ejecuta pruebas, análisis de seguridad, build de imágenes Docker y despliegue continuo para ambos proyectos.

---

## 🧪 Análisis de Calidad y Seguridad (SonarCloud)

### 🔍 Backend

[![SonarCloud Back-devsecops](https://github.com/navia20/backend-devsecops/actions/workflows/sonarcloud.yml/badge.svg)](https://github.com/navia20/backend-devsecops/actions/workflows/sonarcloud.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=navia20_backend-devsecops&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=navia20_backend-devsecops)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=navia20_backend-devsecops&metric=vulnerabilities)](https://sonarcloud.io/summary/new_code?id=navia20_backend-devsecops)
[Ver análisis en SonarCloud](https://sonarcloud.io/project/overview?id=navia20_backend-devsecops)

El backend es analizado automáticamente en cada push y pull request. El análisis incluye:

- Calidad del código
- Seguridad
- Mantenibilidad
- Duplicación
- (Opcional) Cobertura de tests

---

### 🎨 Frontend

[![SonarCloud Front-devsecops](https://github.com/navia20/frontend-devsecops/actions/workflows/sonarcloud.yml/badge.svg)](https://github.com/navia20/frontend-devsecops/actions/workflows/sonarcloud.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=navia20_frontend-devsecops&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=navia20_frontend-devsecops)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=navia20_frontend-devsecops&metric=vulnerabilities)](https://sonarcloud.io/summary/new_code?id=navia20_frontend-devsecops)
[Ver análisis en SonarCloud](https://sonarcloud.io/project/overview?id=navia20_frontend-devsecops)

El frontend también es analizado automáticamente en cada push y pull request, con métricas similares a las del backend.

---

## 🚀 Build y despliegue de Docker

Ambos proyectos cuentan con un `Dockerfile` y están preparados para ser construidos y ejecutados en contenedores Docker.

- El pipeline ejecuta el build de las imágenes Docker para backend y frontend usando los archivos `Dockerfile` de cada submódulo.
- Se utiliza `docker-compose` para levantar ambos servicios de forma conjunta y facilitar pruebas de integración y despliegue local.
- Los pasos principales del pipeline incluyen:
  - Build de imágenes Docker (`docker build`)
  - Levantado de servicios con Docker Compose (`docker-compose up`)
  - Healthchecks automáticos para verificar que los servicios estén corriendo correctamente

Puedes probar localmente:

```bash
# Clona el repositorio raíz con submódulos
git clone --recurse-submodules https://github.com/usuario/myapp-segura.git

# Entrar al proyecto
cd myapp-segura

# Levantar con Docker Compose
docker-compose up --build
```

---

## ⚙️ ¿Cómo funciona?

- Cada push o pull request ejecuta el pipeline de CI/CD.
- Se instalan dependencias, se ejecutan pruebas, se realiza el análisis de calidad y seguridad con SonarCloud y se construyen las imágenes Docker.
- Los resultados son visibles en los badges de arriba y en los enlaces directos a SonarCloud.

---

## 🔗 Enlaces rápidos

- [Pipeline DevSecOps](https://github.com/EduM1randa/myapp-segura/actions/workflows/pipeline.yml)
- [SonarCloud Backend](https://sonarcloud.io/project/overview?id=navia20_backend-devsecops)
- [SonarCloud Frontend](https://sonarcloud.io/project/overview?id=navia20_frontend-devsecops)
