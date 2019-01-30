# README
Proyecto de clasificación de documentos: Tratamiento de datos y metodología

Proyecto de Data Science que he llevado a cabo en una de mis pasantías:

Se trataba de automatizar la clasificación de documentos.
Es decir, que dado un documento se clasificara automáticamente según el tipo que fuera.
Para la explicación, y con fines explicativos, pongamos que la empresa recibía 3 tipos diferentes de documentos: contratos, honorarios y facturas otras.
Por tanto, por ejemplo, si se recibía una factura de un abogado (honorario) tendría que clasificarse dentro de la categoría de honorarios.

Fases del proyecto:

1. Todo el proyecto se desarrollaría en Python.
2. Lectura del documento (normalmente estaban escaneados)
3. Conversión a texto
4. Tratamiento datos (todo a mayúscula, quitar signos raros, etc)
5. ¿Qué palabras buscar?
  5.1. “Train set”: Seleccionar X documentos de cada categoría y sacar las palabras más comunes de cada tipo.
  5.2. Brainstorming
6. Creación del algoritmo
  6.1. Fase I: Aproximación – Propuesta
  6.2. Fase II: Desarrollo completo
7. Validación y Revisión errores
8. Implementación IT

Debido a que me iba a Estados Unidos, no pude acabar todo el proyectoy me quedé en el punto 6, fase I, la aproximación-propuesta de un algoritmo.

Fase 2: La lectura del documento.

La lectura del documento fue un punto que acarreó muchos problemas.
No encontrábamos ninguna librería de Python que leyese realmente bien documentos escaneados, o incluso es escritos a mano.

Problemas: Los documentos estaban escaneados, escritos a mano e incluso girados.
No encontrábamos ninguna librería que leyese mínimamente bien los documentos para pasarlos a texto.

Solución: Decidimos utilizar el algoritmo de lectura de Google (En Google docs) como solución temporal alternativa.
Los documentos girados los trataríamos aparte.

Fase 3: Conversión a texto.

El algoritmo de lectura de Google (Google docs) transformaba el documento con una precisión bastante alta a texto.
Por tanto, nos basamos en los resultados que sacaba dicho algoritmo.

(Nota: Faltaba ver cómo implementar este método al algoritmo que se quería crear)

Fase 4: Tratamiento datos.

Una vez tenía el documento pasado a texto, se tenía que “limpiar”.
Esto quiere decir que aplicamos lo siguiente (en todo el texto):

1. Todo a mayúscula
2. Eliminar las stopwords (a, ahí, acá, etc)
3. Quitar signos raros como: “?¿!¡:+.>>/-–°º,”^#<(”)”*________________”
4. Separar todo el texto con espacios ” “(no saltos de párrafo)
5. Convertirlo en unicode
6. Pasar todo el texto a una lista

No hubieron muchos problemas durante la limpieza de textos.
Al final se consiguió lo que se buscaba. Un texto plano.


Fase 5: ¿Qué palabras buscar?

Esta fase consistía en definir qué palabras debía buscar el algoritmo para hacer la clasificación.
Se hizo mediante dos técnicas: Brainstorming y Buscando las palabras más comunes de cada categoría a partir de los documentos.
Es decir, seleccionar X documentos de cada categoría y sacar las palabras más comunes de cada tipo.
El código para este último punto era algo similar a:

word_counter = collections.Counter(wordcount)
for word, count in word_counter.most_common(text):
    print(word, ": ", count)
    
Una vez acabado este paso, creé una librería con las palabras más frecuentes y que tenían sentido de cada categoría.

Fase 6: Creación del algoritmo.

Fase I: Aproximación – Propuesta

En esta fase ya teníamos el texto trabajado y las palabras que correspondían a las categorías: contratos, honorarios y facturas.
Durante la creación del algoritmo me surgieron bastantes formas de abarcarlo.
Algunos de los inconvenientes los solucioné de la siguiente manera:

1. Necesitaba obtener algunos números con cifras determinadas para una mejor clasificación, como el IBAN, NIF, CIF.
Para extraer estos números específicos sin equivocarme, implementamos una función que, dado una de estas palabras, buscaba el número más próximo que cumpliese con las condiciones que requería esa palabra.

2. En algunos textos, la lectura de los documentos escaneados hacía que determinadas palabras no se separaran:
Por ejemplo: “NIF45634253”. Lo solucioné implementando una función que buscara la palabra dentro de la lista independientemente si seguía de espacio o no.
De ahí agarraba el número que me interesaba.

3. Aquellas palabras o números que no se leían en su totalidad (“IBA”,”CIF34252″, “HONORA“) no se les aplicaba ningún tratamiento específico.
Simplemente no se trataban.

Una vez solucionadas las casuística que me surgieron, se exportaban las documentos a un fichero .csv según a la categoría que perteneciesen.

Fase II: Desarrollo completo

A partir de esta fase yo no continué el proyecto, puesto que me iba a USA a estudiar.
Se pretendía mejorar y optimizar la estructura del algoritmo ya creado y validarlo (ver si realmente clasificaba bien).
Por último, se pretendía implementar de manera automática.
