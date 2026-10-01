## Lista de eventos

| # | Evento | Tipo | Flujo de entrada | Respuesta del sistema |
|---|---|---|---|---|
| 1 | Dueño del negocio solicita reporte sobre un periodo | Evento de flujo | Solicitud de reporte sobre un periodo | El sistema genera y entrega reportes ejecutivos (KPIs) a los dueños del negocio. |
| 2 | Empleado realiza transacción de venta | Evento de flujo | Transacciones de venta | El sistema registra la venta, actualiza saldos y entrega información de los productos al empleado. |
| 3 | Empleado envía actualizaciones de inventario | Evento de flujo | Actualizaciones de inventario | El sistema actualiza los registros de existencias de los productos correspondientes en su base de datos. |
| 4 | Empleado registra transacción de compra | Evento de flujo | Transacciones de compra | El sistema guarda los datos de la compra para reflejar el ingreso de nueva mercancía. |
| 5 | Es fin de día | Evento temporal | (ninguno) | El sistema realiza un cierre o corte de caja diario y guarda los registros para futuros reportes. |