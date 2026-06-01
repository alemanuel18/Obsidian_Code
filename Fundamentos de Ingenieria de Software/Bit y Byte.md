El **byte** es una unidad de información en informática y telecomunicaciones compuesta por 8 bits. Cada bit corresponde a un lugar en una tabla binaria. Aunque no hay un símbolo universal para representar el byte, se usa “B” en países de habla inglesa y “o” en países de habla francesa. Además, se le conoce indistintamente como “octeto”.

![](https://static.platzi.com/media/user_upload/imagen1-28893471-cab6-4355-931d-a64879100023.jpg)

# ¿Para qué sirve un byte?

El **byte** es utilizado para medir la capacidad de almacenamiento de un dispositivo o la cantidad de información que se transmite por segundo en una red, lo que significa que puede representar 256 combinaciones diferentes de ceros y unos.

Por ejemplo, si tienes un archivo de 1 megabyte, esto significa que estás almacenando aproximadamente 1 millón de bytes de información. Además, la capacidad de almacenamiento de un dispositivo se mide en términos de bytes, por lo que es importante conocer la cantidad de bytes que necesitas para almacenar tus archivos y programas.

Los bytes también son fundamentales para la **representación de caracteres** a través de la tabla ASCII, donde cada símbolo (letras, números, caracteres especiales) tiene asignado un número específico. Por ejemplo, el símbolo @ corresponde al número 64 en esta tabla.

# Historia del byte

El concepto que conocemos como byte comenzó a emplearse en la década de 1950 como una unidad de almacenamiento de información en los primeros ordenadores.

Originalmente, un byte estaba compuesto por cualquier número de bits necesarios para representar un único carácter alfanumérico, como una letra o un número. Sin embargo, **en la década de 1960 se estandarizó en 8 bits por byte.  
**  
Esta estandarización tiene raíces históricas conectadas con IBM, una de las empresas pioneras en la computación moderna. Los procesadores se diseñaron con 8 cables internos para realizar cálculos simultáneamente, siendo la forma más eficiente y económica de fabricarlos. Curiosamente, los procesadores soviéticos en los años 70 utilizaban sistemas de 12, 18, 24 o 48 bits, lo que hacía que sus computadoras no fueran compatibles con las occidentales.

# ¿Qué es un bit?

El **bit** es la unidad mínima de información que se emplea en informática, este puede tener dos estados: uno o cero y comúnmente están asociados a que un dispositivo se encuentre apagado o encendido. Proviene del funcionamiento del transistor, lo que quiere decir que tiene un impulso eléctrico o no lo tiene.

**Representa la contraposición entre dos valores:**

- 0 y 1
- Apagado y encendido
- Falso y verdadero
- Abierto y cerrado

![](https://static.platzi.com/media/user_upload/imagen0-280287cf-d1e9-4672-b0a8-9ff94606a67f.jpg)

En los circuitos eléctricos, estos bits se representan mediante niveles de voltaje: un nivel alto (5V) representa un uno, mientras que un nivel bajo (0V) representa un cero. Estas transiciones entre niveles ocurren en intervalos precisos, cuya duración depende de la velocidad del procesador.

Comprender el funcionamiento de los bits nos permitirá realizar conteos u operaciones matemáticas en un sistema que entienden las computadoras: [el sistema binario](https://platzi.com/clases/3221-pensamiento-logico/50671-que-es-el-sistema-binario/). Este tipo de numeración nos permite codificar valores como números, letras o imágenes por series de unos y ceros. Las series de unos y ceros después serán decodificadas para ser interpretadas en una forma más sencilla y menos abstracta.

También los unos y ceros se podrían agrupar en diferentes longitudes, pero el estándar de agrupación es de una longitud de ocho valores, dando nacimiento a un nuevo concepto: el byte.

# ¿Cuántos bits tiene un byte?

**Un byte tiene 8 bits y puede tomar valores entre cero y 255**. Cada uno de estos, representa algún tipo específico de valor y para conocerlo, usamos la tabla ASCII. Cada archivo de texto, cada imagen, cada canción que está en nuestra computadora tiene un peso en bytes, que depende de la cantidad de información que contiene.

![](https://static.platzi.com/media/user_upload/2018-12-19_14-59-36-9d0311c0-7788-4b3a-a1c0-eb9536f2895d-7c0299e8-a386-4343-9ce5-7f861ac7d9cb.jpg)

Los bytes están presentes en nuestra vida digital cotidiana. Por ejemplo, las direcciones IP como 192.168.1.1 son combinaciones de 4 bytes (por eso ningún número supera el 255). Las imágenes digitales son grupos de bytes organizados en cuadrículas donde cada píxel tiene un color determinado por la intensidad de rojo, verde y azul. Incluso los emojis requieren 4 bytes para ser representados en el estándar Unicode.

Un dato interesante es que Sebastián Delmont, venezolano y antiguo miembro del equipo Platzi, fue responsable de integrar el emoji de la arepa al estándar UTF 🫓

# ¿Cuál es el bit más significativo?

Los bits dentro de un byte poseen diferentes valores que van incrementando de acuerdo a su posición. El bit dentro de un byte con el valor más alto se le conoce como el bit más significativo o _**Most Significant Bit (MSB)**_ por sus siglas en inglés. Este suele ser por convención el bit del extremo izquierdo.

![](https://static.platzi.com/media/user_upload/imagen2-59efa6e0-9383-417a-a4da-ebd13f095756.jpg)

Tabla de equivalencia de bytes, Kilobytes, Megabytes y Gigabytes

Medida

Equivalencia

1 byte

8 bits

1 Kilobyte

1024 Bytes

1 Megabyte

Son 1024 Kilobytes

1 Gigabyte

1024 Megabytes

1 Terabyte

1024 Gigabytes

Valor total de un byte

Para conocer el **valor total de un byte** solo se necesita hacer la suma de los bits que tiene activos (que están en uno) para determinar su valor. Si sumas todos los valores dentro de un byte te darás cuenta de que el valor máximo que puede tener es de 255.

![](https://static.platzi.com/media/user_upload/imagen4-a30dfa10-b313-4cb5-8222-8f970d371a7c.jpg)

¿Qué otros sistemas numéricos se utilizan en programación?

Aunque estamos acostumbrados al sistema decimal (base 10), en programación se utilizan varios sistemas numéricos:

- **Binario** (base 2): Solo utiliza 0 y 1.
- **Hexadecimal** (base 16): Utiliza dígitos del 0 al 9 y letras de la A a la F para representar valores del 0 al 15.

El sistema hexadecimal es especialmente útil en programación porque permite representar valores binarios de forma más compacta. Por ejemplo, un byte (8 bits) puede representarse con solo dos dígitos hexadecimales.

La estandarización de estos sistemas es crucial para la interoperabilidad de nuestros dispositivos. El **Unicode Consortium** es el organismo internacional que regula las equivalencias entre números y símbolos, asegurando que cuando enviamos un mensaje desde cualquier dispositivo, se interprete correctamente en el receptor.

En conclusión, desde mensajes simples hasta complejas imágenes y emojis, todo lo que vemos en nuestros dispositivos digitales está construido sobre la sencilla pero poderosa base de los bits y bytes. Entender estos conceptos nos brinda una nueva perspectiva sobre la tecnología que usamos todos los días.