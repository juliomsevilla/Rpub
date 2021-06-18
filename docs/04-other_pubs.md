# Otras de formas de publicación en R {#other_pubs}

En este capítulo, veremos otras formas de publicar en R pero no las únicas. Si es de interés, recomendamos visitar la web [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/basics.html), donde hay abundante material sobre el tema.

## Notebooks
Un notebook es un documento de RMarkdown que puede ejecutar trozos de código de forma independiente y de forma interactiva. Para crear un documento, lo podremos hacer facilemnte desde RStudio en File>New File>R Notebook. Una vez creado contaremos con un fichero `*.rmd` que contendrá todas nuestras partes de código y texto y que, una vez lo guardemos, nos generará un nuevo fichero, con extensión `*.nb.html` que contendrá el notebook en un formato amigable para ejecutar.

## Presentaciones
Además de generar reportes en pdf, html, docx,..., cuando generamos nuestro fichero `.Rmd` podemos indicarle que la salida sea del tipo presentación. En este caso, cada uno de los títulos que definamos, se convertirá en un slide de la presentación, la cual puede, evidentemente, contener fragmentos de códigos ejecutables, tal y como se han descrito en estos apuntes. Podemos ver un ejemplo de una presentación [en este enlace](https://juliomsevilla.gitlab.io/rsentinel).


## Páginas web y libros
Con Rmarkdown y RStudio, podremos desarrollar páginas web estáticas muy facilmente. Ya hemos visto lo sencillo que es generar un fichero `HTML` por lo que si disponemos de un hospedaje web podremos subirlo y disponibilizarlo de forma pública.

### Bookdown

Una opción que da un paso más allá es la librería `bookdown`. Mediante esta libreria, podremos escribir libros y publicarlos online empleando R Markdown de forma rápida y sencilla, por loq ue se convierte en la forma ideal de generar el documento y, asu vez publicarlo. Para publicarlo, podemos usar repositorios como [Github](https://github.com) o [Gitlab](https://gitlab.com/), que nos ofrecen un almacenamiento gratuito.

Existen varias formas para generar un documento de este tipo, pero sin duda la más sencilla es instalar la libreria con `devtools::install_github('rstudio/bookdown')`, crear un proyecto en RStudio, clonando el repositorio [https://github.com/yihui/bookdown-minimal.git](https://github.com/yihui/bookdown-minimal.git) y, además de generar nuestro contenido deberemos editar la cabecera del fichero `index.Rmd`:


```r
--- 
title: "A Minimal Book Example"
author: "Yihui Xie"
date: "2019-03-25"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
bibliography: [book.bib, packages.bib]
biblio-style: apalike
link-citations: yes
github-repo: rstudio/bookdown-demo
description: "This is a minimal example of using the bookdown package to write a book. The output format for this example is bookdown::gitbook."
---
```

Para publicar el libro en Gitlab a modo de página web, dentro del proyecto, a su vez deberemos crear un fichero `.gitlab-ci.yml` con, al menos el siguiente contenido:


```r
image: rocker/verse:3.4.1

before_script:

pages:
  stage: deploy
  script:
  - Rscript -e "bookdown::render_book('index.Rmd', 'all', output_dir = 'public')"
  artifacts:
    paths:
    - public
  only:
  - master
```

Si deseamos hacer en Github, deberemos realizar lo siguiente:

- Crear el directorio `docs` dentro del repositorio creado
- Incluir dentro del directorio `docs` incluir el contenido de nuestro libro
- Crear dentro del directorio `docs` un archivo `.nojekyll`, que, si estamos en Windows, podremos hacer incluso con el comando de R `file.create('.nojekyll')`.
- Finalmente, en Github, tendremos que decirle que nuestro master branch es `\docs\`:

![](C:/TEMP/rpub2/images/github_bookdown.png)
Otra opción, quizás más sencilla es usar las posibilidades del paquete RStudio Connect `rsconnect`, un producto de RStudio que le permite implementar una variedad de aplicaciones relacionadas con R hacia un servidor, incluyendo documentos R Markdown, aplicaciones Shiny, gráficos de R, etc. Instalando previamente esta librería, podremos subir nuestro nuevo libro digital a los servidores de [bookdown.org](https://bookdown.org/) mediante el comando `bookdown::publish_book("usuario")`, disponiendo en *usuario*, nuestro identificador (si no tenemos cuenta aún, en el proceso, nos facilitará crearla).




### Distill
Si bien `Bookdown` está muy centrado en la redacción científica, el paquete [`Distill`](https://pkgs.rstudio.com/distill/) es multipropósito, y nos servirá para crear facilmente blogs y webs estáticas.

Para ello, instalaremos la susodicha librería (`install.packages("distill")`) y, una vez instalado, desde RStudio, podremos genera un nuevo proyecto de web o blog, mediante File>New Project>New Directory y, de las opciones elegimos Distill Blog o Distill Website

Una vez lo nombremos y lo guardemos en la ruta que elijamos, nos generará varios ficheros tales como el encabezado (`_site.yml`), la portada (`index.Rmd`), poágina de presentación (`about.Rmd`),... así como entradas de blog ficticias o páginas web, que podremos en todos los casos cambiar y reconfigurar.

LA creación o modificación de páginas es muy sencilla, ya que en todo momento usaremos `Rmarkdown`para escribir y posteriormente, para crear la página en lenguaje `html` deberemois "tejer" la misma, mediante el comando `knitr`. Para finalizar y montar la web completa, procedemos a pulsar sobre la pestaña `Build` de RStudio que se encargará de montarlo todo.

Para añadir nuevas páginas o post, en la consola de comandos, deberemos ejecutar `distill::create_post()`con el nombre del post dentro del paréntesis (encerrado en comillas).

## Cuadros de mando

### Flexdashboard 
La libreria [flexdashboard](https://rmarkdown.rstudio.com/flexdashboard/) consiste en un conjunto de utilidades con las que generaremos facilmente cuadros de mando dinámicos. Su uso es bien sencillo; una vez cargada la libreria, cada título que definamos se convertirá en un marco donde podremos depositar la información a mostrar:

![](C:/TEMP/rpub2/images/flexdash.png)


### Shinny
Shiny se basa en el uso de Programación Reactiva (Reactive Programming), esto es: existen unos valores que pueden variar en el tiempo y que son registrados por unas expresiones que posteriormente las reproducen. Junto a este motor de razonamiento, incorpora adaptadas los clásicos elementos HTML (botones, cuadros de texto, barras de desplazamiento,…) junto con las potentes gráficas de R y su estructura de datos.Básicamente se compone de dos ficheros que se crean en nuestro directorio local: `ui.R`, que gestiona la salida visual y el aspecto de la aplicación y `server.R` con las instrucciones para que la misma función, siendo en esta última donde se embebe el motor de cálculo en realizado en R. En las últimas versiones del paquete, ambos ficheros vienen embebidos en uno solo `app.R`. Estos archivos son publicados en nuestro servidor web o en las distintas plataformas que lo interpreten como GitHub.

![](C:/TEMP/rpub2/images/shinny1.png)
![](C:/TEMP/rpub2/images/shinny2.png)

Las posibilidades de Shiny se amplían al admitir incorporaciones al código nativo de todos los elementos que actualmente conforman los ecosistemas HTML, CSS y Javascript, lo que implica que los desarrollos que se puedan hacer con esta herramienta son casi ilimitados. Esto la convierte en una herramienta muy poderosa para la construcción de cuadros de mando y para mostrar los resultados de nuestros desarrollos usando las capacidades analíticas de R, de forma que el receptor de nuestra información pueda interactuar fácilmente con ella (por ejemplo [como en este caso](https://juliomsevilla.shinyapps.io/ModeloGlobulusHuelva/)).




