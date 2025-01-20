# Microservicios Chidos 🤠

Este proyecto consiste en una arquitectura de microservicios que incluye servicios independientes para la gestión de cursos y estudiantes. Los servicios se comunican utilizando Feign y manejan entidades como estudiantes y cursos, con operaciones RESTful para crear, asignar y consultar.

## Características

- **Microservicio de Cursos:** Gestiona la creación, consulta y asignación de estudiantes a cursos.
- **Microservicio de Estudiantes:** Proporciona operaciones CRUD para la entidad de estudiantes.
- **Comunicación entre servicios:** Implementada con Feign para realizar llamadas entre microservicios.
- **Persistencia de datos:** Utiliza una base de datos relacional manejada por JPA/Hibernate.

---

## Tecnologías utilizadas

- **Java 17**  
- **Spring Boot 3.1.x**
- **Spring Data JPA**
- **PostgreSQL**
- **Feign** para comunicación entre microservicios
- **Docker** para contenerización
- **Maven** como herramienta de construcción

---

## Endpoints principales

### Microservicio de Cursos

**Base URL:** `http://localhost:8003/api/cursos`

- **Listar cursos**
  ```http
  GET /api/cursos
  ```

- **Buscar curso por ID**
  ```http
  GET /api/cursos/{id}
  ```

- **Crear un curso**
  ```http
  POST /api/cursos
  Content-Type: application/json

  {
      "nombre": "Curso de Java",
      "descripcion": "Introducción a Java 17"
  }
  ```

- **Asignar estudiante a un curso**
  ```http
  PUT /api/cursos/asignar-estudiante/{cursoId}
  Content-Type: application/json

  {
      "id": 7,
      "nombre": "Bandida 5",
      "apellido": "Desconocido",
      "email": "bandidita@uce.com",
      "fechaNacimiento": "2002-02-19",
      "telefono": "0982343621",
      "creadoEn": "2025-01-19T20:32:57"
  }
  ```

### Microservicio de Estudiantes

**Base URL:** `http://localhost:8002/api/estudiantes`

- **Listar estudiantes**
  ```http
  GET /api/estudiantes
  ```

- **Buscar estudiante por ID**
  ```http
  GET /api/estudiantes/{id}
  ```

- **Crear un estudiante**
  ```http
  POST /api/estudiantes
  Content-Type: application/json

  {
      "nombre": "Bandida 5",
      "apellido": "Desconocido",
      "email": "bandidita@uce.com",
      "fechaNacimiento": "2002-02-19",
      "telefono": "0982343621"
  }
  ```

---

## Ejecución con Docker

### Requisitos

- Docker y Docker Compose instalados

### Pasos

1. Genera los archivos `JAR` para los microservicios:
   ```bash
   mvn clean install
   ```

2. Construye las imágenes de Docker:
   ```bash
   docker-compose build
   ```

3. Inicia los contenedores:
   ```bash
   docker-compose up
   ```

4. Accede a los servicios desde los puertos configurados (e.g., `8003` para cursos, `8002` para estudiantes).

---

## Estructura del proyecto

```
Microservicios Chidos
├── micro-cursos
│   ├── src/main/java/com/espe/micro_cursos
│   ├── Dockerfile
│   └── ...
├── micro-estudiantes
│   ├── src/main/java/com/espe/micro_estudiantes
│   ├── Dockerfile
│   └── ...
├── docker-compose.yml
└── README.md
```

---

## Notas importantes

1. **Formato de fechas:** Se debe respetar el formato ISO 8601 para los campos `LocalDate` (`yyyy-MM-dd`) y `LocalDateTime` (`yyyy-MM-dd'T'HH:mm:ss`).
2. **Errores comunes:** Verifica que las URLs en Feign estén configuradas correctamente y que los IDs enviados en las solicitudes sean válidos.
3. **Extensibilidad:** Puedes añadir más microservicios o funcionalidades siguiendo la misma estructura modular.
