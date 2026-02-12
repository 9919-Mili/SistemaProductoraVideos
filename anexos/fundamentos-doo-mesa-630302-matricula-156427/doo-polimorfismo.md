# Polimorfismo

_Explicación de Polimorfismo como principio y su importancia en el diseño orientado
a objetos. Cómo se relaciona con los principios SOLID y los patrones de diseño_

El polimorfismo es la capacidad de los objetos de diferentes clases relacionadas por herencia de responder a la misma operación o método de distintas formas. Esto permite que diferentes tipos de objetos, compartan clases de manera flexible sin atarse ciertos atributos o comportamientos que estan definidos en un clase.

## Ejemplo en el proyecto

Incluir un diagrama UML que muestra cómo la clase o las clases del proyecto se
relacionan entre sí al aplicar abstracción. Incluir una imagen incrustada, así como el
enlace correctamente referenciado para ver el diagrama en detalle. Describe cómo
el diagrama de las clases seleccionadas refleja el polimorfismo. Incluir
justificación técnica de cómo esas clases seleccionadas del proyecto cumplen
el fundamento.

**Justificación técnica:** Al abstraer el concepto de "archivo" en una clase base, se logra polimorfismo que permite que `Etapa` trabaje con cualquier tipo de `Archivo` sin depender de implementaciones específicas. Esto cumple con el Principio de Inversión de Dependencias (DIP), donde `Etapa` depende de la abstracción `Archivo` en lugar de clases concretas.

## Ejemplo de Código

Incluir un fragmento de código que demuestre la implementación de polimorfismo en
el proyecto (puede ser pseudocódigo o un lenguaje como C#, JavaScript, Python o
Java, etc.). Incluir justificación técnica de cómo este fragmento de código
cumple el fundamento