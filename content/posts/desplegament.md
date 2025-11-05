+++
title = 'Desplegament de Hugo a Github.'
date = 2025-11-05T08:57:43+01:00
draft = false 
+++

S'han de seguir  les instruccions [d'aquest enllaç](https://gohugo.io/host-and-deploy/host-on-github-pages/) per a dur-ho a terme.

Els principis són simples: crees una carpeta amb el projecte (bloc) al teu PC i ho sincronitzes amb un "repositori" creat a Github. Es configuraaquest repositori de forma que publiqui el contingut a la web de Github. La publicació és estàtica, és a dir, no es modifica fins que no tornis a fer una sincronització. Aquesta nova publicació és (o pot ser) automàtica.

L'esquema és simple. La construcció no ho es tant i es pot convertir en un camp de mines. Fem un breu esquema per assenyalar les dificultats més rellevants que he hagut de resoldre.

1. Instal·lar Hugo i crear el primer projecte en local. (sols crear-lo. No cal afegir contingut ni cap tema o plantilla).

2. Crear el compte i el repositori a Github.

3. Enllaçar el projecte local amb el repositori de Github.

4. Fer el contingut del repositori a Github explicit a través del servei Github Pages. És a dir, activar o permetre la seva publicació web.

Amb aquestes passes el lloc web estarà actiu i visible al món. Els nous posts o les modificacions dels existents es fan en local i es fan públics mitjançant la sincronització.

## El primer error. La comunicació ssh.

Els punts 1 i 2 de l'esquema no tenen per què donar problemes. El primer que em va aparèixer va ser amb la comunicació entre el meu projecte i el repositori. Vaig anar per la via de connexió ssh i vaig afegir la meva clau pública al lloc equivocat `User > Sttings > Deploy keys`. El correcte és asociar la clau a l'usuari.  `User > Settings > Ssh and GPG keys`.

Aquest pas previ d'assegurar una correcta comunicació ssh és bàsica per al `remote`de l'apartat 4 de l'esquema. 

## La sincronització.

La sincronització es fa en local, en el terminal i des de dins de la carpeta del projecte. És un procés amb tres ordres consecutives:

> ```bash
> ~/Bloc$ git add .
> ~/Bloc$ git commit -m "un_comentari"
> ~/Bloc$ git push

## Errors afegits que han dificultat la publicació.

Vaig triar l'opció de publicació a través de Github Actions. això automatitza les publicacions, asociant-les a les sincronitzacions.

### .gitmodules

Per algun motiu aquest fitxer `.gitmodules`no existia a l'arrel del meu projecte. El vaig haver de crear amb el següent contingut:

> ```bash
> [submodule "themes/hugo-blog-awesome"]
>    path = themes/hugo-blog-awesome
>   url = https://github.com/hugo-sid/hugo-blog-awesome.git   

### Error per compatibilitat de versions.

Sembla que el meu `theme`exigia uns requisits específics del programari d'execució en el servidor de Github. Aixó ho vaig poder corregir amb una modificació del fitxer `.github/workflows/gh-pages.yml`.

> ```bash
>- name: Setup Hugo
>  uses: peaceiris/actions-hugo@v2
>  with:
>    hugo-version: 'latest'
>    extended: true   

## Conclusions.

El resultat és molt bo. Net, simple, markdown.

D'entrada la publicació queda lligada a la màquina sincronitzada. Per tant no pots publicar (o jo no sé com) sense accedir al teu PC. M'imagino que podras copiar el directori del projecte i les claus ssh per portar-lo a un altre ordinador

El desplegament del projecte no és gens trivial. Potser seria més profitos un allotjament en un servidor propi, si el tens. A no ser que en treguis un bon profit de l'ús dels repositoris de Github. Ara be, la feina està feta. Si les còpies de seguretat es fan correctament, tinc bloc per una bona estona.



