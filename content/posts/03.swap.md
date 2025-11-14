+++
title = 'Swap'
date = 2025-11-04T07:06:43+01:00
draft = false 
+++

Això és una reflexió sobre la Swap surgida com a consequència de l'encriptació que vaig fer d'un ordinador portàtil.

El problema pràctic al que t'enfrontes amb l'encriptació és el d'haver de posar la contrassenya tantes vegades com particions encriptis. I això no és cómode. El primer que se t'acudeix és agrupar-ho tot a la partició arrel. És a dir, parteixes d'un esquema /boot, / i swap. /boot no pot anar encriptada a l'arrencada i, a més a més, mai té contingut sensible. / és l'objecte de l'encriptació. Swap és el tema que ens ocupa. 

La swap pot tenir contingut sensible i per aquest motiu es recomana encriptar-la. Tenim així la necessitat de posar dues contrassenyes. Tampoc és massa greu.

Una altra alternativa és suprimir la partició swap (si no necessites hivernació) o "emular-la" a través d'un fitxer. És cridanera la solució adoptada per Fedora, realment eficient, de crear una ram comprimida (zram). Aquesta darrera solució amplia la ram disponible, comprimint-la, a costa d'un lleuger treball afegit de la cpu. He de dir que funciona molt bé fins hi tot en sistemes de pocs recursos. Però no hi ha swap, a no ser que també en creis una. Però llavors tornem a necessitar una altra contrassenya.

Quan revises la proposta que aporta FreeBSD, entens el sentit del problema. FreeBSD està enfocat a l'estabilitat. Assumeixen què el desbordament de la ram sempre pot passar i consideren que no hi ha cap motiu rellevant per a suprimir la swap. Si el problema és l'encriptat i la contrassenya de la partició d'intercanvi, doncs això té solució.

## Una solució d'encriptació automàtica de la swap a FreeBSD.

Es tracta de dit-li al sistema que l'encripti a l'arrencada amb Geli. Per fer-ho fes el següent:

1. Desactiva la wap `swapoff -a`.

2. Encripta la partició swap amb una contrassenya temporal: `geli onetime /dev/your-swap-partition`. Per identificar la partició pots utilitzar l'ordre `gpart show`.

3. Activa la swap encriptada: `swapon /dev/your-swap-partition.eli`.

4. Activa el mòdul a l'arrencada: Afegeix `"geom\_eli\_load="YES"` a `/boot/loader.conf`.

5. Configura `/etc/fstab`: Canvia la línia correponent a la swap per afegir el sufix `eli`. Per exemple, `/dev/ada0p4.eli` en lloc de `/dev/ada0p4`.

6. Reinicia el sistema. Es crearà automàticament una clau temporal per encriptar la swap a cada inici.

D'aquesta manera la swap quedarà encriptada i no necessitaras introduïr cap altra contrassenya. Pots verificar l'estat de la swap amb l'ordre `swapinfo`. Si tot és correcte, la sortida tindrà un sufix `.eli`com per exemple `/dev/ada0p4.eli`.

# I a Linux?

Doncs sí, a Linux també es pot fer, però amb eines diferents. Debian i Ubuntu sembla que ho duen incorporat. 
