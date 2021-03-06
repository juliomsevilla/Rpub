# Instalación de R, RStudio y librerias {#install}

## Instalación de R
R funciona bajo Windows, Linux, Mac o Solaris. Para instalar R accederemos a su página (en este caso, un mirror de España): [http://cran.es.r-project.org/](http://cran.es.r-project.org/) y descargaremos la versión adecuada a nuestro sistema operativo.

En el caso de Windows, la instalación es muy sencilla y solo deberemos seguir los pasos que se nos indica. Si todo ha ido correctamente, cuando pulsemos sobre el icono de R, se abrirá su espartana interfaz en la que, además de la barra de herramientas, destaca la consola donde escribiremos y ejecutaremos nuestro código.

Algo bastante interesante de R es su portabilidad. R, una vez instalado en un PC puede funcionar de forma autónoma al mismo. Por ello, una simple copia del directorio donde lo hayamos instalado y su posterior "pegado" en una memoria flash, nos permitirá ejecutarlo en cualquier lugar, llevándonos así nuestra configuración personal, paquetes, entornos y demás.

## Actualización de R
Cada cierto tiempo es recomendable realizar la actualización de R. Generalmente, un par de veces al año, el sistema es actualizado, misión que lleva a cabo un reducido grupo de especialistas (conocido como el R Core team) y los paquetes (que en próximos capítulos explicaremos) se adaptan a la nueva actualización, dejando, algunas veces de ser útiles en las versiones obsoletas.

La actualización de R puede ser automatizada o realizarse de forma manual si bien este último recurso no es la mejor opción debido a que se actualizará creando una nueva instalación manteniendo la anterior. Este echo se debe a que en la actualidad es la única forma de que no perdamos nuestras configuraciones y, sobre todo, la posible incompatibilidad con alguno de los paquetes que tengamos instalados.Para realizar una actualización automática del sistema, podemos usar la siguiente sentencia usando el paquete `installr` [@R-installr] (despues veremos el lugar de ejecutarla):


```r
if(!require(installr)) {
  install.packages("installr"); require(installr)} 
 
updateR()
```


## El Sistema R
Una vez instalamos R, nos encontramos con una interfaz gráfica de usuario que nos puede resultar "anticuada" sobre todo si trabajamos con los sistemas operativos más recientes. Este aspecto no debe confundirnos de cuál es la visión del sistema R: un lenguaje de programación con una clara vocación estadístico-matemática.

![](C:/TEMP/rpub2/images/R_startup.png)

Dentro de R encontramos una pantalla situada a la izquierda (por defecto) en la que en el prompt, escribiremos los comandos a ejecutar. Los resultados de estos comandos aparecerán a continuación de los mismos en este mismo sector. En esta pantalla, aparece también la versión de R que tenemos instalada, y ciertos comandos como la forma de consultar la ayuda (`help()`) o ejemplos básicos de trabajo con R (`demo()`).

A la derecha, en su momento, aparecerá la pantalla de visualización de los gráficos resultantes de los comandos que programemos.

Finalmente, en la pantalla superior, se nos muestra la línea de herramientas, con una cantidad muy reducida de opciones para un software actual. Entre estas opciones, las más usuales son las de abrir y guardar nuestros códigos (en un formato nativo de extensión .R) o nuestros espacios de trabajo, para que la próxima vez que iniciemos R lo hagamos con la sesión anterior (se guarda en un formato propio con extensión .RData). Evidentemente también existen las opciones de utilización de portapapeles (copiar y pegar) y podremos definir el aspecto visual de nuestro software.

Asimismo, existe una opción de una importancia capital en R: Packages y que requiere un capítulo aparte.

## Las librerias de R

Vamos a banalizar el sistema R: cuando instalamos R tenemos una cajón "vacío", si podremos guardar cosas, pero poco más. Ahora bien, para nuestro cajón existen accesorios que los completan y lo hacen más útil y versátil, por ejemplo un separador para bolígrafos. Pues bien, este separador "especializado" sería una librería o paquete. Y aquí radica la potencia de R: cuando nos enfrentemos a un problema, seguramente alguien ya se habrá enfrentado y encontraremos un paquete que realice la función que necesitemos (actualmente existen más de 7.500 disponibles). Se pueden consultar todos los disponibles en el repositorio oficial de paquetes de R conocido por el nombre CRAN (Comprehensive R Archive Network): [https://cran.r-project.org/web/packages/](https://cran.r-project.org/web/packages/).

El sistema base de R contiene el paquete básico que se requiere para su ejecución y la mayoría de las funciones fundamentales. Los otros paquetes contenidos en la “base” del sistema incluye a `utils`, `stats`, `datasets`, `graphics`, `grDevices`, `grid`, `tools`, `parallel`, `compiler`, `splines`, `tcltk` y `stats4`.

Para comenzar, vamos a ver la lista de paquetes que tenemos instalados escribiendo `library()` en la pantalla de código. Si deseamos instalar un paquete que no tengamos tenemos la opción de hacerlo desde Packages>Install Package(s) eligiendo previamente un mirror de descarga, o bien escribiendo en la consola el comando `install.packages (“nlme”, dep = T)`. nlme es un fantástico paquete dedicado a modelos mixtos lineales y no lineales [@R-nlme] y dep=T, le indica a R que instale cualquier otro paquete que sea necesario para el correcto funcionamiento del paquetes principal a instalar).

Finalmente, existe una opción más tediosa, a través de un zip local. Si nuestro paquete, por la razón que sea, no está en un repositorio web de R, podremos instalarlo desde nuestro ordenador mediante Packages>Install package(s) from local zip file... Finalmente no queda más que cargar el paquete deseado y empezar a trabajar con él. Para ello, escribiremos el comando `library (nlme)` y, automáticamente se cargará (y sus paquetes dependientes si lo necesita). 

Todos los paquetes de R están perfectamente documentados según un estándar de la comunidad y si esto no es poco, los paquetes más importantes disponen de incluso bibliografía especifica que en muchas ocasiones los creadores del paquete escriben para facilitar su aprendizaje. Estos manuales están a la venta en las librerías en formato papel y las más de las veces son descargables de forma gratuita (como ejemplo valga [http://www-bcf.usc.edu/~gareth/ISL/](http://www-bcf.usc.edu/~gareth/ISL/)).

## Interfaces gráficas de R

Como vemos, R no destaca por el aspecto visual de su interfaz gráfica de usuario nativa. Por ello existen toda una serie de "capas" para el mismo que enriquecen la experiencia del usuario tanto desde el punto de vista de su aspecto visual como desde el punto práctico. En este punto, encontramos ejemplos como [RKWard](https://rkward.kde.org/) [Rattle](http://rattle.togaware.com/) o [Deducer](http://www.deducer.org/), pero quizas los más destacados sean [R Commander](http://socserv.mcmaster.ca/jfox/Misc/Rcmdr/) y sobre todo [RStudio](http://rstudio.org/) que se ha convertido casi en el hermano gemelo de R.

### Rcommander

Rcommander [@R-Rcmdr] es una interfaz gráfica de R, diseñada para realizar los trabajos estadísticos y analíticos más comunes sin la necesidad de dominar el lenguaje R. En simples palabras convierte el sistema R en un software "estadístico" tradicional. Sin duda, si nuestro propósito es realizar análisis sencillos o buscamos algo rápido, Rcommander es el ganador.

Rcommander se instala como cualquier paquete, por ejemplo mediante el comando `install.packages (“Rcmdr”)` y lo cargaremos con `library(Rcmdr)`.

![](C:/TEMP/rpub2/images/Rcmdr-screenshot.jpg)

### RStudio

RStudio es un entorno de desarrollo integrado (IDE) para R y es un paso más allá de Rcommander. En concreto y según la definición de sus autores se trata de una consola, editor de sintaxis que apoya la ejecución de código, así como herramientas para el trazado, la depuración y la gestión del espacio de trabajo, es decir un completo gestor del entorno R que se ha convertido en parte inseparable del mismo: si alguien usa R seguro, que con un 95% de probabilidad lo hace con RStudio.

![](C:/TEMP/rpub2/images/rstudio-windows.png)

La instalación de RStudio se realiza desde su página web [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/) y no difiere de una instalación estándar de los sistemas operativos habituales.

Su uso es muy sencillo y lo iremos descubriendo a lo largo de estas notas. Básicamente  se compone de cuatro ventanas configurables por el usuario donde se escriben todas las operaciones, se muestran nuestras "tablas de datos", los resultados gráficos y numéricos, se facilita la gestión del histórico, instalación y carga de paquetes,... en fin un largo etcétera que hace más sencilla la creación de soluciones en el sistema R. Una de las grandes ventajas de RStudio es la existencia de un editor de sintaxis que apoya la ejecución de código, facilitando la escritura del mismo y ayudando a recordar los innumerables comandos y funciones. Por otro lado, el trabajar con los proyectos de Rstudio, nos facilitará tener almacenado todo nuestro trabajo para recuperarlo cada vez que queramos, despreocupándonos de los ficheros origen de datos.
