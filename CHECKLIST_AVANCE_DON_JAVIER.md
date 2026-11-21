# Checklist de avance: addon de inventario y distribución Don Javier

**Actualizado:** 21 de noviembre de 2026.

**Hora local registrada antes de publicar esta actualización del checklist:** 2026-11-21 10:52 UTC-03:00. No es la marca de tiempo exacta de envío ni de recepción del servidor.

**Fecha de una actualización anterior según GitHub:** 2026-11-21 04:26:13 UTC-03:00 (`2026-11-21 07:26:13 UTC`), commit [`c4c9ed4`](https://github.com/RAVS-TECH-MEDIA-SpA/aether-addon-inventory-management/commit/c4c9ed4b65248a31ce2b8e45e9c7a4fcd72337cf). Es la fecha de ese commit, no una confirmación independiente del instante exacto del push; puede diferir del reloj local. Las publicaciones posteriores pueden consultarse en el [historial de cambios](https://github.com/RAVS-TECH-MEDIA-SpA/aether-addon-inventory-management/commits/main/CHECKLIST_AVANCE_DON_JAVIER.md).

**Referencia:** [Informe ejecutivo](INFORME_ADDON_GESTION_INVENTARIO_DON_JAVIER.md).

**Estado general:** desarrollo en curso. La rama `feat/don-javier-demo` incluye hasta el commit `110e0de`: recuperación POS, seguimiento inicial de despachos, etiquetas y propuesta manual de carga, además de las etapas previas. Subir la rama no equivale a desplegar: no se ha desplegado el addon, creado una demo persistente ni hecho merge a `main`. No equivale a una solución lista para producción.

## Estimación global

**Avance estimado: alrededor de 55 %** del alcance integral acordado, no de preparación para producción. Es una valoración manual y aproximada, no una medición de esfuerzo restante ni una garantía de fecha. Incluye informe, web, app móvil para cinco roles, multiempresa y entrega; no incluye implementación tributaria legal ni nuevas funcionalidades de Meta.

Para dar continuidad a futuras actualizaciones se asignó a cada área un peso y un grado aproximado de 0 %, 25 %, 50 %, 75 % o 100 %. Se multiplican peso por grado y se suman los resultados. Un área parcialmente funcional no se considera terminada.

| Área | Peso | Grado estimado |
|---|---:|---:|
| 1. Tienda y preparación | 5 % | 0 % |
| 2. Inventario centralizado | 10 % | 75 % |
| 3. Inventario inicial | 5 % | 75 % |
| 4. Recepción y OCR | 10 % | 25 % |
| 5. Stock mínimo y reposición | 8 % | 75 % |
| 6. Traslados y despachos | 10 % | 75 % |
| 7. Punto de venta y códigos | 9 % | 50 % |
| 8. Productos padre/hijo | 5 % | 75 % |
| 9. Cuentas por cobrar | 8 % | 75 % |
| 10. Documentos ficticios | 3 % | 75 % |
| 11. Reportes y análisis | 8 % | 75 % |
| 12. Web, app y roles | 10 % | 25 % |
| 13. Multiempresa, planes y seguridad | 5 % | 50 % |
| 14. Preparación y entrega | 4 % | 0 % |

El cálculo ponderado es 54,75 %, redondeado a 55 %. El grado de traslados y despachos aumenta por el seguimiento inicial de conductor, QR de identificación y una propuesta manual de carga; no significa que el área esté terminada ni que el plan garantice seguridad. Se añadió además recuperación POS y una primera propuesta de etiquetas. Siguen pendientes funciones fundamentales, dispositivos reales y validación operacional. Los pesos y grados son criterios de seguimiento sujetos a revisión.

**Leyenda:** `[x]` implementado y probado en el alcance indicado, generalmente con datos temporales; `[ ]` pendiente o incompleto. Una casilla marcada no implica despliegue ni aceptación final.

## 1. Tienda y preparación

- [ ] Crear y activar una tienda persistente Don Javier con el addon y una suscripción elegible.
- [ ] Crear las tres bodegas y la sala de venta, con nombres y estructura confirmados.
- [ ] Crear usuarios de prueba para administración, vendedor, bodega, despacho y cliente.
- [ ] Cargar productos, códigos, precios, clientes y datos ficticios de prueba.
- [ ] Completar conteos físicos iniciales.
- [ ] Configurar marca, catálogo y dominio, y verificar la landing pública.

Existe una plantilla de storefront compartida y dinámica por tienda; crear un tenant no garantiza que DNS, hosting, dominio, marca y catálogo estén listos. No se han creado durante este trabajo una tienda, usuarios ni productos persistentes de Don Javier. Las pruebas usaron datos sintéticos temporales. Antes de crear datos o aplicar migraciones en un entorno compartido se requiere autorización.

## 2. Inventario centralizado

- [x] Crear ubicaciones de tipo bodega o sala.
- [x] Consultar existencias por producto y ubicación.
- [x] Registrar movimientos y consultar su historial.
- [x] Filtrar el inventario por producto y ubicación, y exportar el resultado a CSV.
- [x] Mostrar un gráfico local de registros filtrados por ubicación, sin sumar cantidades de productos distintos.
- [ ] Validar rendimiento y usabilidad con más de 500 productos y las ubicaciones reales.
- [ ] Completar actualización automática de todas las vistas de inventario.

Las consultas reflejan los datos al cargar o actualizar; no se ha verificado actualización integral en tiempo real.

## 3. Inventario inicial

- [x] Registrar conteo inicial por producto y ubicación.
- [x] Distinguir «sin conteo» de stock cero.
- [ ] Definir y completar el proceso de conteo físico, revisión y puesta en marcha de todas las ubicaciones.
- [x] Exigir conteo inicial en destino antes de recibir o trasladar; rechazar el traslado sin descontar origen.

Los saldos anteriores a este control pueden haberse creado sin conteo físico; deben revisarse durante la puesta en marcha.

## 4. Recepción de proveedores y OCR

- [x] Registrar manualmente una recepción y consultar el movimiento.
- [ ] Tomar o subir una fotografía de la guía.
- [ ] Procesar documentos privados mediante OCR con IA de GCP, con aislamiento entre tiendas.
- [ ] Revisar y corregir productos y cantidades antes de confirmar.
- [ ] Asociar la recepción completa al proveedor y documento, conservando auditoría.
- [ ] Probar el flujo completo y medir tiempos.

No se ha integrado OCR de distribución. Los documentos de prueba serán ficticios.

## 5. Stock mínimo y reposición

- [x] Configurar mínimos por producto y ubicación.
- [x] Mostrar faltantes calculados, stock en otras bodegas y alternativas de producto padre.
- [x] Exportar el reporte de mínimos y reposición a CSV.
- [x] Visualizar en el entorno local los mínimos al día, con faltante y sin conteo inicial.
- [x] Intentar notificar al personal autorizado cuando una venta, traslado o conversión cruza el mínimo hacia abajo.
- [ ] Cubrir cambios de mínimo y conteos iniciales según la política que se defina.
- [ ] Crear órdenes de reposición y recomendaciones de compra basadas en ventas y tendencias.
- [ ] Validar entrega push real en dispositivos y el comportamiento con usuarios desconectados.

La demo local reutiliza el mecanismo SSE existente, solo para clientes conectados; fuera de ella se usa push. La entrega es de mejor esfuerzo, sin bandeja persistente ni garantía de entrega.

## 6. Traslados y despachos

- [x] Registrar traslados internos atómicos entre ubicaciones, con responsable, fecha, producto, cantidad y referencia.
- [x] Descargar un comprobante ficticio del movimiento.
- [ ] Gestionar órdenes y estados de traslado, incluido tránsito.
- [x] Registrar pedidos B2B manuales y despachar el pedido completo desde una ubicación, con descuento transaccional y anulación auditada.
- [ ] Completar pedidos B2B con acceso de clientes, precios y despachos parciales.
- [x] Asignar un conductor activo y registrar estados de traslado y entrega declarada, con auditoría y aislamiento por tienda.
- [ ] Completar seguimiento del despacho y experiencia del conductor: reasignación, direcciones, rutas, confirmación del cliente y pruebas reales.
- [x] Preparar una propuesta manual de carga sin apilar, con medidas, capacidad y paradas indicadas por el usuario.
- [ ] Validar físicamente la propuesta: no controla ejes, sujeción, centro de gravedad ni compatibilidad de alimentos, y no garantiza seguridad.
- [x] Generar comprobante ficticio específico para despacho a clientes.

Ninguno de los comprobantes es una guía de despacho legal. Crear pedidos no reserva stock; el despacho no acredita entrega ni está conectado a cobranza. La entrega declarada por el conductor no prueba recepción ni pago. No hay reasignación de conductor: si se revoca o desactiva, el seguimiento queda bloqueado.

## 7. Punto de venta y códigos de barras

- [x] Asociar y consultar códigos de barras por tienda.
- [x] Buscar productos por nombre o código y agregarlos a una venta.
- [x] Registrar ventas de varias líneas y descontar stock de la sala transaccionalmente.
- [x] Validar precio, stock y permisos; consultar historial y descargar comprobante ficticio.
- [x] Reintentar una misma venta con identificador estable mientras se conserva en pantalla.
- [x] Conservar el identificador localmente y resolver el resultado incierto tras recarga o cierre en el mismo navegador y usuario.
- [ ] Registrar medios de pago, descuentos, devoluciones e impuestos.
- [ ] Implementar cierre de caja.
- [ ] Probar lector de códigos e impresora físicos.

Los precios existentes usan `Float`; el POS rechaza precios con más de dos decimales. Este flujo no configura moneda ni acredita pagos. Si se borra el almacenamiento del navegador o se cambia de dispositivo, no se recupera automáticamente el intento.

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
- [ ] Vincular créditos con pedidos o ventas y definir conciliación.
- [ ] Mantener o recuperar la clave de reintento de forma segura tras recarga o cierre.

El libro es manual y ficticio; no acredita pagos reales ni está conectado a POS o pedidos. Las deudas y pagos originales son inmutables; las anulaciones agregan eventos auditados. La zona comercial de distribución es independiente del país del comprador y puede cambiar qué deudas aparecen vencidas y a qué día pertenecen ventas históricas. La configuración implementada no configura la tienda general ni sus mercados internacionales. `America/Santiago` debe seleccionarse explícitamente: no se ha configurado una tienda persistente Don Javier.

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
- [ ] Ampliar el análisis histórico con pedidos B2B, estacionalidad y tendencias.
- [ ] Incorporar reportes completos de clientes, deudas y pagos que no dependan solo de páginas cargadas.
- [ ] Desarrollar proyecciones de reposición y compra, incluido el reporte semestral.
- [ ] Completar un panel ejecutivo integrado y actualizado para la operación diaria.

El reporte de ventas no es un cierre de caja ni una recomendación de compras. Sus fechas usan la zona comercial de distribución indicada en el reporte y CSV; cambiarla puede desplazar ventas históricas entre días, sin cambiar los instantes almacenados en UTC. La estimación extrapola solo ventas POS, no contempla pedidos B2B, stock, estacionalidad ni compras en tránsito; cero ventas no demuestra ausencia de demanda. Se pueden incluir productos actualmente activos sin ventas, no productos descontinuados sin ventas. Las cantidades de productos con distintas unidades no son directamente comparables. El CSV incluye todos los productos del alcance seleccionado, no solo los 10 del gráfico. Las equivalencias usan reglas actuales y son alternativas que no deben sumarse.

## 12. Web, app y roles

- [x] Inicio de sesión inicial para personal de distribución.
- [x] Base de permisos para administración, bodega, vendedor y despacho.
- [x] Panel web inicial adaptable con menús y acciones por rol, diferenciado de Mayro.
- [ ] Completar experiencias de administración, vendedor y bodega.
- [ ] Desarrollar portal y experiencia de cliente.
- [ ] Completar experiencia de despacho y conductor; existe una vista inicial para consultar asignaciones, leer QR y declarar estados.
- [ ] Terminar diseño propio de la web y landing de Don Javier.
- [ ] Crear una app móvil por tienda para los cinco roles y generar su APK.
- [ ] Probar los flujos de extremo a extremo en teléfonos y dispositivos reales.

Una pantalla responsive no equivale a una app móvil terminada. Los cinco roles previstos son cliente, vendedor, administrador, bodega y despacho.

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
- [x] Incluir las cinco migraciones de distribución en el commit y validarlas en orden sobre una línea base Prisma y PostgreSQL temporal aislado.
- [ ] Aplicar y verificar las migraciones en un entorno existente autorizado.
- [x] Hacer commit y push de los gráficos y exportaciones a la rama del addon; commit `5e62d07` confirmado en GitHub.
- [x] Hacer commit y push de la serie diaria, reportes paginados de cobranza y zona comercial de ventas; commit `35af531` confirmado en GitHub.
- [x] Publicar pedidos y despachos iniciales, anulaciones, controles de conteo y reportes en `938cc99`.
- [x] Publicar recuperación POS, seguimiento inicial, etiquetas y propuesta manual de carga en `110e0de`.
- [ ] Crear y validar la demo persistente con autorización.
- [ ] Probar teléfonos, conexión, lector, impresora y notificaciones push reales.
- [ ] Resolver el problema de estilos pendiente en la APK de Mayro y verificar sus cambios junto con los de distribución.
- [ ] Validar con Don Javier ubicaciones y eventual integración con su software actual.
- [ ] Planificar capacitación y medir las metas de precisión, tiempo, stock, cobranza y cierre.
- [ ] Revisar los cambios pendientes y completar la validación integral antes de hacer merge a `main`; no se hará merge hasta completar la tienda Don Javier.

La base subida se validó con 42 pruebas API y 55 pruebas web dirigidas. La etapa de pedidos, anulaciones y reportes pasó 34 pruebas API y 59 web dirigidas. La etapa actual pasó 22 pruebas API de inventario/POS, 9 de pedidos y seguimiento, 34 web de POS/panel y 39 web de seguimiento, etiquetas, carga y panel; se repitió además una prueba del planificador tras su último ajuste. Las diez migraciones de distribución se aplicaron en orden a PostgreSQL temporal aislado. Angular compiló para producción y `local-mobile`; la API pasó verificación de tipos. Persisten advertencias de CSS Mayro, `qrcode` y `ts-jest`; Jest requirió `--forceExit`. No se ha generado ni probado una APK con estos cambios.

## Decisiones y límites vigentes

- Distribución se activa individualmente por tienda y debe coexistir con otros addons desde PRO.
- Una app por tienda debe cubrir los cinco roles; la identidad visual de Don Javier debe ser distinta de Mayro.
- Los documentos y registros legales son ficticios por ahora, sin validez tributaria.
- Para cobranza y reportes de ventas de distribución, UTC es el valor inicial y la zona puede ajustarse por tienda; hay avisos diarios de mejor esfuerzo para la demo, no garantizados en producción. Las reglas IANA de Node y PostgreSQL deben mantenerse actualizadas y compatibles.
- La configuración o ampliación de Meta no forma parte de esta etapa y no se presume validada.
- La entrega SSE local no es una bandeja persistente ni garantiza recepción cuando el usuario está desconectado.
- La base de distribución se subió en `31be971`; la rama remota contiene también `b35a2d5`, los gráficos y CSV en `5e62d07`, los reportes diarios en `35af531`, la etapa de pedidos en `938cc99` y la etapa actual en `110e0de`. Las correcciones de Mayro deben verificarse aparte; no se han aplicado migraciones a bases existentes.

## Historial de actualización

| Fecha y hora | Avance |
|---|---|
| 2026-11-21, hora de publicación no registrada | Primera versión persistente: inventario y POS iniciales, avisos de mínimos, cobranza manual, resumen, configuración de zona comercial y equivalencias aproximadas. |
| 2026-11-21 04:23:23 UTC-03:00 (envío local); 04:26:13 UTC-03:00 (fecha del commit en GitHub) | Actualización del estado remoto y local, avisos de cobranza, validación de migraciones, gráficos y CSV; estimación aproximada de 44 %. |
| 2026-11-21 entre 04:27:35 y 04:27:43 UTC-03:00 (reloj local) | Push del commit `5e62d07` de gráficos y CSV a `feat/don-javier-demo`, confirmado en GitHub. El intervalo corresponde al inicio y fin observados del comando, no al instante exacto de recepción. No hubo despliegue ni merge. |
| 2026-11-21 entre 05:21:28 y 05:21:33 UTC-03:00 (reloj local) | Push del commit `35af531` de zona comercial, serie diaria y reportes paginados a `feat/don-javier-demo`, confirmado en GitHub. El intervalo corresponde al inicio y fin observados del comando, no al instante exacto de recepción. No hubo despliegue ni merge. |
| 2026-11-21 entre 07:43:15 y 07:43:20 UTC-03:00 (reloj local) | Push del commit `938cc99` de pedidos, anulaciones, conteos y reportes a `feat/don-javier-demo`, confirmado en GitHub. Estimación aproximada: 52 %. No hubo despliegue ni merge. |
| 2026-11-21 entre 10:52:18 y 10:52:25 UTC-03:00 (reloj local) | Push del commit `110e0de` de recuperación POS, seguimiento inicial, etiquetas y propuesta manual de carga a `feat/don-javier-demo`, confirmado en GitHub. Estimación aproximada: 55 %. No hubo despliegue ni merge. |
