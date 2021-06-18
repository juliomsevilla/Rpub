# Gestión de bibliografías con Bibtex {#bibtex}

## Sobre Bibtex
[Bibtex](http://www.bibtex.org/) es una herramienta auxiliar de LaTeX, diseñada para facilitar el manejo de la bibliografía y es un estandar de almacenamiento de referencias. Su uso es muy sencillo: a modo de base de datos, en un fichero con extensión `bib` alamacenaremos todas nuestras referencias bibliográficas, independientemente de que las usemos o no en el documento actual, algo que es una gran ventaja, pues podremos crear nuestro fichero, único, de referencias bibliográficas, que usaremos en todos nuestros proyectos. 


La cita de la fuente es muy sencilla:simplemente, en nuestro documento LaTeX, deberemos llamar al identificador de la referencia, para que el compilador la muestre de forma adecuada. Veamos unos ejemplos:

```r
@Manual{R-base,
  title = {R: A Language and Environment for Statistical Computing},
  author = {{R Core Team}},
  organization = {R Foundation for Statistical Computing},
  address = {Vienna, Austria},
  year = {2019},
  url = {https://www.R-project.org/},
}

@article{article12,
  author  = {Peter Adams}, 
  title   = {The title of the work},
  journal = {The name of the journal},
  year    = 1993,
  number  = 2,
  pages   = {201-213},
  month   = 7,
  note    = {An optional note}, 
  volume  = 4
}
```
En estos casos, el identificador de cada referencia es el texto que va a continuación de {, `R-base` o `article12`.

En internet, podremos encontrar software específico para gestionar nuestros ficheros `bib` como https://truben.no/latex/bibtex/ o http://www.jabref.org/ aunque, si bien, el fichero `bib`no es más que un fichero de texto, por lo que cualquier editor (hasta el simple notepad del sistema nos servirá).


## Referencias bibliográficas en Rmarkdown.
Existen varias formas de gestionar las referencias bibliográficas en el documento, pero lo más recomendable es trabajar con el estilo de citas BiBtex y el almacenamiento en este formato, especialmente si el resultado buscado es `pdf` y/o `tex`.


```r
@Manual{R-base,
  title = {R: A Language and Environment for Statistical
    Computing},
  author = {{R Core Team}},
  organization = {R Foundation for Statistical Computing},
  address = {Vienna, Austria},
  year = {2019},
  url = {https://www.R-project.org/},
}
```

Para que Rmarkdown reconozca la cita, deberemos añadir a nuestro encabezado YAML la ruta donde almacenaremos todas nuestras referencias bibliográficas (nuestra base de datos en formato `bib`). Si este se ubica en el mismo lugar que el fichero `Rmd` podremos usar simplemente:


```r
---
title: "Untitled"
author: "Julio M. Sevilla"
date: "20/6/2019"
output: html_document
bibliography: bibliografia.bib
---
```

Por otro lado, en el documento que estemos escribiendo, será tan simple como usar la llamada que hayamos definido con anterioridad en nuestra base de datos: en este ejemplo, `@R-base` que generará “@R-base” o `[@R-base]` que creará “[@R-base]”. Pandoc, a su vez, creará un listado de referencias bibliográficas al final del documento. Este listado, se basa en el [manual de estilo de Chicago](https://www.chicagomanualofstyle.org/tools_citationguide/citation-guide-2.html) por lo que si deseamos otro, lo deberemos definir a partir de un fichero `csl` (un manual muy util es [http://docs.citationstyles.org/en/1.0.1/primer.html](http://docs.citationstyles.org/en/1.0.1/primer.html)), el cual debe tambien incluirse en el YAML:


```r
---
title: "Untitled"
author: "Julio M. Sevilla"
date: "20/6/2019"
output: html_document
bibliography: bibliografia.bib
csl: biomed-central.csl
---
```
## La documentación de los paquetes
Como sabemos todos los paquetes o librerias que usamos en R deben ser correctamente referidos. Evidentemente, esta gestión dentro del propio R es muy sencillo. Para ello, al comenzar nuestro documento Rmarkdown, podemos definir un comando para que nos cree automaticamente las referencias bibliográficas adecuadas de cada paquete mediante la sintaxis:


```r
knitr::write_bib(c(.packages(), 'ggplot2', 'nlme'), 'packages.bib')
```
Por supuesto, ahora, tendremos que decirle al compilador que debe "buscar" en dos ficheros `bib` para lo cual deberemos extender el YAML de la siguente forma:


```r
---
title: "Untitled"
author: "Julio M. Sevilla"
date: "20/6/2019"
output: html_document
bibliography: ["packages.bib", "bibliografia.bib"]
---
```

De esta forma, se generará, automaticamente, un fichero específico, en formato `bib`con las referencias bibliográficas de todos los paquetes que le digamos y despues será tan simple, como, de nuevo, escribir en el texto markdown la referencia al paquete a modo `@R-nlme` o `@R-ggplot2` generando, en el primer caso: @R-nlme
