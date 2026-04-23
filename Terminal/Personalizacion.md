Optimizar tu terminal es fundamental para mejorar tu productividad en actividades de desarrollo y administración de sistemas. Usando ZSH, junto con los temas Oh My ZSH y Powerlevel10k, lograrás personalizar tu espacio de trabajo digital al máximo, haciendo tu trabajo diario más cómodo y ágil.

# ¿Qué es ZSH y por qué deberías instalarla?

ZSH es una alternativa potente a la shell predeterminada (generalmente Bash) en sistemas basados en Unix. Al instalar ZSH obtienes funcionalidades avanzadas como:

- Autocompletado más eficiente.
- Personalización extensa de funciones.
- Soporte mejorado para scripts y plugins avanzados.

Para instalar ZSH ejecuta en tu terminal:

`sudo apt install zsh`

Luego, asegúrate de establecer ZSH como tu shell predeterminada.

# ¿Cómo mejora Oh My ZSH la experiencia de uso de tu terminal?

Oh My ZSH es un conjunto de scripts que aumentan considerablemente tu productividad en la terminal. Al instalarlo, consigues:

- Autocompletados inteligentes.
- Amplio rango de colores y caracteres especiales.
- Posibilidad de trabajar de manera rápida y ordenada.

Instalar Oh My ZSH es sencillo, copiando y ejecutando su script de instalación desde su web oficial:

`sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

# ¿Qué valor añade el tema Powerlevel10k?

Powerlevel10k es un tema avanzado que lleva la personalización de tu terminal a otro nivel, ofreciendo:

- Visualización de símbolos especiales y personalizables.
- Configuración detallada y adaptada a tus necesidades específicas.
- Representación visual clara de ramas Git, hora, sistema operativo y mucho más.

# Instalación de fuentes recomendadas

Antes de activar Powerlevel10k, instala previamente la fuente Meslo NerdFont para visualizar correctamente iconos y símbolos específicos:

1. Descarga las fuentes recomendadas desde el repositorio oficial.
2. Instálalas en tu sistema operativo mediante selección y opción instalar.

Activación del tema Powerlevel10k

Clona el repositorio en tu carpeta de Oh My ZSH:

`git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k`

Modifica el archivo `.zshrc` ubicando la variable `ZSH_THEME` y ajustándola a:

`ZSH_THEME="powerlevel10k/powerlevel10k"`

Finalmente, aplica los cambios en tu archivo de configuración con:

`source ~/.zshrc`

Durante la configuración inicial podrás personalizar cómo se verá exactamente tu terminal según tu gusto personal, mejorando así tu experiencia día a día.