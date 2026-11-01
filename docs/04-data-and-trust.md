# Datos, verificación y protección

## Unidades conceptuales

No es todavía un esquema de API o base de datos.

| Unidad | Campos conceptuales |
|---|---|
| Evento | Identidad de ejecución, procedencia, operación, herramienta, versión, resultado observable y contexto relevante |
| Experiencia | Referencias a intentos, error, alternativa, evidencia del resultado y condiciones |
| Guía | Recomendación breve, condiciones, referencias de evidencia, versión, autor y estado |
| Corrección | Referencia al original, motivo, autor y nueva declaración |
| Compromiso | Huella de contenido o raíz de lote, versión de formato y referencia a prueba |

Los timestamps capturados localmente son declaraciones del productor. El anclaje no certifica el instante exacto de ejecución.

## Dos dimensiones separadas

**Integridad:** pendiente, verificado, no coincide, no se pudo verificar.

**Utilidad/vigencia:** candidata, habilitada, cuestionada, reemplazada. Son estados propuestos; el criterio de habilitación sigue pendiente.

Una guía equivocada puede estar íntegramente verificada. Una guía útil pendiente de anclaje no se etiqueta verificada. Para el recorrido inicial proponemos recomendar automáticamente sólo guías habilitadas y verificadas; la política definitiva de candidatas requiere decisión.

## El verificador, en simple

Se calcula una huella del contenido conservado. Después se vuelve a calcular y se comprueba contra el compromiso confirmado. Si se agrupan eventos mediante un árbol Merkle, una prueba de inclusión conecta cada huella con la raíz publicada. Ese mecanismo concreto es candidato, no dependencia seleccionada.

- Coincidencia: el contenido corresponde al comprometido.
- Discrepancia: copia alterada o contenido/prueba equivocados; se descarta para recomendación.
- Falta de acceso: no demuestra alteración; se informa que no pudo verificarse.
- Original perdido: el hash no permite recuperarlo.

La definición exacta de serialización, hash, asociación entre guías y evidencia, y tratamiento de metadatos necesita especificación antes de implementar. No debemos permitir que representaciones equivalentes generen huellas ambiguas o que se sustituya la prueba de una versión por otra.

## Correcciones y actualizaciones

No se sobrescribe silenciosamente. Se agrega una corrección con autor y motivo. Un fallo real seguido de éxito es una secuencia, no una corrección del fallo.

Una guía cuestionada deja de recomendarse al conocerse su estado. Los dispositivos desconectados pueden conservar estados antiguos; el refresco al inicio y en fondo reduce pero no elimina la ventana. El borrado de contenido privado requiere política de retención; su compromiso público podría permanecer.

## Privacidad

1. Minimizar y filtrar antes de persistir y anclar. El filtrado no se asume perfecto: se debe probar con secretos sintéticos.
2. Reemplazar detalles privados por parámetros en guías reutilizables.
3. Cifrar eventos, guías, índices y respaldos persistidos. Gestión de claves pendiente.
4. No publicar prompts, comandos, rutas, guías ni nombres privados de proyectos onchain.
5. Revisar metadatos públicos y ataques de adivinación sobre contenidos predecibles; un hash no anonimiza. Aleatorización de compromisos y sus consecuencias quedan por diseñar.
6. Separar permisos de consulta y publicación. Contenido recuperado nunca amplía permisos.

## Publicación voluntaria posterior

El usuario selecciona una experiencia, revisa una versión minimizada y elige destinatarios. Se genera un compromiso propio de esa versión. El resumen es otro documento: su huella no demuestra fidelidad a los logs privados. Un vínculo al origen tampoco prueba por sí solo esa transformación. Memoria comunitaria, moderación y reputación quedan fuera del MVP.
