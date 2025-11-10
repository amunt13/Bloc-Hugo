+++
title = 'Configuració bàsica de Neovim per a Markdown.'
date = 2025-11-10T06:08:21+01:00
draft = false
+++

Fa uns anys vaig tenir contacte amb Làtex amb l'objecte de fer un document de certa envergadura. Va ser un procés d'aprenentatge important i els resultats van ser molt bons. Però, sigui per la falta de necessitat de repetir l'experiència, sigui per l'especial dificultat de Làtex, ja no ho he repetit. Sospito que el major problema és la dificultat d'ús de Làtex i a més a més, la falta de netedat del text font que generes.

Per aquest motiu, ara estic investigant les possibilitats de markdown. Vull veure fins a quin punt aquest sistema de marcat de text plà, pot ajudar a la redacció de textos raonablement complexos. I com es pot manipular aquest text font per a generar documents d'un nivell correcte. Sense necessitat d'un ús intensiu de Làtex i evitant els textos complexos que genera i no són fàcils de llegir ni corregir.

## Per què Neovim.

Si del que es tracta és d'escriure amb text pia, doncs necessites un editor de text. Si aquest editor ha de sustentar una feina important, ha de tenir característiques potents per ajudar-te, poc a poc, a millorar la teva eficiència. I si ja estas enfangat en la feina, també necessites que aporti totes les avantatges que puguis, de comoditat i d'extensió.

La meva aproximació als editors potents va ser a través de vim. Per això ara estic amb Neovim. La xarxa n'està plena de documentació i comentaris al respecte. Ben fonamentats i molt tècnics. No cal insistir en el tema.

## Els primers passos amb Neovim.

Si ets usuari de vim, començçar amb Neovim és inmediat. En el meu cas, usuari de Debian, tan simple com fer `sudo apt install neovim`.

El programa s'inicia amb l'ordre `nvim`. Això et condueix a una pantalla semblant a la de vim, en tots els sentits.

L'ús bàsic de Neovim és idèntic al de vim. Però clar, ja que hi som, cal fer millores en el seu comportament per aprofitar-se de les seves funcionalitats.

Doncs això no és simple. No ho és perquè hi ha un món de possibilitats que no sempre són adients a les teves necessitats. I la configuració és totalment nova per a mí. Per tant l'objectiu inicial és el de cercar la simplicitat. Així que els primers objectius de configuració serà sols el referent al "resaltat de text" i a la correcció ortogràfica.

## La primera configuració.

La configuració de nvim es realitza al fitxer `~/.config/nvim/init.lua`. I és segur que una vegada instal·lat nvim, no existeix. L'has de crear manualment i després editar-lo. La meva configuració és la següent:

> ```bash
> require("lazy").setup({
>  {
>    "nvim-treesitter/nvim-treesitter",
>    build = ":TSUpdate",
>    config = function()
>      require("nvim-treesitter.configs").setup({
>        ensure_installed = { "markdown", "markdown_inline" },
>        highlight = { enable = true },
>        indent = { enable = true },
>      })
>      -- Configuración adicional dentro del plugin
>      vim.g.markdown_fenced_languages = { 'lua', 'python', 'javascript', 'html', 'bash' }
>    end
> },
> })
>
> -- Autocomando fuera del setup
> vim.api.nvim_create_autocmd("FileType", {
>  pattern = "markdown",
>  callback = function()
>    vim.opt_local.spell = true
>    vim.opt_local.spelllang = "ca"
>  end
> })

## Un exemple de la potència de nvim. Insertar un caràcter a l'inici de varies línies.

Vaig aprofitant per anar anotant els meus avenços en vim. Com està veient, estic incorporant al text moltes entrades de codi, com a exemples de configuració. Això exigeix crear els anomenats "blockquote" on cada línia ha de començar pel símbol \>. Aquí és on destaca la potència de vim, ja que aquest procés es pot automatitzar. Hi ha varies maneres de fer-ho:

### Usar el "mode visual en bloc (recomanat per a seleccions específiques).

1. Prem `Esc` per assegurar-te estar en mode normal.
2. Mou el cursor a la primera línia on vulguis inserir el caràcter.
3. Pressiona `ctrl+v` per entrar en mode "visual bloc".
4. Selecciona la resta de línies verticalment usant `j` o les fletxes.
5. Pressiona `I` (i majúscula) per entrar en mode inserció a l'inici de les línies seleccionades.
6. Escriu el caràcter que vulguis inserir (per exemple \>).
7. Pressiona `Esc`i el caràcter s'insertarà a totes les línies seleccionades.

### Métode global. (Ideal per tot el text o rangs).

Utilitza el comandament `:s`(substituir) amb un rang.

#### Inserir \> a l'inici de totes les línies de l'arxiu:

> :%s/^/>/   

#### Inserir \> sols en un rang (ex. línies 5 a 10):

> :5,10s/^/>/   

+ \% = tot l'arxiu.
+ \^ = inici de lìnia.
+ \> = caràcter a inserir.

### Usar :norm en combinació amb comandaments.

> `:%norm I>`

+ `%norm` = aplica el següent comandament, en mode normal, a cada línia.
+ `I>` = insereix \> a l'inici de cada línia.

També pots seleccionar un rang visualment i després posar `:norm I>`. 



