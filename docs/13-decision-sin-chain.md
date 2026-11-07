# Decisión: ¿vale la pena la idea sin blockchain?

**Estado:** hipótesis para discutir, rama `idea/consolidated-map`. No hay resultados. Complementa [12](12-mapa-consolidado.md); no modifica [01](01-vision.md) ni el protocolo de [11](11-poc-simulado-onchain.md).

## Hipótesis

> Un historial **local** de fallos de herramientas, destilado en guías **con condiciones y evidencia** y reutilizable **entre harnesses**, reduce exploración repetida más que lo que ya tiene el usuario (skills, `AGENTS.md`/`CLAUDE.md`, memoria nativa del harness, Mem0/Membase).

Sin cadena en el camino crítico. El anclaje queda como extensión posterior, sólo si aparece un tercero que desconfía del operador ([10 §5](10-validacion-onchain.md)). Firma + log append-only cubre la integridad local mientras tanto.

## Por qué hay que dudar (del propio repo)

- Memoria de agentes ya está ocupada: Mem0, ElizaOS, Recall y, sobre todo, Membase/Unibase, descrito en [10 §1](10-validacion-onchain.md) como «competidor directo sustancial».
- [10 §8](10-validacion-onchain.md): «memoria con evidencia y correcciones» no basta como diferencial; hay que ganarle a esas alternativas, no sólo a no tener memoria.
- Un playbook fijo o una skill pueden resolver el patrón ([11 §3](11-poc-simulado-onchain.md)). Si es así, la memoria dinámica sobra para ese patrón.
- Sin mediciones propias ([README](../README.md)).
- `[INFERENCIA]` Los harnesses (p. ej. Claude Code) ya tienen memoria nativa y skills. No verificado en este repo.

## Qué podría ser diferencial (a demostrar, no asumido)

1. Captura de **fallos de herramientas/harness**, no preferencias ni hechos.
2. Guías con **condición de aplicabilidad** y rechazo explícito si no corresponde.
3. **Portabilidad** entre harnesses.
4. Evidencia enlazada a la traza de origen.

Si ninguno de los cuatro supera a las alternativas en los chequeos de abajo, no hay producto.

## Chequeos de descarte

Orden: barato → caro. Parar en el primer «descarte».

| # | Chequeo | Cómo | Descarte si… |
|---|---|---|---|
| 1 | **Repetición real** | Listar 5 fallos de herramientas que *vos* viste repetirse en sesiones reales. Registrar harness, herramienta, síntoma, cuántas veces. | No hay 3+ casos que se repitieron en tareas distintas. Sin repetición no hay hipótesis ([10 §8](10-validacion-onchain.md)). |
| 2 | **¿Lo cubre una regla fija?** | Para cada caso, escribir la línea de `AGENTS.md`/skill que lo habría evitado. | 4 de 5 se resuelven con una línea estática. |
| 3 | **¿Lo cubre memoria nativa/existente?** | Repetir los casos restantes con la memoria nativa del harness y con Mem0 y/o Membase (instalar, cargar la experiencia, probar tarea equivalente). | Alguna alternativa logra lo mismo con costo de preparación similar. |
| 4 | **Condicionalidad** | Para los casos que sobreviven, armar una variante incompatible. ¿La alternativa aplica ciegamente la solución previa? | La alternativa distingue bien la variante incompatible. |
| 5 | **Costo neto** | Medir tiempo/tokens de preparar la guía vs. ahorro por reutilización ([06](06-validation.md)). | No amortiza en un número plausible de reutilizaciones. |

Reglas: mismo modelo, herramientas y presupuesto en ambos brazos; guardar también empates y regresiones; no debilitar el control ([11 §1, §3](11-poc-simulado-onchain.md)).

## Decisión

| Resultado | Acción |
|---|---|
| Descarte en 1 o 2 | Detener o rediseñar: la memoria dinámica no aporta. Documentar el hallazgo. |
| Descarte en 3 o 4 | Adoptar la alternativa; contribuir lo diferencial (si queda) como plugin/skill en vez de producto propio. |
| Sobrevive 1–5 | Seguir con el POC de [11](11-poc-simulado-onchain.md) **sin** cadena; evaluar anclaje sólo con contraparte real. |

## Pendiente

- Quién lista los 5 casos del chequeo 1 (propuesta: ambos, de forma independiente, y comparar).
- Qué alternativas entran en el chequeo 3 (mínimo: memoria nativa del harness usado + Mem0 + Membase).
- Confirmar con Santi que dejar la cadena fuera del camino crítico es aceptable: contradice el énfasis de blockchain del README.
