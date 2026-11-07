# POC simulado: memoria operacional para agentes onchain

## Estado y decisión de esta rama

**Alcance acordado para documentar:** un experimento propio, pequeño y controlado antes de reclutar equipos. No exige entrevistas, clientes ni acceso a incidentes privados para empezar. La validación de mercado queda para después; no se considera completada por una demo.

**Estado actual:** protocolo documentado, sin implementación ni ejecuciones. No hay métricas observadas, ahorro demostrado ni red o harness seleccionados. Documentar este protocolo no autoriza por sí solo a implementar ni publicar transacciones.

Este POC antecede al [MVP de dos harnesses](05-poc-and-mvp.md) y acota la siguiente acción de la [investigación onchain](10-validacion-onchain.md). No pretende completar sus tres experimentos ni todas las capacidades del producto.

## 1. Pregunta y límites de la prueba

> ¿Una experiencia comprobada ayuda a una sesión nueva a resolver una tarea similar, y reconoce cuándo esa experiencia no corresponde?

Se busca observar transferencia entre sesiones, no probar portabilidad entre harnesses, aprendizaje del modelo ni adopción comercial. Los fallos son inducidos y las tareas sintéticas: eso debe figurar tanto en la demo como en la presentación.

Separar dos preguntas:

- **Utilidad operacional:** si recuperar una experiencia mejora el diagnóstico frente a herramientas y documentación adecuadas.
- **Integridad:** si una copia alterada deja de coincidir con un compromiso previamente conservado. No demuestra verdad del contenido ni utilidad de blockchain frente a otras alternativas.

Un empate o una regresión es un resultado válido. No elegir exclusivamente tomas donde la memoria gana.

## 2. Alcance mínimo

- Un harness y un modelo, con versiones y configuración registradas.
- Sesiones nuevas y aisladas para preparación y evaluación.
- Una blockchain EVM local reiniciable, con cuentas y fondos exclusivamente de prueba.
- Un contrato sencillo y una familia de tareas: desplegarlo y dejar una configuración verificable.
- Un patrón de fallo de herramienta o entorno, con variante compatible e incompatible.
- Un playbook fijo disponible en ambos brazos y una guía local de experiencia sólo en B.
- Consulta local explícita tras observar el síntoma definido; no una consulta antes de cada comando.
- Trazas, verificación externa y resultados por ejecución, aunque la captura inicial sea manual.

No requiere una plataforma, dos adaptadores, generación automática de guías, sincronización, embeddings, marketplace, reputación, token, multichain, trading ni custodia de fondos reales. La blockchain local es el entorno de la tarea; no implica que la memoria ya esté anclada.

## 3. Selección y preflight del ejercicio

La tarea de negocio es la misma en A y B: desplegar y configurar el contrato. Antes de medir, fijar las postcondiciones: código presente en la dirección correcta, propietario esperado y valor de configuración esperado. El evaluador las comprueba fuera de la conversación del agente, contra la instancia y chain ID acordados. Un hash de transacción o la declaración «terminé» no bastan.

**Candidato, no fallo confirmado:** una limitación de un endpoint RPC que afecta un paso de verificación durante el despliegue/configuración. La experiencia recogería cómo se identificó esa limitación y qué procedimiento compatible permitió completar la tarea. No consistiría en reutilizar un nonce, una dirección histórica o una transacción firmada.

El fallo exacto se fija después de un preflight, antes de las ejecuciones medidas. Debe cumplir:

1. Se reproduce con estado inicial conocido y se puede retirar o cambiar sin fondos reales.
2. Las herramientas no lo recuperan automáticamente. Su recuperación normal permanece habilitada en A y B.
3. Existen al menos dos causas plausibles del síntoma; la guía aporta una comprobación condicionada, no una orden incondicional de repetir el arreglo.
4. La variante incompatible cambia una condición relevante: la recomendación anterior no corresponde y el diagnóstico habitual debe continuar.
5. El playbook fijo contiene las comprobaciones y salvaguardas conocidas antes de preparar la experiencia; no se oculta documentación al control.

Si sólo hace falta corregir una configuración estable o agregar una regla obvia al playbook, registrarlo: ese caso no justifica memoria dinámica. No fabricar una carencia de la herramienta ni aumentar la dificultad de A para lograr una victoria. Un fallo inyectado debe ser una condición real del entorno de prueba, no un error escrito en una diapositiva ni una respuesta falsa atribuida al programa.

## 4. Preparar la primera experiencia

Ejecutar una sesión separada hasta obtener un resultado comprobado. Conservar también los intentos fallidos. Si no se resuelve, queda como historial, no como guía de éxito.

La guía puede redactarse y revisarse manualmente a partir de la traza. Registrar el tiempo humano y cualquier uso de modelo para prepararla; no presentar ese trabajo como automatización implementada.

Contenido mínimo de la guía:

| Campo | Contenido |
|---|---|
| Origen | Identificador de la ejecución y referencia a su traza redactada |
| Síntoma | Error o comportamiento observable, sin atribuir causa sólo por coincidencia de texto |
| Contexto | Herramienta y versión, chain ID, tipo de endpoint y condiciones relevantes |
| Aplicabilidad | Qué se debe comprobar antes de usar el diagnóstico y cuándo rechazarlo |
| Resolución | Procedimiento y comprobaciones que funcionaron; no credenciales ni estado transaccional para copiar |
| Evidencia | Resultado del evaluador y postcondiciones observadas |
| Estado | Revisión humana, fecha y si sigue habilitada, cuestionada o retirada |

Congelar la guía y el playbook antes de medir. No incluir soluciones de las tareas de evaluación, cuyo contrato, parámetros o condiciones concretas deben diferir de los de preparación. Que B reciba información episódica adicional es el tratamiento; la prueba sólo mide su utilidad incremental sobre el control, no superioridad frente a cualquier documentación posible.

## 5. Ejercicios de la demo

| Ejercicio | Qué ocurre | Qué observar |
|---|---|---|
| Primera experiencia | Una sesión encuentra el fallo inducido, lo resuelve y aporta evidencia para la guía | Origen de la experiencia y trabajo real de preparación |
| Reutilización compatible | Sesiones nuevas de A y B reciben una tarea equivalente con detalles nuevos y el mismo contexto aplicable | Si B reduce diagnóstico sin dejar incompleta la tarea |
| Contexto incompatible | Sesiones nuevas encuentran un síntoma similar, pero una condición de aplicación no se cumple | Si B reconoce el límite, no aplica el arreglo anterior y continúa con el diagnóstico correcto |

Añadir una comprobación de continuidad sin guía disponible: B debe poder seguir con las herramientas habituales. Es una comprobación funcional, no una estimación de rendimiento en tareas nuevas.

En la variante incompatible se puede recuperar la guía para examinarla. Lo incorrecto es ejecutar su resolución sin cumplir las condiciones; el evaluador debe observar las acciones, no confiar sólo en que el agente diga que la rechazó.

## 6. Comparación controlada A/B

- **A:** herramientas, documentación y playbook fijo, sin la experiencia episódica.
- **B:** exactamente lo mismo, con acceso a la guía local preparada en el apartado 4.

El enunciado de negocio, modelo, presupuesto, herramientas, permisos y condiciones iniciales son equivalentes dentro de cada par. Ambos disponen de las mismas comprobaciones de estado, recuperación y límites de seguridad. B puede consultar al aparecer el síntoma; A no tiene una respuesta artificialmente peor ni una pausa impuesta para compensar la consulta.

Para cada ejecución:

1. Restablecer cadena, archivos de trabajo, artefactos de deploy y estado del entorno de fallo a la misma condición del par.
2. Abrir una sesión nueva, sin conversación ni memoria persistente heredada. Si el harness no permite aislarla, declarar la contaminación y no atribuir causalmente la diferencia a la guía.
3. Usar una tarea de evaluación congelada y el presupuesto acordado; alternar A→B y B→A entre pares.
4. Registrar inicio, acciones, consulta si ocurre, intervenciones humanas y final. Aplicar el mismo límite de tiempo y llamadas a ambos brazos.
5. Ejecutar el evaluador externo y conservar su salida. Si se puede, no mostrarle el brazo hasta emitir el resultado.
6. Guardar la fila de métricas y la traza, incluyendo fallos y ejecuciones agotadas.

Objetivo exploratorio: **cinco pares compatibles y cinco pares incompatibles**, además de la sesión de preparación y la comprobación de continuidad. Es una muestra pequeña, no una prueba estadística ni una medición de frecuencia de incidentes reales. Si se ejecutan menos pares, informar el número real y no describirlo como el protocolo completo.

No actualizar la guía con los resultados de una ejecución y seguir contando las siguientes como parte del mismo experimento congelado. Una corrección inicia una nueva versión y un nuevo conjunto de evaluación. No reintentar sólo las ejecuciones desfavorables ni descartar outliers sin informar el motivo.

## 7. Métricas y evidencia

Aplicar la contabilidad de [validación económica](06-validation.md), sin sumar segundos, tokens y dinero en una misma cifra.

| Medida | Definición y fuente |
|---|---|
| Tarea correcta | Todas las postcondiciones satisfechas según salida del evaluador; timeout y presupuesto agotado cuentan como no completada |
| Seguridad del procedimiento | Envíos duplicados no previstos, operaciones fuera de alcance o intervención necesaria, según traza y estado; cero observado no prueba seguridad general |
| Diagnóstico | Llamadas destinadas a investigar el fallo y repeticiones del mismo intento sin cambio relevante, etiquetadas con el mismo criterio en A y B |
| Tiempo total | Tiempo de pared desde el inicio hasta resultado o límite, incluyendo consulta y acciones restantes |
| Tokens | Entrada y salida reportadas por el harness, incluida la guía; si no son observables, marcar «no disponible» |
| Preparación | Tiempo humano, llamadas de modelo y tokens usados para producir/revisar la guía, separados de cada reutilización |
| Compatibilidad | Condición incumplida observada y si B ejecutó o evitó la resolución incompatible |
| Consulta y captura | Si consultó, qué guía recibió, si falló la consulta y qué partes de la ejecución quedaron sin capturar |

Cada fila de resultados identifica par, escenario, brazo, versiones, tarea, entorno inicial, guía/playbook usados, resultado del evaluador y ubicación de la evidencia. Preservar datos por ejecución: mostrar resultados pareados y denominadores, no sólo un promedio.

Fijar el criterio de «intento repetido» antes de comparar y revisar las etiquetas contra las trazas. Menos llamadas no es mejora si se omite una comprobación necesaria o la tarea queda mal configurada.

Para hablar de ahorro acumulado, descontar preparación y consultas de las reutilizaciones realmente observadas. Si sólo hay menos tiempo de ejecución en B pero no se amortiza la preparación, decirlo. No extrapolar gas local/testnet a gasto mainnet, inferir ROI de clientes ni inventar tokens no expuestos por el harness.

## 8. Prueba independiente de integridad

Esta demostración no forma parte del tratamiento A/B y no puede explicar una mejora del agente:

1. Fijar los bytes exactos de una guía y conservar su compromiso en una referencia separada y conocida por el verificador.
2. Comprobar que el original coincide.
3. Alterar una copia y comprobar que no coincide con esa misma referencia.
4. Distinguir «no coincide», «referencia inaccesible» y «anclaje pendiente» si corresponde.

Comparar contra el mismo compromiso conocido: reemplazar el archivo y recalcular su hash al verificar no demuestra detección de alteraciones. No incluir secretos ni trazas privadas en compromisos públicos; usar sólo material sintético revisado.

Un hash o un compromiso conservado localmente demuestra esa comprobación de integridad, no una necesidad de blockchain. Publicarlo en una cadena local demuestra el mecanismo local, no garantías de una red pública. Si se implementa anclaje en testnet, identificar red, contrato, transacción y política de finalidad y comprobar la referencia efectivamente publicada; hasta entonces no afirmar que existe anclaje público.

La resistencia a sustitución de todo el historial por el operador y el valor para un tercero pertenecen al [experimento B/C posterior](10-validacion-onchain.md), no se dan por demostrados al alterar una copia.

## 9. Entregables y presentación

Al ejecutar el POC, conservar:

- Instrucciones de entorno, versiones, mecanismo de fallo y reinicio, tareas y límites congelados.
- Contrato y evaluador con postcondiciones explícitas.
- Playbook común, guía revisada y traza de preparación redactada.
- Trazas y resultados por ejecución, con métricas medidas y campos no observables declarados.
- Evidencia de original/copia alterada si se realiza la prueba de integridad.
- Presentación con conclusión y límites; grabación de respaldo identificada como tal si se utiliza.

Estos son entregables futuros de la ejecución, no archivos ni resultados ya existentes.

Guion sugerido de presentación:

1. **Problema e hipótesis:** diagnóstico repetido entre sesiones; aún no hay demanda validada.
2. **Protocolo:** qué fallo inducimos, qué conserva A y qué información adicional obtiene B.
3. **Demostración:** origen de la experiencia, una reutilización y un rechazo por incompatibilidad. Aclarar si la toma es ilustrativa, en vivo o grabada; no confundir una toma con todo el benchmark.
4. **Resultados:** tabla con datos reales, número de pares y costo de preparación. Mostrar empates, errores y campos no disponibles; sin cifras de relleno.
5. **Integridad y límites:** prueba separada, si se ejecutó, y alcance exacto local/testnet.
6. **Decisión:** continuar, ajustar o descartar este patrón; qué falta validar con usuarios.

Frase admisible, ajustada al resultado observado: «En este escenario controlado evaluamos si reutilizar una experiencia reduce diagnóstico repetido y si se evita aplicarla fuera de contexto. Estos son los resultados. La frecuencia del problema y la demanda comercial siguen pendientes».

## 10. Criterios de cierre y siguiente etapa

**POC ejecutado:** preparación y ejercicios realizados, comparación conservada con todos sus resultados, postcondiciones comprobadas y límites visibles. Una ejecución que falla no invalida el experimento; ocultarla sí invalida la comparación. La prueba de integridad se informa por separado y puede no haberse realizado.

**Señal técnica favorable, no validación comercial:** B conserva el éxito de A, no aplica resoluciones incompatibles y reduce trabajo o costo observado después de contabilizar la memoria. Si todavía no amortiza la preparación, informar sólo la mejora por reutilización y el costo pendiente. No generalizar más allá de estas tareas y condiciones.

**Ajustar o descartar el caso:** el playbook basta, no hay mejora, se aplica una guía incompatible o el trabajo de preparación supera el beneficio observado. Investigar el resultado sin cambiar retrospectivamente el control ni los criterios para declarar victoria.

**Después:** buscar equipos con incidentes recurrentes, comprobar qué no resuelven sus herramientas actuales, comparar con memoria existente y evaluar un piloto. Sólo entonces retomar demanda, precio, transferencia entre harnesses y utilidad del anclaje para una contraparte independiente. Los equipos del piloto no son un prerrequisito de esta primera simulación.

## 11. Backlog y trabajo con dos developers

El plan de ejecución está en el [issue coordinador #1](https://github.com/Santiagocetran/onchain-agent-registry/issues/1). Los issues contienen alcance, dependencias, propiedad de archivos y aceptación observable; no representan implementación realizada.

El [Full-Plan-Layout](Full-Plan-Layout.md) organiza la jornada de nueve horas incluyendo desarrollo, integración, análisis exploratorio, preparación/pulido de la presentación y ensayo. Sus cortes de trabajo no reducen los requisitos del benchmark; si faltan corridas, se informa el estado parcial.

| Issue | Responsable funcional | Dependencia |
|---|---|---|
| [#2 Preflight e interfaces](https://github.com/Santiagocetran/onchain-agent-registry/issues/2) | Ambos developers | Inicio; confirmar fallo, aislamiento y contratos |
| [#3 Entorno y evaluador](https://github.com/Santiagocetran/onchain-agent-registry/issues/3) | Developer A | #2 |
| [#4 Memoria y runner](https://github.com/Santiagocetran/onchain-agent-registry/issues/4) | Developer B | #2; en paralelo con #3 |
| [#5 Preparación y evaluación A/B](https://github.com/Santiagocetran/onchain-agent-registry/issues/5) | B ejecuta; A revisa evidencia | #3 y #4 |
| [#7 Resultados y demo](https://github.com/Santiagocetran/onchain-agent-registry/issues/7) | A prepara; ambos ensayan | Preparación en paralelo con #5; cierre con evidencia integrada |
| [#6 Integridad local opcional](https://github.com/Santiagocetran/onchain-agent-registry/issues/6) | Quien esté disponible sin desplazar el camino crítico | Guía revisada de la preparación; no requiere acabar el benchmark |

La jornada de nueve horas con dos developers es el contexto del plan, no una garantía de entrega: el preflight debe confirmar stack, fallo y aislamiento; además, las veinte corridas medidas consumen tiempo de modelo. No reducir silenciosamente las repeticiones para afirmar que se completó el protocolo. Una demo con evidencia parcial debe decirlo y conservar abierto el trabajo pendiente.

Después del preflight, separar archivos de entorno/evaluador de archivos de memoria/runner y fijar comandos de reset, ejecución y verificación. Paralelizar desarrollo y preparación del informe, no corridas sobre una misma cadena o workspace mutable. No se asignan personas ni se inicia implementación al crear estos issues.
