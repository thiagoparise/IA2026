# Lógica difusa: resumen completo

## Alcance

Este resumen desarrolla el contenido de la unidad sobre lógica booleana y difusa, conjuntos difusos, funciones de pertenencia, proposiciones simples y compuestas, operadores, reglas, árboles de proposiciones, Fuzzy Tree Studio y aplicaciones.

El material lleva por título *Sistema de inferencia difusa - Mamdani*, pero se concentra principalmente en las bases proposicionales. Por eso también se explica brevemente su relación con Mamdani. Sugeno queda fuera de este archivo porque se estudiará por separado.

---

## 1. ¿Qué problema resuelve la lógica difusa?

La lógica clásica trabaja con afirmaciones que solo pueden ser verdaderas o falsas. Esto funciona bien para conceptos precisos:

- “El número 8 es par”: verdadero.
- “El número 9 es par”: falso.

Pero muchos conceptos reales no poseen una frontera natural exacta:

- persona joven;
- velocidad alta;
- temperatura caliente;
- buen servicio;
- candidato apropiado;
- presión elevada.

En estos casos, imponer un corte rígido puede generar decisiones poco naturales. Una escala clásica de multas, por ejemplo, puede cobrar lo mismo por exceder el límite en 1 km/h que en 9 km/h, y producir un gran salto en la multa al pasar apenas al intervalo siguiente.

La lógica difusa representa estas transiciones de manera gradual. En lugar de decidir únicamente si “la velocidad está en infracción”, calcula **en qué grado** se cumple esa afirmación.

Si el grado fuera 0,7, una posible política sería:

**multa = multa máxima × grado de verdad de “la velocidad es alta”**

La lógica difusa no es una lógica incorrecta o poco rigurosa. Es una herramienta matemática para modelar conceptos vagos o graduales.

---

## 2. Generalización de la lógica booleana

| Modelo | Valores de verdad |
|---|---|
| Lógica booleana | solamente 0 o 1 |
| Lógica difusa | cualquier valor del intervalo [0, 1] |

Interpretación:

- 0: completamente falso;
- 1: completamente verdadero;
- entre 0 y 1: verdad parcial o gradual.

Se generalizan tres elementos:

1. **Pertenencia a un conjunto:** pasa de “pertenece/no pertenece” a “pertenece en cierto grado”.
2. **Valores de verdad:** pasan de {0, 1} al intervalo [0, 1].
3. **Operadores lógicos:** AND, OR, NOT e implicación pasan a ser funciones numéricas que combinan grados.

La lógica booleana queda incluida como caso particular. Cuando las entradas solo valen 0 o 1, los operadores difusos deben reproducir el comportamiento clásico.

---

## 3. Conjuntos clásicos y difusos

### 3.1. Conjunto clásico o nítido

En un conjunto clásico A, un elemento x solo puede estar dentro o fuera:

- μA(x) = 1 si x pertenece a A;
- μA(x) = 0 si x no pertenece a A.

Esta asignación se denomina **función característica**.

Ejemplo: si JOVEN se define como “menor de 30 años”, una persona de 29 años pertenece y una de 30 no. La frontera es abrupta.

### 3.2. Conjunto difuso

Un conjunto difuso A sobre un universo X se describe como:

**A = {(x, μA(x)) : x pertenece a X}**

Su función de pertenencia cumple:

**μA(x) está entre 0 y 1**

El valor μA(x) expresa cuánto se ajusta x al concepto:

- μA(x) = 0: no es compatible;
- 0 < μA(x) < 1: es parcialmente compatible;
- μA(x) = 1: es totalmente compatible.

### 3.3. Elementos necesarios para definirlo

1. **Universo de discurso:** dominio de valores posibles.
2. **Variable:** magnitud o característica evaluada.
3. **Etiqueta lingüística:** nombre del concepto difuso.
4. **Función de pertenencia:** asigna un grado a cada valor.
5. **Parámetros:** determinan posición, anchura y pendiente.

Ejemplo:

- Universo: edades entre 0 y 100.
- Variable lingüística: edad.
- Etiquetas: joven, adulto, mayor.
- Función JOVEN: alta para edades pequeñas y decreciente con la edad.

### 3.4. Conceptos complementarios

- **Soporte:** valores con pertenencia mayor que 0.
- **Núcleo:** valores con pertenencia igual a 1.
- **Frontera difusa:** valores con pertenencia entre 0 y 1.
- **Altura:** máximo grado alcanzado por el conjunto.
- **Conjunto normal:** alcanza el grado 1.
- **Corte alfa:** conjunto clásico formado por los elementos cuyo grado es mayor o igual que un valor α elegido.

---

## 4. Dualidad entre conjunto y proposición

Sea la afirmación:

**p(x): “El píxel x es gris oscuro”.**

Equivale a decir:

**“El píxel x pertenece al conjunto difuso GRIS OSCURO”.**

Por lo tanto:

**grado de verdad de p(x) = grado de pertenencia de x a GRIS OSCURO**

En un conjunto clásico, el píxel sería oscuro o no oscuro. En uno difuso, distintas intensidades reciben distintos grados.

### Predicado y proposición

En sentido lógico estricto, p(x) es un predicado porque contiene la variable libre x. Al reemplazarla por un caso concreto, como p(píxel 25), se obtiene una proposición evaluable. Fuzzy Tree Studio usa la palabra “predicado”, aunque en la actividad también se los llama proposiciones difusas.

---

## 5. Pertenencia no significa probabilidad

- **Grado de pertenencia:** cuánto se ajusta un valor conocido a un concepto gradual.
- **Probabilidad:** incertidumbre acerca de qué hecho ocurrió u ocurrirá.

Si una temperatura conocida tiene grado 0,8 en CALIENTE, significa que es muy compatible con el concepto. No significa que haya un 80 % de probabilidad de que sea caliente.

Puede haber lógica difusa sin incertidumbre probabilística: el dato puede conocerse exactamente, mientras que la frontera del concepto es vaga.

---

## 6. Funciones de pertenencia

Una función de pertenencia transforma una entrada en un grado entre 0 y 1.

### 6.1. Funciones mostradas en el material

| Función | Nombre habitual | Característica |
|---|---|---|
| Trapezoidal | trapmf | Sube, posee una meseta en 1 y luego baja. |
| Campana generalizada | gbellmf | Campana suave con anchura y pendiente ajustables. |
| Triangular | trimf | Sube linealmente hasta un máximo y luego baja. |
| Gaussiana | gaussmf | Campana suave y simétrica. |
| Gaussiana doble | gauss2mf | Combina dos gaussianas y puede formar una meseta. |
| Curva S | smf | Crece suavemente de 0 a 1. |
| Curva Z | zmf | Decrece suavemente de 1 a 0. |
| Producto de sigmoides | psigmf | Puede crear una región elevada entre dos transiciones. |
| Diferencia de sigmoides | dsigmf | Forma una región mediante dos sigmoides. |
| Curva pi | pimf | Crece, permanece alta y luego decrece suavemente. |
| Sigmoidea | sigmf | Transición creciente o decreciente según sus parámetros. |

Las triangulares y trapezoidales son simples e interpretables. Las gaussianas, sigmoidales y de campana producen transiciones más suaves.

### 6.2. Sigmoide

El apunte utiliza:

**f(x) = 1 / (1 + e elevado a −P(x − C))**

- C ubica el centro de la transición, donde el grado ronda 0,5.
- P controla la pendiente.
- Si P es positivo, la función crece.
- Cuanto mayor es el valor absoluto de P, más abrupta es la transición.

Es apropiada para “velocidad alta”: el grado aumenta continuamente con la velocidad.

### 6.3. Elección de la función

Puede definirse mediante:

- conocimiento experto;
- suavización de umbrales existentes;
- análisis de datos;
- encuestas;
- aprendizaje u optimización;
- combinación de esas fuentes.

No existe una función universalmente correcta. Debe representar el significado del concepto en su dominio y ser validada.

### 6.4. Solapamiento

Las etiquetas suelen superponerse. Una temperatura puede pertenecer a TEMPLADA con grado 0,7 y a CALIENTE con 0,3.

No es una contradicción: expresa que el valor está en una zona de transición.

---

## 7. Proposiciones difusas

Una proposición difusa puede tener cualquier grado de verdad entre 0 y 1.

### 7.1. Proposición simple

Contiene un solo criterio:

- “El píxel es gris oscuro”.
- “El servicio es bueno”.
- “El sistema es apropiado”.
- “El candidato es joven”.

### 7.2. Cómo obtener su grado

#### Mediante una función de pertenencia

Se evalúa una entrada numérica en la función de una etiqueta. Por ejemplo, una intensidad en GRIS OSCURO.

#### Mediante opciones discretas

El material usa una escala de Likert:

| Respuesta | Grado |
|---|---:|
| Totalmente en desacuerdo | 0 |
| En desacuerdo | 0,25 |
| Ni de acuerdo ni en desacuerdo | 0,50 |
| De acuerdo | 0,75 |
| Totalmente de acuerdo | 1 |

#### Mediante valoración experta

Un experto asigna cuán cierta considera una proposición, por ejemplo “El sistema es apropiado” con grado 0,8.

“Subjetivo” no significa arbitrario: la asignación debe basarse en criterios, experiencia y validación.

---

## 8. Operadores booleanos

| p | q | p AND q | p OR q | p implica q |
|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 1 | 1 | 1 | 1 |

La negación intercambia 0 y 1.

En lógica difusa, los operadores se implementan mediante funciones aritméticas:

- c(a, b): conjunción;
- d(a, b): disyunción;
- n(a): negación.

Deben coincidir con las tablas booleanas cuando las entradas son 0 o 1.

---

## 9. Negación, conjunción y disyunción

### 9.1. Negación NOT

Negación estándar:

**NOT(a) = 1 − a**

Si JOVEN vale 0,8, NO JOVEN vale 0,2.

### 9.2. Conjunción AND: t-normas

Una t-norma generaliza AND. Debe ser conmutativa, asociativa, monótona y cumplir T(a, 1) = a.

| Nombre | T(a, b) |
|---|---|
| Mínimo | min(a, b) |
| Producto algebraico | a × b |
| Producto drástico | min(a, b) si max(a, b) = 1; si no, 0 |
| Łukasiewicz o diferencia acotada | max(0, a + b − 1) |
| Producto de Einstein | (a × b) / (2 − a − b + a × b) |
| Producto de Hamacher | (a × b) / (a + b − a × b) |
| Yager, k > 0 | 1 − min(1, raíz k-ésima de ((1−a)^k + (1−b)^k)) |

En Hamacher, cuando a = b = 0, el resultado se define por continuidad para evitar 0/0.

### 9.3. Disyunción OR: s-normas

Una s-norma generaliza OR. Debe ser conmutativa, asociativa, monótona y cumplir S(a, 0) = a.

| Nombre | S(a, b) |
|---|---|
| Máximo | max(a, b) |
| Suma algebraica o probabilística | a + b − a × b |
| Suma drástica | max(a, b) si min(a, b) = 0; si no, 1 |
| Łukasiewicz o suma acotada | min(1, a + b) |
| Suma de Einstein | (a + b) / (1 + a × b) |
| Suma de Hamacher | (a + b − 2 × a × b) / (1 − a × b) |
| Yager, k > 0 | min(1, raíz k-ésima de (a^k + b^k)) |

En Hamacher, cuando a = b = 1, el resultado se define por continuidad.

### 9.4. Operadores compensatorios

Para dos entradas:

- AND geométrico = raíz cuadrada de (a × b).
- OR dual = 1 − raíz cuadrada de ((1−a) × (1−b)).

Para n entradas:

- AND = raíz n-ésima de (a₁ × a₂ × … × aₙ).
- OR dual = 1 − raíz n-ésima de ((1−a₁) × … × (1−aₙ)).

La media geométrica permite compensación, pero estrictamente no es una t-norma: por ejemplo, raíz cuadrada de (a × 1) no siempre es igual a a.

### 9.5. Comparación

Para a = 0,8 y b = 0,6:

| Modelo | AND | OR |
|---|---:|---:|
| Mínimo / máximo | 0,600 | 0,800 |
| Producto / suma algebraica | 0,480 | 0,920 |
| Geométrico / dual | 0,693 | 0,717 |

La elección del operador cambia el resultado y, por lo tanto, forma parte del significado del modelo.

---

## 10. Implicación

En lógica booleana:

**p implica q equivale a (NOT p) OR q**

Otra forma equivalente correcta es:

**NOT(p AND NOT q)**

Una extensión difusa posible es:

**I(a, b) = S(1 − a, b)**

donde S es la disyunción elegida. No existe una única implicación difusa.

### Corrección del apunte

La diapositiva también escribe **(NOT p) AND (p OR q)** como equivalente a la implicación. Esa equivalencia es incorrecta. Por ejemplo, si p = 0 y q = 0, la implicación vale 1, pero esa expresión vale 0.

---

## 11. Proposiciones compuestas

Una proposición compuesta combina proposiciones simples.

Ejemplo:

**“El candidato es joven y tiene experiencia”.**

- q: el candidato es joven.
- r: tiene experiencia.
- p = q AND r.

Con el modelo estándar:

**grado de p = min(grado de q, grado de r)**

Con el AND geométrico compensatorio:

**grado de p = raíz cuadrada de (grado de q × grado de r)**

### Corrección del apunte

La diapositiva de “Proposiciones compuestas” presenta el máximo para evaluar q AND r. Esto contradice las definiciones anteriores:

- mínimo es el AND estándar;
- máximo es el OR estándar.

---

## 12. Árboles de proposiciones

Un árbol representa una proposición compuesta:

- hojas: proposiciones simples;
- nodos internos: AND, OR, NOT o implicación;
- raíz: proposición final.

Se evalúa desde abajo hacia arriba:

1. calcular el grado de cada hoja;
2. aplicar cada operador;
3. enviar el resultado al nodo superior;
4. obtener en la raíz el grado final.

La estructura importa:

**a AND (b OR c)** no es igual a **(a AND b) OR c**.

El árbol elimina ambigüedades y muestra qué operación se realiza primero.

---

## 13. Ejemplo completo del candidato

Proposición:

**“El candidato es apropiado cuando es joven, tiene buena formación o experiencia en el tema, y se expresa correctamente”.**

Proposiciones:

- j: es joven;
- f: tiene buena formación;
- e: tiene experiencia;
- w: se expresa correctamente.

Estructura:

**p = j AND (f OR e) AND w**

Valores del apunte:

- j = 0,75;
- f = 0,92;
- e = 0,23;
- w = 0,66.

### Paso 1: f OR e

Con el dual geométrico:

**f OR e = 1 − raíz cuadrada de ((1−0,92) × (1−0,23)) ≈ 0,752**

### Paso 2: AND de los tres criterios

**p = raíz cúbica de (0,75 × 0,752 × 0,66) ≈ 0,719**

El candidato resulta apropiado con grado aproximado **0,72** bajo ese modelo.

### Inconsistencia numérica del apunte

La diapositiva muestra 0,73 como valor intermedio, aunque la fórmula con 0,92 y 0,23 da 0,752. Si se usa 0,73, el resultado final ronda 0,71, como figura allí. El procedimiento es correcto, pero los valores impresos no son completamente coherentes. Aquí se corrigió el cálculo.

---

## 14. Reglas difusas

Forma general:

**SI x es A Y/O y es B, ENTONCES z es C.**

- **Antecedente:** condiciones posteriores a SI.
- **Consecuente:** conclusión posterior a ENTONCES.
- **Fuerza de activación:** grado obtenido al evaluar el antecedente.

Tanto el antecedente como el consecuente contienen proposiciones difusas:

- “x es A”;
- “y es B”;
- “z es C”.

Ejemplo:

**SI temperatura es ALTA Y humedad es ALTA, ENTONCES ventilador es RÁPIDO.**

Si los antecedentes valen 0,8 y 0,6:

- AND mínimo: 0,6;
- AND producto: 0,48;
- AND geométrico: aproximadamente 0,693.

---

## 15. Relación con Mamdani

Un sistema Mamdani completo suele seguir:

1. **Fuzzificación:** convierte entradas numéricas en grados.
2. **Evaluación de reglas:** obtiene la fuerza de los antecedentes.
3. **Implicación y agregación:** modifica y combina los conjuntos difusos de salida.
4. **Defuzzificación:** convierte la salida difusa en un valor numérico.

Ejemplo:

**SI temperatura es ALTA, ENTONCES ventilador es RÁPIDO.**

En Mamdani, RÁPIDO es un conjunto difuso. Si el antecedente vale 0,7, ese grado se utiliza para limitar o escalar dicho conjunto, según el operador elegido.

El apunte desarrolla sobre todo las bases de las primeras etapas: funciones, proposiciones, operadores y árboles.

---

## 16. Fuzzy Tree Studio

Es una herramienta desarrollada conjuntamente por la Universidad Nacional de Mar del Plata y la Universidad CAECE. Permite construir y evaluar árboles de proposiciones para soporte de decisiones.

### 16.1. Elementos

Proposiciones simples:

- variable difusa;
- etiqueta;
- valor numérico continuo.

Proposiciones compuestas:

- AND;
- OR;
- NOT;
- implicación.

### 16.2. Flujo de trabajo

1. Construir gráficamente el árbol.
2. Definir propiedades y funciones.
3. Seleccionar un conjunto de datos.
4. Elegir uno o más modelos de operadores.
5. Evaluar el diagrama.
6. Examinar grados intermedios y finales.

### 16.3. Modelos mostrados

| Modelo | AND | OR |
|---|---|---|
| Estándar / Máx-Mín | mínimo | máximo |
| Probabilístico / Algebraico | producto | suma probabilística |
| GMBCL | media geométrica | dual geométrico |
| AMBCL | compensación basada en media aritmética | dual correspondiente |
| Personalizado | definido por el usuario | definido por el usuario |

La comparación permite estudiar cuánto depende la decisión de los operadores elegidos.

### 16.4. Resultados

Puede mostrar:

- entradas;
- grados de nodos intermedios;
- resultado final;
- comparación entre modelos;
- árbol coloreado por grados;
- cuantificadores.

En el gráfico mostrado, amarillo representa valores bajos y rojo valores altos.

### 16.5. Cuantificadores

Para un conjunto finito de casos, en el modelo estándar:

- grado de “existe un caso que cumple p” = máximo de todos los grados;
- grado de “todos los casos cumplen p” = mínimo de todos los grados.

Otros modelos pueden usar agregaciones alternativas.

---

## 17. Ejemplo del material: recomendación de emergencia

Proposición:

**“El paciente debe llamar a emergencias cuando tiene fiebre alta y además presenta tos, dolor de garganta o dificultad para respirar”.**

- f: fiebre alta;
- t: tos;
- g: dolor de garganta;
- r: dificultad para respirar.

Estructura:

**p = f AND (t OR g OR r)**

Primero se combinan los síntomas alternativos mediante OR. Luego el resultado se combina con fiebre mediante AND.

Es un ejemplo académico de soporte de decisiones, no una regla médica validada.

---

## 18. Aplicación: presión arterial

### 18.1. Clasificación nítida de referencia

| Categoría | Sistólica | Relación | Diastólica |
|---|---:|---|---:|
| Normal | menor que 120 | Y | menor que 80 |
| Elevada | 120 a 129 | Y | menor que 80 |
| Hipertensión grado 1 | 130 a 139 | O | 80 a 89 |
| Hipertensión grado 2 | 140 o más | O | 90 o más |
| Hipertensión severa | mayor que 180 | Y/O | mayor que 120 |

El problema es que mediciones casi iguales pueden quedar en categorías diferentes. Fuzzificar suaviza las fronteras sin eliminar las categorías.

> Modelo exclusivamente didáctico; no sirve para diagnosticar ni indicar tratamientos.

### 18.2. Variables

- S: presión sistólica en mmHg.
- D: presión diastólica en mmHg.

### 18.3. Etiquetas

Para S: normal, elevada, grado 1, grado 2 y severa.

Para D: normal, grado 1, grado 2 y severa.

ELEVADA no necesita una etiqueta diastólica propia: requiere sistólica elevada y diastólica normal.

### 18.4. Funciones propuestas

| Etiqueta | Transición ilustrativa |
|---|---|
| Sistólica normal | 1 hasta 115; baja a 0 entre 115 y 125. |
| Sistólica elevada | sube entre 115 y 120; vale 1 hasta 129; baja a 0 en 135. |
| Sistólica grado 1 | sube entre 125 y 130; vale 1 hasta 139; baja a 0 en 145. |
| Sistólica grado 2 | sube entre 135 y 145; permanece alta hasta acercarse a 180. |
| Sistólica severa | crece desde 175 y llega a 1 cerca de 185. |
| Diastólica normal | 1 hasta 75; baja a 0 entre 75 y 85. |
| Diastólica grado 1 | sube entre 75 y 80; vale 1 hasta 89; baja a 0 en 95. |
| Diastólica grado 2 | sube entre 85 y 95; permanece alta hasta acercarse a 120. |
| Diastólica severa | crece desde 115 y llega a 1 cerca de 125. |

Son funciones trapezoidales o de hombro superpuestas. Los valores deben validarse con especialistas en una aplicación real.

### 18.5. Árboles de clasificación

Con mínimo y máximo:

- NORMAL = sistólica normal AND diastólica normal.
- ELEVADA = sistólica elevada AND diastólica normal.
- GRADO 1 = sistólica grado 1 OR diastólica grado 1.
- GRADO 2 = sistólica grado 2 OR diastólica grado 2.
- SEVERA = sistólica severa OR diastólica severa.

En grados:

- normal = mínimo(normal sistólica, normal diastólica);
- elevada = mínimo(elevada sistólica, normal diastólica);
- grado 1 = máximo(grado 1 sistólica, grado 1 diastólica);
- grado 2 = máximo(grado 2 sistólica, grado 2 diastólica);
- severa = máximo(severa sistólica, severa diastólica).

Se usa AND en NORMAL y ELEVADA porque deben cumplirse ambas condiciones. Se usa OR en hipertensión porque cualquiera de las mediciones puede ubicar el caso en la categoría mayor.

### 18.6. Ejemplo: 128/82 mmHg

Con las funciones anteriores:

- sistólica elevada = 1;
- diastólica normal = 0,3;
- sistólica grado 1 = 0,6;
- diastólica grado 1 = 1;
- grado 2 = 0;
- severa = 0.

Resultados:

- NORMAL = 0;
- ELEVADA = min(1; 0,3) = 0,3;
- GRADO 1 = max(0,6; 1) = 1;
- GRADO 2 = 0;
- SEVERA = 0.

El caso conserva pertenencia parcial a ELEVADA por estar cerca de la frontera, pero GRADO 1 predomina debido al valor diastólico.

Un sistema podría mostrar todos los grados, elegir el mayor o aplicar una política conservadora que priorice riesgo. En medicina real también deben considerarse mediciones repetidas, técnica, síntomas, antecedentes y criterio profesional.

---

## 19. Metodología para diseñar un sistema difuso

1. Definir el problema y la salida.
2. Identificar variables de entrada.
3. Definir universos de discurso.
4. Elegir etiquetas lingüísticas.
5. Diseñar funciones de pertenencia.
6. Escribir proposiciones o reglas.
7. Construir el árbol respetando los paréntesis.
8. Elegir operadores.
9. Evaluar casos normales y fronterizos.
10. Comparar modelos.
11. Validar con datos y expertos.
12. Ajustar funciones, reglas y parámetros.

Los casos fronterizos son especialmente importantes, porque allí se aprecia la ventaja frente a los umbrales rígidos.

---

## 20. Ventajas y limitaciones

### Ventajas

- Representa conceptos graduales.
- Evita saltos artificiales.
- Expresa conocimiento en reglas comprensibles.
- Combina criterios cualitativos y cuantitativos.
- Puede producir modelos interpretables.
- Es útil en control y soporte de decisiones.

### Limitaciones

- Las funciones y reglas deben diseñarse.
- La elección de operadores afecta el resultado.
- Puede reproducir errores o sesgos expertos.
- Necesita validación en el dominio.
- Un grado final no prueba que una decisión sea correcta.
- En ámbitos críticos debe apoyar, no reemplazar, al profesional.

### Aplicaciones

- control de temperatura, velocidad, frenado o climatización;
- evaluación multicriterio;
- diagnóstico asistido;
- riesgo;
- procesamiento de imágenes;
- calidad;
- selección de candidatos;
- recomendación;
- gestión ambiental;
- automatización industrial.

---

## 21. Errores frecuentes

1. **Confundir grado y probabilidad.** El grado mide compatibilidad, no probabilidad.
2. **Creer que 0,5 significa desconocimiento.** Puede ser pertenencia intermedia.
3. **Usar máximo para AND estándar.** AND usa mínimo; OR usa máximo.
4. **Creer que existe un único operador.** Hay varias familias.
5. **Ignorar paréntesis.** Cambia la estructura del árbol.
6. **Evitar todo solapamiento.** Puede reintroducir saltos.
7. **Elegir funciones solo por su aspecto.** Deben representar y validar el dominio.
8. **Tomar el resultado como verdad absoluta.** Depende del modelo diseñado.
9. **Confundir fuzzificación y defuzzificación.** La primera obtiene grados desde entradas; la segunda obtiene un valor desde una salida difusa.

---

## 22. Respuestas a la autoevaluación

### 1. ¿Qué se generaliza al pasar de lógica booleana a difusa?

Se generaliza el dominio de verdad desde {0, 1} a [0, 1]. También se generaliza la función característica de un conjunto: en vez de indicar únicamente pertenencia o no pertenencia, asigna un grado. Por último, los operadores booleanos se extienden mediante funciones aritméticas, como t-normas, s-normas y negaciones. Para entradas 0 o 1 deben conservar el comportamiento booleano.

### 2. Defina un conjunto difuso y lo necesario para determinarlo

Un conjunto difuso A sobre un universo X asigna a cada elemento x un grado μA(x) entre 0 y 1. Para determinarlo se especifican el universo, la variable, la etiqueta lingüística, la forma de la función de pertenencia y sus parámetros. El grado indica cuánto se ajusta el elemento al concepto. La función puede basarse en expertos, normas, datos o aprendizaje y debe validarse.

### 3. Indique una regla difusa genérica y sus partes

**SI x es A Y y es B, ENTONCES z es C.**

El antecedente contiene las proposiciones difusas “x es A” y “y es B”, unidas mediante AND. El consecuente es la proposición difusa “z es C”. El grado del antecedente determina la fuerza de activación de la regla y la contribución del consecuente.

---

## 23. Repaso final

- La lógica difusa utiliza grados entre 0 y 1.
- Un conjunto difuso se define mediante una función de pertenencia.
- Pertenencia y verdad proposicional son dos lecturas del mismo grado.
- Un grado no es una probabilidad.
- Las etiquetas lingüísticas representan conceptos como BAJO, MEDIO y ALTO.
- Las funciones pueden ser triangulares, trapezoidales, gaussianas o sigmoidales, entre otras.
- AND, OR, NOT e implicación poseen extensiones numéricas.
- El modelo estándar usa AND = mínimo, OR = máximo y NOT = 1 − a.
- Producto/suma algebraica y las lógicas compensatorias son alternativas.
- Los árboles se evalúan desde las hojas hacia la raíz.
- Una regla tiene antecedente, consecuente y fuerza de activación.
- Fuzzy Tree Studio permite construir árboles y comparar modelos.
- Mamdani agrega las salidas de reglas y luego defuzzifica.
- El resultado depende de funciones, operadores, reglas y estructura.

---

## Fuentes

- Gustavo Javier Meschino, *Lógica proposicional. Sistema de inferencia difusa - Mamdani*, material de la asignatura.
- American Heart Association, [Understanding Blood Pressure Readings](https://www.heart.org/en/health-topics/high-blood-pressure/understanding-blood-pressure-readings), usada como referencia para el ejemplo didáctico de presión arterial.

