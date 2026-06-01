Al prender tu computadora o teléfono, **una señal eléctrica viaja hacia la tarjeta madre**, dando inicio a una secuencia cuidadosamente coordinada para activar tu dispositivo. Este proceso es fundamental y lo utilizan tanto computadoras como móviles y otros dispositivos cotidianos como televisores inteligentes o relojes.

# ¿En qué consiste el proceso eléctrico inicial al encender un dispositivo?

Al presionar el botón de encendido, la electricidad viaja desde la fuente de energía (batería o conexión a la red) hacia la **tarjeta madre**, principal placa electrónica del dispositivo. Esta electricidad se interpreta como ondas, pulsos altos y bajos, que en lenguaje binario se representan como **ceros (0)** y **unos (1)**, denominados **bits**.

Estos **bits** llegan a un chip especial dentro de la tarjeta madre que ejecuta procesos esenciales al inicio, llamados:

- En computadoras: **UEFI (Unified Extensible Firmware Interface)** o la antigua **BIOS (Basic Input Output System)**.
- En dispositivos Android: **Primary Boot Loader (PBL)**.
- En dispositivos iPhone: **Secure ROM** y posteriormente **iBoot**.

# ¿Qué pasos realiza el sistema antes de abrir el sistema operativo?

Ese primer chip inicial hace una revisión de los componentes y su correcto funcionamiento mediante un procedimiento conocido como **POST (Power On Self Test)**, que verifica:

- Pantalla.
- Teclado.
- Puertos y otros componentes físicos.

Cualquier sonido inusual al inicio indica un fallo detectado por el POST. Si todo está en orden, se procede a buscar en la memoria permanente (disco duro) las instrucciones que iniciarán el sistema operativo.

Esta memoria puede ser:

- Una unidad externa en computadoras grandes.
- Un pequeño chip soldado en dispositivos móviles o portátiles compactos.

# ¿Qué sucede al arrancar el sistema operativo?

Al identificar el código guardado en el disco duro, éste es enviado a la **unidad central de procesamiento (CPU)**, el circuito que ejecuta las órdenes matemáticas y digitales mediante el lenguaje de ensamblaje (_assembler_). Desde aquí se gestionan procesos como imagen, sonido y demás interacciones del dispositivo.

La información generada por esta forma primitiva de instrucciones, esencial para el buen manejo del sistema operativo, es almacenada en la **memoria RAM**, espacio rápido y temporal.

En esta etapa aparece el código central conocido como **kernel**, intermediario crucial del software y hardware que traduce códigos programados específicamente para realizar acciones eficaces según órdenes de usuario.

# ¿Qué papel desempeñan los usuarios y contraseñas en el arranque?

Una vez cargado el kernel, se activan procesos para gestionar seguridad, generando accesos a información privada bajo usuarios y contraseñas. Posteriormente, se configuran periféricos como pantallas usando matrices de puntos luminosos denominados **pixeles**.

Además, por la gran cantidad de dispositivos y periféricos disponibles, **se usan controladores (_drivers_)** que contienen instrucciones específicas para cada hardware y habilitan la comunicación efectiva entre periférico y dispositivo principal.

Tras ingresar usuario y contraseña, un proceso criptográfico permite que la información cifrada sea accesible solo a quien corresponda, garantizando la seguridad y personalización de uso en cada dispositivo.

Esta secuencia básica de arranque es común a tus dispositivos más cercanos como relojes inteligentes, teléfonos móviles y televisores modernos, estableciendo las bases fundamentales para quienes quieran desempeñarse profesionalmente en el ámbito del desarrollo de software y tecnología.