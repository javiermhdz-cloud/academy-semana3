1) **Qué es el concepto y qué problema resuelve, en tus palabras:** Es un framework asincrono y no bloqueante que puede procesar una gran cantidad de peticiones concurrentes con un numero reducido de hilos de sistema operativo.

   - *Flujo (Reactive Stream):* Es una secuencia continua de datos o eventos emitidos a lo largo del tiempo de forma asincrona. Como aprendido en clase, un flujo reactivo procesa los datos a medida que van llegando o generandose. Un flujo puede tener tres tipos de señales:
     - Dato (onNext): Emite el elemento producido.
     - Error (onError): Notifica que ocurrio un fallo y detiene el flujo.
     - Completado (onComplete): Notifica que ya no van a haber mas elementos y el flujo finalizo con exito.
   - *Mono vs. Flux:*
     - Mono<T>: Es un flujo reactivo asincrono que emite cero o un elemento. Es usado para busquedas por ID, actualizaciones y respuestas.
     - Flux<T>: Representa un flujo reactivo asincrono que emite cero o multiples elementos. Puede transmitir datos de forma continua en el tiempo, ideal para streaming de videos como Netlflix y Youtube.

   - Flujo Lazy: En este caso, nada ocurre en el codigo hasta que alguien se suscribe. La ejecucion real de la tarea o consulta a base de datos se dispara cuando la peticion HTTP de un cliente web solicita los datos.
     - Cuando *NO* vale la pena WebFlux:
       - Operaciones bloqueantes no migradas: Si la aplicacion consulta bases de datos tradicionales o usa librerias sincronas, el hilo de WebFlux se bloquea de todas formas, perdiendo todo el beneficio.
       - Carga de trafico baja: Si la aplicacion *NO* maneja miles de peticiones concurrentes, por ejemplo *I/O*, el modelo declarativo reactivo suma complejidad innecesaria. 

     - Reactivo vs Bloqueante:
    
       - Comportamiento en Version Bloqueante (Spring MVC/Tomcat):
          - Cada peticion HTTP entrante consume un hilo del servidor de peticiones
          - Situacion 100 peticiones: Si 1000 usuarios realizan peticiones simultaneas a un endpoint que tarda 5 segundos en responder, el servidor bloquea 100 hilos durante 5 segundos completos consumiento memoria. Al agotarse los hilos disponibles, las siguientes peticiones quedan en cola o fallan por timeout.
          
       - Comportamiento en Version Reactiva (Spring WebFlux):
          - WebFlux procesa las peticiones mediante un `Event Loop` utilizando pocos hilos (generalmente 1 hilo por nucleo de CPU).
          - Situacion 100 peticiones: En la misma situacion de 100 peticiones con un retraso de 5 segundos, el hilo registrz la tarea asincrona y queda inmediatamente libre para aceptar nuevas conexiones. Pasados los 5 segundos, una notificacion de evento avisa que el dato esta lista y el servidor da una respuesta sin haber pausado o retenido los hilos.

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

   
