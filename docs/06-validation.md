# Validación: tiempo, dinero y tokens

## Pregunta principal

¿El ahorro de reutilizar experiencias supera el costo de capturarlas, prepararlas, almacenarlas, verificarlas y consultarlas sin empeorar el resultado?

## Tres variantes

| Variante | Propósito |
|---|---|
| A: sin memoria | Referencia de comportamiento y costo |
| B: memoria sin blockchain | Aislar el valor de recuperar experiencias |
| C: memoria con blockchain | Medir costo y garantía adicional del anclaje |

Mantener equivalentes el agente, modelo, herramientas, tarea y entorno cuando corresponda. Repetir ejecuciones, controlar orden y reiniciar estados para evitar que una variante herede accidentalmente experiencias de otra. Separar preparación de memoria y tareas de evaluación. Incluir tareas recurrentes, nuevas y parecidas pero incompatibles. Estos son experimentos futuros, sin resultados aún.

## Métricas

- Resultado correcto según criterio externo a la declaración del agente.
- Intentos fallidos evitables y llamadas totales a herramientas.
- Tiempo total y tiempo añadido por consulta; distribución, no sólo promedio.
- Tokens de entrada/salida y preparación de guías.
- Costo monetario de modelo, infraestructura y transacciones.
- Costo local de almacenamiento, CPU y mantenimiento, aunque no tenga factura inmediata.
- Guías incorrectas aplicadas, recomendaciones incompatibles y correcciones.
- Integridad: alteraciones detectadas, pruebas pendientes y fallos de comprobación.

No contar menos comandos como éxito si el objetivo quedó incompleto. No sumar tokens, segundos y dinero como si fueran una sola unidad.

## Amortización

Costo acumulado con memoria = preparación + captura/mantenimiento + consultas + ejecución restante + anclaje/verificación.

Ahorro neto = costo de referencia para las mismas tareas correctas − costo acumulado con memoria.

Si una experiencia cuesta F en preparación y mantenimiento asignable, y ahorra s por reutilización después del costo de consulta, el punto simplificado de equilibrio es N > F / s, sólo cuando s > 0. Se calcula por dimensión y con supuestos explícitos; no es una predicción del proyecto.

No fijamos todavía porcentajes ni presupuestos: se decidirán con una línea base. Registrar gastos testnet no permite inferir directamente costo mainnet; estimarlo separadamente cuando se elija una red.

## Criterios de aceptación propuestos

- Ahorro neto tras reutilizaciones declaradas en tareas recurrentes, sin pérdida de éxito.
- Sobrecosto acotado y explícito en tareas nuevas.
- Contenido alterado tras el anclaje no se recomienda.
- Guías incompatibles no se aplican automáticamente.
- Correcciones conocidas retiran guías cuestionadas.
- Caída de memoria o lentitud no bloquea al agente.
- Toda rama intenta registrar su resultado, pero los huecos reales se reconocen.

## Casos de verificación

| Caso | Resultado esperado |
|---|---|
| Evento alterado | Discrepancia detectada |
| Prueba no accesible | No verificable, no acusación automática de alteración |
| Anclaje pendiente | Etiqueta pendiente |
| Guía íntegra pero equivocada | Se puede corregir; la integridad no impide el error |
| Contexto distinto | Resolución habitual y posible nueva variante |
| Fallo sin solución | Historial, sin guía de éxito |
| Éxito equivalente ya conocido | Aporte de evidencia, evitar duplicado innecesario |
| Evento omitido antes de captura | No prometer detección criptográfica |
| Secreto sintético en evento | Filtro evita persistencia según reglas probadas |
