+++
title = 'Instal·lar Hugo'
date = 2025-10-30T10:05:25+01:00
draft = false 
+++
He instal·lat Hugo amb el tema Awesome amb l'ajuda d'aquesta web: https://rodosilva.github.io/myblog/posts/blog-con-hugo-y-githubpages/

Per configurar-ho en català (com a únic idioma) i, a més, configurar una barra de menú bàsica, he posat aquestes línies a hugo.toml:

> L'idioma:
> ```bash
> languageCode = 'ca'
> defaultContentLanguage = "ca"

> I així el  menú:
> ```bash
> [menu]
> [[menu.main]] 
>  identifier = "home" 
>  name = "Inici" 
>  url = "/"
>  weight = 1
>  [[menu.main]]
>    identifier = "blog"
>    name = "Bloc"
>    url = "/posts/"
>   weight = 2
> [[menu.main]]
>  identifier = "about"
>  name = "Sobre mi"
>  url = "/about/"
>  weight = 3


## Una imatge i iinformació del bloc.

Per personalitzar una mica el bloc, es pot afegirr un segment de text al fitxer *hugo.toml*:


> ```bash
> [params.author]
>  avatar = "avatar.jpg" \# put the file in assets folder; also ensure that image has same height and width
> \# Note: image is not rendered if the resource(avatar image) is not found. No error is displayed.
>  intro = "Linux, BSD i altres herbes."
>  name = "amunt25"
>  description = "Un espai per compartir experiències linuxeres."

## Fletxa per anar al principi.

És útil posar un enllaç a baix del text per facilitar tornar a la part superior de la pàgina. Això és tan simple com afegir `goToTop = true` al fitxer hugo.toml.

## El contingut de "Sobre mi".

Aquest contingut és un fitxer anomenat index.md, ubicat a lla carpeta "about" dins de "content". Per crear-lo, crees primer la carpeta "about" manualment i després sols has de picar `hugo new content/about/index.md`, sempre des de dins de la carpeta principal del projecte.

## L'índex de continguts.

El tema Awesome ja du incorporada la creació automàtica de l'index a cada post. El que passa és que no està activada per defecte.

Es pot activar de forma global al fitxer `hugo.toml`, afegint el següent:

> ```bash
> [params]
> toc = true   

També es pot activar/desactivar a cada post, posant al "front matter" el text `toc = true` o `toc = false`. Quedaria alguna cosa així:

> ```bash
> +++
> title: "Your Post Title"
> date: 2023-05-02
> toc: true
> +++   

Com és fàcil que hi hagi posts sense títols, el que jo faig és posar una política global a `hugo.toml` i després en els posts que no sigui necessari l'índex, sols a aquests, hi pos `toc = false`. Així evito que aparegui un enllaç d'índex buit de continguts.

L'índex apareix tancat per defecte. Per canviar aquesta opció a "obert", ho pots fer igual que abans, de forma global o per post. El text a col·locar a `hugo.toml`i/o a cada post és: `tocOpen = true`o `tocOpen = false`.

Això crea autoáticament els índex de cada post. Però no apareix cap text a sobre de l'enllaç. Per solucionar-ho, fes el següent:

### Text a l'índex de continguts.

La configuració dels índex es realitza al fitxer `themes/hugo-awesome-blog/layouts/partials/toc.html`que "crida" als fitxers d'idioma per trobar el text.  Això es fa al fitxer corresponent al teu idioma. Aquests fitxers són a la carpeta `i18n`de l'arrel del projecte. Has de crear un fitxer de nom `ca.toml`, on `ca`és l'indicatiu d'idioma. Hi has de posar el teu. El contingut del fitxer ha de ser:

> ```bash
> [single.table_of_contents]
> other = "Table of Contents"  # Change this to "Index" or your preferred text   

Has de substituir "Table of contents" per la paraula o frase que consideris adient.


