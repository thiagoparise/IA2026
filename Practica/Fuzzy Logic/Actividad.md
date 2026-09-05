# Diagnóstico difuso de hipertensión arterial
En la siguiente infografía se informan criterios para definir la tensión arterial.

Los límites son demasiado estrictos. Intente fuzzificar este concepto con una variable difusa y un árbol básico de proposiciones. 

Defina algunas (o todas) las diferentes clasificaciones. Las proposiciones a evaluar serían "El paciente tiene la presión normal", "El paciente presenta presión elevada", "El paciente es hipertenso grado X", etc.

<img src="PresionArterial2017.jpg" alt="Clasificación de la presión arterial según la Guía AHA 2017" width="500" />

## Resolución:

1. Comenzamos definiendo cuales serán las entradas de nuestro sistema.
    Las mediciones concetras de un paciente:
        - Presión sistólica: PS, por ejemplo de 128 mmHg.
        - Presión diastólica: PD, por ejemplo de 82 mmHg.
    Estos serán valores precisos o crisp.

2. Luego, definimos las variables linguisticas y los términos difusos asociados.

| Variable           | Universo aproximado | Términos difusos posibles                       |
| ------------------ | ------------------: | ----------------------------------------------- |
| Presión sistólica  |         80–250 mmHg | normal, elevada, grado 1, grado 2, severa |
| Presión diastólica |         50–150 mmHg | normal, elevada, grado 1, grado 2, severa |

Cada término tiene su función de pertenencia. Por ejemplo:
    μ(sistólica normal) = f

<img src="pertenencia_sistolica.png" width="500"/>
<img src="pertenencia_diastolica.png" width="500" />


3. Luego, tenemos las proposiciones difusas, que afirman que una variable toma un término linguistico.

    - “La presión sistólica es normal”.
    - “La presión diastólica es normal”.
    - “La presión sistólica es elevada”.

4. Por último, podemos clasificar la situación de un paciente.

    Por ejemplo, para evaluar: p = "La presión del paciente Pérez es normal" = (PS normal) AND (PD normal)

    Y aquí tenemos que utilizar un método para calcular la verisitud de la preposición compuesta.
    Tomaremos 𝝁𝒑 ≡ (𝝁𝑞 x 𝝁𝑟)^1/2 para AND y 𝝁𝒑 ≡ 1 - ((1-𝝁𝑞) x (1-𝝁𝑟))^1/2 para OR.

    Por lo tanto si se midieron la presion sistólica y diastólica de el paciente Perez con valores PS = 128 mmHg y PD = 82

    Evaluamos la preposición

    p = (PS normal) AND (PD normal)

    𝝁PS normal(128) = 0.194
    𝝁PD normal(82) = 0.369

    𝝁𝒑 = (0.194 x 0.369)^1/2 = 0.268

    Por lo tanto "La presión de Pérez es normal" tiene un grado de verdad aproximado de 0.268.