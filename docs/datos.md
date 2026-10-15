## De almacenes a entidades

| Almacén del DFD | Qué guarda (una oración) | Entidad candidata | Identificador |
|---|---|---|---|
| Productos | Guarda la información detallada de los productos registrados en la tienda y su cantidad disponible en inventario. | Producto | @id_producto |
| Ventas | Guarda el registro de cada transacción de venta realizada por los empleados junto con su total y fecha. | Venta | @folio_venta |
| Compras | Guarda el historial de adquisiciones de mercancía realizadas a los proveedores con su costo y fecha. | Compra | @folio_compra |

**Decisión:** Los almacenes de **Ventas** y **Compras** unen a la entidad **Producto** con las interacciones de los empleados/proveedores y almacenan datos propios como fechas, horas y montos totales, por lo que se consideran entidades transaccionales dentro del modelo Entidad-Relación.

## Diccionario de datos

### 1. Definición de almacenes

Ventas = @folio_venta + fecha + hora + total_venta + {id_producto + cantidad + precio_unitario}  
`*Registro de cada transacción de venta realizada en la tienda*`

Compras = @folio_compra + fecha + total_compra + {id_producto + cantidad + costo_unitario} + (proveedor)  
`*Historial de adquisiciones y abastecimiento de mercancía*`

### 2. Definición de flujos que cruzan la frontera

Transacciones de venta = id_producto + cantidad + (metodo_pago)  
`*Flujo que entra desde la entidad externa Empleados*`

Reportes ejecutivos (KPIs) = fecha_inicio + fecha_fin + total_ventas + total_compras + ganancia_neta  
`*Flujo que sale hacia la entidad externa Dueños del negocio*`

### 3. Valores posibles de un dato con estados o categorías

estado_producto = ["disponible" | "agotado" | "descontinuado"]  
`*Categoría que define la condición actual de inventario de un producto*`

## Declaración de uso de IA

| Herramienta | Para qué la usaron | Qué verificaron |
|---|---|---|
| IA Generativa | Apoyo en la estructuración de la tabla de almacenes a entidades, definición del diccionario de datos e integración de la notación adecuada. | Se verificó que los almacenes coincidan exactamente con los DFDs de Nivel 1 y Nivel 2, que los identificadores usen el prefijo `@` de forma válida y que la notación del diccionario respete las reglas de la práctica. |