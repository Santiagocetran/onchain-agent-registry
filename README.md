# Onchain Agent Registry — revisión de la propuesta

**Cambiá de asistente. No pierdas lo aprendido.**

Esta rama, `research/portable-agent-memory`, revisa la visión original de [main](https://github.com/Santiagocetran/onchain-agent-registry/tree/main) y continúa la [investigación de Mateo](docs/10-validacion-onchain.md). Propone conservar la memoria de experiencias entre asistentes, acotar el problema inicial y dejar de tratar blockchain como un componente necesario de la primera solución.

**Estado:** investigación y reflexión de producto. No hay implementación ni resultados experimentales, ahorro demostrado o demanda validada. Las diferencias que siguen son recomendaciones para discutir entre Santi y Mateo, no una decisión conjunta cerrada. El nombre del repositorio se conserva; no implica que el anclaje siga siendo obligatorio.

## De dónde partimos

La visión de `main` propone capturar experiencias de uso de herramientas, convertirlas en guías con evidencia y condiciones, y recuperarlas entre harnesses —los entornos en los que trabajan los asistentes—. El historial sería privado y controlado por el usuario; blockchain conservaría compromisos criptográficos, no los comandos ni las guías privadas.

La idea surgió de explorar blockchain como registro de acciones y de observar asistentes que prueban varios comandos antes de completar tareas, incluso al escribir archivos o usar `gh`. Esa observación motivó una pregunta: ¿cuánto de ese trabajo podría evitarse conservando lo que ya se aprendió?

`main` ya distingue utilidad de memoria e integridad, reconoce alternativas al anclaje y no promete ahorro demostrado. Esta rama profundiza esas dudas y cambia las prioridades: antes de elegir la infraestructura, identificar una investigación repetida que valga la pena evitar.

## Qué pusimos en duda

- **Varios intentos no significan necesariamente un problema de memoria.** Explorar puede ser necesario. Una herramienta mal diseñada, una instrucción ausente o un error del SDK pueden requerir una corrección directa.
- **Guardar experiencias no garantiza mejorar al agente.** Hay que recuperar la adecuada, comprobar si aplica y verificar el resultado. Una guía desactualizada puede empeorar la ejecución.
- **La memoria debe aportar más que documentación, skills y playbooks.** Si una regla fija resuelve el caso, no hace falta memoria dinámica. También existen productos de memoria con evidencia y vigencia, como los revisados en la investigación.
- **La portabilidad no viene dada por registrar eventos.** Cada harness expone información distinta. Capturar actividad y conseguir que otro asistente la aproveche son problemas diferentes.
- **Integridad no equivale a una recomendación segura.** Una guía incorrecta puede estar perfectamente firmada y anclada. Blockchain no demuestra veracidad, captura completa ni compatibilidad con el entorno actual.
- **Un experimento sintético no demuestra una necesidad transversal.** Una prueba favorable entre sesiones tampoco demuestra transferencia entre harnesses ni demanda comercial.

## Qué diferencias proponemos respecto de main

| Aspecto | Visión original de `main` | Propuesta de esta rama |
|---|---|---|
| Centro del relato | Memoria verificable de experiencias de herramientas | Evitar volver a investigar un problema ya resuelto, sin reutilizar una receta incompatible |
| Ámbito inicial | Uso de herramientas entre harnesses y proyectos | Explorar diagnósticos de herramientas de desarrollo onchain como primer caso acotado |
| Arquitectura | CLI común, adaptadores, historial y anclaje; MVP local para dos harnesses | Mantener la portabilidad como objetivo, sin dar por elegida una capa universal ni sus integraciones |
| Papel de blockchain | Componente del diseño, con costo y utilidad por justificar | Capacidad separada y no prioritaria hasta identificar una necesidad de referencia independiente |
| Comparación decisiva | Memoria frente a ausencia de memoria; anclaje frente a alternativas | Exigir además comparación con documentación, skills, playbooks y recuperación de herramientas bien configuradas |
| Criterio de continuidad | Validar utilidad e integridad por separado | Simplificar o cambiar de dirección si una regla fija basta o si el problema real es conocer el estado de una operación |

Conservamos el control del usuario sobre su historial, la privacidad, las guías con evidencia y condiciones, las correcciones explícitas y la continuidad del asistente cuando no hay una experiencia útil. No proponemos reemplazar esas precauciones.

## La herramienta que recomendamos explorar

> Tu asistente pasó varios intentos descubriendo cómo usar una herramienta en tu entorno. Mañana abrís otra sesión o cambiás de asistente y empieza de cero. Proponemos conservar qué funcionó, cómo se comprobó y cuándo sirve, para que el próximo asistente pueda aprovechar esa experiencia.

El usuario candidato es un desarrollador u operador que supervisa asistentes y vuelve a investigar incidentes ya resueltos. La herramienta recuperaría antecedentes contextualizados, no comandos para reproducir ciegamente.

**Ejemplo hipotético:** una sesión descubre una limitación de un proveedor RPC y comprueba una resolución. Otra encuentra un síntoma parecido. La experiencia anterior ayuda a elegir qué comprobar, pero su resolución se rechaza si las condiciones no coinciden. Todavía no demostramos que este recorrido mejore el desempeño ni que se repita con frecuencia suficiente.

El producto sería independiente y utilizable en diferentes ecosistemas. InfiniteZero se revisó como fuente de antecedentes operacionales, **no como destinatario de una herramienta interna ni como dependencia del producto**. Su experiencia también mostró que algunos problemas se resuelven mejor corrigiendo código y documentación.

El recorte onchain proviene de la investigación de Mateo y del contexto que conoce el equipo. No prueba que sea el mejor mercado ni limita permanentemente la visión. Una integración compartida entre harnesses es una posibilidad, no una capa transparente capaz de observar todo automáticamente.

## Por qué no priorizamos blockchain

Los agentes serían quienes consultan y verifican el historial. Eso no determina por sí solo la necesidad de blockchain: importa quién controla el contenido y la referencia contra la que se verifica.

Un anclaje permitiría detectar que un contenido no coincide con un compromiso publicado previamente, bajo las garantías de la red y del verificador. **No asegura que el historial nunca fue modificado**, ni detecta eventos omitidos antes de capturarlos o afirmaciones falsas registradas desde el principio.

Para memoria privada bajo control de un mismo usuario, firmas, versiones y referencias conservadas fuera del almacenamiento principal son alternativas que comparar. Blockchain tendría una justificación más clara si un servicio pudiera reescribir el historial y los agentes necesitaran verificarlo sin confiar exclusivamente en ese servicio, o si varias organizaciones necesitaran una referencia común independiente.

Explorar esa garantía por aprendizaje es válido, pero debe presentarse por separado. El ahorro atribuible a memoria no justifica por sí mismo el anclaje. Operar sobre blockchain y usar blockchain para registrar experiencias son decisiones distintas.

## Qué aprendimos y qué sigue abierto

La revisión encontró solapamiento con herramientas existentes y antecedentes concretos de fricción operacional. **No encontró evidencia suficiente para afirmar que la memoria propuesta sea necesaria, más económica o superior a esas alternativas.** Las fuentes y sus límites están en la [síntesis completa](docs/12-reflexion-memoria-portable.md).

Las preguntas que pueden cambiar la dirección son:

1. ¿Qué diagnóstico real se investigó nuevamente después de haber sido resuelto?
2. ¿Por qué no alcanzó una skill, documentación actualizada o una corrección de la herramienta?
3. ¿Se necesita transportar ese conocimiento entre sesiones y harnesses?
4. ¿La reutilización compensa preparar, revisar, consultar y mantener las experiencias?
5. ¿Se rechazan las guías cuando cambia el contexto?
6. ¿Quién podría reescribir el historial y quién necesita una referencia independiente para detectarlo?

Si una regla fija obtiene el mismo resultado, conviene simplificar. Si el dolor principal es determinar qué quedó hecho tras una interrupción, puede convenir una herramienta de diagnóstico de estado. Si aparecen casos recurrentes y mejora sobre alternativas bien configuradas, se fortalece la hipótesis de memoria portable.

## Cómo se relaciona con la investigación de Mateo

El [documento 10](docs/10-validacion-onchain.md) analiza el recorte onchain, competencia y límites de evidencia. El [documento 11](docs/11-poc-simulado-onchain.md) propone un experimento con un harness, sesiones aisladas y casos compatible e incompatible. [Full-Plan-Layout](docs/Full-Plan-Layout.md) organiza su ejecución futura.

Esos documentos se conservan como antecedentes y propuestas. Esta rama vuelve a discutir la dirección del producto: **no presenta sus planes como una decisión nueva de implementación**. Un POC con guías manuales podría mostrar utilidad de información adicional, sin demostrar todavía automatización rentable, portabilidad o demanda.

El objetivo expresado para HackaTwin es aprender y presentar algo de lo que el equipo se sienta orgulloso. La recomendación es una herramienta independiente con un problema acotado y afirmaciones respaldadas, sin exigir una plataforma universal ni forzar blockchain como titular.

## Guía de lectura

| Documento | Qué aporta |
|---|---|
| [Reflexión de memoria portable](docs/12-reflexion-memoria-portable.md) | Conversación, fuentes revisadas, alternativas, recomendación y preguntas pendientes |
| [Investigación de agentes onchain](docs/10-validacion-onchain.md) | Análisis de Mateo sobre competencia, problema y posibles evaluaciones |
| [POC simulado](docs/11-poc-simulado-onchain.md) | Protocolo propuesto; sin ejecuciones ni resultados |
| [Full-Plan-Layout](docs/Full-Plan-Layout.md) | Plan previo de ejecución, conservado como antecedente |
| [Visión](docs/01-vision.md) · [Arquitectura](docs/02-architecture.md) · [Flujos](docs/03-flows.md) | Diseño original; no todas sus decisiones son compromisos de esta propuesta |
| [Datos y confianza](docs/04-data-and-trust.md) | Integridad, privacidad, correcciones y límites |
| [POC y MVP](docs/05-poc-and-mvp.md) · [Validación económica](docs/06-validation.md) | Alcances previos y criterios para evaluar costos y resultados |
| [Referencias](docs/07-references.md) | Fuentes del diseño original |

Se aceptan discusiones y propuestas. No publicar logs reales, secretos ni información privada en issues. Documentación bajo licencia MIT.
