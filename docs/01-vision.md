# Visión y decisiones

## Usuario y necesidad

El usuario inicial es un desarrollador que trabaja con harnesses como Codex, Claude Code o Hermes. Esos nombres describen integraciones candidatas, no compatibilidad implementada. Quiere reducir intentos evitables de herramientas y reutilizar experiencias entre harnesses y proyectos.

## Casos guía aceptados

| Patrón | Evidencia observable | Mejora buscada |
|---|---|---|
| Invocación incorrecta | Argumentos rechazados o formato inválido | Consultar el contrato correcto y sus condiciones |
| Repetición sin adaptación | Llamadas repetidas con el mismo error | Reconocer el patrón y cambiar el diagnóstico |
| Aceptación confundida con finalización | Respuesta pendiente seguida de declaración de éxito | Consultar el estado antes de declarar finalización |
| Exploración Bash repetida | Varios intentos antes del resultado esperado | Reutilizar un procedimiento compatible ya comprobado |

Los errores pueden pertenecer al agente, al harness o al entorno. Se permite causa desconocida; un fallo no demuestra automáticamente un mal uso por el agente.

## Decisiones aceptadas durante la conversación

- Probar utilidad de memoria e integridad mediante blockchain; medir ambas por separado.
- Historial de ejecuciones como núcleo, no directorio o ranking de agentes.
- Proyecto como contexto opcional cuando influye en el problema.
- Guías breves con condiciones y evidencia, no reproducción ciega de comandos.
- Consulta selectiva y local; no una llamada obligatoria antes de cada comando.
- Consultas sin una llamada adicional al modelo para decidir si conviene buscar.
- Registro y generación de guías fuera del camino inmediato cuando sea posible.
- Correcciones agregadas sin reemplazo silencioso; guías cuestionadas no se recomiendan.
- Filtrado antes de persistir, minimización y cifrado del contenido privado.
- CLI común y adaptadores por harness; cobertura de captura explícita.
- Copias verificadas localmente; refresco al inicio de sesión y en segundo plano.
- Continuidad del agente ante fallos o demora de memoria; rechazo de contenido que no coincide con su prueba.
- Open source y despliegue controlado por el usuario; servicio pago opcional posterior.
- Primer MVP local para dos harnesses. Sin sincronización comercial en la hackathon.
- Todas las resoluciones alimentan el historial, también cuando la guía era incompatible.

## Lo que no prometemos

No garantizamos que el historial esté completo, que las declaraciones sean verdaderas, que una guía funcione en cualquier contexto o que blockchain mejore la inteligencia del agente. El POC actual es documental: el ahorro y la integración siguen sin demostrarse.
