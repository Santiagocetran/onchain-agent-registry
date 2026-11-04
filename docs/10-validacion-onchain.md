# Validación de la cuña: agentes que operan onchain

## Veredicto: hueco parcial, todavía no validado comercialmente

**[INFERENCIA] Hay una cuña investigable en diagnósticos de fallos de herramientas, privados, contextuales y reutilizables entre harnesses; no un espacio vacío en «agentes + memoria + blockchain».** AgentKit y los MCP ya conectan agentes con wallets y contratos; Hardhat Ignition ya gestiona recuperación transaccional; ElizaOS ofrece memoria; Unibase/Membase se solapa directamente en memoria privada portable e identidad onchain; ERC-8004 aborda identidad, reputación y validación. [AgentKit][agentkit], [thirdweb][thirdweb], [Ignition][ignition], [ElizaOS][eliza], [Membase][unibase], [ERC-8004][8004].

**[INFERENCIA] Priorizar equipos que despliegan y operan contratos con agentes de coding**, donde se puede medir repetición y transferencia entre harnesses. Comparar contra herramientas bien configuradas más un playbook fijo, no contra un agente deliberadamente desprotegido. El anclaje merece una prueba separada cuando hay contraparte que no confía en el operador; no se justifica solamente porque el agente use una wallet.

**Balance de evidencia:** la mecánica del riesgo está documentada; su frecuencia y costo atribuibles a agentes, mucho menos. Hay actividad onchain cuantificada por Olas, pero no un censo comparable de equipos compradores. Un reporte público de AgentKit alega pérdidas sin datos reproducibles y con una interpretación problemática del gas. [Ethereum][gas], [Olas Explorer][olas-data], [issue #958][issue958]. No hay resultados propios: los experimentos de abajo son propuestas.

### Alcance y lectura de la evidencia

Consulta de **todos los enlaces externos: 2026-11-04**; la misma fecha figura en el título de cada referencia. Fuentes primarias: especificaciones, documentación y tarifas oficiales, repositorios y declaraciones de sus autores. Una declaración del proveedor prueba lo que ofrece o afirma, no su eficacia. «No identificado en estas fuentes» no significa inexistente. Lo no verificado y los juicios propios llevan **[INFERENCIA]**; los umbrales experimentales son decisiones propuestas, no resultados.

Se conserva el alcance de [README](../README.md), [visión](01-vision.md) y [validación](06-validation.md): historial privado y guías con evidencia; no wallet nueva, motor de transacciones, ranking ni red comercial de sincronización. Esta investigación continúa en la rama `research/onchain-agents`, separada del track CI/DevOps.

**Actualización de alcance acordada en esta rama:** empezar por el [POC simulado de un harness](11-poc-simulado-onchain.md), sin equipos externos como prerrequisito. Los experimentos con trazas consentidas, dos harnesses y pilotos comerciales de este documento quedan como etapas posteriores; no son requisitos para la primera demo ni resultados ya obtenidos.

## 1. Competencia: qué existe y dónde se pisa la idea

La última columna es **[INFERENCIA] comparativa**, no una auditoría exhaustiva de funcionalidades ni una afirmación de exclusividad.

| Proyecto existente | Qué cubre según su fuente primaria | Qué no demuestra / solapamiento con esta propuesta |
|---|---|---|
| **Coinbase AgentKit** | Toolkit wallet/framework-agnostic para dar wallets y acciones onchain a agentes; extensiones de frameworks y MCP. [Repositorio][agentkit] | Resuelve acceso/ejecución. El README consultado no demuestra un historial privado de fallos convertido en guías portables con evidencia. Integrarse encima, no reemplazarlo. |
| **ElizaOS** | Runtime TypeScript, plugins Ethereum/Solana y memoria persistente de interacciones. [Docs][eliza] | Memoria ya existe: no vender «el agente recuerda» como novedad. La página no acredita portabilidad a harnesses ajenos ni validación de playbooks transaccionales. |
| **Olas / Mech** | Solicitudes y entregas de trabajo por agentes, pagos y registros operacionales. `mech info` informa entregas propias/por terceros; distingue benchmarks declarados de datos de cadena; la documentación menciona Karma como reputación onchain del marketplace. [Mech Client][olas-mech] | Solapamiento real en historial/reputación, no sólo marketplace. No equivale a memoria privada cross-harness. La propia fuente advierte que solicitudes offchain nunca entregadas no aparecen en esos conteos. |
| **Virtuals** | EconomyOS: identidad/wallet; ACP: contratación y comercio entre agentes con registro onchain; tokenización. [Whitepaper][virtuals] | Solapa en trazabilidad comercial y accountability, no demuestra en esa página aprendizaje de fallos de RPC/CLI. Un token de agente no acredita autonomía o cliente de memoria. |
| **Safe + ERC-4337** | Safe: multisig, módulos, permisos y guards. ERC-4337: `UserOperation`, bundlers, `EntryPoint`, paymasters. [Safe][safe], [ERC-4337][4337] | Autorización y ejecución, no memoria/reputación. Son complementos de seguridad, no sustituibles por recomendaciones. Safe no es sinónimo de ERC-4337: dispone de módulo 4337. |
| **MCP blockchain / wallets para agentes** | thirdweb MCP expone wallets, `deployContract`, lecturas/escrituras y consulta de transacciones; Alchemy Agent Wallets ofrece sesiones aprobadas/revocables y comandos de estado sin entregar la clave privada al agente. [thirdweb][thirdweb], [Alchemy][alchemy-wallets] | La interfaz cross-harness de herramientas ya existe. No acredita memoria portable de experiencias. El diferencial no puede ser sólo «un MCP para blockchain». |
| **Foundry / Hardhat Ignition** | Foundry guarda artefactos/recibos de broadcast y ofrece reanudación; Ignition journal, reconciliación, simulación, confirmaciones y fee bumps. [Foundry][foundry], [Ignition][ignition] | Sustitutos fuertes para recuperación de deploys. Recuperar estado de una ejecución no es aprender de experiencias entre tareas, pero reduce mucho el hueco propuesto. |
| **ERC-8004 — borrador en la página consultada** | Registros de identidad, reputación y validación; feedback con URI y hash opcionales, respuestas y revocación; compromisos de inputs/outputs para validadores. Pagos son ortogonales. [Especificación][8004] | Ya existe el diseño de registro público de experiencias/calificaciones con evidencia referenciada. No prescribe captura local privada, diagnóstico ni recuperación de guías. Hash no prueba feedback verdadero; la especificación reconoce Sybil/spam. |
| **Unibase / Membase** | Declara memoria cifrada propiedad de la wallet, recall local, identidad onchain e integraciones MCP/ElizaOS/Virtuals/Swarms. El quickstart distingue un SDK de protocolo privado/no publicado del producto distribuido, de API distinta. [Overview][unibase], [quickstart][membase] | **Competidor directo sustancial**, no infraestructura meramente adyacente. No se ejecutó ni auditó. Falta comprobar si captura errores de herramientas y genera guías con condiciones/resultados verificables: posible diferencia, no ventaja demostrada. |
| **Mem0 / Recall** | Mem0 ofrece memoria y enlaza MCP/OpenMemory; Recall se presenta como mercado descentralizado de skills. [Mem0][mem0], [Recall][recall] | Sustitución por memoria genérica o skills, incluso sin cadena. La landing leída de Recall no basta para atribuirle hoy una memoria privada verificable ni para descartarla. |

**[INFERENCIA] Posicionamiento defendible para probar:** «reutilizá el diagnóstico de una ejecución fallida, con contexto y evidencia, entre tus harnesses». No «primer registro de agentes», «primera memoria onchain» ni «tu agente nunca repite un error». ERC-8004 podría consumir señales derivadas si alguna vez se necesita reputación pública; no es requisito del MVP privado.

## 2. Dolor: mecánica comprobada ≠ incidencia comprobada

### Fallos que sí tienen fundamento técnico

| Situación | Hecho documentado | Consecuencia para la hipótesis de memoria — [INFERENCIA] |
|---|---|---|
| **Aceptada ≠ incluida ≠ finalizada** | `eth_sendRawTransaction` devuelve hash; un recibo no existe para una tx pendiente y puede devolver `null` si no se encuentra. El recibo trae bloque y `status`. Ethereum distingue `latest`, `safe` y `finalized`; finalidad PoS es una propiedad de consenso, no del mensaje del agente. [JSON-RPC][rpc], [PoS][pos] | No inferir «pendiente» exclusivamente de `null`, ni «finalizada» de un hash o de `status=1`. Verificar inclusión canónica, política de confirmación/finalidad y postcondición de negocio. |
| **Nonce y reemplazos** | RPC consulta el contador con un estado de bloque; Geth tiene política configurable `txpool.pricebump` — 10% en la versión documentada. Foundry `--resume` no vuelve a simular y exige nonces compatibles. [RPC][rpc], [Geth][geth], [forge script][forge-ref] | Contextualizar por wallet, concurrencia, proveedor y versión. Ni un nonce recordado ni «subir siempre 10%» es una guía universal. Un timeout no prueba que el envío no ocurrió. |
| **Gas y revert** | Una transacción ejecutada paga gas aunque falle; `REVERT` revierte cambios y no consume por sí mismo todo el gas restante. Gas no utilizado se devuelve; rechazo previo a inclusión no es ejecución con gas perdido. [Gas][gas], [EIP-140][140] | Separar error de validación, simulación fallida y revert incluido. No convertir todos los errores de herramientas en pérdida monetaria onchain. |
| **Quirks de RPC** | Geth documenta límites configurables de gas para `eth_call`/estimación y timeout EVM; Ethereum recomienda verificar soporte de APIs por cliente. [Geth][geth], [RPC][rpc] | Guardar cliente/proveedor, chain ID, bloque/estado y versiones. Un cap del proveedor no prueba defecto del contrato; extrapolar una solución a otro RPC puede empeorarla. |
| **Deploy parcialmente completado** | Foundry distingue simular de `--broadcast` y conserva recibos. Ignition registra pasos, reconcilia despliegues, espera confirmaciones y puede abortar por drop/reemplazo inesperado. Una simulación exitosa puede terminar en revert real. [Foundry][foundry], [Ignition][ignition], [errores][ignition-errors] | La oportunidad es elegir/interpretar la recuperación correcta, no volver a implementar el journal ni recomendar borrar estado o rebroadcast a ciegas. |
| **Wallet de agente / ERC-4337** | La unidad `UserOperation` no es la transacción del bundler que la incluye; cuenta, bundler y paymaster tienen validaciones/roles distintos. [ERC-4337][4337] | Separar hash de operación, tx contenedora y resultado individual. No transportar sin condiciones un playbook de EOA a smart account. |

Para EVM, el recibo permite calcular el componente de ejecución como `gasUsed × effectiveGasPrice`; eso no es `gasLimit × maxFeePerGas`. [Campos RPC][rpc], [tarifas][gas]. **[INFERENCIA]** El costo completo del incidente debe sumar por separado fees adicionales de la red/servicio cuando apliquen, modelo, RPC, tiempo humano y operaciones duplicadas; registrar cadena, moneda y fecha de conversión. No extrapolar testnet a dólares mainnet.

### Qué evidencia específica de agentes se encontró

| Tipo de evidencia | Resultado y límite |
|---|---|
| **Reporte del autor de una herramienta, no medición validada** | [AgentKit #958][issue958], abierto 2026-02-15: dice analizar **16 wallets en Base**, con dos agentes en **25–56%** de fallos y aproximadamente **US$918/mes** de «waste». Menciona nonce/retry y gas limits sobredimensionados. No publica wallets, tx hashes, ventana temporal, muestreo ni cálculo; no es un resultado confirmado por Coinbase. |
| **Objeción económica al reporte** | El issue asocia límites de gas ~20 veces el uso con gasto desperdiciado. En EVM el gas no utilizado se devuelve. Por tanto, esa relación no demuestra la pérdida alegada; el monto no sirve como ROI del producto. [Issue][issue958], [Ethereum][gas]. **[INFERENCIA]** Es una pista para entrevistar al autor, no evidencia financiera suficiente. |
| **Pérdida de fondos atribuible al agente** | No se identificó en la búsqueda acotada un postmortem primario con transacciones y atribución reproducible de pérdida por estos fallos operacionales. **[INFERENCIA]** Puede existir; no convertir exploits DeFi, puzzles deliberados ni bugs de RPC genéricos en «pérdidas de agentes evitables con memoria». |

**[INFERENCIA] Conclusión de dolor:** plausibilidad técnica alta; frecuencia, recurrencia evitable y pérdida incremental por agente todavía sin validar. Un revert conserva el riesgo de gas, pero no prueba pérdida del principal; una transferencia equivocada exitosa es otro tipo de riesgo. Memoria no sustituye simulación, límites de gasto, permisos ni aprobación humana.

## 3. Tamaño real: actividad visible, compradores sin censo

Datos de primera parte, **no auditados en esta investigación**. El [Explorer de Olas][olas-data] reporta estos valores para **2026-11-03**, actualización **2026-11-04 06:50 UTC**:

| Producto/economía Olas | Daily active agents declarados |
|---|---:|
| Omenstrat / Predict | 197 |
| Polystrat / Predict | 20 |
| Optimus / BabyDegen | 17 |
| Basius / BabyDegen | 8 |
| Mech | 13 |
| Connect | 2 |

La fuente además atribuye **16.929.875 transacciones** a Omenstrat entre 2023-07-12 y 2026-11-03. Es actividad de una familia de agentes según su proveedor, no millones de agentes/clientes. [Olas][olas-data].

- **Dato:** existen productos con actividad reportada diariamente; ERC-8004, en cambio, define registros y señales, no un censo de actividad. [Olas][olas-data], [ERC-8004][8004].
- **Estimación defendible:** no se construye una del total de industria con estas fuentes. **[INFERENCIA]** No sumar la tabla como agentes únicos: falta demostrar deduplicación, definición comparable y ausencia de incentivos que sesguen actividad.
- **Equipos independientes activos hoy:** no se obtuvo un conteo verificable. **[INFERENCIA]** DAA, wallet, identidad registrada, token, descarga e integrante de un equipo son unidades diferentes; ni cada agente compra ni cada registro opera onchain.
- **Opinión / [INFERENCIA]:** hay suficiente actividad para buscar pilotos focalizados, no para justificar un TAM ni una tesis de escala comercial. El nicho de agentes de coding que hacen deploys puede no coincidir con las economías Olas medidas.

## 4. Comprador, venta y precios comparables

**[INFERENCIA] Comprador inicial:** responsable de ingeniería/operaciones de un equipo que mantiene agentes con wallet o pipelines de contratos y puede mostrar incidentes recurrentes. Usuario: desarrollador/SRE que cambia entre harnesses. Segundo candidato: autor de tool/MCP interesado en diagnosticar misuso, sólo si dispone de trazas consentidas. No asumir que un agente tokenizado, un trader individual o compliance comprarán.

| Comparable oficial | Tarifa/unidad visible al consultar | Lectura comercial — [INFERENCIA] |
|---|---|---|
| [Privy][privy] — wallets/firmas | Developer: gratis 0–499 MAU, US$299/mes 500–2.499, US$499/mes 2.500–9.999; 50.000 firmas/mes incluidas. Excedentes tienen condiciones y base PAYG de US$2.000 en FAQ. | Hay presupuesto adyacente, no precio por agente. Firma tampoco equivale necesariamente a tx ejecutada. |
| [Alchemy][alchemy-price] — RPC | Gratis 30 millones CU/mes; PAYG **US$0,52/millón CU**. | Competir sólo por ahorrar llamadas RPC podría tener poco valor; CU no es una transacción ni un agente. |
| [Tenderly][tenderly] — debug/simulación/monitorización | Free individual con simulación UI, sin API; equipos por contrato, **sin tarifa numérica pública** en la página leída. | Sustituto para diagnóstico/evidencia. Evitar duplicar observabilidad que el equipo ya compra. |
| [Mem0][mem0] — memoria | Free: primeros 30 días, 10.000 adds y 1.000 retrievals/mes; con clave LLM propia, 50.000 y 10.000. Custom negociado; no precio unitario pagado publicado allí. | Memoria genérica tiene alternativa gratuita; no demuestra disposición a pagar por experiencias onchain. |

Son **ofertas publicadas**, no ventas observadas ni pruebas de willingness-to-pay específica. No se verificó una tarifa directamente comparable de «playbooks onchain cross-harness con evidencia».

**[INFERENCIA] Venta mínima:** CLI local open source como canal de prueba; vender después un piloto de reducción de incidentes y playbooks privados de equipo, no un hash ni una promesa de cero errores. Pedir trazas redactadas de los últimos 30 días y un responsable de presupuesto; mostrar ahorro neto incluyendo preparación/mantenimiento. Hosting/sync cifrado y catálogos curados siguen fuera de la hackathon. Si el comprador sólo quiere logs y alertas, integrar con lo existente o descartar la cuña.

## 5. ¿Blockchain agrega algo frente a firma + append-only?

**Sí, una referencia compartida resistente a sustitución unilateral; no mejor diagnóstico ni verdad del relato.** El comparador serio no es un archivo sin protección: Certificate Transparency ya especifica firmas, árboles Merkle, pruebas de inclusión/consistencia y advierte sobre vistas divergentes de un log. RFC 3161 permite timestamping mediante una autoridad confiable sin blockchain. [RFC 9162][9162], [RFC 3161][3161]. La aplicación a este producto es **[INFERENCIA] de diseño**, no una garantía implementada.

| Garantía/amenaza | Firma + log append-only | Qué agregaría C correctamente diseñado — [INFERENCIA] |
|---|---|---|
| Archivo alterado respecto de un compromiso conocido | Hash/firma y prueba de inclusión ya lo detectan. | No agrega detección criptográfica básica. |
| Operador reescribe todo y firma otro historial; lector nuevo sin checkpoint | Una clave del operador puede firmar versiones distintas. Clientes con checkpoints conservados o testigos pueden detectar divergencia. | Raíz publicada y finalizada en ubicación acordada, verificable sin pedir al operador que elija qué historial mostrar. Cambia la confianza del operador por consenso/red, contrato y verificación. |
| Operador muestra dos vistas | Pruebas de consistencia y comparación entre lectores/testigos ayudan; un lector aislado puede no descubrirlo. | Referencia canónica para un mismo log/secuencia **si** contrato y clientes impiden ambigüedad, sobreescritura y rollback. Publicar raíces arbitrarias sin esas reglas no elimina equivocación. |
| Antigüedad/orden | Firma sola no da tiempo externo; TSA o checkpoints presenciados sí pueden hacerlo. | Evidencia de compromiso incluido en determinado bloque/orden, no hora exacta de captura ni prueba de que el evento ocurrió entonces. |
| Veracidad, captura completa, corrección o disponibilidad de la guía | No las demuestra. | Tampoco. Un evento omitido antes de captura es invisible; una raíz no recupera contenido borrado ni vuelve cierto un RPC mentiroso. |

La resistencia a reorganización/finalidad depende de la red; no existe una garantía universal por esperar cualquier número de bloques. En Ethereum PoS, finalidad corresponde al consenso y sus supuestos económicos. [PoS][pos]. **[INFERENCIA]** En una L2 habría que especificar separadamente aceptación del secuenciador, publicación/liquidación y política del verificador. Un único RPC no confiable no basta para demostrar independientemente una raíz canónica.

**[INFERENCIA] A quién le importa:** cliente que contrata un operador de agentes, dos organizaciones en disputa o un auditor que necesita verificar qué evidencia se comprometió antes de un incidente, aun si el operador cambia su servidor o pierde confiabilidad. Importa menos a un solo desarrollador que controla ambos extremos: checkpoints firmados fuera de la máquina pueden bastar. Si ese tercero no aparece en las entrevistas, B es la opción por defecto.

**[INFERENCIA] Condiciones mínimas para probar C:** acordar chain ID/contrato/log ID, secuencia y encadenamiento de raíces; conservar contenido y prueba; fijar política de finalidad y correcciones append-only. Nada de claves, URLs RPC con credenciales o logs privados en cadena. Un hash de contenido predecible puede revelar información por comparación: no asumir que hash equivale a anonimización. El costo por lote debe amortizarse y medirse fuera del camino transaccional crítico.

**[INFERENCIA] Estar en la misma cadena que la tx sólo facilita correlacionar referencias.** La cadena ya registra la tx incluida; anclar ese hash otra vez añade poco. El objeto diferencial serían intentos offchain, respuestas, versiones, condiciones y la guía derivada. Eso sigue sin demostrar que la captura sea fiel. Blockchain «nativo» no equivale a blockchain necesario.

## 6. Riesgos que pueden invalidar la apuesta

Todos son **[INFERENCIA]** salvo las capacidades documentadas arriba:

- **Memoria innecesaria:** una máquina de estados, configuración correcta o skill fija resuelve el patrón; B no mejora a A con herramientas robustas. No enseñar al modelo lo que el SDK debería garantizar.
- **Transferencia insegura:** versión, cadena, contrato, wallet y proveedor cambian; una guía vieja puede causar reemplazos, fees o envíos duplicados. Nunca reproducir firmas, nonces o tx históricas como receta.
- **Captura parcial/privacidad:** faltan intentos fuera del harness; trazas pueden contener claves, calldata privada o estrategia. Menos datos compartibles significa menos reutilización.
- **Memoria envenenada:** evidencia firmada/íntegra pero falsa o instrucciones maliciosas. Consultar una guía no autoriza mover fondos; correcciones deben retirar recomendaciones, no sólo acumularse.
- **Mercado pequeño y distribución difícil:** instancias incentivadas o muchos agentes del mismo operador no son muchos compradores. Frameworks/infra pueden incorporar el diagnóstico; Membase ya ocupa parte del posicionamiento.
- **Anclaje sin contraparte:** gas, latencia, disponibilidad y gestión de claves sin beneficio comprador. No financiar C con ahorro hipotético de B.

## 7. Tres experimentos concretos y regla de decisión

Variantes de [doc 06](06-validation.md): **A sin memoria; B memoria sin blockchain; C misma memoria con blockchain**. Diseño y umbrales siguientes: **propuestas [INFERENCIA]**, no resultados ni compromisos de rendimiento.

| Experimento | Diseño y variantes | Medición y decisión propuesta |
|---|---|---|
| **1. ¿La memoria evita repetición real?** | **A/B.** Conseguir tres trazas consentidas: éxito prematuro con tx pendiente; conflicto de nonce/timeout ambiguo; deploy parcial o revert/RPC. Reproducir en devnet/fork sin fondos reales. Preparar guías con ejecuciones separadas y evaluar dos harnesses. A conserva simulación, journal/recuperación y un playbook fijo igual para todos; B añade sólo experiencias. Incluir tareas nuevas y una variante incompatible por patrón. Al menos 5 pares por patrón/harness, orden aleatorio y estado reiniciado. | Juez externo: recibo/estado canónico y postcondición del contrato, no declaración del agente. Éxito, falsas finalizaciones, envíos duplicados, intentos evitables, tokens, latencia y costo total de doc 06. Continuar sólo si B produce ahorro neto a una reutilización declarada, sin reducir éxito ni aplicar guías incompatibles. Si empata con el playbook fijo, descartar memoria dinámica para ese patrón. |
| **2. ¿C compra una garantía distinta?** | **B/C**, mismos bytes, firmas, Merkle y guías. B conserva checkpoints firmados; añadir un control B con checkpoint en poder de un tercero. C ancla raíz por lote en una testnet, con log/secuencia y finalidad explícitos. Dos lectores, uno nuevo: alterar un evento; reemplazar todo el historial y volver a firmar; presentar dos vistas; omitir un evento antes de capturarlo. Probar también prueba inaccesible y anclaje pendiente. | Ambos deben detectar alteración contra compromiso conocido; ninguno debe prometer detectar omisión precaptura. Mostrar cuándo C resuelve referencia para lector nuevo y cuándo B con testigo ya alcanza. Pendiente ≠ final; inaccesible ≠ alterado. Medir gas/lote, tiempo hasta prueba final, verificación y dependencias. C continúa sólo con una contraparte que valore esa diferencia; no se le atribuye ahorro de memoria. |
| **3. ¿Hay comprador, no sólo interés?** | Reclutar **8 equipos independientes** que operaron onchain en los últimos 30 días; pedir evidencia redactada y dueño de presupuesto. Piloto concierge **A/B** de dos semanas sobre tareas recurrentes, con permiso y sin control de claves; ofrecer **C** por separado para evidencia ante un tercero. Probar una oferta concreta de **US$100/equipo/mes** por playbooks privados y seguimiento del piloto, no sync comercial aún. | Registrar equipos elegibles, incidentes recurrentes, horas/fees atribuibles, reutilizaciones y costo de preparación/soporte. Umbral: 3 equipos aportan casos reproducibles y al menos 2 aceptan pagar ese monto — pago o pedido de compra, no encuesta de intención. Para C exigir además contraparte, amenaza y presupuesto identificados. Si sólo pagan B, seguir sin cadena; si no hay repetición/pago, descartar esta cuña y contrastar autores de tools. |

Para 1 y 3: mantener modelo, herramientas, versiones y presupuesto equivalentes; no dejar que A herede guías de B. Contabilizar fallos de consulta/captura y su cobertura. Reportar distribución y casos individuales, no sólo promedio; extrapolaciones mainnet con supuestos separados. Es una aplicación de los controles de [doc 06](06-validation.md), no una medición realizada.

### Fit con HackaTwin — 7 de noviembre de 2026

La [convocatoria de Twin][hackatwin] anuncia 12 horas de build, tracks AI/Blockchain/Fintech, equipos de hasta cuatro, entrega a las 18:00 y demo a las 19:00. La página consultada figura **Event Full / waitlist**. No contiene en el texto leído rúbrica detallada, montos de premios ni obligación de usar una cadena concreta; no se presupone ninguno.

**Alcance inmediato acordado:** el [protocolo de POC simulado](11-poc-simulado-onchain.md) define una cadena local, un harness con sesiones aisladas, un patrón de fallo inducido y una comparación A/B con playbook fijo. Incluye una variante incompatible y contabilidad de preparación. No exige reclutar equipos ni completar el MVP de dos harnesses para la demo; no guionar un fracaso de A ni ocultar un empate.

**Prueba de integridad separada:** si se realiza, verificar original y copia alterada contra un compromiso conocido. Una prueba local no se presenta como anclaje público ni como demostración del valor incremental de blockchain. El experimento B/C, las trazas reales y el piloto comercial continúan pendientes.

**Decisión propuesta [INFERENCIA]:** avanzar a pruebas A/B de la cuña «agentes de coding que despliegan/operan contratos»; mantener C como prueba adversarial independiente. No declarar mercado ni ahorro validados hasta obtener trazas, denominadores y compromisos de pago.

## 8. Recorte de producto: qué validar antes de construir

Síntesis de brainstorming, **propuesta [INFERENCIA], no resultado experimental**. El paso inmediato acordado se acota en el [POC simulado](11-poc-simulado-onchain.md); la segmentación y los controles siguientes orientan las etapas posteriores y no sustituyen la investigación anterior.

### «Agentes onchain» todavía no es un segmento

| Recorte | Usuario y trabajo | Juicio para esta propuesta — [INFERENCIA] |
|---|---|---|
| Agentes de coding que despliegan y mantienen contratos EVM | Equipo de ingeniería que diagnostica ejecuciones con herramientas y cambia entre harnesses | Primer candidato: conserva el usuario y el historial de herramientas de la idea original. Hay que comprobar que realmente cambia de harness y repite diagnósticos. |
| Agentes autónomos que operan protocolos recurrentemente | Operador de una estrategia o servicio con wallet | Segundo candidato, no equivalente al anterior: puede necesitar estado persistente, permisos y recuperación determinista antes que guías para un agente. No asumir que el volumen de transacciones implica demanda de memoria. |
| Directorio o ranking público de agentes | Contratante que selecciona proveedores | Otro producto y otro problema. Identidad, reputación y validación ya son el objeto de ERC-8004; no convertir esta cuña privada en un registro reputacional. [ERC-8004][8004] |

**Hipótesis de producto [INFERENCIA]:** «Ayudamos a equipos que usan agentes de coding para operar contratos a reutilizar diagnósticos comprobados entre harnesses, sin volver a explorar el mismo fallo ni aplicar una receta de otro entorno».

No prometer prevenir pérdidas de fondos, mejorar rentabilidad ni garantizar ejecución correcta. El impacto buscado es menos diagnóstico repetido y menos intervención humana para completar correctamente la misma tarea.

**Competencia verificada en esta revisión:** Membase documenta observaciones inmutables, relaciones de sustitución, ventanas de vigencia, recuperación local determinista sin LLM y citas. [Memory & Recall][membase-memory]. Son capacidades declaradas, no auditadas aquí. **[INFERENCIA]** «Memoria con evidencia y correcciones» tampoco basta como diferencial: habrá que demostrar mejor diagnóstico operacional sobre esas alternativas, no sólo sobre ausencia de memoria.

### Por qué acotar podría mejorar la evaluación

**Hecho:** JSON-RPC expone recibos con bloque y estado de ejecución; un recibo ausente devuelve `null`, que no identifica por sí solo la causa. [Ethereum JSON-RPC][rpc].

**[INFERENCIA]** Esto permite un juez parcialmente externo al relato del agente: contrastar recibo, estado del contrato y objetivo acordado. No basta con `status=1`: un deploy exitoso puede tener configuración incorrecta. Tampoco mide decisiones offchain ni demuestra el origen de un incidente. El evaluador debe fijar red, política de finalidad y postcondición antes de ejecutar.

**[INFERENCIA]** Elegir una familia de tareas, una cadena y un stack reduce variables y facilita reproducir incidentes. No demuestra que el nicho sea fácil de vender: puede haber pocos equipos independientes, poco cambio entre harnesses o una solución determinista más barata. «Más pequeño» no equivale a «más atacable».

### Filtro para elegir el primer incidente

**[INFERENCIA]** Para la fase posterior con trazas reales del experimento 1, exigir un caso consentido que cumpla estas condiciones. No es un prerrequisito del POC sintético:

1. El diagnóstico ya se repitió en tareas distintas; no es sólo reanudar el mismo deploy.
2. El SDK/journal, la configuración correcta y un playbook fijo siguen disponibles en el control.
3. Hay contexto aprendido útil para elegir el diagnóstico, y una variante cercana donde esa guía debe rechazarse.
4. Se puede restablecer el entorno y comprobar una postcondición sin fondos reales.

Un timeout después de un envío o un deploy parcial son **candidatos**, no prueba de que haga falta memoria. Si una regla fija basta, conservar esa regla y descartar memoria dinámica para ese patrón. No debilitar el control para conseguir una demo favorable.

### Encaje con el evento y siguiente decisión

**Hecho:** la convocatoria indica elegir un track: AI incluye agentes y automatizaciones; Blockchain incluye infraestructura y herramientas para builders. No demuestra que se pueda concursar simultáneamente en ambos. [HackaTwin][hackatwin].

**Recomendación [INFERENCIA]:** presentar AI como problema principal —mejorar la ejecución del agente con experiencias— y evidencia onchain como componente verificable. Blockchain es una presentación alternativa si la rúbrica prioriza infraestructura; confirmar rúbrica y reglas de trabajo previo con la organización. No elegir red por la mera presencia de un sponsor.

**Siguiente acción acordada:** documentar primero el [POC simulado y su evaluación controlada](11-poc-simulado-onchain.md), sin reclutamiento como bloqueo. **Validación posterior [INFERENCIA]:** buscar tres equipos del recorte de coding dispuestos a mostrar su último incidente, solución actual y repetición; preguntar qué conservaron en logs, skills o memoria nativa y por qué no alcanzó. Ese filtro no reemplaza el piloto de ocho equipos del apartado 7.

**Canal secundario, no comprador demostrado:** Olas distingue builders que crean código de operadores que ejecutan herramientas y ofrece documentación, academia y repositorios públicos. [Olas Builders][olas-builders]. **[INFERENCIA]** Son pistas para reclutar operadores del segundo recorte, no evidencia de que usen agentes de coding ni cambien entre harnesses; no mezclar sus entrevistas con el segmento elegido sin registrar esa diferencia.

**Regla de salida [INFERENCIA]:** sin repetición demostrable no hay hipótesis de memoria; sin mejora sobre el control no hay diferencial; sin contraparte que necesite una referencia independiente no hay justificación de producto para el anclaje. El fit de hackathon no resuelve ninguna de esas tres preguntas.


[agentkit]: https://github.com/coinbase/agentkit "Coinbase AgentKit — consulta: 2026-11-04"
[eliza]: https://docs.elizaos.ai/ "ElizaOS Overview — consulta: 2026-11-04"
[olas-mech]: https://stack.olas.network/mech-client/ "Olas Mech Client, incluido historial y límites de conteo — consulta: 2026-11-04"
[virtuals]: https://whitepaper.virtuals.io/ "Virtuals Protocol, overview — consulta: 2026-11-04"
[safe]: https://docs.safe.global/advanced/smart-account-overview "Safe Smart Account architecture — consulta: 2026-11-04"
[4337]: https://eips.ethereum.org/EIPS/eip-4337 "ERC-4337 — consulta: 2026-11-04"
[8004]: https://eips.ethereum.org/EIPS/eip-8004 "ERC-8004, borrador consultado — consulta: 2026-11-04"
[thirdweb]: https://portal.thirdweb.com/ai/mcp "thirdweb MCP server — consulta: 2026-11-04"
[alchemy-wallets]: https://www.alchemy.com/docs/agent-wallets "Alchemy Agent Wallets — consulta: 2026-11-04"
[unibase]: https://docs.unibase.com/ "Unibase y Membase, capacidades declaradas — consulta: 2026-11-04"
[membase]: https://docs.unibase.com/get-started/membase-quickstart/ "Membase Quick Start, límites de SDK/API — consulta: 2026-11-04"
[recall]: https://docs.recall.network/ "Recall, landing de documentación — consulta: 2026-11-04"
[foundry]: https://www.getfoundry.sh/forge/scripting "Foundry scripting — consulta: 2026-11-04"
[forge-ref]: https://www.getfoundry.sh/reference/forge/script "forge script: --resume y --slow — consulta: 2026-11-04"
[ignition]: https://hardhat.org/ignition/docs/explanations/execution.md "Hardhat Ignition, ejecución y journal — consulta: 2026-11-04"
[ignition-errors]: https://hardhat.org/ignition/docs/explanations/error-handling.md "Hardhat Ignition, manejo de errores — consulta: 2026-11-04"
[rpc]: https://ethereum.org/developers/docs/apis/json-rpc/ "Ethereum JSON-RPC — consulta: 2026-11-04"
[pos]: https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/ "Ethereum PoS y finalidad — consulta: 2026-11-04"
[gas]: https://ethereum.org/en/developers/docs/gas/ "Ethereum gas y fees — consulta: 2026-11-04"
[140]: https://eips.ethereum.org/EIPS/eip-140 "EIP-140, REVERT — consulta: 2026-11-04"
[geth]: https://geth.ethereum.org/docs/fundamentals/command-line-options "Geth, opciones y valores de la versión documentada — consulta: 2026-11-04"
[issue958]: https://github.com/coinbase/agentkit/issues/958 "Reporte de tercero, AgentKit #958 — consulta: 2026-11-04"
[olas-data]: https://olas.network/agent-economies/explorer "Olas Agent Economy Explorer, datos al 2026-11-04 06:50 UTC — consulta: 2026-11-04"
[privy]: https://www.privy.io/pricing "Privy pricing — consulta: 2026-11-04"
[alchemy-price]: https://www.alchemy.com/pricing "Alchemy pricing — consulta: 2026-11-04"
[tenderly]: https://tenderly.co/pricing "Tenderly pricing — consulta: 2026-11-04"
[mem0]: https://mem0.ai/pricing "Mem0 pricing — consulta: 2026-11-04"
[9162]: https://www.rfc-editor.org/rfc/rfc9162.html "RFC 9162, inclusión/consistencia y vistas divergentes — consulta: 2026-11-04"
[3161]: https://www.rfc-editor.org/rfc/rfc3161.html "RFC 3161, Time-Stamp Protocol — consulta: 2026-11-04"
[hackatwin]: https://luma.com/cudf7cqz "Twin, convocatoria HackaTwin — consulta: 2026-11-04"
[membase-memory]: https://docs.unibase.com/membase/memory/ "Membase Memory & Recall — consulta: 2026-11-04"
[olas-builders]: https://build.olas.network/docs "Olas Builder Documentation — consulta: 2026-11-04"
