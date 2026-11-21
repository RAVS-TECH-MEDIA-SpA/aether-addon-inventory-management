# Checklist de avance: addon de inventario y distribución Don Javier

**Actualizado:** 21 de noviembre de 2026.

**Hora de envío de la actualización anterior del checklist a GitHub:** 2026-11-21 04:23:23 UTC-03:00. Hora local registrada inmediatamente antes de iniciar la publicación; no es la marca de tiempo exacta de recepción del servidor.

**Fecha del commit de la actualización de avances según GitHub:** 2026-11-21 04:26:13 UTC-03:00 (`2026-11-21 07:26:13 UTC`), commit [`c4c9ed4`](https://github.com/RAVS-TECH-MEDIA-SpA/aether-addon-inventory-management/commit/c4c9ed4b65248a31ce2b8e45e9c7a4fcd72337cf). Es la fecha del commit registrada por GitHub, no una confirmación independiente del instante exacto del push; puede diferir del reloj local. Las publicaciones posteriores pueden consultarse en el [historial de cambios](https://github.com/RAVS-TECH-MEDIA-SpA/aether-addon-inventory-management/commits/main/CHECKLIST_AVANCE_DON_JAVIER.md).

**Referencia:** [Informe ejecutivo](INFORME_ADDON_GESTION_INVENTARIO_DON_JAVIER.md).

**Estado general:** desarrollo en curso. La base del addon, gráficos y exportaciones están subidos a `feat/don-javier-demo`, incluido el commit `5e62d07`. Subir la rama no equivale a desplegar: no se ha desplegado el addon, creado una demo persistente ni hecho merge a `main`. No equivale a una solución lista para producción.

## Estimación global

**Avance estimado: alrededor de 44 %** del alcance integral acordado, no de preparación para producción. Es una valoración manual y aproximada, no una medición de esfuerzo restante ni una garantía de fecha. Incluye informe, web, app móvil para cinco roles, multiempresa y entrega; no incluye implementación tributaria legal ni nuevas funcionalidades de Meta.

Para dar continuidad a futuras actualizaciones se asignó a cada área un peso y un grado aproximado de 0 %, 25 %, 50 %, 75 % o 100 %. Se multiplican peso por grado y se suman los resultados. Un área parcialmente funcional no se considera terminada.

| Área | Peso | Grado estimado |
|---|---:|---:|
| 1. Tienda y preparación | 5 % | 0 % |
| 2. Inventario centralizado | 10 % | 75 % |
| 3. Inventario inicial | 5 % | 50 % |
| 4. Recepción y OCR | 10 % | 25 % |
| 5. Stock mínimo y reposición | 8 % | 75 % |
| 6. Traslados y despachos | 10 % | 25 % |
| 7. Punto de venta y códigos | 9 % | 50 % |
| 8. Productos padre/hijo | 5 % | 75 % |
| 9. Cuentas por cobrar | 8 % | 50 % |
| 10. Documentos ficticios | 3 % | 50 % |
| 11. Reportes y análisis | 8 % | 50 % |
| 12. Web, app y roles | 10 % | 25 % |
| 13. Multiempresa, planes y seguridad | 5 % | 50 % |
| 14. Preparación y entrega | 4 % | 0 % |

El cálculo ponderado es 43,75 %, redondeado a 44 %. El cambio respecto de 42 % refleja los gráficos y exportaciones incorporados al área de reportes, no una medición automática. Los pesos y grados son criterios de seguimiento sujetos a revisión.

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
- [ ] Resolver la recepción manual que puede crear stock sin un conteo previo explícito.

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
- [ ] Gestionar pedidos y despachos a clientes B2B.
- [ ] Desarrollar seguimiento del despacho y experiencia del conductor.
- [ ] Generar documentos ficticios específicos para despacho a clientes.

El comprobante de movimiento no es una guía de despacho legal.

## 7. Punto de venta y códigos de barras

- [x] Asociar y consultar códigos de barras por tienda.
- [x] Buscar productos por nombre o código y agregarlos a una venta.
- [x] Registrar ventas de varias líneas y descontar stock de la sala transaccionalmente.
- [x] Validar precio, stock y permisos; consultar historial y descargar comprobante ficticio.
- [x] Reintentar una misma venta con identificador estable mientras se conserva en pantalla.
- [ ] Mantener o recuperar de forma segura el identificador de reintento tras recarga o cierre.
- [ ] Registrar medios de pago, descuentos, devoluciones e impuestos.
- [ ] Implementar cierre de caja.
- [ ] Probar lector de códigos e impresora físicos.

Los precios existentes usan `Float`; el POS rechaza precios con más de dos decimales. Este flujo no configura moneda ni acredita pagos.

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
- [x] Configurar para cobranza un país opcional y una zona horaria por tienda; UTC es el valor inicial.
- [x] Intentar avisos diarios de cobranza en la demo local, con fecha comercial por tienda y deduplicación.
- [ ] Configurar un disparador externo seguro para producción y validar la entrega real de avisos.
- [ ] Diseñar correcciones o anulaciones auditadas para errores de captura.
- [ ] Vincular créditos con pedidos o ventas y definir conciliación.
- [ ] Mantener o recuperar la clave de reintento de forma segura tras recarga o cierre.

El libro es manual y ficticio; no acredita pagos reales ni está conectado a POS o pedidos. Las deudas y pagos son inmutables y todavía no existe procedimiento de corrección. La zona de cobranza es independiente del país del comprador y puede cambiar qué deudas aparecen vencidas. La configuración implementada no configura la tienda general ni sus mercados internacionales.

Los avisos se intentan desde las 09:00 de la zona comercial cuando hay saldo vencido y destinatarios autorizados. En la demo local se usa SSE para usuarios conectados. La entrega es de mejor esfuerzo: no hay bandeja persistente ni reintento garantizado; el temporizador interno no garantiza ejecución en Cloud Run.

## 10. Documentos ficticios

- [x] Comprobante ficticio de venta con productos, cantidades y valores.
- [x] Comprobante ficticio de movimiento de inventario.
- [x] Identificación de los comprobantes como sin validez tributaria.
- [ ] Comprobante ficticio específico de despacho a cliente.
- [ ] Impresión y pruebas con impresora física.
- [ ] Emisión tributaria legal: fuera del alcance actual y pendiente de definición de proveedor.

## 11. Reportes y análisis

- [x] Consultar stock, mínimos, movimientos, conversiones e historial de ventas.
- [x] Consultar ventas por producto y período, con CSV y fechas inclusivas UTC.
- [x] Consultar equivalencias padre/hijo aproximadas usando las reglas actuales.
- [x] Consultar un resumen manual de cobranza de toda la tienda.
- [x] Ordenar productos vendidos por cantidad y comparar gráficamente hasta 10 por cantidad, importe o número de ventas, incluyendo mayores o menores.
- [x] Mostrar gráficos y CSV para ventas, existencias filtradas, mínimos y resumen de cobranza; los vencidos son parte del total, no un importe adicional.
- [x] Mostrar gráficos y exportar a CSV movimientos cargados y hasta las últimas 50 conversiones, indicando el alcance parcial.
- [x] Compilar las visualizaciones adaptables para web y configuración móvil local y subir el commit de los gráficos a la rama del addon.
- [ ] Implementar cierre diario automático y calendario comercial para ventas.
- [ ] Incluir productos sin ventas, análisis histórico de tendencias y gráficos temporales.
- [ ] Exportar y visualizar individualmente los listados paginados de clientes, deudas y pagos.
- [ ] Desarrollar proyecciones de reposición y compra, incluido el reporte semestral.
- [ ] Completar un panel ejecutivo integrado y actualizado para la operación diaria.

El reporte de ventas no es un cierre de caja ni una proyección de compras. Su período aún se interpreta en UTC, independientemente de la zona de cobranza. Los gráficos de productos solo incluyen los que tuvieron ventas; las cantidades de productos con distintas unidades no son directamente comparables. Los valores se muestran de forma exacta y las barras o porcentajes son representaciones relativas aproximadas. El CSV de ventas incluye todos los productos vendidos, no solo los 10 del gráfico. Las equivalencias usan reglas actuales y son alternativas que no deben sumarse.

## 12. Web, app y roles

- [x] Inicio de sesión inicial para personal de distribución.
- [x] Base de permisos para administración, bodega, vendedor y despacho.
- [x] Panel web inicial adaptable con menús y acciones por rol, diferenciado de Mayro.
- [ ] Completar experiencias de administración, vendedor y bodega.
- [ ] Desarrollar portal y experiencia de cliente.
- [ ] Desarrollar experiencia de despacho y conductor.
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
- [ ] Crear y validar la demo persistente con autorización.
- [ ] Probar teléfonos, conexión, lector, impresora y notificaciones push reales.
- [ ] Resolver el problema de estilos pendiente en la APK de Mayro y verificar sus cambios junto con los de distribución.
- [ ] Validar con Don Javier ubicaciones y eventual integración con su software actual.
- [ ] Planificar capacitación y medir las metas de precisión, tiempo, stock, cobranza y cierre.
- [ ] Revisar los cambios pendientes y completar la validación integral antes de hacer merge a `main`; no se hará merge hasta completar la tienda Don Javier.

La base subida se validó con 42 pruebas API y 55 pruebas web dirigidas, y las cinco migraciones se aplicaron en orden a PostgreSQL temporal aislado. Posteriormente, los gráficos y CSV subidos pasaron 48 pruebas web dirigidas; Angular compiló para producción y para `local-mobile`. La compilación de producción conserva advertencias existentes de CSS de Mayro y de la dependencia `qrcode`. No se ha generado ni probado una APK con los cambios gráficos.

## Decisiones y límites vigentes

- Distribución se activa individualmente por tienda y debe coexistir con otros addons desde PRO.
- Una app por tienda debe cubrir los cinco roles; la identidad visual de Don Javier debe ser distinta de Mayro.
- Los documentos y registros legales son ficticios por ahora, sin validez tributaria.
- Para cobranza, UTC es el valor inicial y la zona puede ajustarse por tienda; hay avisos diarios de mejor esfuerzo para la demo, no garantizados en producción.
- La configuración o ampliación de Meta no forma parte de esta etapa y no se presume validada.
- La entrega SSE local no es una bandeja persistente ni garantiza recepción cuando el usuario está desconectado.
- La base de distribución se subió en `31be971`; la rama remota contiene también `b35a2d5` y los gráficos y CSV en `5e62d07`. Las correcciones de Mayro deben verificarse aparte; no se han aplicado migraciones a bases existentes.

## Historial de actualización

| Fecha y hora | Avance |
|---|---|
| 2026-11-21, hora de publicación no registrada | Primera versión persistente: inventario y POS iniciales, avisos de mínimos, cobranza manual, resumen, configuración de zona comercial y equivalencias aproximadas. |
| 2026-11-21 04:23:23 UTC-03:00 (envío local); 04:26:13 UTC-03:00 (fecha del commit en GitHub) | Actualización del estado remoto y local, avisos de cobranza, validación de migraciones, gráficos y CSV; estimación aproximada de 44 %. |
| 2026-11-21 entre 04:27:35 y 04:27:43 UTC-03:00 (reloj local) | Push del commit `5e62d07` de gráficos y CSV a `feat/don-javier-demo`, confirmado en GitHub. El intervalo corresponde al inicio y fin observados del comando, no al instante exacto de recepción. No hubo despliegue ni merge. |
