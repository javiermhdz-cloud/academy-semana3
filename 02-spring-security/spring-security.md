1) **Qué es el concepto y qué problema resuelve, en tus palabras:** Spring Security es un framework poderoso y flexible que se utiliza para proporcionar autenticación (quién eres) y autorización (qué puedes hacer/a qué tienes acceso) en aplicaciones desarrolladas en Java. En nuestra clase aprendimos sobre los diferentes métodos de acceso Basic, JWT y Oauth2.0 usando Spring Security. Los problemas que este framework resuelve son centralizar los métodos de acceso, previamente mencionados, sin duplicar la lógica de validación. Uno de los beneficios es el manejo seguro de credenciales, porque evita el almacenamiento de contraseñas en texto plano al implementar `BCrypPasswordEncoder` para encriptaras con un hashing seguro. Finalmente como el rest de Spring, centraliza la lógica para filtrar las peticiones HTTP antes de que alcancen los controladores, llamado en el código visto en clase @RestController.

   - HTTP Basic: Comparte el usuario y contraseña codificados en Base64. Como vimos en clase, se utiliza para pruebas rápidas o en integración de microservicios internos.
   - JWT (JSON Web Token): Se validan las credenciales del usuario y se devuelve un token firmado digitalmente que expira con el tiempo. Se utiliza un Bearer token. Como vimos en clase, es un mecanismo de autenticación stateless.
   - OAuth2.0: Este protocolo está construido sobre JWT y, como mencionado en clase, se utiliza principalmente para proveedores. Este mecanismo delega la autorización, donde un proveedor de identidad autentica el usuario con sus respectivas credenciales. Esto es seguro para aplicaciones complejas y con muchas integraciones, debido a que el cliente recibe una autorización sin almacenar contraseñas del usuario. Por consiguiente, la aplicación cliente nunca ve la contraseña del usuario. Dicho en otras palabras, el usuario autentica directamente en la interfaz del Authorization Server (en nuestro caso, Keycloak). El servidor de autorización solamente devuelve a nuestra aplicación de Spring un Access Token (token de acceso). Como resultado, se garantiza que las credenciales del usuario no pasen ni se almacenen en la apliación cliente. Los actores de Oauth 4.0 son los siguientes:
     
      -  Resource Owner (Usuario): El dueño de la cuenta.
      -  Client (Aplicación Cliente): Quiere acceder a los recursos en nombre del usuario.
      -  Authorization Server (Keycloak): Autentica al usuario y emite los tokens.
      -  Resource Server (API Rest): Protege las APIs y valida el token recibido.
   
2) **Dónde se ve en tu código:** En todos los casos, la configuración de seguridad tiene el archivo `SecurityConfig.java`

   - Basic: está configurado con `.httpBasic()` en el archivo `SecurityConfig.java`
   - JWT: tiene las anotaciones para las llaves públicas y privadas. Además, tiene funciones para codificar, decodificar y autenticar el Bearer token en `SecurityConfig.java`. Adicionalmente, tiene otro RestController llamado `AuthController.java`, dónde se expone el endpoint para recibir las credencias y responder con el token usando el método POST.
   - Oauth 2.0: tiene el código simplificado, porque Spring descarga la configuración para la dirección del JWKS y de ahí descarga la llave pública. Con esto, se evita escribir código sobre las llaves, encoder y decoder. Solamente se le tiene que indicar que los tokens son emitidos por otro servidor en el archivo `application.properties`. En nuestro proyecto visto en clase, usamos el servidor de Indetity and Access Management (IAM) para hacer un Single Sign-On (SSO) Keycloak. De esta forma, Keycloak autentica el usuario y emite el JWT lo que da como resultado que la aplicación de Spring no gestiona registro de usuarios, contraseña y tokens.

3) **Qué pasa si no lo usas:** El no usar Spring Security afecta mucho la aplicación de Java. Por ejemplo, las contraseñas están en texto plano, lo cual hace que las credenciales de todos los usuarios queden comprometidas al tener una falla en la seguridad de la base de datos. Además, los endpoints de la aplicación quedan totalmente expuestos al público, lo cual hace que cualquier usuario pueda consumir , modifical o eliminar datos si conoce las rutas Rest, sin necesidad de autenticazación y autorización. Siguiente, no se tendría el bloqueo (**HTTP 401 Unathorized**) a la información con Bearer tokens faltantes, caducados o alterados en el caso de JWT y Oauth2.0. Esto crearía una vulnerabilidad, porque cualquier usuario puede hacer peticiones no autorizadas. Finalmente, el usuario tiene que crear y gestionar contraseñas locales para cada servicio sin la integración del protocolo Oauth2.0.

4) **Cómo correrlo:**
   
   - HTTP Basic:
   ```bash 
   cd 17-seguridad-autenticacion/01-security-basic
   mvnw spring-boot:run
   ```

   - JWT:
   ```bash
   cd 17-seguridad-autenticacion/02-security-jwt
   mvnw spring-boot:run
   ```

   - OAuth2.0:
   ```bash
   cd 17-seguridad-autenticacion/03-security-oauth2
   mvnw spring-boot:run
   ```
