# POC conceptual y primer MVP

## POC actual

Este repositorio es el POC conceptual: documenta arquitectura, recorridos, modelo de confianza, alcance y experimento. No ejecuta agentes, no publica transacciones y no prueba ahorro. El término POC aquí no significa validación técnica completada.

## Siguiente paso acordado: POC simulado onchain

Antes del MVP completo, esta rama documenta un [protocolo de simulación controlada](11-poc-simulado-onchain.md): un harness, sesiones aisladas, una cadena EVM local, una familia de tareas y un patrón de fallo inducido. Compara herramientas y playbook fijo contra lo mismo más una experiencia local, incluyendo contexto incompatible y costo de preparación.

No requiere reclutar equipos ni integrar dos harnesses para empezar. La prueba de integridad es independiente y no exige anclaje público en esta etapa. Todavía no se implementó ni ejecutó; no hay métricas observadas. La validación comercial queda para después.

El alcance de dos adaptadores, tres patrones y lotes en testnet que sigue corresponde al MVP posterior, no a los requisitos de esta primera demo.

## MVP funcional propuesto

- Instalación local controlada por el usuario.
- Dos adaptadores, seleccionados después de comprobar capacidades reales.
- CLI de registro, consulta y verificación; sintaxis todavía no definida.
- Historial protegido, correcciones y cobertura de captura declarada.
- Guías breves con condiciones y evidencia; búsqueda local acotada.
- Tres patrones iniciales y ejemplo Bash, sin prometer universalidad.
- Publicación de lotes en testnet por seleccionar.
- Verificación local reutilizable y refresco de correcciones.
- Continuidad ante fallos; todas las ramas aportan resultados cuando la captura es posible.
- Instrumentación del costo total y evaluación comparativa.

## Fuera de alcance

Servicio comercial, sincronización entre dispositivos, cuentas y facturación, memoria comunitaria, reputación, token propio, entrenamiento de modelos, registro completo de cualquier harness, certificación de ejecución real y auditoría productiva de seguridad.

## Secuencia de validación sugerida para el MVP posterior

1. Comprobar puntos de captura y consulta de dos harnesses. Documentar eventos no observables.
2. Definir esquema, criterio de éxito y condiciones de aplicación usando ejemplos sintéticos.
3. Evaluar memoria local sin blockchain y medir si evita exploración repetida.
4. Agregar compromisos y verificación, medir costo incremental.
5. Probar correcciones, incompatibilidades, alteraciones y fallos de disponibilidad.
6. Comparar resultados y decidir si ampliar, ajustar o detener el desarrollo.

No es un cronograma aprobado ni autorización para implementar ahora.

## Decisiones pendientes antes de código

| Decisión | Qué debe resolverse |
|---|---|
| Harnesses | Dos integraciones y cobertura observada; ninguna compatibilidad garantizada |
| Habilitación de guías | Evidencia mínima, revisión humana y manejo de falsos éxitos |
| Captura | Eventos mínimos, límites de tamaño, buffering y huecos |
| Consulta | Recuperación, deduplicación, presupuesto y compatibilidad |
| Blockchain | Red, mecanismo de compromiso, tamaño/frecuencia de lotes y finalidad |
| Formato criptográfico | Serialización, hashes, pruebas, privacidad de metadatos |
| Claves | Firmas, cifrado, respaldo y recuperación |
| Retención | Qué conservar, cuánto tiempo y cómo borrar copias privadas |
| Actualización | Frecuencia, caducidad y comportamiento offline |
| Economía | Umbrales aceptables y número de reutilizaciones para amortizar |

## HackaTwin

El alcance se orienta al evento del 7 de noviembre de 2026. Según la información conversada, inicio 9:00 y entrega 18:00 ART: no asumir doce horas continuas. Rúbrica, trabajo previo permitido y requisitos de red/API siguen pendientes de confirmación oficial. El servicio pago no se desarrollará para la hackathon.
