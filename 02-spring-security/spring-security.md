1) Qué es el concepto y qué problema resuelve, en tus palabras - Spring Security es un framework poderoso y flexible que se utiliza para proporcionar autenticación (quién eres) y autorización (qué puedes hacer/a qué tienes acceso) en aplicaciones desarrolladas en Java. En nuestra clase aprendimos sobre los diferentes métodos de acceso Basic, JWT y Oauth2.0 usando Spring Security. Los problemas que este framework resuelve son centralizar los métodos de acceso, previamente mencionados, sin duplicar la lógica de validación. Uno de los beneficios es el manejo seguro de credenciales, porque evita el almacenamiento de contraseña en texto plano al implementar algoritmos de hashing. Finalmente como el rest de Spring, centraliza la lógica para filtrar las peticiones HTTP antes de que alcancen los controladores, llamado en el código visto en clase @RestController.
   - HTTP Basic: Comparte el usuario y contraseña codificados en Base64. Como vimos en clase, se utiliza para pruebas rápidas o en integración de microservicios internos.
   - JWT (JSON Web Token): Se validan las credenciales del usuario y se devuelve un token firmado digitalmente que expira con el tiempo. Se utiliza un Bearer token. Como vimos en clase, es un mecanismo de autenticación stateless.
   - OAuth2.0: Este protocolo está construido sobre JWT y, como mencionado en clase, se utiliza principalmente para proveedores. Este mecanismo delega la autorización, donde un proveedor de identidad autentica el usuario con sus respectivas credenciales. Esto es seguro para aplicaciones complejas y con muchas integraciones, debido a que el cliente recibe una autorización sin almacenar contraseñas del usuario.
   
2) Dónde se ve en tu código -

3) Qué pasa si no lo usas - El no usar Spring Security afecta mucho la aplicación de Java. Por ejemplo, las contraseñas están en texto plano, lo cual hace que las credenciales de todos los usuarios queden comprometidas al tener una falla en la seguridad de la base de datos. Además, los endpoints de la aplicación quedan totalmente expuestos al público, lo cual hace que cualquier usuario pueda consumir , modifical o eliminar datos si conoce las rutas Rest, sin necesidad de autenticazación y autorización. Siguiente, no se tendría el bloqueo a la información con Bearer tokens caducados o alterados en el caso de JWT y Oauth2.0. Finalmente, el usuario tiene que crear y gestionar contraseñas locales para cada servicio sin la integración del protocolo Oauth2.0.

4) Cómo correrlo -

    1- Compilar y levantar la aplicación Spring Boot
   `mvn spring-boot:run`

   2- Probar login JWT y obtener el token (o hacer petición con HTTP Basic)
   `curl -X POST http://localhost:8080/api/v1/auth/login -H "Content-Type: application/json" -d '{"username":"user","password":"password"}'  `
