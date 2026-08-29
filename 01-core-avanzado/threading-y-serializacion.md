1) **Qué es el concepto y qué problema resuelve, en tus palabras:**

  - Hilos: Permiten ejecutar múltiples tareas en paralelo aprovechando procesadores multinúcleo. `ExecutorService` evita la sobrecarga de instanciar hilos manualmente (uno por uno).
  - El problema de la concurrencia (¿Qué pasa cuándo dos hilos tocan el mismo dato y cómo lo resuelves?): Como visto en clase, se crea una condición de carrera (race condition) cuando dos hilos tocan el mismo dato. Esto puede resultar en que los datos pierdan actualizaciones o que el valor final quede corrupto e inconsistente. Se resuelve aplicando mecanismos de seguridad, conocidos como thread-safety. Aprendimos en clase que se usan bloques de exclusión mutua (`synchronized`), tipos atómicos (`AtomicInteger`) o colecciones concurrentes (`ConcurrentHashMap`).
  - Archivos (Leer y escribir archivos): Proporciona la habilidad al programador de leer, escribir y manipular rutas en el sistema de archivos usando `java.nio.file.Files` o con `FileInputStream`/`FileOutputStream` (Streams). Para poder gestionar los recursos de forma segura, se utiliza `try-with-resources`. Como resultado, se garantiza que los descriptores de archivos (files descriptor) se cierren automáticamente sin fugas de memoria (memory leaks).
  - Serialización (Guardar un objeto a disco y volverlo a leer): En el código es llamado `Serializable`. Esto es un proceso para convertir el estado de un objeto Java a un flujo de bytes para almacenar en disco duro o transmitirlo por red. Posteriormente, se reconstruye en la memoria. Todo esto es posible con `ObjectInputStream` y `ObjectOutputStream`.
  - ¿Por qué exoste el `serialVersionUID`?: Es un identificador de versión que garantiza la compatibilidad entre el objeto serializado en disco y la clase cargada en JVM. Si la clase sufre cambios en sus atributos, pero conserva el mismo identificador, Java permite deserializar el objeto. Asimismo, si la versión no coincide entre la escriture y la lectura, Java lanza la excepción `InvalidClassException`. Esto es usado por Java para verificar que el emisor (quien serializó el objeto) y el receptor (quien lo desearliza) carguen versiones de la clase que sean compatibles. Todo esto con la finalidad de evitar cargar un objeto con una estructura corrupta o incomptable en memoria. Basicamente, existe para proteger tu programa para leer datos incompatibles. De esta forma, se evita que el programa cargue a la memoria un objeto guardado en el pasado usando unado una versión de una clase del presente que ya no coincide en su estructura.
  - ¿Qué le pasa a un campo marcado `transient`?: Le indica a JVM que el campo debe omitirse durante la serialización. Cuando el objeto se deserializa, el campo va a tomar por defecto asignado a su tipo de dato: `null` - para objetos, `0` - para numéricos y `false` - para booleans. Se utiliza con la aplicación de ignorar datos importantes, como contraseñas, o campos que no requieren persistencia. 
  
2) **Dónde se ve en tu código:** El código compartido es de Miguel: https://github.com/cursosmrugerio/cursoJava17_21/tree/main/chapter14
  - Serialización:
    - `Chimpanzee.java` implementa `Serializable` y marca atributos como `transient`.
    - `PrincipalObjectOutput.java` serializa una lista de objetos `Chimpanzee` y los guarda en disco con el nombre `data/chimpanzees.data` con `ObjectOutputStream`, `BufferedOutputStream` y `FileOutputStream`.
    - `PrincipalObjectInput.java` deserializa y recupera los objetos. Maneja el fin del archivo con la excepción `EOFException`.
  - Archivos con Java NIO (`Path` y `Files`):
    - `PrincipalPath01.java` lee y escribe archivos utilizando la API moderna `java.nio.file.Files`.
    - `PathExample.java` y `Principal2.java` construyen y manipulan rutas del sistema operativo.
  - Threading (Concurrencia): En este código no hay hilos ni problemas de concurrencia. Como hemos visto en clase, la ejecución en paralelo y asíncrona de hilos se puede manejar con un `Thread`, `Runnable` o `ExecutorService` para coordinar tareas concurrentes antes o durante la persistencia de datos. Para evitar las previamente mencionadas condiciones de carrera, al modificar variables compartidas entre hilos, se implemente con bloques `synchronized` o `AtomicInteger`.

3) **Qué pasa si no lo usas:**
  - Sin Concurrencia (Threading): Las operaciones occuren secuencialmente de forma síncrona, bloqueando el hilo principal durante lectureas o escrituras en disco. Esto haría el código extremadamente lento.
  - Sin Manejo de Concurrencia (Race Conditions): Cuando múltiples hilos intentan escribir o actualizar la misma variable, se produce como resultado inconsistencias por accesos simultáneos y pérdida de datos.
  - Sin Try-with-resources: Los streams de los archivos quedarían abiertos en el sistema operativo, causando fugas de memoria (`memory leaks`) o bloquea los archivos impidiendo su modificación por otros procesos.
  - Sin Serialización: 

4) **Cómo correrlo:**
