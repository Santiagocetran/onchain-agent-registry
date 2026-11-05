# Reflexión de producto: memoria portable para asistentes

**Fecha:** 2026-11-05.  
**Estado:** síntesis de la investigación y conversación con Santi; recomendación provisional, no validación experimental ni decisión conjunta con Mateo.  
**Rama:** `research/portable-agent-memory`, creada desde `research/onchain-agents` (`e264c7f`). La visión de `main` revisada corresponde a `83abbff`.

## 1. Resultado de esta reflexión

**Recomendación:** conservar la hipótesis de reutilizar experiencias contextualizadas entre asistentes; explorar herramientas de desarrollo onchain como primer ámbito de aplicación; mantener el producto independiente de cualquier protocolo y no priorizar el anclaje blockchain sin una necesidad de integridad independiente identificada.

> Cambiá de asistente. No pierdas lo aprendido.

La herramienta propuesta conservaría qué funcionó, cómo se comprobó y bajo qué condiciones. Otra sesión o asistente podría consultar esa experiencia, comprobar su aplicabilidad y verificar el resultado. La promesa no es recordar todo ni eliminar errores, sino recuperar conocimiento útil sin trasladarlo ciegamente entre entornos.

**No hay resultados experimentales.** No se implementó ni ejecutó un POC durante esta reflexión. No se demostraron ahorro, mejora de desempeño, transferencia entre harnesses, demanda, clientes ni disposición a pagar. Los “resultados” de este documento son hallazgos documentales y conclusiones de la conversación.

No se incluye un plan de desarrollo, cronograma o guion de demo: el propósito es decidir qué problema vale la pena resolver.

## 2. Cómo leer la evidencia

- **[REPOSITORIO]:** afirmaciones encontradas en la documentación o código revisados; no necesariamente verificadas mediante ejecución.
- **[EXTERNO]:** capacidades o información contrastadas en fuentes primarias durante la conversación, el 2026-11-05. Documentación de un proveedor no equivale a eficacia auditada.
- **[USUARIO]:** motivaciones y restricciones expresadas por Santi.
- **[HIPÓTESIS]:** interpretación, oportunidad o recomendación pendiente de validación.

Se leyeron primero los documentos de `main` y después la investigación de Mateo, especialmente [10](10-validacion-onchain.md), [11](11-poc-simulado-onchain.md) y [Full-Plan-Layout](Full-Plan-Layout.md). También se consultó, en modo lectura, el checkout local de InfiniteZero y antecedentes de onboarding. No se auditó exhaustivamente ninguno de los productos externos.

## 3. Origen y motivaciones aclaradas

**[USUARIO]** La idea nació de explorar blockchain como registro de acciones, fuera de su asociación habitual con wallets y criptomonedas. Luego se conectó con observar asistentes que prueban varios comandos antes de resolver tareas, incluso escribir archivos o usar `gh`.

**[USUARIO]** Blockchain no es obligatoria: parecía un titular atractivo. El objetivo principal de HackaTwin es aprender y presentar algo de lo que el equipo se sienta orgulloso.

**[USUARIO]** El producto debe ser independiente y utilizable en distintos ecosistemas. InfiniteZero se propuso como ejemplo, no como destino de una herramienta interna.

**[HIPÓTESIS]** Estas motivaciones justifican una exploración técnica honesta sin exigir validación comercial en la hackathon. No justifican afirmar que varios intentos implican desperdicio: parte de la exploración puede ser necesaria y más barata que preparar y consultar memoria.

## 4. Visión original y evolución de Mateo

**[REPOSITORIO] Visión original:** memoria privada de experiencias de herramientas, controlada por el usuario, reutilizable entre harnesses. Eventos observables se transforman en guías con condiciones y evidencia. Blockchain conserva compromisos del contenido, no los logs privados. El nombre no describe un directorio o ranking de agentes.

**[REPOSITORIO] Documento 10:** Mateo propone acotar a equipos que usan asistentes de coding para desplegar y operar contratos. Identifica competencia y mecanismos de fallo, pero distingue plausibilidad técnica de frecuencia y costo demostrados. Propone comparar contra herramientas robustas y playbooks, no contra un agente artificialmente desprotegido.

**[REPOSITORIO] Documento 11:** reduce la prueba inicial a un harness, sesiones aisladas, una cadena local y un fallo inducido con variantes compatible e incompatible. Permite preparar manualmente la guía y exige contabilizar ese trabajo. La comparación conserva documentación y playbook en ambos brazos.

**[REPOSITORIO] Full-Plan-Layout:** organiza la ejecución futura en una jornada; no aporta resultados adicionales. Su existencia no demuestra necesidad del producto.

**[HIPÓTESIS] Tensiones importantes:**

- Una prueba entre sesiones no demuestra portabilidad entre harnesses.
- Un caso sintético favorable no demuestra frecuencia del problema ni demanda.
- Una guía manual eficaz puede demostrar el valor de documentación adicional, sin demostrar que automatizar su preparación y mantenimiento sea rentable.
- Operar sobre blockchain no implica necesitar blockchain para almacenar compromisos de memoria.
- Acotar el experimento mejora su interpretación, pero no sustituye identificar un usuario y una consecuencia relevante.

## 5. Problema candidato y alternativas más simples

**[HIPÓTESIS] Problema candidato:** “Nuestro equipo ya resolvió este incidente, pero una nueva sesión vuelve a investigarlo porque la solución quedó perdida, incompleta o sin contexto”. Usuario: desarrollador u operador que supervisa asistentes. Consecuencias plausibles: interrupciones y diagnóstico duplicado; no cuantificadas aquí.

| Causa | Primera alternativa que considerar |
|---|---|
| Falta una instrucción estable | Documentación, skill o playbook |
| La herramienta comunica mal estados o errores | Corregir la herramienta |
| Hay que esperar y comprobar una operación | Seguimiento determinista |
| Se perdió una resolución particular del entorno | Memoria contextual |
| Una contraparte puede reemplazar evidencia histórica | Registro con referencia independiente |

**[HIPÓTESIS]** La oportunidad está entre dos extremos: una experiencia demasiado particular se reutiliza poco; una regla general y estable suele pertenecer a documentación o código. Hace falta recurrencia suficiente y variación contextual relevante.

Memoria y skills no son opuestos. Una experiencia puede convertirse en una skill. Descubrir, revisar y mantener ese conocimiento podría ser más valioso que construir otro almacén de memoria.

### Competencia contrastada

| Fuente primaria | Capacidad documentada | Implicación para la propuesta |
|---|---|---|
| [AgentKit](https://github.com/coinbase/agentkit) | Acciones onchain, proveedores de wallets e integraciones con frameworks | Acceso y ejecución ya tienen herramientas; no equivale a resolver diagnóstico contextual |
| [Hardhat Ignition](https://hardhat.org/ignition/docs/explanations/error-handling) | Simulación y tratamiento de errores de contratos y red | No atribuir a memoria lo que resuelve la recuperación normal |
| [Membase Memory & Recall](https://docs.unibase.com/membase/memory/) | Memoria persistente, observaciones inmutables, sustitución, recuperación local con citas y ventanas de vigencia | “Memoria con evidencia” no basta como diferenciación |

**[EXTERNO]** Se verificaron esas capacidades declaradas, no su desempeño. **[HIPÓTESIS]** El diferencial tendría que ser mejor resolución de una clase de incidentes o menor esfuerzo de mantenimiento del conocimiento.

Las cifras de actividad, precios y pérdidas citadas por Mateo no se adoptan como evidencia comercial. No se verificaron nuevamente todas esas cifras. El propio documento 10 cuestiona la reproducibilidad y cálculo del reporte de pérdidas de AgentKit. No fundamenta ROI para este proyecto.

## 6. Qué aportó el ejemplo de InfiniteZero

**[REPOSITORIO LOCAL]** Se revisaron `DevNet/README.md`, `Developer/design/din-architecture.md`, `Developer/BACK_LOG.md`, documentación de agregadores, helpers de transacciones y notas históricas de onboarding. InfiniteZero coordina entrenamiento distribuido mediante contratos, CLI, almacenamiento de artefactos y procesos de trabajo. Eso no equivale a que un LLM opere el protocolo. La extensión “Agentic dind” figura en el backlog consultado como idea futura.

Los antecedentes de onboarding documentan fricción real: dependencias innecesarias entre comandos, mensajes confusos y diferencias entre versiones y entornos. Parte de ese trabajo se convirtió en correcciones de código y documentación. Son antecedentes históricos; no se afirma que esos defectos persistan hoy ni que fueran causados por agentes.

El código consultado también muestra que algunas situaciones ambiguas se abordan mediante lógica explícita de transacciones. La documentación distingue producir, comprometer y revelar un resultado: recordar una experiencia no sustituye consultar el estado actual del protocolo.

**[HIPÓTESIS]** InfiniteZero puede aportar casos reales para investigar diagnóstico contextual. No demuestra todavía repetición entre asistentes ni superioridad sobre una skill. No se necesita reproducir su arquitectura ni convertirlo en dependencia del producto.

**Corrección de alcance expresada por Santi:** una propuesta inicial de asistente específico para operadores de InfiniteZero se descartó como dirección del producto. El recorte debe ser por clase de problema, no por organización.

Se omiten de esta síntesis rutas operativas, direcciones de infraestructura y datos privados de los antecedentes locales. Las notas históricas no constituyen una fuente pública ni una auditoría reproducible para lectores externos.

## 7. Memoria e integridad: decisiones separadas

**[USUARIO]** Los verificadores previstos serían los propios agentes, que consultarían el historial para mejorar el uso de herramientas. Se planteó blockchain como una “capa segura” que impediría modificaciones del historial.

**[HIPÓTESIS DE DISEÑO]** Esa garantía debe expresarse con precisión: verificar un compromiso publicado permite detectar que el contenido consultado no coincide con esa referencia previa. No prueba que nunca se modificó, que la captura fue completa, que los hechos ocurrieron ni que la recomendación sea correcta.

Ejemplo hipotético: una guía equivocada que recomienda `--force` puede estar perfectamente firmada y anclada. Su integridad no la hace segura para reutilizar.

| Pregunta | Mecanismo relevante |
|---|---|
| ¿Qué intentó el agente? | Captura de eventos |
| ¿Qué acciones pertenecen a una tarea? | Identificadores y relaciones |
| ¿Quién declaró el evento? | Firmas y gestión de identidades |
| ¿Coincide con una referencia anterior? | Hashes y compromisos conservados |
| ¿Puede el operador reemplazar unilateralmente esa referencia? | Referencia independiente; blockchain es una opción |

Que verifique un agente y no una persona no cambia el problema de confianza. Importa quién controla el almacenamiento y la referencia.

- **Memoria privada bajo un mismo usuario:** firmas, versiones y referencias independientes del almacenamiento principal son comparadores razonables. Blockchain no está justificada por defecto.
- **Servicio de almacenamiento potencialmente deshonesto:** un anclaje independiente podría limitar la sustitución del historial.
- **Intercambio entre organizaciones sin administrador común:** la justificación es más fuerte, pero sigue sin resolver veracidad o utilidad.

**[EXTERNO]** El sellado de tiempo tampoco exige blockchain: [RFC 3161](https://www.rfc-editor.org/rfc/rfc3161.html) especifica una alternativa basada en una autoridad de confianza.

**[HIPÓTESIS] Recomendación:** no priorizar blockchain en la primera propuesta. Reconsiderarla si se identifica quién podría reescribir el historial, quién necesita detectarlo y por qué firmas, checkpoints o terceros no alcanzan. Si se explora por aprendizaje, presentar su garantía separadamente y no atribuirle el ahorro de memoria.

## 8. Producto independiente y alcance conceptual

**[HIPÓTESIS]** Una memoria compartida entre harnesses tiene sentido como servicio consultable mediante integraciones. “Debajo de los harnesses” no debe prometer una capa transparente que observa y controla todo: la cobertura depende de cada integración.

Capturar eventos y conseguir que un agente use bien una experiencia son problemas distintos. La portabilidad debe demostrarse. No se seleccionó arquitectura, API, harness, red ni mecanismo de captura en esta conversación.

Se consideraron dos direcciones:

1. **Memoria de diagnósticos:** evita volver a investigar conocimiento ya obtenido. Conserva mejor la idea original.
2. **Diagnóstico de operaciones incompletas:** reconstruye qué quedó hecho y qué falta. Es fácil de explicar, pero su núcleo es observabilidad y recuperación, no memoria.

La recomendación provisional favorece la primera. La segunda sigue siendo una alternativa si los casos reales muestran que la ambigüedad de estado pesa más que el conocimiento perdido.

## 9. Otras aplicaciones consideradas

Todas son **[HIPÓTESIS]**, no demanda demostrada.

| Aplicación | Usuario y situación | Aporte posible | Cuándo basta algo más simple / supuesto a validar |
|---|---|---|---|
| Incidentes de integraciones | Agencia que mantiene automatizaciones para distintos clientes y repite diagnósticos | Experiencias por entorno, versión y proveedor | Manual o skill si hay pocas variantes; comprobar recurrencia y costo de mantenimiento |
| Procedimientos de soporte | Equipo que vuelve a escalar una excepción ya resuelta | Convertir resoluciones en instrucciones revisables y retirar obsoletas | Base de conocimiento bien mantenida; comprobar qué falla hoy y esfuerzo de revisión |
| Evidencia de trabajos de agentes | Proveedor y cliente discrepan sobre acciones o autorizaciones | Historial versionado y compromisos verificables | Logs compartidos y recibos firmados; identificar contraparte y disputa concreta |

La tercera cambia el beneficio principal hacia evidencia independiente y podría justificar mejor blockchain. No debe confundirse con mejorar el desempeño del agente.

## 10. Encaje con HackaTwin y caminos posibles

**[EXTERNO]** La [convocatoria](https://luma.com/cudf7cqz) consultada incluye tracks AI, Blockchain y Fintech. Anuncia 12 horas de evento/build y agenda kickoff a las 09:00, entrega a las 18:00 y demo a las 19:00. No se encontró una rúbrica detallada que permita anticipar la evaluación. No se asumen reglas de trabajo previo ni requisitos de cadena.

**[HIPÓTESIS]** Para aprender y presentar algo defendible, una herramienta independiente con un problema acotado tiene mejor historia que una infraestructura universal. El riesgo es explicar demasiadas piezas antes de mostrar una consecuencia para el usuario.

| Camino | Ganancia | Riesgo o pérdida |
|---|---|---|
| Memoria general desde el inicio | Visión amplia y portabilidad como horizonte | Alcance difícil y fuerte solapamiento |
| Memoria acotada a diagnósticos de herramientas onchain | Problema y evidencia más interpretables | El playbook puede bastar; generalización pendiente |
| Pivot a diagnóstico de estado o evidencia | Consecuencia más directa y potencial usuario distinto | Cambia la tesis; exige investigar otra necesidad |

La recomendación no supone que el enfoque onchain sea el mejor mercado. Es un primer ámbito compatible con la investigación de Mateo y la experiencia del equipo.

## 11. Narrativa propuesta

**Titular recomendado:** “Cambiá de asistente. No pierdas lo aprendido”.

> Tu asistente pasó varios intentos descubriendo cómo usar una herramienta en tu entorno. Mañana abrís otra sesión o cambiás de asistente y empieza de cero. Proponemos conservar qué funcionó, cómo se comprobó y cuándo sirve, para que el próximo asistente pueda aprovechar esa experiencia.

Titulares alternativos:

- “Tu próximo agente no debería empezar de cero”.
- “Lo resolviste una vez. Que tu próximo asistente lo sepa”.
- “Experiencias comprobadas para agentes que usan herramientas”.
- “Una memoria compartida entre tus asistentes, bajo tu control”.

Son propuestas de posicionamiento, no descripciones de capacidades implementadas. “Comprobada” requiere evidencia del resultado y condiciones; no significa universalmente correcta. No prometer “nunca repite errores”, ahorro no medido, compatibilidad universal ni aprendizaje del modelo.

## 12. Qué falta saber y qué cambiaría la recomendación

- **Episodio real:** ¿qué diagnóstico se volvió a investigar después de haber sido resuelto? Observar varios comandos no basta.
- **Comparador:** ¿por qué no alcanzó documentación, skill, memoria existente o corrección del SDK?
- **Transferencia:** ¿el usuario cambia efectivamente de sesiones/harnesses y necesita transportar ese conocimiento?
- **Economía:** ¿la reutilización compensa captura, preparación, revisión, consulta y mantenimiento?
- **Compatibilidad:** ¿la experiencia ayuda en el caso correcto y se rechaza cuando corresponde?
- **Confianza:** ¿hay un operador del historial del que un verificador necesite independizarse?

**A favor de continuar:** casos recurrentes, mejora sobre alternativas bien configuradas y preparación amortizable. **A favor de simplificar:** una skill o regla fija obtiene el mismo resultado. **A favor de cambiar de dirección:** el dolor dominante es determinar estado o recuperar operaciones, no recordar diagnósticos. **A favor de blockchain:** contraparte y amenaza identificadas que requieran una referencia independiente.

Santi expresó interés en la formulación final y pidió documentar la reflexión. Eso no equivale a validar las hipótesis ni a cerrar una decisión con Mateo. El siguiente debate sigue siendo sobre el problema y sus alternativas, no sobre ejecutar automáticamente los planes existentes.
