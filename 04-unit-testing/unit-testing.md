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
    
      - Qué colaborador SÍ mockear: como mencionado en clase, se debe de implementar Mockito en los colaboradores que realicen mucho I/O, conexiones a red, llamadas a API externas constantes y a busques en bases de datos. Mockito soluciona las pruebas lentas, impredecibles y dependientes del entorno de desarrollo.
      - Qué colaborador NO mockear: Tengo entendido que Mockear objetos de datos le quita realismo a las pruebas y no agrega beneficios; por ende, no se debe de implementar en entidades, clases sin estado y Objetos de Transferencia de Datos `DTOs`.

2) **Dónde se ve en tu código:**
   - JUnit:
      - Ciclo de Vida y Manejo de Exepciones: `ExcepcionesTest.java` tiene la anotacion `@BeforeEach` y `assertThrows`
      - Control de Tiempo: `TiempoTest.java` y `CondicionesTest.java` tienen pruebas con tiempo limite `assertTimeout` y `assertTimeoutPreemptively`.
 
3) **Qué pasa si no lo usas:** Al no utilizar Mockito, se complica mucho probar la logica de negocio, porque se necesitaria una conexion a una base de datos reales. Esto puede ocasionar en fallas en las pruebas por fallos por comunicacion en la infrastructura de red o bases de datos. Ademas, cualquier implementacion de una nueva prueba automatizada o refactorizacion de codigo puede causar errores en funcionalidades (features) ya existentes al implementar pruebas unitarias sin JUnit y Mockito. Por eso es importante implementar JUnit y Mockito junto con pruebas de regresion.

4) **Cómo correrlo:**


   
