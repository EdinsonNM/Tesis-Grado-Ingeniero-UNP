# BERTScore

## Definicion

Metrica automatica de evaluacion de texto que compara una respuesta generada con una referencia usando embeddings contextuales.

## Uso posible en la tesis

Puede ayudar a medir [[Coherencia conversacional]] o similitud semantica entre respuesta generada y respuesta esperada cuando no basta la coincidencia textual exacta.

## Ventaja

Tolera parafrasis. Esto es util porque dos respuestas pueden decir lo mismo con palabras distintas.

## Limitacion

No garantiza verdad factual. Una respuesta semanticamente parecida puede contener un dato incorrecto. Por eso debe complementarse con [[Ground truth]] y medicion de [[Tasa de alucinacion]].

## Conceptos relacionados

- [[IQCR]]
- [[Coherencia conversacional]]
- [[Exactitud de respuesta]]

