# Flujos y ejemplos

## Momento 1: descubrir una experiencia

```mermaid
flowchart TD
    A["El agente intenta una tarea"] --> B["Una herramienta falla"]
    B --> C["Prueba una alternativa"]
    C --> D["Registra contexto, intentos y resultado"]
    D --> E{"¿Resultado comprobado?"}
    E -->|Sí| F["Preparar guía candidata o sumar evidencia"]
    E -->|No| G["Conservar fallo sin recomendar solución"]
    F --> H["Versionar contenido y publicar compromiso en fondo"]
    G --> H
```

## Momento 2: reutilizar o descubrir otra variante

```mermaid
flowchart TD
    A["Nueva operación"] --> B{"¿Conviene consultar?"}
    B -->|Sí| C["Búsqueda local acotada"]
    B -->|No| H["Resolución habitual"]
    C --> D{"¿Guía aplicable, vigente y verificada?"}
    D -->|Sí| E["Comprobar condiciones actuales"]
    E -->|Compatibles| F["Usar guía y comprobar resultado"]
    E -->|Incompatibles| H
    D -->|No, error o demora| H
    F --> R["Registrar intentos y resultado"]
    H --> R
    R --> S{"¿Hay solución comprobada?"}
    S -->|Sí| T["Nueva guía candidata o evidencia adicional"]
    S -->|No| U["Historial de fallo sin solución recomendada"]
```

**Incompatibilidad no significa que la guía original sea incorrecta.** Una experiencia Bash/Linux puede no aplicar a PowerShell/Windows. Conservaríamos ambas variantes si cada una tiene evidencia y condiciones propias.

No se crea necesariamente una guía por ejecución. La deduplicación y el aporte de evidencia evitan crecimiento y costos innecesarios. Ante indisponibilidad del registro, el trabajo continúa; se propondrá una cola local acotada cuando sea posible. Si no puede capturarse, debe quedar explícito el hueco, sin prometer historial completo.

## Ejemplo narrado

1. En el harness A, el agente intenta localizar archivos con una utilidad no disponible.
2. Prueba una alternativa y verifica que encuentra los archivos esperados.
3. Se guardan eventos filtrados y una guía candidata: objetivo, condiciones, alternativa y evidencia.
4. Se publica el compromiso en fondo. Sólo se marca verificado después de comprobar la prueba confirmada.
5. En el harness B aparece una operación parecida. El filtro considera útil consultar.
6. La búsqueda devuelve una guía breve. El agente comprueba las condiciones actuales.
7. Si coinciden, usa el antecedente. Si no, explora normalmente. En ambos casos registra el resultado.
8. Una solución nueva genera una candidata o enriquece una existente.

No afirmamos que esa consulta resulte más barata que ejecutar un comando: ésa es la hipótesis a medir.

## Secuencia técnica de referencia

```mermaid
sequenceDiagram
    participant A as Harness A
    participant R as Registry local
    participant C as Blockchain
    participant B as Harness B
    A->>R: Eventos y evidencia
    R->>R: Filtrar, persistir y preparar candidata
    R->>C: Compromiso por lote en fondo
    C-->>R: Confirmación según política
    R->>R: Comprobar prueba y conservar estado
    B->>R: Consulta selectiva
    alt Guía compatible, vigente e íntegra
        R-->>B: Guía breve, condiciones y referencias
        B->>B: Comprobar condiciones y ejecutar
    else Sin guía utilizable o fuera de presupuesto
        R-->>B: Continuar sin recomendación
        B->>B: Resolver de forma habitual
    end
    B->>R: Intentos y resultado de cualquiera de las ramas
    R->>R: Evidencia adicional, candidata nueva o fallo sin resolver
```
