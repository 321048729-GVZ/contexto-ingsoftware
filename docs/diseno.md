## Módulos y cohesión

| Proceso de nivel 1 | En una oración | Cohesión | Decisión de diseño |
| --- | --- | --- | --- |
| **1 Generar reporte ejecutivo** | Produce las métricas ejecutivas de rendimiento sobre un periodo determinado. | Funcional | **Se queda como está**, debido a que todo el proceso contribuye únicamente a la tarea de emitir reportes ejecutivos. |
| **2 Registrar venta** | Consulta datos de productos, procesa el cobro y guarda la transacción realizada. | Comunicacional | **Se divide en** 2.1 Consultar productos, 2.2 Procesar transacción y 2.3 Registrar venta realizada, los cuales sí poseen cohesión funcional. |
| **3 Actualizar inventario** | Registra modificaciones de stock en el catálogo de productos. | Funcional | **Se queda como está**, ya que es el único módulo responsable de escribir directamente en el almacén Productos. |
| **4 Registrar compra** | Asienta la transacción de entrada de mercancía en el almacén de compras. | Funcional | **Se queda como está**, porque su única tarea es el registro de comprobantes de compra a proveedores. |
| **5 Realizar corte de caja** | Consolida los registros de ventas y compras para calcular el saldo final de caja. | Comunicacional | **Se divide en** 5.1 Obtener acumulado de transacciones y 5.2 Calcular arqueo final, permitiendo que cada submódulo resultante sea funcional. |

## Acoplamiento

| Entre | Qué comparten | Acoplamiento | Decisión de diseño |
| --- | --- | --- | --- |
| **2.2 Procesar transacción → 2.3 Registrar venta realizada** | El registro o estructura completa de la transacción (*Detalle de venta validada*). | Estampado | Pasar únicamente los atributos indispensables (*id_venta*, *monto_total* y *desglose_artículos*) para transformar la interacción en acoplamiento de datos. |
| **2.1 Consultar productos → 2.2 Procesar transacción** | Valores individuales de *Precios y stock* para la verificación del cobro. | De datos | Se mantiene el acoplamiento de datos, transmitiendo solo las variables simples necesarias (*precio_unitario* y *existencia_disponible*). |
| **3 Actualizar inventario ↔ 4 Registrar compra** | Escritura directa sobre el almacén de datos *Productos*. | Común | **3 Actualizar inventario** es el dueño exclusivo del almacén *Productos*. **4 Registrar compra** únicamente le solicita el incremento de existencias sin modificar el almacén por su cuenta. |

## Declaración de uso de IA

| Herramienta | Para qué la usaron | Qué verificaron |
|---|---|---|
| **Gemini** | Estructuración del formato Markdown de las tablas, redacción de las oraciones sintéticas por módulo y análisis de las interacciones entre procesos y almacenes a partir de las imágenes de los DFD de nivel 1 y nivel 2. | Verificación manual de que la clasificación de cohesión y acoplamiento coincidiera estrictamente con la escala y definiciones del PDF, que las decisiones de diseño iniciaran con la sintaxis obligatoria ("Se queda como está" / "Se divide en...") y que los nombres de los módulos correspondieran fielmente a los diagramas del proyecto. |