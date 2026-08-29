1) **Qué es el concepto y qué problema resuelve, en tus palabras:** 

   - Unit Testing: Es la metodologia de verificar el comportamiento de una unidad pequeña de codigo de forma aislada, usualmente un metodo o clase. Esto con la finalidad de detectar errores en las fases tempranas del desarrollo de una aplicacion.
     
   - JUnit:
      - Ciclo de Vida (`@BeforeEach`): Esta anotacion permite inicializar el estado del objeto o sus dependencia antes de cada prueba. Asi como esta anotacion, existen diferentes anotaciones que ayudan a ejecutar las pruebas unitarias de forma independiente. Se puede limpiar la memoria o establecer parametros antes o despues de cada prueba.
      - Aserciones (`assertThrows`): Permite validar el error esperado. De esta forma, se comprueba que el codigo lance la excepcion esperada con inputs invalidos o errores de usuario.

   - Mockito:
      - `@Mockito`: crea una instancia falsa de la dependencia.
      - `@InjectMocks`: create la instancia real de la clase que se va a probar y automaticamente inyecta esos mocks en la clase.
      - `when(...).thenReturn(...)`: es usado para configurar un objeto Mock para regresar un value especifico cuando un metodo especifico es llamado.
      - `verify(...)`: es usado para checar si un metodo en especifico fue llamado en un objeto Mock con argumentos exactos. Asimismo, confirma que la clase interactuo con sus colaboradores el numero de veces esperado.

2) *Dónde se ve en tu código:*

   - *Mono:*
      - Simulacion de Latencia No Bloqueante e Inmutabilidad: `EmployeeRepository.java` y `Employee.java`
      - Endpoints Reactivos con `Mono<T>`: `EmployeeRestController.java`
      - Evidencia del Event Loop: `HiloRestController.java`
      - Demostracion de la Propiedad `Lazy`/Evaluaciones en Pruebas: `EmployeeRepositoryTest.java`

   - *Flux:*
      - Emision Asincrona Infinito/Stream Continuo: `SensorService.java`
      - Operadores Reactivos del Flujo: `LecturaRestController.java`
 
3) **Qué pasa si no lo usas:** En esta situacion, ocurriria algo llamado `Thread Starvation`, Agotamiento de Hilos. Al tener una arquitectura de microservicios con alta latencia de red u operaciones I/O intensas, el servidor Tomcat agota su cantidad de hilos disponibles lo cual resulta en un aumento en el tiempo de respuesta. Asimismo, se consumo una mayor cantidad de recursos, porque para mantener miles de hilos activos en el sistema operativo se necesita memoria RAM y CPU.

4) **Cómo correrlo:**

   - Mono:
   ```bash
   cd 01-webflux-mono
   mvnw.cmd clean spring-boot:run
   ```

   - Flux:
   ```bash
   cd 02-webflux-flux
   mvnw.cmd clean spring-boot:run
   ```

   
