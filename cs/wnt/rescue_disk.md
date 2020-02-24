# Odvirování Windows pomocí záchranného disku
Pokud selže odstranění malware přes OS, případně nelze OS ani zavést, je nutné použít *live OS s antimalware systémem* na externím CD / USB disku. I k tomuto postupu je nezbytný přístup k internetu. Nejkomfortnějším způsobem je připojení síťovým kabelem. Níže naleznete postup pro **Bitdefender Rescue CD** a **Kaspersky Rescue Disk** &ndash; použitelné jsou obě varianty, i jejich kombinace.

<br>

## Bitdefender Rescue CD
### Stáhnutí a vytvoření záchranného disku:
- Stáhněte si ISO soubor [Bitdefender Rescue CD](https://download.bitdefender.com/rescue_cd/latest/bitdefender-rescue-cd.iso).
- Vytvořte instalační médium z ISO souboru, pro USB doporučím program [Rufus](https://rufus.akeo.ie/) (návod [zde](http://www.cnews.cz/navody/rufus-vytvorte-zavadeci-flash-disk-s-nejrychlejsim-nastrojem-ze-vsech)).
- Nabootujte z vytvořeného instalačního média (většinou klávesa **F12** při BIOS/UEFI uvítací obrazovce).

<br>

### Odstranění malware:
- Zkontrolujte, zdali máte zvolenou možnost <span class="green">Start the Bitdefender Rescue CD in English</span>, a stiskněte **Enter**.
- Vyčkejte na dokončení všech příprav, dokud se neobjeví uvítací okno aplikace **Bitdefender Rescue CD**.
- Odsouhlaste licenční podmínky aplikace.
- Automaticky bude inicializována aktualizace a následný sken.
- Po dokončení skenu se zobrazí nalezené hrozby. Rozklikněte nejvýše položený box pro globální volbu akce a zvolte možnost <span class="green">Disinfect</span>.
- V dolní liště klikněte na tlačítko <span class="green">Fix issues</span>.
<li style="list-style-type: none">![bdresc](https://guides.securityhandbook.cz/img/en/bdresc.png)</li>
- Zůstanou-li na seznamu položky, které nebylo možné dezinfikovat, zvolte pro ně možnost **Delete** nebo **Rename** a znovu klikněte na <span class="green">Fix issues</span>.
- Jakmile budou zneškodněny všechny nalezené hrozby, klikněte na <span class="green">Finish</span> a následně <span class="green">Done</span>.
- Restartujte zařízení.

<div class="alert success"><p><em class="icon-ok-circled"></em>**Úspěch**<br>
Váš OS by měl nyní být zbaven aktivního malware a schopný zavedení. Pokud ne, můžete zkusit ještě možnost uvedenou níže.</p></div>

<br><br><hr><br>

## Kaspersky Rescue Disk
### Stáhnutí a vytvoření záchranného disku:
- Navštivte stránky Kaspersky a stáhněte si ISO soubor [Kaspersky Rescue Disk](https://support.kaspersky.com/viruses/rescuedisk).
- Vytvořte instalační médium z ISO souboru, pro USB doporučím program [Rufus](https://rufus.akeo.ie/) (návod [zde](http://www.cnews.cz/navody/rufus-vytvorte-zavadeci-flash-disk-s-nejrychlejsim-nastrojem-ze-vsech)).
- Nabootujte z vytvořeného instalačního média (většinou klávesa **F12** při BIOS/UEFI uvítací obrazovce).

<br>

### Odstranění malware:
- Klávesou **1** odsouhlaste licenční podmínky.
- Zkontrolujte, zdali máte zvolenou možnost <span class="green">Kaspersky Rescue Disk. Graphic Mode</span>, a stiskněte **Enter**.
- Vyčkejte na dokončení všech příprav, dokud se neobjeví okno aplikace **Kaspersky Rescue Disk**.
- V hlavním panelu se přesuňte do záložky **My Update Center** a zvolte možnost <span class="green">Start update</span>.
<li style="list-style-type: none">![krd](https://guides.securityhandbook.cz/img/en/krd.png)</li>
- Po dokončení aktualizace v horním panelu klikněte na <span class="green">Settings</span>.
- Zvyšte **Security level** na úroveň <span class="green">High</span> a klikněte na <span class="green">OK</span>.
<li style="list-style-type: none">![krd1](https://guides.securityhandbook.cz/img/en/krd1.png)</li>
- V hlavním panelu se přesuňte do záložky **Objects Scan**.
- Zatrhněte všechny dostupné disky pro jejich kontrolu a zahajte sken tlačítkem <span class="green">Start Objects Scan</span>.
<li style="list-style-type: none">![krd2](https://guides.securityhandbook.cz/img/en/krd2.png)</li>
- Po dokončení skenu se v pravém dolním rohu zobrazí vyskakovací okno s nalezenými hrozbami. Zatrhněte možnost <span class="green">Apply to all objects</span> a následně zvolte doporučovanou akci.
<li style="list-style-type: none">![krd3](https://guides.securityhandbook.cz/img/en/krd3.png)</li>
- Postup opakujte pro všechny druhy nalezených hrozeb.
- Aplikaci zavřete a restartujte zařízení.

<div class="alert success"><p><em class="icon-ok-circled"></em>**Úspěch**<br>
Váš OS by měl nyní být zbaven aktivního malware a schopný zavedení.</p></div>

<br><br><hr>

<h3 class="nocol">Hezký den. <img class="smile" src="https://securityhandbook.cz/img/sm/smile.svg" alt="smile"></h3>
