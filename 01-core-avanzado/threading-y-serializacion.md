1) **Qué es el concepto y qué problema resuelve, en tus palabras:**

  - Hilos: Permiten ejecutar múltiples tareas en paralelo aprovechando procesadores multinúcleo. `ExecutorService` evita la sobrecarga de instanciar hilos manualmente (uno por uno).
  - El problema de la concurrencia (¿Qué pasa cuándo dos hilos tocan el mismo dato y cómo lo resuelves?): Bloquea la aplicación durante operaciones pesadas de Entrada/Salida (I/O).
  - Archivos (Leer y escribir archivos): Proporciona la habilidad al programador de leer, escribir y manipular rutas en el sistema de archivos usando `java.nio.file.Files` o con `FileInputStream`/`FileOutputStream` (Streams). Para poder gestionar los recursos de forma segura, se utiliza `try-with-resources`. Como resultado, se garantiza que los descriptores de archivos (files descriptor) se cierren automáticamente sin fugas de memoria (memory leaks).
  - Serialización (Guardar un objeto a disco y volverlo a leer): 
  - ¿Por qué exoste el `serialVersionUID`?
  - ¿Qué le pasa a un marcado `transient`?
  
3) **Dónde se ve en tu código:**

4) **Qué pasa si no lo usas:** 

5) **Cómo correrlo:**
