## De almacenes a entidades

| Almacén del DFD | Qué guarda (una oración) | Entidad candidata | Identificador |
|---|---|---|---|
| Productos | Guarda la información detallada de los productos registrados en la tienda y su cantidad disponible en inventario. | Producto | @id_producto |
| Ventas | Guarda el registro de cada transacción de venta realizada por los empleados junto con su total y fecha. | Venta | @folio_venta |
| Compras | Guarda el historial de adquisiciones de mercancía realizadas a los proveedores con su costo y fecha. | Compra | @folio_compra |

**Decisión:** Los almacenes de **Ventas** y **Compras** unen a la entidad **Producto** con las interacciones de los empleados/proveedores y almacenan datos propios como fechas, horas y montos totales, por lo que se consideran entidades transaccionales dentro del modelo Entidad-Relación.

---

## Diccionario de datos

### 1. Definición de almacenes

**Productos** = @id_producto + nombre_producto + precio + stock + estado_producto  
`*Catálogo general de productos registrados y control de existencias en almacén*`

**Ventas** = @folio_venta + fecha + hora + total_venta + {id_producto + cantidad + precio_unitario}  
`*Registro de cada transacción de venta realizada en la tienda*`

**Compras** = @folio_compra + fecha + total_compra + {id_producto + cantidad + costo_unitario} + (proveedor)  
`*Historial de adquisiciones y abastecimiento de mercancía*`

---

### 2. Definición de flujos que cruzan la frontera

**Solicitud de reporte sobre un periodo** = fecha_inicio + fecha_fin  
`*Flujo que entra desde la entidad externa Dueños del negocio hacia el Proceso 1*`

**Reportes ejecutivos (KPIs)** = fecha_inicio + fecha_fin + total_ventas + total_compras + ganancia_neta  
`*Flujo que sale del Proceso 1 hacia la entidad externa Dueños del negocio*`

**Transacciones de venta** = id_producto + cantidad + (metodo_pago)  
`*Flujo que entra desde la entidad externa Empleados hacia el Proceso 2*`

**Información de los productos** = {id_producto + nombre_producto + precio + stock}  
`*Flujo que sale del Proceso 2 hacia la entidad externa Empleados*`

**Actualizaciones de inventario** = {id_producto + (nombre_producto) + (precio) + stock}  
`*Flujo que entra desde la entidad externa Empleados hacia el Proceso 3*`

**Transacciones de compra** = {id_producto + cantidad + costo_unitario + (proveedor)}  
`*Flujo que entra desde la entidad externa Empleados hacia el Proceso 4*`

---

### 3. Valores posibles de un dato con estados o categorías

**estado_producto** = ["disponible" | "agotado" | "descontinuado" |"baja"]  
`*Categoría que define la condición actual de inventario de un producto*`

**metodo_pago** = ["efectivo" | "tarjeta" | "transferencia"]  
`*Forma de pago utilizada por el cliente en la transacción de venta*`

---

## Declaración de uso de IA

| Herramienta | Para qué la usaron | Qué verificaron |
|---|---|---|
| IA Generativa | Apoyo en la estructuración de la tabla de almacenes a entidades, definición formal del diccionario de datos y sincronización con las conexiones del DFD Nivel 1 actualizado. | Se verificó que los almacenes (`Productos`, `Ventas`, `Compras`) coincidan exactamente con el DFD Nivel 1, que el Proceso 1 lea de `Ventas` y `Compras` para calcular `ganancia_neta`, que los identificadores usen el prefijo `@` y que la notación respectiva cumpla los estándares de la práctica. |