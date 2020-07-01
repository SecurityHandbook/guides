# Čistá instalace Windows 8.1

Pokud nemáte k dispozici instalační DVD, můžete jej jednoduše vytvořit. Budete potřebovat volné médium (DVD, USB disk) o velikosti alespoň *8 GB* a funkční počítač, ze kterého na něj můžete nahrát instalační soubory Windows.

<br>

## Stažení originálního ISO Windows 8.1:

Instalační ISO je volně dosutpné ke stáhnutí ze stránek MS: https://www.microsoft.com/cs-cz/software-download/windows8ISO

<br>

## Vytvoření instalačního média Windows 8.1:

- Vytvořte instalační médium z ISO souboru, pro USB doporučím program [Rufus](https://rufus.ie/) (návod [zde](https://guides.securityhandbook.cz/cs/wnt/rufus.php)).
- Nabootujte z vytvořeného instalačního média.
- Zkontrolujte konfiguraci jazyka a klávesnice a klikněte na tlačítko <span class="green">Další</span>.
- Klikněte na tlačítko <span class="green">Nainstalovat</span>.
- Vložte licenční klíč (máte-li OEM licenci dodanou s NTB, klíč není potřeba).
- Zvolte požadovanou edici OS.
- Přijměte licenční podmínky a pokračujte v instalaci.

<br><br><hr><br>

## DISKPART – vyčištění disku

Pokud vytváříte nový OS z důvodu problémů s předchozí instalací, je rozumné před instalací kompletně vyčistit disk. Tento postup je také standardem při instalaci na nový disk.

<div class="alert exclaim"><p><em class="icon-attention"></em>**Varování**<br>
Vyčištění disku smaže veškerá existující data na příslušném disku! **Pouze pro pokročilé!**</p></div>

> Návod

- Ve výběru možnosti instalace zvolte: Vlastní: Jenom nainstalovat Windows (pokročilé).
- Ve výběru disků stiskněte **Shift** + **F10**.
- Do příkazové řádky postupně zadejte následující příkazy:
<li style="list-style-type: none"><pre><code>diskpart
list disk             //vypíše všechny připojené disky a jejich čísla
select disk X         //místo "X" dosaďte číslo vašeho systémového disku
clean                 //vyčistí zvolený disk
exit
exit</code></pre></li>
<li style="list-style-type: none">![w10diskpart](https://guides.securityhandbook.cz/img/cs/w10diskpart.png)</li>
- Ve výběru disků klikněte na tlačítko: ![upd](https://guides.securityhandbook.cz/img/cs/upd.png)
- Zvolte prázdný vyčištěný systémový disk a pokračujte v instalaci.

<br><br><hr>

<h3 class="nocol">Hezký den. <img class="smile" src="https://securityhandbook.cz/img/sm/smile.svg" alt="smile"></h3>
