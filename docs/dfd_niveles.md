## Agrupación del nivel 1

| Proceso de nivel 1 | Agrupa (procesos preliminares) | Criterio |
|---|---|---|
| 1 Generar reporte ejecutivo | 1 Generar reporte ejecutivo | El DFD preliminar tiene 5 procesos (6 o menos), por lo que no requiere agrupación y se mantiene limpio. |
| 2 Registrar venta | 2 Registrar venta | El DFD preliminar tiene 5 procesos (6 o menos), por lo que no requiere agrupación y se mantiene limpio. |
| 3 Actualizar inventario | 3 Actualizar inventario | El DFD preliminar tiene 5 procesos (6 o menos), por lo que no requiere agrupación y se mantiene limpio. |
| 4 Registrar compra | 4 Registrar compra | El DFD preliminar tiene 5 procesos (6 o menos), por lo que no requiere agrupación y se mantiene limpio. |
| 5 Realizar corte de caja | 5 Realizar corte de caja | El DFD preliminar tiene 5 procesos (6 o menos), por lo que no requiere agrupación y se mantiene limpio. |

## Balanceo del nivel 1

| Flujo del contexto | Entidad externa | Dirección | Proceso del nivel 1 |
|---|---|---|---|
| Solicitud de reporte sobre un periodo | Dueños del negocio | Entrada | 1 Generar reporte ejecutivo |
| Reportes ejecutivos (KPIs) | Dueños del negocio | Salida | 1 Generar reporte ejecutivo |
| Transacciones de venta | Empleados | Entrada | 2 Registrar venta |
| Información de los productos | Empleados | Salida | 2 Registrar venta |
| Actualizaciones de inventario | Empleados | Entrada | 3 Actualizar inventario |
| Transacciones de compra | Empleados | Entrada | 4 Registrar compra |


## Balanceo del nivel 2 – proceso 2

| Flujo del proceso padre (2 Registrar venta) | Entidad / Almacén conectado | Dirección | Subproceso correspondiente |
|---|---|---|---|
| Transacciones de venta | Empleados | Entrada | 2.2 Procesar transacción |
| Información de los productos | Empleados | Salida | 2.1 Consultar productos |
| Lectura de datos de productos | Almacén Productos | Entrada | 2.1 Consultar productos |
| Registro de venta | Almacén Ventas | Salida | 2.3 Registrar venta realizada |