# Čistá instalace Windows 7 na stroji s OEM licencí

Pokud nemáte k dispozici instalační DVD, můžete jej jednoduše vytvořit. Budete potřebovat volné médium (DVD, USB disk) o velikosti alespoň *4 GB* a funkční počítač, ze kterého na něj můžete nahrát instalační soubory Windows.

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Tento návod se vztahuje pouze na **OEM** licenci OS. Máte-li retail licenci, je třeba použít jiný postup.<br>Návod naleznete [zde](https://guide.mople71.cz/cs/wnt/w7install.php).</p></div>

<br>

## Záloha licence v případě funkčního OS:
Je-li předchozí OS, který chcete znovu vytvořit, funkční, je možné předem zálohovat jeho licenci. Tímto se proces aktivace nového OS zrychlí.

> Návod

- Stáhněte si [Advanced Tokens Manager](http://www.majorgeeks.com/mg/getmirror/advanced_tokens_manager,1.html).
- Složku z archivu vyextrahujte <span class="blue">na Plochu</span> a otevřete ji.
- Na aplikaci klikněte pravým tlačítkem a zvolte možnost: ![admin](https://mople71.cz/img/icons/admin.png) **Spustit jako správce**.
- Klikněte na <span class="green">Activation Backup</span> a nechte aplikaci pracovat.
<li style="list-style-type: none">![atm](https://guide.mople71.cz/img/en/atm.png)</li>
- Celou složku s aplikací zálohujte <span class="blue">na vyměnitelné médium</span> a uschovejte pro pozdější aktivaci.

<br><br><hr><br>

## Stažení originálního ISO Windows 7:

Dříve byl k dispozici oficiální zdroj *DigitalRiver*, který již není v provozu. Pokud tedy nejste předplatitelé MSDN, od Microsoftu si nyní originální instalačku nestáhnete. Momentálně je zde jeden spolehlivý zdroj, kde lze nalézt torrent soubory originálních instalací: http://mirror.corenoc.de/digitalrivercontent.net/

Torrenty nejsou ideální varianta. Pokud ovšem budete hledat, naleznete na internetu česká ISO s více edicemi Windows, jako např. zde:

- [64-bit ISO](https://mega.co.nz/#!WVohDDAQ!CG4lRMyTHKK0gUhkc6nyAoNQZ10Zm8IifyblXgxdgxY)
- [32-bit ISO](https://mega.co.nz/#!OBhDlBxD!i8tgReL7wsxi_SzCuJ5x4NNY7YZPvE2TYpBdLwzM1Vo)

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Výše zmíněné ISO soubory byly podrobeny auditu a jsou v pořádku. Mají neznámé SHA-1, jelikož jsou upraveny, aby umožnily instalaci libovolné edice OS.</p></div>

<br>

## Vytvoření instalačního média Windows 7:

- Vytvořte instalační médium z ISO souboru, pro USB doporučím program [Rufus](https://rufus.ie/) (návod [zde](https://guide.mople71.cz/cs/wnt/rufus.php)).
- Nabootujte z vytvořeného instalačního média.
- Zkontrolujte konfiguraci jazyka a klávesnice a klikněte na tlačítko <span class="green">Další</span>.
- Klikněte na tlačítko <span class="green">Nainstalovat</span>.
- Zvolte požadovanou edici OS.
- Přijměte licenční podmínky a pokračujte v instalaci.
- Doporučuji nenastavovat aktualizace Windows a nastavení nechat na později z důvodu ruční instalace aktualizací.

<br><br><hr><br>

## DISKPART &ndash; vyčištění disku

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
<li style="list-style-type: none">![w10diskpart](https://guide.mople71.cz/img/cs/w7diskpart.png)</li>
- Ve výběru disků klikněte na tlačítko: ![upd](https://guide.mople71.cz/img/cs/upd.png)
- Zvolte prázdný vyčištěný systémový disk a pokračujte v instalaci.

<br><br><hr><br>

## Aktivace Windows 7:
Po úspěšné instalaci a připojení k internetu vyzkoušejte, zdali pouhý licenční klíč prošel aktivací.

- Otevřete nabídku **Start**.
- Klikněte pravým tlačítkem na **Tento počítač** a zvolte možnost <span class="green">Vlastnosti</span>.
- Posuňte se kolečkem myši na konec stránky a podívejte se, jestli je kopie Windows aktivována.

Neprošel-li samotný klíč aktivací, využijte jeden ze způsobů aktivace níže. Selže-li první, použijte druhý.

> Obnovení licence pomocí Advanced Tokens Manager

- Připojte vyměnitelné médium obsahující zálohu licence &ndash; složku aplikace *Advanced Tokens Manager*.
- Složku zkopírujte <span class="blue">na Plochu</span> a otevřete.
- Na aplikaci pravým tlačítkem a zvolte možnost: ![admin](https://mople71.cz/img/icons/admin.png) **Spustit jako správce**.
- Klikněte na <span class="green">Activation Restore</span> a vyčkejte na obnovení licence ze zálohy.
<li style="list-style-type: none">![atm1](https://guide.mople71.cz/img/en/atm1.png)</li>
- Restartujte NTB a následně ověřte stav aktivace Windows.

> Aktivace po telefonu

<div class="alert exclaim"><p><em class="icon-attention"></em>**Varování**<br>
Odkaz níže odkazuje na webovou stránku třetí strany.</p></div>

Návod zde: http://www.servispckupka.cz/jak_aktivovat_windows_7_aktivace_po_telefonu.php

<br><br><hr><br>

## Instalace aktualizací Windows 7:
Pro korektní fungování *Windows Update* je nutné dodržet následující postup instalace chybějících aktualizací OS. V opačném případě se později mohou vyskytnout problémy. Aktualizace ručně stáhneme a nainstalujeme, čímž si proces instalace aktualizací zkrátíme o cca. **10 hodin**.

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Nejjednodušší je při instalaci OS nenastavovat *Windows Update*. Pokud jste službu při instalaci již nastavili, dočasně vyhledávání aktualizací v nastavení vypněte. Nevíte-li jak otevřít a změnit nastavení *Windows Update*, nápověda [zde](https://faq.mople71.cz/cs/wnt/index.php#wnt1.2).</p></div>

Postup se liší v závislosti na bitové verzi OS.

> Postup pro 64-bit OS

- Stáhněte a nainstalujte aktualizaci [KB3020369](https://www.microsoft.com/cs-CZ/download/details.aspx?id=46817).
- Restartujte PC.
- Stáhněte a nainstalujte si [KB3125574](http://download.windowsupdate.com/d/msdownload/update/software/updt/2016/05/windows6.1-kb3125574-v4-x64_2dafb1d203c8964239af3048b5dd4b1264cd93b9.msu) (aka Service Pack 2).
- Restartujte PC.
- Stáhněte a nainstalujte [Internet Explorer 11](https://www.microsoft.com/cs-cz/download/internet-explorer-11-for-windows-7-details.aspx).
- Restartujte PC.
- Stáhněte a postupně od nejstarší po nejnovější nainstalujte kumulativní aktualizace za měsíce od července 2016. Po každé jednotlivé aktualizaci restartujte OS.
  - červenec: [KB3172605](https://www.microsoft.com/cs-CZ/download/details.aspx?id=53332)
  - srpen: [KB3179573](https://www.microsoft.com/cs-CZ/download/details.aspx?id=53581)
  - září: [KB3185278](https://www.microsoft.com/cs-CZ/download/details.aspx?id=53873)
  - říjen: [KB3192391](https://www.microsoft.com/cs-CZ/download/details.aspx?id=53990)
  - listopad: [KB3197867](http://download.windowsupdate.com/c/msdownload/update/software/secu/2016/11/windows6.1-kb3197867-x64_6f8f45a5706eeee8ac05aa16fa91c984a9edb929.msu)
- Povolte vyhledávání aktualizací službou *Windows Update* a iniciujte vyhledání zbylých aktualizací.

> Postup pro 32-bit OS

- Stáhněte a nainstalujte aktualizaci [KB3020369](https://www.microsoft.com/cs-CZ/download/details.aspx?id=46827).
- Restartujte PC.
- Stáhněte a nainstalujte si [KB3125574](http://download.windowsupdate.com/d/msdownload/update/software/updt/2016/05/windows6.1-kb3125574-v4-x86_ba1ff5537312561795cc04db0b02fbb0a74b2cbd.msu) (aka Service Pack 2).
- Restartujte PC.
- Stáhněte a nainstalujte [Internet Explorer 11](https://www.microsoft.com/cs-cz/download/internet-explorer-11-for-windows-7-details.aspx).
- Restartujte PC.
- Stáhněte a postupně od nejstarší po nejnovější nainstalujte kumulativní aktualizace za měsíce od července 2016. Po každé jednotlivé aktualizaci restartujte OS.
  - červenec: [KB3172605](https://www.microsoft.com/cs-CZ/download/details.aspx?id=53335)
  - srpen: [KB3179573](https://www.microsoft.com/cs-CZ/download/details.aspx?id=53568)
  - září: [KB3185278](https://www.microsoft.com/cs-CZ/download/details.aspx?id=53867)
  - říjen: [KB3192391](https://www.microsoft.com/cs-CZ/download/details.aspx?id=53995)
  - listopad: [KB3197867](http://download.windowsupdate.com/c/msdownload/update/software/secu/2016/11/windows6.1-kb3197867-x86_2313232edda5cca08115455d91120ab3790896ba.msu)
- Povolte vyhledávání aktualizací službou *Windows Update* a iniciujte vyhledání zbylých aktualizací.

<br><br><hr>

<h3 class="nocol">Hezký den. <img class="smile" src="https://mople71.cz/img/sm/smile.svg" alt="smile"></h3>
