# Práctica 4 — Diagrama de contexto

**Equipo:**
**Sistema:** Sistema de ventas e inventario para negocio minorista.
**Integrantes:** González Vargas Alfredo Zenif

---

## Parte A — Entidades externas y flujos

Antes de dibujar, llenen esta tabla. Una fila por entidad externa. Tomen como punto de partida los participantes que identificaron en E1 y la especificación funcional del lunes.

| Entidad externa | Datos que le entrega al sistema | Datos que recibe del sistema |
|---|---|---|
| Empleados | Información de los productos. | Transacción de venta, transacción de compra, actualización de productos |
| Dueños del negocio | Reportes ejecutivos (KPIs), estado del inventario | Solicitud de reporte por periodo |


**¿Qué quedó fuera del sistema y por qué?** 
Dejamos fuera a los proveedores, ya que no tienen acceso directo al sistema y la información de los productos comprados para el negocio se estaría registrando por medio de los empleados y no por parte de los proveedores. 

> 

---

## Parte C — Declaración de propósito

El sistema existe para centralizar y registrar las operaciones diarias de entrada y salida de mercancía de un negocio minorista. Sirve a los empleados operativos y a los dueños del establecimiento, produciendo el beneficio de mantener un control exacto del inventario y facilitar la toma de decisiones estratégicas mediante reportes de rendimiento.

---

## Parte D — Contenido de los flujos

| Flujo | Origen → Destino | Datos que contiene |
|---|---|---|
| Solicitud de reporte sobre un periodo | Dueños del negocio → Sistema | Fechas de inicio y fin del periodo, y tipo de métricas solicitadas (ventas, ganancias, mermas). |
| Reportes ejecutivos (KPIs) | Sistema → Dueños del negocio | Ingresos totales, productos más vendidos, márgenes de ganancia, alertas de stock y valor del inventario. |
| Transacciones de venta | Empleados → Sistema | Código de barras/ID del producto, cantidad vendida, método de pago y fecha de la transacción. |
| Actualizaciones de inventario | Empleados → Sistema | ID del producto, cantidad ajustada y motivo del ajuste (conteo físico, merma, devolución). |
| Transacciones de compra | Empleados → Sistema | Datos del proveedor, ID de los artículos adquiridos, cantidad recibida y costo unitario de compra. |
| Información de los productos | Sistema → Empleados | Nombre del artículo, precio de venta al público, existencias actuales en anaquel/almacén y descripción. |

---

## Declaración de uso de IA

| Herramienta | Para qué la usaron | Qué verificaron |
|---|---|---|
| Gemini | Redacción de la declaración de propósito (Parte C) y desglose del contenido específico de los flujos de datos (Parte D). | Se verificó que los flujos correspondan exactamente a las flechas del diagrama de contexto y que los datos concretos sean coherentes con la operación del negocio. |