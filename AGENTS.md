# Protocolo para agentes: validar ANTES de hacer push

Objetivo: no generar fallos repetidos ni inundar de alertas de GitHub Actions.

1. Entender el pedido, el estado del repositorio, sus instrucciones y las pruebas/CI existentes.
2. Preparar cambios y revisar `git status --short`, `git diff --check`, `git diff`; descartar credenciales, datos personales y artefactos temporales.
3. Antes de cada commit/push ejecutar en un entorno local o aislado las pruebas relevantes del proyecto. Verificar sintaxis (Python, JS/TS, notebooks, HTML/JSON), test suite, build, rutas, enlaces y QA visual si la modificación afecta interfaces. Para notebooks comprobar estructura JSON y ejecución limpia cuando corresponda.
4. Ejecutar localmente los mismos controles de GitHub Actions que sean reproducibles sin secretos/servicios externos. Las simulaciones no son pruebas de integración. Para operaciones externas usar dry-run cuando exista.
5. Si algo falla o queda sin validar, **NO publicar como si estuviera verificado**. Leer el error, corregir y volver a probar antes de subir. Evitar pushes sucesivos de ensayo-error y no eliminar tests para forzar resultados verdes.
6. Publicar cambios agrupados y solo después de los controles; usar PR para cambios de riesgo. Tras publicar verificar checks y servicio/sitio. Si GitHub Actions falla, leer logs y reproducir localmente antes de otro push.

Informar siempre comandos realmente ejecutados, resultados, limitaciones y URL final. Las instrucciones específicas previas siguen vigentes cuando sean más estrictas.
