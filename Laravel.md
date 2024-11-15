

### **Prueba Técnica para Desarrollador Backend (Laravel PHP)**

**Objetivo:**  
El objetivo de esta prueba es evaluar la capacidad del candidato para desarrollar una API RESTful con Laravel que gestione un catálogo de productos. Queremos observar la estructura del código, la separación de responsabilidades y la capacidad para crear un código escalable y mantenible bajo los principios de Clean Architecture (Arquitectura Limpia).

***

### **Requerimientos:**

1. **Contexto del Proyecto:**
   - Crear una API para gestionar productos en un catálogo de tienda online. Los productos tendrán los siguientes atributos:
     -	id: Identificador único del producto (auto-generado).
	   -	name: Nombre del producto (cadena).
	   -	description: Descripción del producto (cadena).
	   -	price: Precio del producto (decimal).
	   -	category: Categoría a la que pertenece el producto (cadena).
	   -	created_at: Fecha de creación (automática).

2. **Funcionalidades requeridas:**
   La API debe permitir las siguientes operaciones:
   
   - **Crear un producto**:
     - Ruta: `/products`
     - Cuerpo de la petición (JSON):
       ```json
       {
         "name": "string",
         "description": "string",
         "price": "number",
         "category": "string"
       }
       ```
     - Respuesta: Retornar el producto creado con su `id` y `createdAt`.

   - **Listar todos los productos**:
     - Ruta: `/products`
     - Respuesta: Lista de todos los productos.

   - **Obtener un producto por ID**:
     - Ruta: `/products/:id`
     - Respuesta: Detalles del producto correspondiente al `id`.

   - **Actualizar un producto**:
     - Ruta: `/products/:id`
     - Cuerpo de la petición (opcional):
       ```json
       {
         "name": "string",
         "description": "string",
         "price": "number",
         "category": "string"
       }
       ```
     - Respuesta: El producto actualizado.

   - **Eliminar un producto**:
     - Ruta: `/products/:id`
     - Respuesta: Mensaje de confirmación de eliminación.

3. **Arquitectura:**
   Implementar la API siguiendo los principios de Clean Architecture, donde el código se divide en capas claramente separadas. Cada capa debe tener responsabilidades definidas. Las capas sugeridas son:

     ```
    app/
    ├── Domain/
    │   ├── Entities/
    │   │   └── Product.php
    │   ├── Repositories/
    │   │   └── ProductRepositoryInterface.php
    │   └── UseCases/
    │       ├── CreateProduct.php
    │       ├── UpdateProduct.php
    │       ├── DeleteProduct.php
    │       └── GetProducts.php
    ├── Infrastructure/
    │   ├── Persistence/
    │   │   └── ProductRepository.php
    │   └── Framework/
    │       └── Laravel/
    │           └── Controllers/
    │               └── ProductController.php
    ├── Providers/
    │   └── RepositoryServiceProvider.php
    routes/
    ├── api.php
    ```

4. **Requisitos Técnicos:**
   - Crea un proyecto usando la última versión de Laravel.
   - Utiliza MySQL o SQLite para gestionar los datos.
   - Sigue buenas prácticas de Laravel, utilizando Eloquent para la gestión de modelos y Controllers para la lógica de la API.
   - Utiliza las reglas de validación de Laravel en las solicitudes para asegurarte de que los datos enviados por el cliente sean válidos.
   - Implementa un manejo adecuado de errores y devuelve respuestas HTTP coherentes (códigos como 400, 404, 500, etc.).
   - Organizar el código de manera clara y modular.
   - No es necesario implementar un frontend.
   - No es necesario tener muchos productos, 3 son suficientes.

***

### **Opcional: Implementar Autenticación y Autorización usando JWT**

Como apartado opcional, se solicita que implementes una capa de seguridad utilizando **JWT (JSON Web Token)** para autenticar y autorizar las peticiones a la API. Los tokens se deben generar cuando el usuario inicie sesión y se deben verificar en las solicitudes protegidas.

### **Requerimientos adicionales:**

1. **Ruta de autenticación:**
   - Crea una nueva ruta para que los usuarios inicien sesión y obtengan un token JWT.
   - Ruta: `/auth/login`
   - Cuerpo de la petición (JSON):
     ```json
     {
       "username": "string",
       "password": "string"
     }
     ```
   - La respuesta debe incluir un **token JWT** válido si las credenciales son correctas.
   - Puedes usar un conjunto fijo de credenciales o simular una autenticación básica.

2. **Protección de rutas:**
   - Protege las rutas que gestionan productos (`/products`, `/products/:id`, `/products/:id`) con autenticación JWT.
   - El token debe ser enviado en el encabezado `Authorization` usando el formato: `Bearer <token>`.
   - Si el token es inválido o no está presente, se debe devolver un código de estado `401 Unauthorized`.

3. **Verificación del token:**
   - Implementa un middleware para validar el token JWT antes de permitir el acceso a las rutas protegidas.
   - El middleware debe verificar el token y, si es válido, permitir el acceso a la siguiente capa. Si no es válido, debe rechazar la solicitud con un mensaje de error.

### **Ejemplo de flujo:**

1. El usuario envía una solicitud a `/auth/login` con su `username` y `password`.
2. Si las credenciales son correctas, se genera un token JWT y se devuelve al cliente.
3. El cliente incluye el token en el encabezado `Authorization` para las siguientes solicitudes a rutas protegidas.
4. El middleware de autenticación verifica el token en cada solicitud. Si el token es válido, se permite el acceso a la API; de lo contrario, se devuelve un error `401 Unauthorized`.

### **Criterios de evaluación adicionales:**
   - Correcta implementación del flujo de autenticación y autorización con JWT.
   - Uso de pruebas unitarias o de integración con Pest o PHPUnit.
   - Seguridad en la gestión y verificación de tokens.
   - Limpieza y modularidad del código, manteniendo los principios de Clean Architecture.

***

### **Entrega:**

1. Sube el código a un repositorio público en GitHub (o privado y compartir acceso).
2. Incluir un archivo **README** con:
   - Instrucciones para ejecutar el proyecto.
   - Descripción de la arquitectura y las decisiones de diseño tomadas.
   - Menciones a cualquier funcionalidad opcional añadida (por ejemplo, manejo de errores, validación de datos, etc.).
   - Link a video explicativo del proyecto de más o menos 10 minutos de duración donde se vea el proyecto corriendo en local y adicional mostrando el código desarrollado (Utilizar cualquier herramienta gratuita, sugerimos Loom https://www.loom.com) indicar tambien los retos que te enfrentaste en el código.

### **Criterios de Evaluación:**

1. **Estructura del Proyecto**: 
   - ¿Está el proyecto bien organizado según los principios de Clean Architecture?
   - ¿Están las responsabilidades bien distribuidas entre las diferentes capas?

2. **Código limpio y legible**:
   - ¿El código es claro, bien comentado, y sigue buenas prácticas?
   - ¿Es fácil de entender y mantener?

3. **Cumplimiento de Requerimientos**: 
   - ¿La API cumple con todas las funcionalidades solicitadas (crear, listar, obtener, actualizar y eliminar productos)?
   - Importante: Se evaluará el manejo de GIT en el proyecto (avance progresivo en cada commit, uso de ramas, etc).

4. **Manejo de errores**: 
   - ¿Cómo se gestionan los errores, tanto a nivel de validación de datos como de errores de lógica?

5. **Extras (no obligatorios, pero valorados)**:
   - Pruebas unitarias o de integración para la lógica de negocio.
   - Implementación de validaciones de entrada para las solicitudes HTTP.

### **Tiempo Estimado**: 
El candidato debería poder completar la prueba en **4 a 8 horas** de acuerdo a su experiencia, aunque se da flexibilidad en el tiempo de entrega (3 días).
