# Bezpečné čištění OS Windows

<h3 class="red">![ch](https://securityhandbook.cz/img/icons/ccleaner.png) Varování &ndash; CCleaner a podobné čističe</h3>

Čističe OS čistící registry jsou pro OS nebezpečné, nedoporučované a Microsoftem nepodporované.

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Přečtěte si prosím zásady podpory Microsoftu: https://support.microsoft.com/cs-cz/kb/2563254</p></div>

### Rizika užívání čističů registru:
- mohou způsobit nevratné škody vašemu registru => OS
- mohou s sebou do OS přinést malware
- mohou registr spíše zpomalit než zrychlit
- zbaví vás nároku na podporu do MS a většiny diskuzních fór

> Rozebrání problematiky

Spousta problémů s OS, se kterými se denně potkávám na různých fórech, je způsobena právě čističi registru, defragmentátory registru, optimizéry registru apod.

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Registr je velká hierarchická databáze obsahující miliony hodnot, které určují chod OS. Máte-li nějakou databázi, také do ní nevpustíte naprosto cizí program, který vám databázi vyčistí na základě svých generických pravidel.</p></div>

Tyto čističe zaručují zrychlení registru. Pokud bychom měli prohledat celý registr, chvíli to zabere &ndash; nic takového ovšem aplikace nedělají. Aplikace se obracejí do specifických oblastí registru, kde očekávají nějaké své nastavení, případně chtějí manipulovat s COM objekty &ndash; tuto operaci mohou provést během několika milisekund.

Z toho vyplývá, že žádné zrychlení ve většině případu nenastane. Pokud by aplikace chtěla prohledat celý registr, přečtení všech hodnot mého HKCU klíče zabralo OS 314 milisekund &ndash; zrychlení (pokud nějaké) by se pohybovalo v řádu desítek až stovek mikrosekund.

Celé čištění/optimalizování registru je tedy z technického hlediska založeno pouze na tzv. [placebo efektu](https://cs.wikipedia.org/wiki/Placebo).

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Čističe registru hledají chyby v registru na základě svých pravidel. Každá hodnota registru je unikát a může se s jednotlivými OS lišit. ***Nikdo*** nemůže tímto způsobem 100% určit, že hodnota je chybná/nepotřebná.</p></div>

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

<div class="alert success"><p><em class="icon-ok-circled"></em>**Tip**<br>
Pokud chcete i tak používat CCleaner, doporučuji stáhnout si portable verzi a nepoužívat část čistící registr.</p></div>

<br><br><hr><br>

## Bezpečné čištění OS Windows:

K bezpečné údržbě vašeho OS používejte vestavěné nástroje Windows.

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Následující postup je vhodné provádět 1x za několik měsíců.</p></div>

<h3 class="nocol">![cleanmgr](https://securityhandbook.cz/img/icons/cleanmgr.png) Disk Space Cleanup Manager</h3>

- Otevřete si **hledání Windows**, do vyhledávacího pole zadejte:
<li style="list-style-type: none"><pre><code>cleanmgr</code></pre></li>
- Nalezenou položku otevřete.
- Budete-li vyzváni k výběru disku k pročištění, ponechte výchozí nastavení (*systémový disk C*) a klikněte na tlačítko <span class="green">OK</span>.
- Otevře se nabídka souborů ke smazání. Zde zatrhněte veškeré dostupné možnosti kromě **Mezipaměť shaderů DirectX**, **Stažené soubory** a **Miniatury**.
- Klikněte na <span class="green">OK</span> a odsouhlaste odstranění souborů.
- Nechte aplikaci pracovat, po dokončení činnosti se sama ukončí.

<br>

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Následující postup je vhodné provádět 1x za dva týdny, případně měsíčně.</p></div>

<h3 class="nocol">![cmd](https://securityhandbook.cz/img/icons/cmd.png) Čištění TEMP</h3>

- Stiskněte kláv. zkratku <img src="https://securityhandbook.cz/img/icons/wkey.png" alt="win"> <span class="ks">+ X</span> a z nabídky vyberte <span class="green">Windows PowerShell</span>.
- Do příkazové řádky zadejte následující příkaz:
<li style="list-style-type: none"><pre><code>Get-ChildItem -Recurse $Env:TMP | Remove-Item -Recurse -Force</code></pre>
a stiskněte **Enter**.</li>
- Vyčkejte na dokončení požadované akce a aplikaci následně zavřete. Případné chybové hlášky ignorujte, některé soubory nemusí být možné odstranit, pokud jsou používány.

<br><br><hr><br>

## Vsuvka: Málo místa na disku?
Zkuste několik následujících tipů:

> Pročištění záložních souborů

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Po aplikování následujících kroků nebude možné odinstalovat předchozí aktualizace OS.</p></div>

- Stiskněte kláv. zkratku <img src="https://securityhandbook.cz/img/icons/wkey.png" alt="win"> <span class="ks">+ X</span> a z nabídky vyberte <span class="green">Windows PowerShell (správce)</span>.
<li style="list-style-type: none">![wx](https://guides.securityhandbook.cz/img/cs/wx.png)</li>
- Do příkazové řádky zadejte následující příkaz:
<li style="list-style-type: none"><pre><code>sfc /scannow</code></pre></li>
- Spustí se kontrola integrity systémových souborů. Před odstraněním zastaralých záložních souborů je sken žádoucí.
- Po dokončení skenu odstraňte nepotřebné záložní soubory:
<li style="list-style-type: none"><pre><code>dism /online /cleanup-image /startcomponentcleanup /resetbase</code></pre></li>
- Vyčkejte na dokončení požadované akce a následně restartujte OS.


> Hloubkové Vyčištění disku

- Otevřete si **hledání Windows**, do vyhledávacího pole zadejte:
<li style="list-style-type: none"><pre><code>cleanmgr</code></pre></li>
- Na nalezenou položku klikněte na pravým tlačítkem a zvolte možnost: ![admin](https://securityhandbook.cz/img/icons/admin.png) **Spustit jako správce**.
- Budete-li vyzváni k výběru disku k pročištění, ponechte výchozí nastavení (*systémový disk C*) a klikněte na tlačítko <span class="green">OK</span>.
- Otevře se nabídka souborů ke smazání. Zatrhněte veškeré dostupné možnosti.
- Klikněte na <span class="green">OK</span> a odsouhlaste odstranění souborů.
- Nechte aplikaci pracovat, po dokončení činnosti se sama ukončí.
- Restartujte OS.


> Body obnovy

- Stiskněte kláv. zkratku <img src="https://securityhandbook.cz/img/icons/wkey.png" alt="win"> <span class="ks">+ X</span> a z nabídky vyberte <span class="green">Windows PowerShell (správce)</span>.
<li style="list-style-type: none">![wx](https://guides.securityhandbook.cz/img/cs/wx.png)</li>
- Do příkazové řádky zadejte následující příkazy:
<li style="list-style-type: none"><pre><code>vssadmin delete shadows /for=$Env:SystemDrive /all /quiet
vssadmin resize shadowstorage /for=$Env:SystemDrive /on=$Env:SystemDrive /maxsize=2GB</code></pre></li>
- Dojde k odstranění všech bodů obnovy a omezení velikostního limitu na 2 GiB. Vyčkejte na dokončení požadované akce a následně restartujte OS.


> Nepotřebné aplikace (po spuštění)

- Stiskněte kláv. zkratku <img src="https://securityhandbook.cz/img/icons/wkey.png" alt="win"> <span class="ks">+ X</span> a z nabídky vyberte <span class="green">Aplikace a funkce</span>.
- V seznamu identifikujte nepotřebné aplikace, které již pouze zabírají místo na disku, a odinstalujte je.
- V záložce <span class="green">Po spuštění</span> vypněte zbytečné položky zpomalující start OS.
- Aplikaci zavřete.

<br><br><hr><br>

## Automatizace bezpečného čištění OS:

Výše uvedené dva kroky nejsou nijak automatizované, čímž v komfortu výrazně zaostávají za pseudo-čističi třetích stran. Není ovšem problém si výše zmíněné kroky automatizovat sám &ndash; je to práce na pár minut, která přinese kýžený výsledek.

<h3 class="nocol">![cleanmgr](https://securityhandbook.cz/img/icons/cleanmgr.png) Vyčištění disku &ndash; nastavení úlohy</h3>

- Stiskněte kláv. zkratku <img src="https://securityhandbook.cz/img/icons/wkey.png" alt="win"> <span class="ks">+ X</span> a z nabídky vyberte <span class="green">Windows PowerShell</span>.
<li style="list-style-type: none">![wx](https://guides.securityhandbook.cz/img/cs/wx.png)</li>
- Do příkazové řádky zadejte následující příkaz:
<li style="list-style-type: none"><pre><code>cleanmgr /sageset:1</code></pre></li>
- Otevře se konfigurace automatické úlohy Vyčištění disku. Zatrhněte veškeré dostupné možnosti kromě **Mezipaměť shaderů DirectX**, **Stažené soubory** a **Miniatury**.
- Klikněte na <span class="green">OK</span>.

<br>

<h3 class="nocol">![taskschd](https://securityhandbook.cz/img/icons/taskschd.png) Naplánování úlohy &ndash; dusting</h3>

- Stáhněte si skript [Dusting](https://github.com/lhajn/WNT_scripts/releases/download/v1/dusting.zip).
- Uložte a obsah archivu vyextrahujte <span class="blue">na Plochu</span>.
- Skript jménem <span class="green">dusting</span>, který slouží k pravidelnému čištění, přesuňte z Plochy do <span class="blue">kořene systémového disku (**C:\**)</span>.
- Stiskněte kláv. zkratku ![win](https://securityhandbook.cz/img/icons/wkey.png) <span class="ks">+ R</span>, do textového pole zadejte:
<li style="list-style-type: none"><pre><code>taskschd.msc</code></pre>
a stiskněte **Enter**.</li>
- Otevře se Plánovač úloh, v levém menu klikněte na <span class="green">Knihovna plánovače úloh</span>.
- V pravém menu aplikace klikěnte na tlačítko: ![task1](https://guides.securityhandbook.cz/img/cs/duster.png)
- Do položky **Název** vyplňte např. <span class="green">Čištění OS</span> a klikněte na tlačítko <span class="green">Další</span>.
- Zvolte možnost spouštění **Týdně** a klikněte na <span class="green">Další</span>.
- Nastavte opakování na **2** týdny a zatrhněte jeden den, ve který se má úloha spouštět (např. *Pondělí*). Klikněte na <span class="green">Další</span>.
- Nechte zvolenou možnost **Spustit program** a klikněte na <span class="green">Další</span>.
- Ve volbě programu klikněte na <span class="green">Procházet</span> a zvolte skript <span class="green">dusting</span>, který máte uložený v <span class="blue">C:\</span>.
- Výsledek by tedy měl vypadat takto:
<li style="list-style-type: none">![task2](https://guides.securityhandbook.cz/img/cs/duster1.png)</li>
- Klikněte na <span class="green">Další</span>.
- Zatrhněte položku: ![task3](https://guides.securityhandbook.cz/img/cs/duster2.png)
- Klikněte na tlačítko <span class="green">Dokončit</span>.
- Otevřou se vlastnosti úlohy. V horním menu vlastností se přesuňte do záložky **Nastavení**.
- Zde zatrněte následující položku: ![task4](https://guides.securityhandbook.cz/img/cs/duster4.png)
- Klikněte na tlačítko <span class="green">OK</span>.
- Plánovač úloh zavřete.

<div class="alert success"><p><em class="icon-ok-circled"></em>**Úspěch**<br>
Tímto jste nastavili automatické mazání zbytečných souborů, které se spustí jednou za 14 dní. Dále se již o&nbsp;nic nemusíte starat.</p></div>

<br><br><hr>

<h3 class="nocol">Hezký den. <img class="smile" src="https://securityhandbook.cz/img/sm/smile.svg" alt="smile"></h3>
