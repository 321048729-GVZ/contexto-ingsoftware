## Parte A · Procesos primitivos y reparto

| Número | Nombre del proceso (como en el DFD) | ¿Quién lo especifica hoy? | Herramienta |
|---|---|---|---|
| 1 | Generar reporte ejecutivo | Zenif González (para E5) | Español estructurado |
| 2.1 | Consultar productos | Zenif González (para E5) | Español estructurado |
| 2.2 | Procesar transacción | Zenif González | Tabla de decisión |
| 2.3 | Registrar venta realizada | Zenif González (para E5) | Español estructurado |
| 3 | Actualizar inventario | Zenif González (para E5) | Español estructurado |
| 4 | Registrar compra | Zenif González (para E5) | Español estructurado |
| 5 | Realizar corte de caja | Zenif González (para E5) | Español estructurado |

---

### Parte B · Minispecs en español estructurado

#### Minispec · Proceso 1: Generar reporte ejecutivo

| Campo | Detalle |
|---|---|
| **Proceso** | 1 Generar reporte ejecutivo |
| **Entradas** | Solicitud de reporte sobre un periodo |
| **Salidas** | Reportes ejecutivos (KPIs) |
| **Almacenes** | Ventas (lee), Compras (lee) |
| **Lógica** | OBTENER fecha_inicio y fecha_fin de Solicitud de reporte sobre un periodo<br>BUSCAR en Ventas las ventas registradas entre fecha_inicio y fecha_fin<br>BUSCAR en Compras las compras registradas entre fecha_inicio y fecha_fin<br>CALCULAR total_ventas = suma de total_venta del periodo<br>CALCULAR total_compras = suma de total_compra del periodo<br>CALCULAR ganancia_neta = total_ventas - total_compras<br>GENERAR Reportes ejecutivos (KPIs) con fecha_inicio, fecha_fin, total_ventas, total_compras y ganancia_neta<br>EMITIR Reportes ejecutivos (KPIs) |

---

#### Minispec · Proceso 2.1: Consultar productos

| Campo | Detalle |
|---|---|
| **Proceso** | 2.1 Consultar productos |
| **Entradas** | Ninguna |
| **Salidas** | Información de los productos, Precios y stock |
| **Almacenes** | Productos (lee) |
| **Lógica** | PARA CADA producto en Productos<br>&nbsp;&nbsp;&nbsp;&nbsp;LEER id_producto, nombre_producto, precio, stock y estado_producto<br>&nbsp;&nbsp;&nbsp;&nbsp;AGREGAR datos a Información de los productos y a Precios y stock<br>FIN PARA<br>EMITIR Información de los productos a Empleados<br>ENVIAR Precios y stock a Procesar transacción |

---

#### Minispec · Proceso 2.3: Registrar venta realizada

| Campo | Detalle |
|---|---|
| **Proceso** | 2.3 Registrar venta realizada |
| **Entradas** | Detalle de venta validada |
| **Salidas** | Ninguna |
| **Almacenes** | Ventas (escribe) |
| **Lógica** | RECIBIR Detalle de venta validada<br>GENERAR folio_venta, fecha y hora actuales<br>REGISTRAR folio_venta, fecha, hora, total_venta y detalle de productos en Ventas |

---

#### Minispec · Proceso 3: Actualizar inventario

| Campo | Detalle |
|---|---|
| **Proceso** | 3 Actualizar inventario |
| **Entradas** | Actualizaciones de inventario |
| **Salidas** | Ninguna |
| **Almacenes** | Productos (escribe) |
| **Lógica** | PARA CADA ítem en Actualizaciones de inventario<br>&nbsp;&nbsp;&nbsp;&nbsp;BUSCAR ítem en Productos por id_producto<br>&nbsp;&nbsp;&nbsp;&nbsp;SI ítem EXISTE ENTONCES<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ACTUALIZAR stock, precio y estado_producto en Productos<br>&nbsp;&nbsp;&nbsp;&nbsp;SINO<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;REGISTRAR nuevo ítem en Productos con estado "disponible"<br>&nbsp;&nbsp;&nbsp;&nbsp;FIN SI<br>FIN PARA |

---

#### Minispec · Proceso 4: Registrar compra

| Campo | Detalle |
|---|---|
| **Proceso** | 4 Registrar compra |
| **Entradas** | Transacciones de compra |
| **Salidas** | Ninguna |
| **Almacenes** | Compras (escribe), Productos (escribe) |
| **Lógica** | GENERAR folio_compra y fecha actual<br>PARA CADA ítem en Transacciones de compra<br>&nbsp;&nbsp;&nbsp;&nbsp;REGISTRAR folio_compra, fecha, total_compra y detalle en Compras<br>&nbsp;&nbsp;&nbsp;&nbsp;BUSCAR producto en Productos por id_producto<br>&nbsp;&nbsp;&nbsp;&nbsp;ACTUALIZAR stock = stock + cantidad en Productos<br>FIN PARA |

---

#### Minispec · Proceso 5: Realizar corte de caja

| Campo | Detalle |
|---|---|
| **Proceso** | 5 Realizar corte de caja |
| **Entradas** | Ninguna |
| **Salidas** | Ninguna |
| **Almacenes** | Ventas (lee), Compras (lee), Productos (lee) |
| **Lógica** | OBTENER fecha actual<br>CALCULAR total_ventas_dia leyendo registros de la fecha en Ventas<br>CALCULAR total_compras_dia leyendo registros de la fecha en Compras<br>CALCULAR balance_caja = total_ventas_dia - total_compras_dia<br>VERIFICAR consistencia física vs registrada del inventario en Productos |

---

### Parte C · Tabla de decisión

**Proceso elegido:** 2.2 Procesar transacción

| Condiciones / acciones | R1 | R2 | R3 | R4 |
|---|:---:|:---:|:---:|:---:|
| **C1:** ¿Producto existe en el catálogo (`Precios y stock`)? | N | S | S | S |
| **C2:** ¿Estado del producto es "disponible"? | - | N | S | S |
| **C3:** ¿Hay stock suficiente (`stock >= cantidad`)? | - | - | N | S |
| **A1:** Notificar "Producto no encontrado" y rechazar | X | | | |
| **A2:** Notificar "Producto agotado / no disponible" y rechazar | | X | X | |
| **A3:** Generar y emitir `Detalle de venta validada` | | | | X |

---

#### Respuesta a las preguntas de análisis:

**¿Cuántas reglas tenía la tabla completa y a cuántas la redujeron? ¿Qué condición dejó de importar y por qué?**

> La tabla completa tenía **8 reglas** ($2^3$) y se redujo a **4 reglas** (R1, R2, R3 y R4)[cite: 5].
> 
> * En **R1**, si el producto no existe ($C1 = \text{N}$), las condiciones **C2** y **C3** dejan de importar (`-`) porque la transacción se rechaza de inmediato sin evaluar el estado ni el stock[cite: 6].
> * En **R2**, si el producto no está en estado "disponible" ($C2 = \text{N}$), la condición **C3** deja de importar (`-`) porque no se puede vender un producto descontinuado o agotado independientemente de la cantidad solicitada[cite: 6].

---

### Parte D · Verificación contra DFD y diccionario

| Pregunta | Respuesta |
|---|---|
| **¿Todas las entradas y salidas de sus minispecs aparecen en el DFD con el mismo nombre? Si cambiaron alguna, ¿cuál y dónde la corrigieron?** | Sí, todas coinciden exactamente con las flechas de los DFDs de Nivel 1 y Nivel 2 (`Solicitud de reporte sobre un periodo`, `Reportes ejecutivos (KPIs)`, `Información de los productos`, `Precios y stock`, `Transacciones de venta`, `Detalle de venta validada`, `Actualizaciones de inventario` y `Transacciones de compra`)[cite: 1]. Se corrigió el DFD de Nivel 1 agregando el flujo de lectura de almacén de `Compras` al Proceso 1 para poder calcular la ganancia neta. |
| **¿Qué datos que mencionan no estaban en `docs/datos.md`? Escríbanlos aquí y agréguenlos al diccionario.** | Se agregaron los atributos y campos: `estado_producto` (categoría ["disponible" \| "agotado" \| "descontinuado"]), `ganancia_neta` y `total_compras` dentro de `Reportes ejecutivos (KPIs)`, y los campos `fecha_inicio` y `fecha_fin` del flujo `Solicitud de reporte sobre un periodo`[cite: 1]. |
| **¿Algún proceso les resultó demasiado grande para un minispec? ¿Cuál y cómo lo descompondrían?** | El proceso `2.2 Procesar transacción` fue el más complejo por evaluar múltiples reglas de negocio (existencia del producto, estado y stock)[cite: 1]. Por ello se especificó mediante Tabla de decisión[cite: 1]. En caso de requerir descomposición, se separaría en `2.2.1 Validar disponibilidad de productos` y `2.2.2 Formatear venta validada`. |

---

## Declaración de uso de IA

## Declaración de uso de IA
| Herramienta | Para qué la usaron | Qué verificaron |
|---|---|---|
| Gemini | Estructuración y redacción de los minispecs en Español Estructurado (Parte B) para los procesos primitivos 1, 2.1, 2.3, 3, 4 y 5[cite: 1, 14]. | Se verificó que se usaran únicamente verbos en imperativo[cite: 5], sangrías adecuadas[cite: 5], estructuras permitidas (`SI-ENTONCES`, `PARA CADA`)[cite: 5] y que los flujos/almacenes coincidieran exactamente con el DFD[cite: 4]. |
| Gemini | Diseño, combinación y simplificación de la Tabla de Decisión (Parte C) para el proceso 2.2 `Procesar transacción`[cite: 1, 24]. | Se verificó que las 8 reglas iniciales ($2^3$) se redujeran correctamente a 4 reglas mediante el símbolo de indiferencia (`-`)[cite: 5, 24], asegurando que no quedara ningún caso sin cubrir ni contradicciones en las acciones[cite: 6]. |
| Gemini | Verificación de consistencia DFD-Diccionario (Parte D) y actualización del archivo `docs/datos.md`[cite: 1, 28]. | Se verificó que todos los datos y campos mencionados en los minispecs (`estado_producto`, `ganancia_neta`, `fecha_inicio`, etc.) existieran en el diccionario de datos y que los almacenes leídos/escritos respetaran la notación oficial[cite: 4, 28]. |