# Referencias y estado de evidencia

Estas referencias provienen de la exploración previa a este repositorio. No se ejecutaron aquí, no están auditadas por este proyecto y no son dependencias seleccionadas. Sus capacidades actuales deben revisarse antes de adoptar código.

| Referencia | Qué estudiar | Límite |
|---|---|---|
| [Verifiable Agent Memory](https://github.com/26dos/verifiable-agent-memory) | Trazas offchain, compromisos y lotes Merkle; contratos y SDK Python | Prototipo de referencia; no demuestra mejora del workflow ni entrenamiento |
| [Ethereum Attestation Service](https://docs.attest.org/docs/easscan/offchain) y [contratos](https://github.com/ethereum-attestation-service/eas-contracts) | Declaraciones estructuradas, firmadas y verificables | No captura actividad ni vuelve verdadera una afirmación |
| [OpenTimestamps](https://github.com/opentimestamps/opentimestamps-client) | Prueba de existencia mediante Bitcoin | No almacena logs ni aporta búsqueda; confirmación asíncrona |
| [Daryl](https://github.com/daryl-labs-ai/daryl) | Memoria, auditoría y replay offchain | En la revisión previa el anclaje blockchain estaba diferido; no asumirlo implementado |

## Fundamentos

- [Ethereum: disponibilidad de datos](https://ethereum.org/developers/docs/data-availability/).
- [Ethereum: estrategias de almacenamiento](https://ethereum.org/developers/docs/data-availability/blockchain-data-storage-strategies).
- [OpenTelemetry: convenciones semánticas](https://opentelemetry.io/docs/concepts/semantic-conventions/). Referencia de esquema, no integración universal resuelta.
- [OWASP: prevención de prompt injection](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html). Las guías recuperadas siguen siendo datos no confiables.
- [HackaTwin: convocatoria](https://luma.com/cudf7cqz). Verificar reglas antes de implementar para el evento.

El diseño se elaboró mediante entrevista con Santi, incorporando decisiones de la conversación sobre el proyecto de Santi y Mateo. No se publica la transcripción ni enlaces a documentos privados.
