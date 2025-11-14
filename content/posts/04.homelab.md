+++
title = 'El meu Homelab'
date = 2025-11-05T16:57:03+01:00
draft = true
toc = false
+++

Tenc un servidor domèstic. Vaig començar amb aquest tema amb un  aparell molt bàsic construit a partir d'un NSLU2 de Linksys. Un dispositiu dissenyat per enllaçar discos durs a la xarxa sense necessitat de cap servidor dedicat. Molt ben documentat i feia la seva feina. Com diuen, fins hi tot una cafetera suporta Debian. Així que hi vaig crear un petit servidor. Era molt lleuger i la transferencia de fitxers era lenta . Això seria al voltant de l'any 2008.

Després, al febrer de l'any 2010,  vaig adquirir un minipc Wyse winterm j400 de segona mà. De molt baix consum, portava una font d'alimentació externa de tipus portàtil. Encara portava discos IDE. El processador era limitat, un Intel de 32 bits, no PAE. Va durar fins que es va trencar el disc dur i vaig decidir reemplaçar-ho per una màquina similar, però aquesta vegada construida "ad hoc".

A principis del 2016 vaig adquirir una placa mini ITX Asrock N3150B-ITX, amb cpu integrada i refrigeració passiva. Li vaig posar una font d'alimentació PicoPSU80 de Mini-box i 4 Gb de ram. Aquest aparell ja suporta discos SATA 3 i te un rendiment més que suficient amb consums per davall dels 10w. Encara funciona i és l'aparell que ara faig servir. Totalment compatible amb Debian.

Aquest mini PC ha fet una mica de tot. Però ara fa una funció bàsica de magatzem de còpies de seguretat, em permet accés remot a les còpies en cas de necessitat i és també un servidor DNS.

Fent una descripció detallada, te els següents serveis:

1. ddclient, per actualitzar l'adreça pública i fer-lo accessible des d'internet.
2. Servidor d'impressió. Per compartir una vella impressora làser.
3. Servidor NFS. M'ajuda a fer les còpies de seguretat. Muntatge manual de les carpetes compartides. Més seguretat.
4. Un servidor DNS construit a base de PiHole asociat al servidor recursiu Unbound.

Ara alliberat del Bloc.
