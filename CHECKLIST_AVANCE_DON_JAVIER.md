# Checklist de avance: addon de inventario y distribución Don Javier

**Actualizado:** 22 de noviembre de 2026.

**Hora local registrada antes de una actualización anterior del checklist:** 2026-11-21 10:52 UTC-03:00. No es la marca de tiempo exacta de envío ni de recepción del servidor.

**Fecha de una actualización anterior según GitHub:** 2026-11-21 04:26:13 UTC-03:00 (`2026-11-21 07:26:13 UTC`), commit [`c4c9ed4`](https://github.com/RAVS-TECH-MEDIA-SpA/aether-addon-inventory-management/commit/c4c9ed4b65248a31ce2b8e45e9c7a4fcd72337cf). Es la fecha de ese commit, no una confirmación independiente del instante exacto del push; puede diferir del reloj local. Las publicaciones posteriores pueden consultarse en el [historial de cambios](https://github.com/RAVS-TECH-MEDIA-SpA/aether-addon-inventory-management/commits/main/CHECKLIST_AVANCE_DON_JAVIER.md).

**Referencia:** [Informe ejecutivo](INFORME_ADDON_GESTION_INVENTARIO_DON_JAVIER.md).

**Estado general:** desarrollo en curso. La rama `feat/don-javier-demo` incluye hasta el commit `43343f5`, con datos ficticios aislados, perfil independiente, portal de cliente y despachos parciales experimentales deshabilitados por defecto. Subir la rama no equivale a desplegar: no se ha desplegado el addon, creado una demo persistente ni hecho merge a `main`. No equivale a una solución lista para producción.

**Punto de control `43343f5`:** en la demo, existencias y mínimos se vuelven a consultar aproximadamente cada 30 segundos mientras la pantalla está visible. Se conservan formularios y ventas pendientes, se descartan respuestas obsoletas o de una sesión cambiada y se informa si falla la consulta. Pasaron 32 pruebas web dirigidas. Las consultas son independientes, no reservan stock y pueden quedar desfasadas; POS, reportes y otras vistas no se actualizan automáticamente por este mecanismo. La estimación integral no cambia.

**Punto de control `c8ac936`:** la entrada local puede servir también la web compilada y configurar la API en el mismo origen; Chrome abrió la pantalla de acceso con cinco perfiles sin iniciar sesión. Al abrir un aviso de entrega se actualiza el portal si no hay una consulta o recepción en curso, que se conserva en caso contrario; los despachos completos muestran ahora el tránsito. Pasaron 19 pruebas dirigidas de configuración y entrega web, 25 web de portal y avisos, y 4 API de portal con 25 migraciones en PostgreSQL temporal. No se ha probado aún el flujo integral en navegador con esta entrada, ni teléfonos o Wi-Fi. HTTP local no cifra datos y puede impedir el acceso a la cámara; no es una configuración de producción. La estimación integral no cambia.

**Punto de control `c509612`:** la compilación local de Don Javier genera ahora `index.html`. Se agregó una entrada de API de demo separada que no arranca los servicios de otros addons, exige una base ficticia local y avisos locales, y mantiene deshabilitados OCR y documentos privados. Pasaron 15 pruebas de configuración y una comprobación de arranque temporal sin Redis, `ping` y protección de ruta; todavía no se probó el flujo de negocio con esa entrada. La comprobación de tipos completa de la API está bloqueada por cambios SaaS simultáneos ajenos; sí compiló el alcance dirigido de distribución. No hay servidor persistente ni prueba de teléfonos o Wi-Fi. El porcentaje integral no cambia por este punto de control anticipado.

**Avance publicado:** además de los flujos anteriores, hay un generador protegido de datos ficticios, acceso por cinco perfiles, landing local y cliente con solicitud y consulta de pedidos, consulta de saldos y declaración de recepción. El 22 de noviembre pasaron 30 pruebas web dirigidas, 7 pruebas API de demo y CORS y 48 pruebas API de regresión de pedidos e inventario; se aplicaron 22 migraciones de distribución en bases PostgreSQL temporales, se validaron ambos esquemas Prisma y tipos de API, compiló Angular `local-don-javier` y se validaron manifiestos y recursos Android sin generar APK. No se ejecutaron todas las pruebas del repositorio. El OCR y la custodia siguen deshabilitados y no se han probado en condiciones reales.

**Ampliación publicada en la rama:** precios y totales referenciales inmutables en pedidos de cliente y personal, con vista previa y detección de precios cambiados. Pasaron 23 pruebas web, 9 API de demo y CORS y 48 API de regresión, sobre bases temporales con 23 migraciones; compiló `local-don-javier`. La estimación ponderada sigue en 61 %: los despachos parciales y la entrega integral no están completos.

**Decisión para despachos parciales:** permitir anular únicamente las cantidades pendientes; los envíos ya realizados conservan su historial y no devuelven stock automáticamente. Seguimiento y recepción deben distinguir cada envío. Aún no está disponible para usuarios.

**Despachos parciales experimentales en la rama:** se agregaron tablas, servicios, rutas e interfaces para crear envíos parciales, descargar un comprobante ficticio por envío, anular solo el saldo, asignar y reasignar conductor, declarar cambio de custodia en tránsito, declarar entrega y declarar recepción por envío. La creación está deshabilitada por defecto y el indicador experimental se activó únicamente en pruebas; la ruta anterior bloquea operaciones incompatibles si existen envíos parciales. Con 24 migraciones en PostgreSQL temporal pasaron 29 pruebas de pedidos y 15 de reportes; la carrera entre cambio de custodia y entrega se serializa. Pasaron también 7 pruebas de demo que incluyen un recorrido por API entre cliente, bodega, administración y conductor, 68 pruebas web dirigidas y compiló `local-don-javier`; se validaron tipos y ambos esquemas Prisma. En `1fae154` no había avisos de cambio de conductor por envío; se agregaron posteriormente como se indica abajo. La custodia debe coordinarse físicamente. Faltan pruebas físicas y validación integral antes de habilitar el flujo. No se ha aplicado la migración en una base compartida.

**Punto de control publicado en `65e5ebb`:** cobranza manual por envío parcial, con selección por cliente, una deuda por envío incluso si se anula y validación de tienda y cliente. No se genera deuda desde la cotización. Pasaron 43 pruebas API de pedidos y cobranza, 7 API de demo y 41 pruebas web dirigidas; compiló `local-don-javier`. Se volvió a ejecutar la prueba dirigida con creación concurrente de claves distintas y restricciones de base. Las 25 migraciones se probaron en PostgreSQL temporal, no en una base compartida. También se agregó al POS una balanza virtual manual, total estimado del carrito y terminal de tarjeta visual simulado. Los envíos parciales guardan el intento local para reintentar tras recargar en el mismo navegador y usuario; la reasignación y cambio de custodia intentan avisar a ambos conductores con mensajes genéricos de mejor esfuerzo. Pasaron 30 pruebas web dirigidas de pedidos y POS, una prueba API de avisos locales y compiló `local-don-javier`. No se conectaron dispositivos ni se procesa pago alguno. Este punto de control anticipado no modifica la estimación del 61 %.

**Avance posterior local, sin publicar:** pasaron las 31 pruebas API de pedidos y envíos, incluidas concurrencia, aislamiento, cobranza y avisos, en PostgreSQL temporal con 25 migraciones. Se agregaron avisos genéricos de mejor esfuerzo al asignar y reasignar conductor, tanto en despachos completos como parciales; pasaron dos pruebas dirigidas de asignación, cambios, reintentos y aislamiento y se validaron tipos API. En la demo local los avisos se muestran dentro de la app conectada, no son push con la app cerrada; falta probarlos en teléfonos reales. Jest requirió `--forceExit`. Este avance aún no está publicado.

## Estimación global

**Avance estimado: alrededor de 61 %** del alcance integral acordado, no de preparación para producción. Es una valoración manual y aproximada, no una medición de esfuerzo restante ni una garantía de fecha. Incluye informe, web, app móvil para cinco roles, multiempresa y entrega; no incluye implementación tributaria legal ni nuevas funcionalidades de Meta.

Para dar continuidad a futuras actualizaciones se asignó a cada área un peso y un grado aproximado de 0 %, 25 %, 50 %, 75 % o 100 %. Se multiplican peso por grado y se suman los resultados. Un área parcialmente funcional no se considera terminada.

| Área | Peso | Grado estimado |
|---|---:|---:|
| 1. Tienda y preparación | 5 % | 25 % |
| 2. Inventario centralizado | 10 % | 75 % |
| 3. Inventario inicial | 5 % | 75 % |
| 4. Recepción y OCR | 10 % | 50 % |
| 5. Stock mínimo y reposición | 8 % | 75 % |
| 6. Traslados y despachos | 10 % | 75 % |
| 7. Punto de venta y códigos | 9 % | 50 % |
| 8. Productos padre/hijo | 5 % | 75 % |
| 9. Cuentas por cobrar | 8 % | 75 % |
| 10. Documentos ficticios | 3 % | 75 % |
| 11. Reportes y análisis | 8 % | 75 % |
| 12. Web, app y roles | 10 % | 50 % |
| 13. Multiempresa, planes y seguridad | 5 % | 50 % |
| 14. Preparación y entrega | 4 % | 0 % |

El cálculo ponderado registrado es 61 %, frente a 57,25 % anterior. Tienda y preparación pasa de 0 % a 25 % por el generador y las pruebas con datos temporales, no por una tienda persistente. Web, app y roles pasa de 25 % a 50 % por el perfil independiente y las funciones iniciales del cliente; la APK y la validación física siguen pendientes. Los pesos y grados son criterios manuales sujetos a revisión.

**Cómo interpretar el estancamiento:** cada grado cambia en bloques de 25 puntos por área, por lo que avances internos pueden no alterar la cifra global. Desde el cálculo anterior se agregaron cotizaciones referenciales, envíos parciales experimentales, cobranza por envío, balanza virtual, simulación de tarjeta y recuperación de envíos; todavía no corresponde dar por terminadas esas áreas. Para no esconder avances ni inventar precisión, el porcentaje conserva su método y los hitos y pruebas posteriores se informan por separado. El 61 % incluye preparación y entrega; no predice cuánto tiempo falta para la demo ni representa únicamente código.

**Leyenda:** `[x]` implementado y probado en el alcance indicado, generalmente con datos temporales; `[ ]` pendiente o incompleto. Una casilla marcada no implica despliegue ni aceptación final.

## 1. Tienda y preparación

- [ ] Crear y activar una tienda persistente Don Javier con el addon y una suscripción elegible.
- [ ] Crear las tres bodegas y la sala de venta, con nombres y estructura confirmados.
- [ ] Crear usuarios de prueba para administración, vendedor, bodega, despacho y cliente.
- [ ] Cargar productos, códigos, precios, clientes y datos ficticios de prueba.
- [ ] Completar conteos físicos iniciales.
- [ ] Configurar marca, catálogo y dominio, y verificar la landing pública.

Existe un generador para una base local aislada y vacía, probado con tienda, cuatro cuentas de personal, una de cliente, tres clientes, cuatro ubicaciones y 24 productos ficticios. No se han creado una tienda, usuarios ni productos persistentes de Don Javier. Las pruebas usaron datos temporales. La landing local no equivale a dominio o hosting público. Antes de crear datos o aplicar migraciones en un entorno compartido se requiere autorización.

## 2. Inventario centralizado

- [x] Crear ubicaciones de tipo bodega o sala.
- [x] Consultar existencias por producto y ubicación.
- [x] Registrar movimientos y consultar su historial.
- [x] Filtrar el inventario por producto y ubicación, y exportar el resultado a CSV.
- [x] Mostrar un gráfico local de registros filtrados por ubicación, sin sumar cantidades de productos distintos.
- [ ] Validar rendimiento y usabilidad con más de 500 productos y las ubicaciones reales.
- [ ] Completar actualización automática de todas las vistas de inventario; la demo consulta existencias y mínimos periódicamente mientras la pantalla está visible.

Las consultas reflejan los datos al cargar o actualizar; no se ha verificado actualización integral en tiempo real.

## 3. Inventario inicial

- [x] Registrar conteo inicial por producto y ubicación.
- [x] Distinguir «sin conteo» de stock cero.
- [ ] Definir y completar el proceso de conteo físico, revisión y puesta en marcha de todas las ubicaciones.
- [x] Exigir conteo inicial en destino antes de recibir o trasladar; rechazar el traslado sin descontar origen.

Los saldos anteriores a este control pueden haberse creado sin conteo físico; deben revisarse durante la puesta en marcha.

## 4. Recepción de proveedores y OCR

- [x] Registrar manualmente una recepción y consultar el movimiento.
- [x] Preparar localmente lectura asistida de fotografías mediante Vertex AI y revisión humana; validada con respuestas simuladas, deshabilitada por defecto.
- [x] Registrar localmente varias líneas revisadas en una recepción atómica, con historial de proveedor, documento y movimientos; validado con base temporal.
- [x] Detectar coincidencias textuales de proveedor y número de guía, exigiendo motivo auditado para otra recepción; no detecta variantes o errores de digitación.
- [x] Seleccionar localmente una fotografía y adjuntarla explícitamente a una recepción confirmada, con acceso restringido por tienda y rol; la custodia está deshabilitada por defecto.
- [x] Preparar eliminación auditada de los bytes de la fotografía por administración, con confirmación, clave idempotente y controles de base de datos; deshabilitada por defecto y probada localmente.
- [ ] Procesar documentos privados mediante OCR con IA de GCP, con aislamiento entre tiendas.
- [x] Revisar y corregir sugerencias y seleccionar manualmente productos y cantidades antes de confirmar, en el alcance local probado.
- [ ] Asociar la recepción completa al proveedor y documento, conservando auditoría.
- [ ] Probar el flujo completo y medir tiempos.

La lectura asistida no guarda la imagen ni registra stock por sí sola; la recepción se confirma aparte y adjuntar la fotografía es otro paso explícito. Requiere configuración y prueba autorizada en Google Cloud. La custodia guarda bytes en PostgreSQL sin cifrado adicional de aplicación. La eliminación auditada los quita del registro activo, pero no garantiza borrado físico inmediato ni los elimina de WAL, réplicas, respaldos o archivos descargados; conserva metadatos y SHA-256. No existe sustitución auditada ni análisis antivirus. Antes de habilitar la custodia o eliminación deben aprobarse cifrado, accesos, respaldos, capacidad y política integral de retención. Pasaron 10 pruebas API y 35 web con datos temporales y compilaron web y configuración móvil local; no se ha aplicado la nueva migración en entornos compartidos ni generado una APK. El control de duplicados compara texto y admite excepciones justificadas; no constituye todavía una recepción documental completa.

## 5. Stock mínimo y reposición

- [x] Configurar mínimos por producto y ubicación.
- [x] Mostrar faltantes calculados, stock en otras bodegas y alternativas de producto padre.
- [x] Exportar el reporte de mínimos y reposición a CSV.
- [x] Visualizar en el entorno local los mínimos al día, con faltante y sin conteo inicial.
- [x] Intentar notificar al personal autorizado cuando una venta, traslado o conversión cruza el mínimo hacia abajo.
- [x] Intentar avisos al registrar un conteo inicial bajo el mínimo o al crear/subir un mínimo que deje bajo un saldo conocido; se evita repetir avisos mientras sigue bajo.
- [ ] Crear órdenes de reposición y recomendaciones de compra basadas en ventas y tendencias.
- [ ] Validar entrega push real en dispositivos y el comportamiento con usuarios desconectados.

La demo local reutiliza el mecanismo SSE existente, solo para clientes conectados; fuera de ella se usa push. La entrega es de mejor esfuerzo, sin bandeja persistente ni garantía de entrega. Conteo inicial y mínimo se serializan para no perder la primera alerta si ocurren a la vez; pasaron 23 pruebas API de inventario y POS en PostgreSQL temporal. No se ha validado entrega física en dispositivos.

## 6. Traslados y despachos

- [x] Registrar traslados internos atómicos entre ubicaciones, con responsable, fecha, producto, cantidad y referencia.
- [x] Descargar un comprobante ficticio del movimiento.
- [ ] Gestionar órdenes y estados de traslado, incluido tránsito.
- [x] Registrar pedidos B2B manuales y despachar el pedido completo desde una ubicación, con descuento transaccional y anulación auditada.
- [x] Permitir solicitudes de pedidos por clientes autenticados y declaración de recepción tras la entrega declarada, probadas con datos temporales y aislamiento por tienda y cliente.
- [ ] Completar pedidos B2B con acceso de clientes, precios y despachos parciales.
- [x] Asignar un conductor activo y registrar estados de traslado y entrega declarada, con auditoría y aislamiento por tienda.
- [x] Reasignar un conductor antes del traslado, con motivo, auditoría y pérdida de acceso del conductor anterior; migración y concurrencia probadas en bases temporales.
- [x] Registrar localmente un cambio administrativo de conductor durante el tránsito, con motivo, revisión de asignación, confirmación declarada y acceso revocado al anterior; migración y concurrencia probadas en base temporal.
- [x] Intentar avisar a ambos conductores tras una transferencia, con mensaje genérico; SSE y navegación simulada probados localmente.
- [x] Intentar avisar al conductor al asignar y a ambos conductores al reasignar, en despachos completos y parciales; SSE probado con datos temporales.
- [x] Intentar avisar al cliente vinculado al iniciar tránsito o declarar entrega, en despachos completos y parciales; SSE, aislamiento, reintentos y navegación simulada probados localmente.
- [x] Registrar una dirección opcional al crear el pedido y mostrar la vigente al conductor asignado; conservar la original y permitir correcciones auditadas hasta declarar la entrega. Avisar si falta y rechazar inicio o entrega con revisión de dirección obsoleta.
- [x] Intentar avisar al conductor asignado al corregir una dirección, sin incluir datos privados en el aviso; probado con SSE local y navegación simulada de aviso local/push hacia despachos.
- [ ] Completar seguimiento del despacho y experiencia del conductor: entrega efectiva de avisos, verificación física de custodia, rutas, confirmación del cliente y pruebas reales.
- [x] Preparar una propuesta manual de carga sin apilar, con medidas, capacidad y paradas indicadas por el usuario.
- [x] Probar localmente alternativas de orden y giros autorizados cuando la primera propuesta de filas no cabe; conserva la separación por parada.
- [ ] Validar físicamente la propuesta: no controla ejes, sujeción, centro de gravedad ni compatibilidad de alimentos, y no garantiza seguridad.
- [x] Generar comprobante ficticio específico para despacho a clientes.

Ninguno de los comprobantes es una guía de despacho legal. Crear pedidos no reserva stock; el despacho no acredita entrega ni genera automáticamente una deuda. La entrega declarada por el conductor no prueba recepción ni pago. La corrección de dirección durante tránsito requiere comunicar el cambio directamente al conductor, pues el aviso es de mejor esfuerzo, sin confirmación ni garantía de entrega. La comparación de revisión en correcciones e inicio/entrega detecta incluso cambios que regresan al valor anterior; clientes antiguos deben actualizarse para pedidos corregidos. El aviso push no se ha probado en un dispositivo real. La transferencia en tránsito solo puede declararla administración, tras coordinar custodia fuera de la aplicación. No constituye prueba física; los avisos genéricos a ambos conductores son de mejor esfuerzo y no reemplazan la coordinación directa. Clientes antiguos deben actualizarse para registrar la entrega tras una transferencia. Pasaron 25 pruebas API de pedidos y seguimiento en PostgreSQL temporal y 5 web dirigidas de avisos; no se aplicó la migración en entornos compartidos ni se generó APK.

La ampliación de avisos se publicó en `7a64054`: pasó 32 pruebas API de pedidos y envíos en PostgreSQL temporal y 6 pruebas web de navegación SSE y push simulado; compiló `local-don-javier`. Los avisos al cliente no contienen identificadores ni dirección y no acreditan recepción ni pago. En ese punto el portal requería actualización manual; el comportamiento posterior se indica en `c8ac936`. Se probó que una falla de notificación no revierte el evento. No hay bandeja persistente ni validación de push en teléfonos. Esta publicación anticipada no cambia la estimación del 61 %.

**Punto de control `06011f5`:** al actualizar el portal se vuelve a consultar también la primera página de envíos del pedido abierto, sin perder una recepción de envío pendiente; una selección aún no enviada debe confirmarse de nuevo. El seguimiento de despachos completos y parciales permite reintentar con la misma clave si la respuesta demora más de 12 segundos, sin asumir que el servidor canceló la operación. La interfaz vincula las acciones de despacho completo a la tienda y usuario originales; la API comprueba ambas cabeceras cuando se envían y conserva compatibilidad con clientes anteriores que no las envíen. Pasaron 32 pruebas API en PostgreSQL temporal y 29 web dirigidas; compiló `local-don-javier`. Tras cerrar la pantalla debe revisarse el estado; no se recupera ese intento automáticamente.

**Validación integral local:** pasaron las 7 pruebas API de demo y 175 pruebas web de distribución, acceso y avisos. Además, el servidor HTTP real completó un recorrido ficticio con los cinco perfiles, recepción, POS, pedido, despacho, seguimiento, recepción declarada y cobranza manual usando PostgreSQL y Redis temporales propios. La prueba HTTP se ejecutó en un árbol compartido que incluía cambios simultáneos ajenos no incluidos en este punto de control. Con Redis inaccesible el recorrido HTTP también completó, pero el servidor general emitió errores y reintentos por servicios adicionales; posteriormente se creó la entrada independiente indicada arriba, cuyo flujo integral aún debe probarse. No se probó el navegador de extremo a extremo, teléfonos, Wi-Fi ni pagos reales. Este punto de control anticipado no cambia la estimación del 61 %.

La ampliación de la heurística de carga pasó 6 pruebas web de geometría, paradas, restricciones y componente. No garantiza una disposición segura ni reemplaza la revisión física y la sujeción.

## 7. Punto de venta y códigos de barras

- [x] Asociar y consultar códigos de barras por tienda.
- [x] Buscar productos por nombre o código y agregarlos a una venta.
- [x] Registrar ventas de varias líneas y descontar stock de la sala transaccionalmente.
- [x] Validar precio, stock y permisos; consultar historial y descargar comprobante ficticio.
- [x] Reintentar una misma venta con identificador estable mientras se conserva en pantalla.
- [x] Conservar el identificador localmente y resolver el resultado incierto tras recarga o cierre en el mismo navegador y usuario.
- [x] Mostrar el total estimado del carrito con cálculo decimal por línea; publicado en la rama.
- [x] Incorporar balanza virtual con peso ingresado manualmente; publicada en la rama.
- Balanza Bluetooth física: fuera del alcance actual; se evaluará si el cliente la solicita.
- [x] Incorporar una experiencia visual de tarjeta **simulada**, claramente rotulada como demo y sin datos reales de tarjetas; publicada en la rama.
- [ ] Registrar medios de pago, descuentos, devoluciones e impuestos.
- [ ] Implementar cierre de caja.
- [ ] Probar lector de códigos e impresora físicos.

Los precios existentes usan `Float`; el POS rechaza precios con más de dos decimales. Este flujo no configura moneda ni acredita pagos. El peso manual solo debe aplicarse a productos cuyo precio y stock se expresen por kg; no se verifica físicamente. El terminal simulado no registra pagos ni se conecta a un proveedor; la venta y descuento de stock ya se registraron antes de mostrarlo. Si se borra el almacenamiento del navegador o se cambia de dispositivo, no se recupera automáticamente el intento.

## 8. Productos padre/hijo

- [x] Configurar relación padre/hijo y factor de conversión.
- [x] Abrir unidades padre y generar unidades hijo transaccionalmente.
- [x] Guardar historial, responsable y referencia de la conversión.
- [x] Mostrar padres disponibles cuando falta un hijo con mínimo configurado.
- [x] Mostrar equivalencias aproximadas de ventas de hijos, en pantalla y CSV.
- [x] Comparar gráficamente en el entorno local alternativas padre para un hijo seleccionado.
- [ ] Registrar equivalencias históricas según la regla vigente en cada venta.
- [ ] Recomendar compras de sacos a partir de ventas históricas.

Las equivalencias actuales usan la regla configurada al consultar, no necesariamente la vigente cuando se vendió; los posibles padres son alternativas y no deben sumarse. No incluyen ventas del padre.

## 9. Cuentas por cobrar y créditos

- [x] Consultar clientes, deudas manuales ficticias, saldos y vencimientos por tienda.
- [x] Registrar pagos parciales o totales, sin permitir sobrepago; consultar historial.
- [x] Filtrar clientes morosos en el servidor antes de paginar.
- [x] Consultar resumen global de saldos, deudas y clientes vencidos.
- [x] Configurar un país opcional y una zona horaria comercial por tienda para cobranza y reportes de ventas de distribución; UTC es el valor inicial.
- [x] Intentar avisos diarios de cobranza en la demo local, con fecha comercial por tienda y deduplicación.
- [ ] Configurar un disparador externo seguro para producción y validar la entrega real de avisos.
- [x] Anular deudas sin pagos activos y pagos con motivo y auditoría, conservando el historial y recalculando saldos.
- [x] Vincular localmente una deuda manual ficticia a un pedido despachado del mismo cliente, evitando duplicar el vínculo y conservando el historial.
- [x] Vincular una deuda manual ficticia a un envío parcial del mismo cliente; publicado en la rama.
- [ ] Completar precios, vínculo con ventas, reemplazo de vínculos anulados y conciliación de créditos.
- [x] Recuperar localmente intentos inciertos de deudas, pagos y anulaciones tras recarga en el mismo navegador y usuario, con barrera para solicitudes tardías.

El libro es manual y ficticio; no acredita pagos reales ni está conectado a POS. El vínculo opcional a un pedido despachado no genera una deuda automáticamente ni valida precio, venta o entrega. Solo se permite una deuda vinculada por pedido, incluso si se anula: todavía no existe reemplazo vinculado. Las deudas manuales sin vínculo pueden duplicar una operación y requieren conciliación. Las deudas y pagos originales son inmutables; las anulaciones agregan eventos auditados. La zona comercial de distribución es independiente del país del comprador y puede cambiar qué deudas aparecen vencidas y a qué día pertenecen ventas históricas. La configuración implementada no configura la tienda general ni sus mercados internacionales. `America/Santiago` debe seleccionarse explícitamente: no se ha configurado una tienda persistente Don Javier.

El vínculo local se probó en PostgreSQL temporal con validación de cliente y tienda, despacho, restricciones de base, concurrencia y reintentos. El selector consulta pedidos disponibles por cliente en páginas y vuelve a comprobar la disponibilidad al guardar; las respuestas obsoletas se descartan. Pasaron 35 pruebas API de pedidos y cobranza, 23 pruebas API de pedidos y paginación en una segunda base y 24 web; se validaron ambos esquemas y compilaron web y configuración móvil local. La migración no se aplicó en entornos compartidos; no se generó APK.

La recuperación local conserva solo identificadores por tienda y usuario; si se borra el almacenamiento, se cambia de dispositivo o se opera simultáneamente con claves distintas en varias pestañas o dispositivos, no garantiza evitar duplicados. Los clientes anteriores sin cabeceras de identidad no incorporan esta protección de interfaz. La configuración comercial descarta respuestas de una identidad anterior y comprueba la identidad indicada al guardar. Pasaron 13 pruebas API de cobranza en PostgreSQL temporal, una prueba API dirigida de configuración y 22 web dirigidas; compilaron web y `local-mobile`. La migración correspondiente está publicada en la rama, pero no se aplicó en un entorno compartido.

Los avisos se intentan desde las 09:00 de la zona comercial cuando hay saldo vencido y destinatarios autorizados. En la demo local se usa SSE para usuarios conectados. La entrega es de mejor esfuerzo: no hay bandeja persistente ni reintento garantizado; el temporizador interno no garantiza ejecución en Cloud Run.

## 10. Documentos ficticios

- [x] Comprobante ficticio de venta con productos, cantidades y valores.
- [x] Comprobante ficticio de movimiento de inventario.
- [x] Identificación de los comprobantes como sin validez tributaria.
- [x] Comprobante ficticio específico de despacho a cliente, sin acreditar entrega.
- [x] Preparar etiquetas monocromáticas de 1 kg y ½ kg y de despacho, con formato y cantidad seleccionables.
- [x] Identificar el despacho mediante QR y consultar solo el asignado al conductor autenticado.
- [ ] Impresión y pruebas con impresora física.
- [ ] Emisión tributaria legal: fuera del alcance actual y pendiente de definición de proveedor.

Las etiquetas de envasado se imprimen desde el navegador y no contienen lote, vencimiento ni otros datos reglamentarios. Su QR no registra inventario ni funciona como código de venta. El QR de despacho no contiene datos del cliente ni credenciales y solo identifica el pedido; escanearlo no acredita entrega. Es indispensable probar tamaños, lectura y calidad en la impresora, papel y cámara reales. La cantidad de etiquetas se elige manualmente según necesidad; no se ha supuesto un número por bodega.

## 11. Reportes y análisis

- [x] Consultar stock, mínimos, movimientos, conversiones e historial de ventas.
- [x] Consultar ventas por producto y período, con CSV y fechas inclusivas en la zona comercial configurada; UTC es el valor inicial.
- [x] Consultar ventas diarias con gráfico por bloques y CSV, incluyendo días sin ventas y aplicando cambios de hora de la zona seleccionada.
- [x] Comparar localmente ventas e importe POS con el período completo inmediatamente anterior de igual duración y exportar la diferencia absoluta a CSV.
- [x] Consultar equivalencias padre/hijo aproximadas usando las reglas actuales.
- [x] Consultar un resumen manual de cobranza de toda la tienda.
- [x] Ordenar productos vendidos por cantidad y comparar gráficamente hasta 10 por cantidad, importe o número de ventas, incluyendo mayores o menores.
- [x] Mostrar gráficos y CSV para ventas, existencias filtradas, mínimos y resumen de cobranza; los vencidos son parte del total, no un importe adicional.
- [x] Mostrar gráficos y exportar a CSV movimientos cargados y hasta las últimas 50 conversiones, indicando el alcance parcial.
- [x] Mostrar gráficos y CSV para las páginas cargadas de clientes, deudas y pagos, indicando si faltan páginas y que no son una instantánea completa.
- [x] Compilar las visualizaciones adaptables para web y configuración móvil local y subir el commit de los gráficos a la rama del addon.
- [ ] Implementar cierre diario automático.
- [x] Incluir opcionalmente productos actualmente activos sin ventas y seleccionar semestres calendario.
- [x] Estimar demanda POS mediante promedio diario para un horizonte elegido y exportar CSV.
- [x] Contrastar opcionalmente la demanda POS con el stock registrado en todas las ubicaciones activas, indicando una brecha orientativa solo cuando la cobertura esté completa; probado localmente.
- [x] Incluir opcionalmente cantidades históricas despachadas B2B separadas de ventas POS y sumarlas para una extrapolación orientativa, con desglose en CSV; probado localmente.
- [x] Consultar opcionalmente pedidos B2B actualmente pendientes y sumarlos a la brecha orientativa cuando hay cobertura completa de stock; probado localmente, sin reservar existencias.
- [ ] Ampliar el análisis histórico con pedidos B2B, estacionalidad y tendencias.
- [x] Exportar clientes del filtro en una consulta de saldos, hasta 10000 registros, sin generar archivos parciales al superar el límite; probado localmente con datos sintéticos.
- [x] Consultar y exportar deudas por cliente y pagos por deuda, hasta 10000 registros por reporte, sin generar archivos parciales al superar el límite; probado localmente con datos sintéticos.
- [ ] Desarrollar proyecciones de reposición y compra, incluido el reporte semestral.
- [ ] Completar un panel ejecutivo integrado y actualizado para la operación diaria.

El reporte de ventas no es un cierre de caja ni una recomendación de compras. Sus fechas usan la zona comercial de distribución indicada en el reporte y CSV; cambiarla puede desplazar ventas históricas entre días, sin cambiar los instantes almacenados en UTC. La estimación usa ventas POS y, solo si se solicita, cantidades B2B despachadas; no extrapola pedidos pendientes ni contempla estacionalidad o compras en tránsito. Opcionalmente muestra pedidos pendientes actuales, sin filtrar por el período histórico, y los suma a la brecha de stock; pueden solaparse con la demanda estimada y exagerar la necesidad. No reservan stock ni se garantiza que lleguen a despacharse. Despachar no acredita venta, entrega ni pago y los canales no están conciliados, por lo que un registro duplicado puede contarse dos veces. Cero ventas no demuestra ausencia de demanda. Se pueden incluir productos actualmente activos sin ventas, y productos inactivos si fueron vendidos, despachados o están pendientes según las opciones seleccionadas. Las cantidades de productos con distintas unidades no son directamente comparables. El CSV incluye todos los productos del alcance seleccionado, no solo los 10 del gráfico. Las equivalencias usan reglas actuales y son alternativas que no deben sumarse.

La comparación de períodos cubre solo POS y exige que el período consultado esté completo y ambas respuestas indiquen la misma zona comercial. Las consultas son independientes; los datos pueden cambiar entre ellas. No ajusta estacionalidad ni predice demanda. Pasaron 18 pruebas web dirigidas, incluido el CSV, años bisiestos y el descarte de respuestas obsoletas; compilaron web y configuración móvil local. No se generó APK.

La estimación local exige que el período termine antes del día comercial actual informado por el servidor, para no promediar días futuros o parciales. También presenta padres enteros equivalentes para cada alternativa vigente, redondeados hacia arriba, sin descontar existencias ni incluir ventas del padre o pendientes: no es una cantidad a comprar. Opcionalmente contrasta demanda y pendientes consultados con stock actual registrado y muestra una brecha solo cuando hay saldos no negativos en todas las ubicaciones activas; no descuenta stock de padres, reservas ni compras entrantes y el stock puede cambiar tras la consulta. La existencia de un saldo no prueba un conteo físico. Los despachos y pendientes se probaron con 14 pruebas API y 16 web dirigidas, incluyendo aislamiento y fechas comerciales; los datos son sintéticos. Pasó la comprobación de tipos API y compilaron web y configuración móvil local; no se generó una APK.

El reporte local de clientes de cobranza usa una consulta por filtro, hasta 10000 filas, y rechaza resultados más grandes sin exportación parcial. Pasaron 11 pruebas API y 45 web dirigidas, incluido el límite con datos sintéticos; no se ha validado rendimiento con datos reales.

Los nuevos reportes locales de deudas y pagos utilizan una consulta por reporte, incluyen anulaciones y descartan respuestas cuando cambia la identidad o la selección. Pasaron 12 pruebas API y 18 web dirigidas, incluidos los límites de 10000 y 10001 filas; también compilaron web y `local-mobile`. No son cierres contables ni se ha probado su rendimiento con datos reales.

## 12. Web, app y roles

- [x] Inicio de sesión inicial para personal de distribución.
- [x] Base de permisos para administración, bodega, vendedor y despacho.
- [x] Panel web inicial adaptable con menús y acciones por rol, diferenciado de Mayro.
- [ ] Completar experiencias de administración, vendedor y bodega.
- [x] Permitir al cliente autenticado consultar sus pedidos y estados declarados, con aislamiento por tienda y cliente; probado con datos sintéticos.
- [x] Permitir al cliente solicitar pedidos, consultar saldos y declarar recepción tras la entrega declarada, con pruebas locales.
- [ ] Completar la experiencia de cliente, incluidos precios confirmados y validación en dispositivos reales.
- [ ] Completar experiencia de despacho y conductor; existe una vista inicial para consultar asignaciones, leer QR y declarar estados.
- [ ] Terminar diseño propio de la web y landing de Don Javier.
- [ ] Crear una app móvil por tienda para los cinco roles y generar su APK.
- [ ] Probar los flujos de extremo a extremo en teléfonos y dispositivos reales.

El pedido no reserva stock ni fija precios: los valores del catálogo son referenciales. La recepción es una declaración del cliente; no comprueba automáticamente el contenido ni acredita pago. La interfaz guarda el intento de pedido en el navegador para reintentos, pero cambiar de navegador o borrar sus datos pierde esa recuperación. Una pantalla responsive no equivale a una app móvil terminada. Los cinco roles previstos son cliente, vendedor, administrador, bodega y despacho.

## 13. Multiempresa, planes y seguridad

- [x] Registrar el addon de distribución independiente de Mayro, con precio cero y mínimo PRO; disponible también para ELITE.
- [x] Controlar acceso por tienda, addon y rol en los flujos implementados.
- [x] Ejecutar pruebas sintéticas de aislamiento entre tiendas y coexistencia con Mayro.
- [ ] Validar la creación real de tienda, suscripción y activación individual del addon.
- [ ] Probar integralmente Meraki, Mayro, Don Javier y múltiples tiendas en un entorno autorizado.
- [ ] Revisar seguridad, auditoría y rendimiento de los flujos pendientes.
- [ ] Validar los mecanismos reales de notificación y aislamiento en producción.

Los addons deben ser independientes entre sí. Las pruebas aisladas todavía no sustituyen una validación integral de todos los addons y tiendas.

## 14. Preparación y entrega

- [x] Compilar Angular para producción y ejecutar pruebas dirigidas de API e interfaz en el alcance implementado.
- [x] Mantener sincronizados los modelos Prisma de API y workers y validar sus esquemas.
- [x] Incluir las 22 migraciones de distribución y validarlas en orden sobre una línea base Prisma y PostgreSQL temporal aislado.
- [ ] Aplicar y verificar las migraciones en un entorno existente autorizado.
- [x] Hacer commit y push de los gráficos y exportaciones a la rama del addon; commit `5e62d07` confirmado en GitHub.
- [x] Hacer commit y push de la serie diaria, reportes paginados de cobranza y zona comercial de ventas; commit `35af531` confirmado en GitHub.
- [x] Publicar pedidos y despachos iniciales, anulaciones, controles de conteo y reportes en `938cc99`.
- [x] Publicar recuperación POS, seguimiento inicial, etiquetas y propuesta manual de carga en `110e0de`.
- [x] Publicar recepción asistida, ajustes de despacho y cobranza, reportes y consulta inicial de pedidos del cliente en `86a79a4`.
- [x] Publicar perfil y datos ficticios de Don Javier, landing local y portal ampliado del cliente en `3ac7057`.
- [ ] Crear y validar la demo persistente con autorización.
- [ ] Probar teléfonos, conexión, lector, impresora y notificaciones push reales.
- [ ] Resolver el problema de estilos pendiente en la APK de Mayro y verificar sus cambios junto con los de distribución.
- [ ] Validar con Don Javier ubicaciones y eventual integración con su software actual.
- [ ] Planificar capacitación y medir las metas de precisión, tiempo, stock, cobranza y cierre.
- [ ] Revisar los cambios pendientes y completar la validación integral antes de hacer merge a `main`; no se hará merge hasta completar la tienda Don Javier.

La base subida se validó con 42 pruebas API y 55 pruebas web dirigidas. La etapa de pedidos, anulaciones y reportes pasó 34 pruebas API y 59 web dirigidas. La etapa de seguimiento inicial pasó 22 pruebas API de inventario/POS, 9 de pedidos y seguimiento, 34 web de POS/panel y 39 web de seguimiento, etiquetas, carga y panel; se repitió además una prueba del planificador tras su último ajuste. Posteriormente se validaron las 20 migraciones en PostgreSQL temporal aislado. Angular compiló para producción y `local-mobile`; la API pasó verificación de tipos. Persisten advertencias de CSS Mayro, `qrcode` y `ts-jest`; Jest requirió `--forceExit`. No se ha generado ni probado una APK con estos cambios.

### Activaciones y verificaciones antes de producción

Pendientes para cuando exista autorización y se restablezca el acceso y la facturación de GCP. Saldar la deuda no implica que los servicios se reactiven automáticamente ni que el sistema quede listo para operar.

- [ ] Verificar el estado real de facturación, proyecto, servicios, cuotas y presupuesto en GCP; revisar costos y alertas antes de habilitar consumo.
- [ ] Definir entorno de producción, dominio, TLS, credenciales y permisos mínimos; preparar copias, restauración, monitoreo y un procedimiento de despliegue y reversión. No usar la base ficticia local como producción.
- [ ] Aprobar y aplicar migraciones en el entorno autorizado, validar aislamiento multiempresa y preparar tienda, usuarios y conteos reales sin afectar Mayro.
- [ ] OCR de guías: revisar privacidad, región, modelo, costos, cuotas e IAM de Vertex AI; configurar las variables requeridas y probar con documentos reales autorizados antes de activar `DISTRIBUTION_OCR_ENABLED`. El OCR actual solo se ha probado con respuestas simuladas.
- [ ] Notificaciones push: configurar y autorizar Firebase/FCM, credenciales y registros de dispositivos; probar permisos y entrega en teléfonos reales. Los avisos SSE de la demo funcionan solo con la app conectada y no son un reemplazo de push ni una bandeja persistente.
- [ ] Avisos programados de cobranza: diseñar y configurar un disparador externo seguro para el entorno de despliegue y validar ejecución y entrega; el temporizador interno puede suspenderse y no garantiza avisos.
- [ ] Custodia y eliminación de fotografías: aprobar cifrado, acceso, retención, respaldos, borrado y controles de archivos antes de habilitar sus flags; las imágenes se almacenan en PostgreSQL, sin cifrado adicional de aplicación.
- [ ] Mantener envíos parciales deshabilitados hasta validar integralmente sus flujos y dispositivos; habilitar solo con autorización. No asumir que una bandera por sí sola los hace aptos para producción.
- [ ] Confirmar requisitos de medios de pago y documentos tributarios con el cliente y proveedor antes de implementar o activar cualquier integración real. El terminal actual es exclusivamente simulado y los comprobantes no tienen validez tributaria.

## Decisiones y límites vigentes

- Distribución se activa individualmente por tienda y debe coexistir con otros addons desde PRO.
- Una app por tienda debe cubrir los cinco roles; la identidad visual de Don Javier debe ser distinta de Mayro.
- Los documentos y registros legales son ficticios por ahora, sin validez tributaria.
- Para cobranza y reportes de ventas de distribución, UTC es el valor inicial y la zona puede ajustarse por tienda; hay avisos diarios de mejor esfuerzo para la demo, no garantizados en producción. Las reglas IANA de Node y PostgreSQL deben mantenerse actualizadas y compatibles.
- La configuración o ampliación de Meta no forma parte de esta etapa y no se presume validada.
- La entrega SSE local no es una bandeja persistente ni garantiza recepción cuando el usuario está desconectado.
- La base de distribución se subió en `31be971`; la rama remota contiene también `b35a2d5`, los gráficos y CSV en `5e62d07`, los reportes diarios en `35af531`, la etapa de pedidos en `938cc99`, el seguimiento inicial en `110e0de`, la recepción asistida en `86a79a4` y la etapa actual en `3ac7057`. Las correcciones de Mayro deben verificarse aparte; no se han aplicado migraciones a bases existentes.

## Historial de actualización

| Fecha y hora | Avance |
|---|---|
| 2026-11-21, hora de publicación no registrada | Primera versión persistente: inventario y POS iniciales, avisos de mínimos, cobranza manual, resumen, configuración de zona comercial y equivalencias aproximadas. |
| 2026-11-21 04:23:23 UTC-03:00 (envío local); 04:26:13 UTC-03:00 (fecha del commit en GitHub) | Actualización del estado remoto y local, avisos de cobranza, validación de migraciones, gráficos y CSV; estimación aproximada de 44 %. |
| 2026-11-21 entre 04:27:35 y 04:27:43 UTC-03:00 (reloj local) | Push del commit `5e62d07` de gráficos y CSV a `feat/don-javier-demo`, confirmado en GitHub. El intervalo corresponde al inicio y fin observados del comando, no al instante exacto de recepción. No hubo despliegue ni merge. |
| 2026-11-21 entre 05:21:28 y 05:21:33 UTC-03:00 (reloj local) | Push del commit `35af531` de zona comercial, serie diaria y reportes paginados a `feat/don-javier-demo`, confirmado en GitHub. El intervalo corresponde al inicio y fin observados del comando, no al instante exacto de recepción. No hubo despliegue ni merge. |
| 2026-11-21 entre 07:43:15 y 07:43:20 UTC-03:00 (reloj local) | Push del commit `938cc99` de pedidos, anulaciones, conteos y reportes a `feat/don-javier-demo`, confirmado en GitHub. Estimación aproximada: 52 %. No hubo despliegue ni merge. |
| 2026-11-21 entre 10:52:18 y 10:52:25 UTC-03:00 (reloj local) | Push del commit `110e0de` de recuperación POS, seguimiento inicial, etiquetas y propuesta manual de carga a `feat/don-javier-demo`, confirmado en GitHub. Estimación aproximada: 55 %. No hubo despliegue ni merge. |
| 2026-11-22 entre 17:51:21 y 17:51:25 UTC-03:00 (reloj local) | Push del commit `86a79a4` a `feat/don-javier-demo`, confirmado en GitHub. Estimación ponderada registrada: aproximadamente 57 %. El intervalo corresponde al inicio y fin observados del comando, no al instante exacto de recepción. No hubo despliegue ni merge. |
| 2026-11-22 entre 17:52:29 y 17:52:31 UTC-03:00 (reloj local) | Publicación del checklist en `382b055`. El intervalo corresponde al inicio y fin observados del comando, no al instante exacto de recepción. La fecha del commit de esta anotación puede consultarse en el historial de GitHub. |
| 2026-11-22, verificado a las 19:17:35 UTC-03:00 (reloj local) | Commit `3ac7057` confirmado en la rama remota. Estimación ponderada aproximada: 61 %. No hubo despliegue, merge ni generación de APK. |
