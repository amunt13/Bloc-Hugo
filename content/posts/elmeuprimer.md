+++
title = 'Instal·lar Hugo'
date = 2025-10-30T10:05:25+01:00
draft = false 
+++
He instal·lat Hugo amb el tema Awesome amb l'ajuda d'aquesta web: https://rodosilva.github.io/myblog/posts/blog-con-hugo-y-githubpages/

He d'assenyalar que el més rellevant ha estat que he fet cas a l'advertència del sistema en relació al nom de la "Branca". Per defecte m'assignava "Master", però em proposava "main". Així ho he fet i ha funcionat.

`git config --global init.defaultBranch main`


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

 Després ja el pots editar.
