1) **Qué es el concepto y qué problema resuelve, en tus palabras:** Es un framework asincrono y no bloqueante que puede procesar una gran cantidad de peticiones concurrentes con un numero reducido de hilos de sistema operativo.

   - *Mono vs. Flux:*
     - Mono<T>: Es un flujo reactivo asincrono que emite cero o un elemento. Es usado para busquedas por ID, actualizaciones y respuestas.
     - Flux<T>: Representa un flujo reactivo asincrono que emite cero o multiples elementos. Puede transmitir datos de forma continua en el tiempo, ideal para streaming de videos como Netlflix y Youtube.

  - Flujo Lazy: En este caso, nada ocurre en el codigo hasta que alguien se suscribe. La ejecucion real de la tarea o consulta a base de datos se dispara cuando la peticion HTTP de un cliente web solicita los datos.
  - Cuando *NO* vale la pena WebFlux:
    - Operaciones bloqueantes no migradas: Si la aplicacion consulta bases de datos tradicionales o usa librerias sincronas, el hilo de WebFlux se bloquea de todas formas, perdiendo todo el beneficio.
    - Carga de trafico baja: Si la aplicacion *NO* maneja miles de peticiones concurrentes, por ejemplo *I/O*, el modelo declarativo reactivo suma complejidad innecesaria. 

  - Reactivo vs Bloqueate:
    - Comportamiento en Version Bloqueante:
    - 
    - 
3) **Dónde se ve en tu código:** En todos los casos, la configuración de seguridad tiene el archivo `SecurityConfig.java`

   - Basic: está configurado con `.httpBasic()` en el archivo `SecurityConfig.java`
   - JWT: tiene las anotaciones para las llaves públicas y privadas. Además, tiene funciones para codificar, decodificar y autenticar el Bearer token en `SecurityConfig.java`. Adicionalmente, tiene otro RestController llamado `AuthController.java`, dónde se expone el endpoint para recibir las credenciales y responder con el token usando el método POST.
   - Oauth 2.0: tiene el código simplificado, porque Spring descarga la configuración para la dirección del JWKS y de ahí descarga la llave pública. Con esto, se evita escribir código sobre las llaves, encoder y decoder. Solamente se le tiene que indicar que los tokens son emitidos por otro servidor en el archivo `application.properties`. En nuestro proyecto visto en clase, usamos el servidor de Identity and Access Management (IAM) para hacer un Single Sign-On (SSO) Keycloak. De esta forma, Keycloak autentica el usuario y emite el JWT lo que da como resultado que la aplicación de Spring no gestiona registro de usuarios, contraseña y tokens.

4) **Qué pasa si no lo usas:** El no usar Spring Security afecta mucho la aplicación de Java. Por ejemplo, las contraseñas están en texto plano, lo cual hace que las credenciales de todos los usuarios queden comprometidas al tener una falla en la seguridad de la base de datos. Además, los endpoints de la aplicación quedan totalmente expuestos al público, lo cual hace que cualquier usuario pueda consumir , modificar o eliminar datos si conoce las rutas Rest, sin necesidad de autenticación y autorización. Siguiente, no se tendría el bloqueo (**HTTP 401 Unauthorized**) a la información con Bearer tokens faltantes, caducados o alterados en el caso de JWT y Oauth2.0. Esto crearía una vulnerabilidad, porque cualquier usuario puede hacer peticiones no autorizadas. Finalmente, el usuario tiene que crear y gestionar contraseñas locales para cada servicio sin la integración del protocolo Oauth2.0.

5) **Cómo correrlo:**
   
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
