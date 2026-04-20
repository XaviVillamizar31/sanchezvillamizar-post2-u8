## Gestión Académica con Spring Boot y JPA/Hibernate
Programación Web — Unidad 8: Persistencia con JPA/Hibernate
Universidad de Santander (UDES) — Ingeniería de Sistemas 2026

## Descripción
Aplicación web de gestión académica implementada con Spring Boot, Spring Data JPA e Hibernate como ORM. Extiende el proyecto del Post-Contenido 1 agregando la entidad Curso y configurando una relación @ManyToMany bidireccional con Estudiante. La tabla de unión curso_estudiante es gestionada automáticamente por Hibernate mediante @JoinTable. Se resuelve el problema N+1 utilizando JOIN FETCH en las consultas del repositorio.

## Diagrama ER
```
+----------------+        +-------------------+        +-------------+
|  estudiantes   |        |  curso_estudiante  |        |   cursos    |
+----------------+        +-------------------+        +-------------+
| PK id          |<------>| FK estudiante_id  |        | PK id       |
|    nombre      |        | FK curso_id       |<------>|    nombre   |
|    apellido    |        +-------------------+        |    creditos |
|    email       |                                     +-------------+
+----------------+
```

Cardinalidad: Un estudiante puede inscribirse en muchos cursos.
              Un curso puede tener muchos estudiantes inscritos. (N:M)

## Estructura del proyecto
```
estudiantes/
├── src/main/java/com/universidad/estudiantes/
│   ├── EstudiantesApplication.java
│   ├── model/
│   │   ├── Estudiante.java
│   │   └── Curso.java
│   ├── repository/
│   │   ├── EstudianteRepository.java
│   │   └── CursoRepository.java
│   ├── service/
│   │   ├── EstudianteService.java
│   │   └── CursoService.java
│   └── controller/
│       ├── EstudianteController.java
│       └── CursoController.java
├── src/main/resources/
│   ├── application.properties
│   └── templates/
│       ├── estudiantes/
│       │   ├── lista.html
│       │   ├── formulario.html
│       │   └── confirmar-eliminar.html
│       └── cursos/
│           ├── lista.html
│           ├── formulario.html
│           └── inscribir.html
└── pom.xml
```
## Prerrequisitos

Java Development Kit (JDK) 17 o superior
Apache Maven 3.8+
IntelliJ IDEA
MySQL 8.0+
Navegador web moderno (Chrome, Firefox)

## Configuración de base de datos
Crear la base de datos en MySQL antes de ejecutar:
sqlCREATE DATABASE estudiantes_db;
Configurar las credenciales en application.properties:
propertiesspring.datasource.url=jdbc:mysql://localhost:3306/estudiantes_db
spring.datasource.username=root
spring.datasource.password=tu_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

## Instrucciones de ejecución
Clonar el repositorio y abrir en IntelliJ
Configurar las credenciales de MySQL en application.properties
Ejecutar en la terminal:

bashmvn spring-boot:run

Esperar a ver en consola Started EstudiantesApplication
Abrir el navegador:

Estudiantes: http://localhost:8080/estudiantes
Cursos: http://localhost:8080/cursos



## Funcionalidades implementadas
Listar todos los cursos con el número de estudiantes inscritos
Crear nuevo curso con nombre y créditos
Inscribir un estudiante en un curso desde la vista de inscripción
Desinscribir un estudiante de un curso
Relación @ManyToMany bidireccional gestionada con helper methods en la entidad
Optimización N+1 resuelta con JOIN FETCH en CursoRepository
Tabla de unión curso_estudiante generada automáticamente por Hibernate

## Capturas de pantalla
Lista de cursos con estudiantes inscritos
<img width="960" height="480" alt="image" src="https://github.com/user-attachments/assets/ada017af-2831-43e6-8ab6-55a5b70e359c" />
Formulario de creación de nuevo curso
<img width="1912" height="914" alt="image" src="https://github.com/user-attachments/assets/1c7b1623-d47e-43f5-82c8-28947cd96869" />

Vista de inscripción de estudiantes a un curso
<img width="1912" height="914" alt="image" src="https://github.com/user-attachments/assets/0c578abf-d526-4160-acb8-eaf193d5f5ee" />

Tabla curso_estudiante en MySQL con inscripciones registradas
<img width="1724" height="838" alt="image" src="https://github.com/user-attachments/assets/0951d82f-4cda-4e9d-a4d3-1a49408f0246" />

Consulta JOIN FETCH en consola — sin problema N+1
<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/525b1546-f0de-43fb-858e-d968a78a3f6c" />

