# Práctica 4 — Diagrama de contexto

**Ingeniería de Software · Grupo 1359 / 1359A · Ciclo 2027-1**
Unidad 3 — Análisis estructurado moderno · Taller del viernes 25 de septiembre · Trabajo en equipo

Hoy empezamos a modelar su sistema. En las unidades 1 y 2 lo describieron con palabras: visión, necesidades, especificación funcional. A partir de hoy lo van a describir con diagramas, y el primero de todos es el **diagrama de contexto**. Todo lo que construyan en la Unidad 3 (el DFD nivel 1, el nivel 2 y la partición por eventos) sale de este diagrama, así que vale la pena hacerlo con cuidado.

Al terminar la sesión van a tener en su repositorio:

- `docs/diagrama_contexto.drawio` con el diagrama de contexto de su sistema.
- `docs/practica4_contexto.md` con la tabla de entidades, la declaración de propósito y el contenido de cada flujo.

---

## Lo que necesitan saber antes de empezar

### El análisis estructurado moderno

El análisis estructurado moderno (Yourdon) describe un sistema con dos modelos:

- **Modelo ambiental:** define la frontera del sistema, es decir, qué queda dentro, qué queda fuera y qué datos cruzan esa frontera. Se compone de la **declaración de propósito**, el **diagrama de contexto** y la **lista de eventos**.
- **Modelo de comportamiento:** describe qué pasa dentro del sistema. Ahí entran los DFD por niveles, el diccionario de datos y las especificaciones de procesos.

Hoy trabajamos el modelo ambiental. Si la frontera está mal, todo lo que dibujen después también lo estará.

### El diagrama de contexto

Es un DFD de nivel 0 y tiene solo tres tipos de elemento:

| Elemento | Símbolo | Qué representa |
|---|---|---|
| Proceso | Círculo | **Su sistema completo**. Lleva el número 0 y el nombre del sistema. Hay uno solo. |
| Entidad externa | Rectángulo | Una persona, área u otro sistema que **está fuera** de su sistema e intercambia datos con él. |
| Flujo de datos | Flecha con nombre | **Datos** que entran o salen del sistema. La dirección de la flecha indica hacia dónde viajan. |

### Las reglas que tienen que cumplir

1. **Un solo proceso.** Si dibujan dos círculos ya están haciendo un DFD de nivel 1, y eso lo vemos el lunes.
2. **Sin almacenes de datos.** Las tablas y los archivos viven dentro del sistema, así que no se ven desde afuera.
3. **Todo flujo toca al sistema.** No dibujen flechas entre dos entidades externas: lo que se dicen entre ellas no le importa a su sistema.
4. **Todo flujo tiene nombre y ese nombre es un dato**, no una acción. Escriban «Solicitud de préstamo» y no «Solicita»; «Comprobante de pago» y no «Da clic en pagar».
5. **Las entidades externas están realmente fuera.** «Base de datos», «Servidor» o «Pantalla de inicio» no son entidades externas: son parte de su sistema.
6. **Toda entidad externa intercambia algo.** Si un rectángulo no tiene flechas, sobra. Y si un participante de su E1 no aparece, pregúntense por qué.

Una persona que usa el sistema desde un teclado **sí** es entidad externa. Lo que no es entidad externa es el teclado.

### Ejemplo resuelto

En `ejemplo/ejemplo_contexto.drawio` está el diagrama de contexto de un *sistema de préstamo de equipo del laboratorio*. Ábranlo para ver cómo se aplican las reglas, pero no lo copien: su sistema tiene otras entidades y otros flujos.

---

## Preparación (10 min)

1. Hagan **fork** de este repositorio. Basta con uno por equipo: el dueño del fork agrega a sus compañeros como colaboradores en *Settings → Collaborators*.
2. En su fork, abran un Codespace desde **Code → Codespaces → Create codespace on main**.
3. Esperen a que termine de cargar. El editor de Draw.io se instala solo.
4. Abran `docs/diagrama_contexto.drawio`. Debe abrirse como diagrama, no como texto.

**Si el editor de diagramas no abre:** entren a [app.diagrams.net](https://app.diagrams.net), elijan *Open Existing Diagram*, abran el `.drawio` que descargaron del repositorio y, al terminar, guárdenlo como `.drawio` y súbanlo a `docs/` desde la página de su fork en GitHub (*Add file → Upload files*). No pierdan más de 10 minutos en este paso.

---

## Parte A — Entidades externas y flujos (15 min)

Todavía no dibujen nada. Abran `docs/practica4_contexto.md` y llenen la tabla de la Parte A.

- Partan de los participantes que identificaron en E1 y de la especificación funcional que redactaron el lunes.
- Para cada entidad externa, anoten qué datos le entrega al sistema y qué datos recibe de él.
- Respondan la pregunta sobre lo que quedó fuera del sistema. Decidir qué **no** es parte del sistema es tan importante como decidir qué sí.

## Parte B — El diagrama (30 min)

En `docs/diagrama_contexto.drawio`:

1. Pongan el nombre de su sistema en el título y dentro del círculo.
2. Dupliquen el rectángulo de ejemplo para crear cada entidad externa de la tabla A.
3. Dibujen cada flujo como una flecha con nombre. Para crear una flecha, pasen el cursor sobre una figura y arrastren desde la flecha azul que aparece hasta la otra figura. Para ponerle nombre, denle doble clic.
4. Revisen el diagrama contra las seis reglas de arriba.
5. Borren la nota amarilla y guarden (**Ctrl+S**).

## Parte C — Declaración de propósito (10 min)

En la sección C de `docs/practica4_contexto.md`, escriban en 2 o 3 líneas para qué existe su sistema, a quién sirve y qué beneficio produce. Es el primer componente del modelo ambiental y debe poder leerlo alguien que nunca ha visto su proyecto.

## Parte D — Contenido de los flujos (15 min)

En la sección D, hagan una fila por cada flecha del diagrama y listen los datos concretos que viajan en ella. Por ejemplo, «Solicitud de préstamo» contiene número de cuenta, clave del equipo y fecha de préstamo.

Esta tabla es el primer borrador de su **diccionario de datos**, que formalizamos en la Unidad 5. Por eso les conviene hacerla bien desde ahora.

---

## Entrega (10 min)

1. En la terminal del Codespace:

   ```bash
   git add docs/
   git commit -m "Práctica 4: diagrama de contexto y declaración de propósito"
   git push
   ```

2. Confirmen en la pestaña **Commits** de su fork que el commit aparece.
3. Llenen el documento de evidencia en Google Docs con sus capturas y entréguenlo en Classroom junto con el enlace a su fork, **al cierre de la sesión**.

Pueden usar IA en esta práctica, siempre que lo declaren en la tabla al final de `docs/practica4_contexto.md`. Ustedes son responsables de todo lo que entregan: si no pueden explicarlo, no lo entregaron ustedes.
