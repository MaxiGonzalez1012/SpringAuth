# SpringAuth

**SpringAuth** es una API RESTful desarrollada con **Spring Boot** que implementa autenticación y autorización basada en **JWT (JSON Web Tokens)**. Brinda un sistema seguro de login y registro de usuarios, control de acceso mediante roles, y protección de endpoints a través de filtros personalizados. Es una base sólida para cualquier aplicación backend moderna.

---

## 🔐 Funcionalidades principales

- Registro e inicio de sesión de usuarios.
- Generación y validación de tokens JWT.
- Encriptación de contraseñas con BCrypt.
- Roles de acceso (`USER`, `ADMIN`).
- Filtro personalizado para validación de token.
- Rutas protegidas y públicas claramente definidas.
- Arquitectura clara, escalable y mantenible.

---

## 🧰 Tecnologías utilizadas

- Java 17  
- Spring Boot 3  
- Spring Security  
- Spring Data JPA  
- JWT 
- Lombok  
- MySQL  
- Maven

---

## 🗂️ Estructura del proyecto

```
src/main/java/com/security/demo_jwt/
├── Auth/ → Lógica de login y registro
├── Config/ → Beans, AuthenticationManager y configuración de seguridad
├── Demo/ → Endpoint de prueba protegido
├── Jwt/ → Filtro e implementación de JWT
├── User/ → Entidad usuario, roles y repositorio
└── DemoJwtApplication.java
```


---

## 🧪 Endpoints disponibles

### Autenticación (`/auth`)

| Método | Ruta             | Descripción               | Token Requerido |
|--------|------------------|---------------------------|------------------|
| POST   | `/auth/register` | Registra un nuevo usuario | ❌               |
| POST   | `/auth/login`    | Devuelve token JWT        | ❌               |

**Ejemplo de `RegisterRequest`:**
json
```
{
  "username": "maxi123",
  "password": "securePass",
  "firstname": "Maxi",
  "lastname": "González",
  "country": "Argentina"
}
```

Respuesta (AuthResponse)
```
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5..."
}
```

Endpoints protegidos

|Método	|Ruta	        |Rol requerido |Descripción                   |
|-------|-------------|--------------|------------------------------|
|POST	  |/api/v1/demo	|USER / ADMIN	 |Retorna mensaje de bienvenida |

Para acceder a este endpoint, se debe enviar el token JWT en el header:

```
Authorization: Bearer {token}
```

---

## 👤 Modelo de usuario (User)
La entidad User implementa la interfaz UserDetails y contiene los siguientes campos:

```
Integer id;
String username;
String password;
String firstname;
String lastname;
String country;
Role role;
```

El campo role está definido como un enum:
```
public enum Role {
    ADMIN,
    USER
}
```

- La seguridad se basa en el rol, usando la autoridad ROLE_USER o ROLE_ADMIN.
- El campo username es único y obligatorio, y se utiliza como identificador principal en la autenticación

---

## 🔐 Seguridad y JWT
- JwtAuthenticationFilter intercepta las peticiones y valida el token.
- JwtService genera tokens firmados con HMAC SHA-256 y extrae claims del JWT.
- SecurityConfig define las rutas públicas y privadas.
- ApplicationConfig configura los beans de Spring Security (encoder, manager, etc.).

---

## ⚙️ Configuración inicial

1. Crear base de datos en MySQL:
```
CREATE DATABASE springauth_db;
```
2. Configurar el archivo application.properties:
```
spring.datasource.url=jdbc:mysql://localhost:3306/springauth_db
spring.datasource.username=tu_usuario
spring.datasource.password=tu_contraseña

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```
3. Ejecutar la aplicación:
```
./mvnw spring-boot:run
```

---

## 👤 Autor

Maximiliano González

Estudiante de Ingeniería en Informática – UADE

LinkedIn (https://www.linkedin.com/in/maximiliano-gonzalez-9453ba281/)
