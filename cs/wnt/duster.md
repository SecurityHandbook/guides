# Bezpečné čištění OS Windows

<h3 class="red">![ch](https://mople71.cz/img/ccleaner.png) Varování &ndash; CCleaner a podobné čističe</h3>

![exclaim](https://mople71.cz/img/sm/exclaim.gif) Čističe OS čistící registry jsou pro OS nebezpečné, nedoporučované a Microsoftem nepodporované.

![idea](https://mople71.cz/img/sm/idea.gif) Přečtěte si prosím zásady podpory Microsoftu: https://support.microsoft.com/cs-cz/kb/2563254

#### Rizika užívání čističů registru:
- mohou způsobit nevratné škody vašemu registru => OS
- mohou s sebou do OS přinést malware
- mohou registr spíše zpomalit než zrychlit
- zbaví vás nároku na podporu do MS a většiny diskuzních fór

> Rozebrání problematiky

Spousta problémů s OS, se kterými se denně potkávám na různých fórech, je způsobena právě čističi registru, defragmentátory registru, optimizéry registru apod.

![idea](https://mople71.cz/img/sm/idea.gif) Registr je velká hierarchická databáze obsahující miliony hodnot, které určují chod OS. Máte-li nějakou databázi, také do ní nevpustíte naprosto cizí program, který vám databázi vyčistí na základě svých generických pravidel.

Tyto čističe zaručují zrychlení registru. Pokud bychom měli prohledat celý registr, chvíli to zabere &ndash; nic takového ovšem aplikace nedělají. Aplikace se obracejí do specifických oblastí registru, kde očekávají nějaké své nastavení, případně chtějí manipulovat s COM objekty &ndash; tuto operaci mohou provést během několika milisekund.

Z toho vyplývá, že žádné zrychlení ve většině případu nenastane. Pokud by aplikace chtěla prohledat celý registr, přečtení všech hodnot mého HKCU klíče zabralo OS 314 milisekund &ndash; zrychlení (pokud nějaké) by se pohybovalo v řádu desítek až stovek mikrosekund.

Celé čištění/optimalizování registru je tedy z technického hlediska založeno pouze na tzv. [placebo efektu](https://cs.wikipedia.org/wiki/Placebo).

![idea](https://mople71.cz/img/sm/idea.gif) Čističe registru hledají chyby v registru na základě svých pravidel. Každá hodnota registru je unikát a může se s jednotlivými OS lišit. <span class="green">Nikdo</span> nemůže tímto způsobem 100% určit, že hodnota je chybná/nepotřebná.

Velmi oblíbená je detekce nepoužívaných klíčů registru. Ne každý nepoužívaný klíč je špatný, právě naopak. Klíč může být opuštěný, jelikož obsahuje hodnoty, které v budoucnu může žádat a potřebovat jiná aplikace.

Čištění registru tedy může být nebezpečné a způsobovat nevratné problémy, které se nutně nemusí projevit ihned. A spíše než zrychlí, váš registr zpomalí...

<br>

OS Windows má vestavěné veškeré nutné nástroje na svou údržbu již od dob Windows XP. Nějaké další čistící aplikace třetí strany tedy nejsou potřeba, jsou spíše nežádoucí.

Možná neposkytují takový komfort (příjemné barevné GUI) jako aplikace třetí strany, ovšem svou práci plní perfektně a ve většině případů lépe než čističe třetí strany.

> Rozebrání na příkladu: CCleaner

CCleaner je mezi širokou veřejností velmi oblíbený.

Jeho základní funkce jsou:

- čištění OS (temp soubory, koš, logy,...; prohlížeče a aplikace)
- čištění registru
- správa aplikací (odinstalace, start po spuštění, kontextové menu, úlohy,...)
- analýza disku, vyhledání duplicitních souborů, čistič disku
- základní správa bodů obnovy

Jediné funkce, které poskytuje navíc oproti OS jsou analýza disku, vyhledání duplicitních souborů a čistič disku - tedy funkce, které nejsou primární.

Stojí to za instalaci nedůvěryhodné aplikace třetí strany, která přichází ve free verzi s foistware a je potenciálně nebezpečná pro OS?

![arrow](https://mople71.cz/img/sm/arrow.gif) Pokud chcete i tak používat CCleaner, doporučuji stáhnout si portable verzi a nepoužívat část čistící registr.

<br><br><hr><br>

## Bezpečné čištění OS Windows:

K bezpečné údržbě vašeho OS používejte vestavěné nástroje Windows.

<h3 class="nocol">![cleanmgr](https://mople71.cz/img/cleanmgr.png) Disk Space Cleanup Manager</h3>

![idea](https://mople71.cz/img/sm/idea.gif) Následující postup je vhodné provádět 1x za měsíc.

- Otevřete si **hledání Windows**, do vyhledávacího pole zadejte:
<li style="list-style-type: none"><pre><code>cleanmgr</code></pre></li>
- Na nalezenou položku klikněte pravým tlačítkem a zvolte možnost: ![admin](https://mople71.cz/img/admin.png) **Spustit jako správce**.
- Budete-li vyzváni k výběru disku k pročištění, ponechte výchozí nastavení (systémový disk C) a klikněte na tlačítko <span class="green">OK</span>.
- Otevře se nabídka souborů ke smazání. Zde zatrhněte veškeré dostupné možnosti a klikněte na <span class="green">OK</span> a následně odsouhlaste odstranění souborů.
- Nechte aplikaci pracovat, po dokončení požadovaného čištění se sama ukončí.

<br>

<h3 class="nocol">![cmd](https://mople71.cz/img/cmd.png) Čištění TEMP</h3>

![idea](https://mople71.cz/img/sm/idea.gif) Následující postup je vhodné provádět 1x týdně.

- Stiskněte kláv. zkratku <img src="https://mople71.cz/img/wkey.png" alt="win"> <span class="ks">+ X</span> a z nabídky vyberte <span class="green">Windows PowerShell (správce)</span>.
<li style="list-style-type: none">![wx](https://mople71.cz/img/cs/wx.png)</li>
- Do příkazové řádky zadejte následující příkaz:
<li style="list-style-type: none"><pre><code>Get-ChildItem -Recurse $Env:TMP | Remove-Item -Recurse -Force</code></pre>
a stiskněte **Enter**.</li>
- Vyčkejte na dokončení požadované akce a aplikaci následně zavřete.

<br><br><hr><br>

## Automatizace výše uvedených kroků:

Výše uvedené postupy nejsou nijak automatizované, čímž mají velikou nevýhodu vůči čističům třetích stran, které v některých případech běží po celou dobu práce s OS (povzdech).

Není ovšem problém si výše zmíněné kroky automatizovat sám &ndash; je to práce na pár minut, která přinese kýžený výsledek.

<h3 class="nocol">![bat](https://mople71.cz/img/bat.png) Duster</h3>

- Stáhněte si [Duster](https://mople71.cz/duster.zip).
- Uložte a obsah archivu vyextrahujte <span class="blue">na Plochu</span>.
- Na skript jménem <span class="green">safesvc</span> klikněte pravým tlačítkem a zvolte možnost: ![admin](https://mople71.cz/img/admin.png) **Spustit jako správce**.
- Postupujte dle pokynů skriptu, na konci procesu vám řekne o souhlas k restartu OS.

<br>

<h3 class="nocol">![taskschd](https://mople71.cz/img/taskschd.png) Naplánování úlohy &ndash; dusting</h3>

- Skript jménem <span class="green">dusting</span>, který slouží k pravidelnému čištění, přesuňte z Plochy do <span class="blue">kořene systémového disku (**C:\**)</span>.
- Stiskněte kláv. zkratku ![win](https://mople71.cz/img/wkey.png) <span class="ks">+ R</span>, do textového pole zadejte:
<li style="list-style-type: none"><pre><code>taskschd.msc</code></pre>
a stiskněte **Enter**.</li>
- Otevře se Plánovač úloh, v levém menu klikněte na <span class="green">Knihovna plánovače úloh</span>.
- V pravém menu aplikace klikěnte na tlačítko: ![task1](https://mople71.cz/img/cs/task1.png)
- Do položky **Název** vyplňte např. <span class="green">Čištění OS</span> a klikněte na tlačítko <span class="green">Další</span>.
- Zvolte možnost spouštění **Týdně** a klikněte na <span class="green">Další</span>.
- Nastavte opakování na **2** týdny a zatrhněte jeden den, ve který se má úloha spouštět (např. *Pondělí*). Klikněte na <span class="green">Další</span>.
- Nechte zvolenou možnost **Spustit program** a klikněte na <span class="green">Další</span>.
- Ve volbě programu klikněte na <span class="green">Procházet</span> a zvolte skript <span class="green">dusting</span>, který máte uložený v <span class="blue">C:\</span>.
- Výsledek by tedy měl vypadat takto:
<li style="list-style-type: none">![task2](https://mople71.cz/img/cs/task2.png)</li>
- Klikněte na <span class="green">Další</span>.
- Zatrhněte položku: ![task3](https://mople71.cz/img/cs/task3.png)
- Klikněte na tlačítko <span class="green">Dokončit</span>.
- Ve vlastnostech zatrhněte následující položku: ![task4](https://mople71.cz/img/cs/task4.png)
- V horním menu vlastností se přesuňte do záložky <span class="green">Nastavení</span>.
- Zde zatrněte následující položku: ![task5](https://mople71.cz/img/cs/task5.png)
- Klikněte na tlačítko <span class="green">OK</span>.
- Plánovač úloh zavřete.

![arrow](https://mople71.cz/img/sm/arrow.gif) Tímto jste nastavili automatické mazání zbytečných souborů, které se spustí 1x za 14 dní. Dále se již o nic nemusíte starat.

<br>

#### Rozebrání funkcí a činností skriptu:

> Funkce skriptu Duster:

- zálohuje uživatelský registr
- otevře seznam aplikací, ze kterého můžete odinstalovat veškeré nevyužívané programy
- maže dočasné soubory
- maže přebytečné věci startující po spuštění
- umožňuje nastavit a následně spouští nástroj Čištění disku
- odstraňuje body obnovy a omezuje velikost jejich úložiště
- odstraňuje přebytečné úlohy
- čistí DNS cache
- kontroluje integritu OS

> Funkce skriptu Dusting:

- zálohuje uživatelský registr
- maže dočasné soubory
- spouští nástroj Čištění disku

<br>

![question](https://mople71.cz/img/sm/question.gif) Máte pomalý počítač? Příčinou může být malware, v takovém případě směřujte spíše do následující sekce: https://forum.zive.cz/forum-927/Viry-a-bezpecnost.html

<br><br><hr>

<span class="green">Hezký den.</span> ![smile](https://mople71.cz/img/sm/smile.gif)
