Contar con varias terminales abiertas al mismo tiempo puede aumentar significativamente tu productividad, especialmente cuando trabajas en entornos remotos sin interfaz gráfica. Para facilitar esta tarea, _Tmux_ es un comando especial que permite gestionar múltiples paneles y ventanas en una única terminal, brindando una experiencia de trabajo más eficiente.

# ¿Qué es Tmux y cómo funciona?

_Tmux_ es una herramienta poderosa que facilita el trabajo simultáneo en varias terminales dentro de una sola ventana. Trabaja mediante lo que se denomina "prefijo", una combinación de teclas específica (generalmente `control+b`), seguida de ciertos comandos para realizar diversas acciones, tales como:

- División vertical (`control+b` seguido de `%`).
- División horizontal (`control+b` seguido de `"`).
- Abrir nuevas ventanas (`control+b` seguido de la tecla `c`).
- Cambiar entre ventanas (prefijo seguido del número índice de la ventana).
- Renombrar ventanas (`control+b` seguido de `,`).

# ¿Cómo instalar Tmux en tu sistema?

Puedes instalar _Tmux_ fácilmente con las siguientes instrucciones según tu sistema operativo:

- Para sistemas basados en Linux:
    
    `sudo apt install tmux`
    
- Para sistemas Mac, usa _Homebrew_:
    
    `brew install tmux`
    

# ¿Cómo manejar paneles y ventanas en Tmux?

Cuando estás trabajando con _Tmux_, llamarás al "prefijo" presionando simultáneamente las teclas `control+b`, lo sueltas, y luego realizas las siguientes acciones:

- **Crear un panel vertical:** presiona `shift + 5 [%]`.
- **Crear un panel horizontal:** presiona `shift + " ["]`.
- **Cerrar un panel activo:** escribe `exit` o usa la combinación `control+d`.
- **Moverse entre paneles:** después del prefijo, utiliza las teclas de flecha para navegar.

Además, las ventanas adicionales dentro de _Tmux_ te permiten organizar mejor tus tareas. Para crear una ventana nueva, utiliza `control+b` seguido de `c`. Para renombrar una ventana existente, usa `control+b` seguido de una coma `,`.

# ¿Cómo gestionar sesiones en segundo plano con Tmux?

Una característica especial de _Tmux_ es su habilidad para mantener en segundo plano las sesiones y paneles activos. Si cierras la terminal o detienes abruptamente tu trabajo, puedes recuperar tus procesos exactamente desde donde los dejaste copiando el siguiente flujo:

- Revisa qué sesiones están activas usando:
    
    `tmux ls`
    
- Para volver a reanudar una sesión previamente creada, utiliza:
    
    `tmux attach`
    

De esta manera, todas las ventanas y paneles estarán disponibles y funcionando tal como los habías configurado previamente, permitiéndote retomar actividades rápidamente y sin complicaciones.