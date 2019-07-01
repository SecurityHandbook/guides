# Zašifrovaná data &ndash; jak postupovat při infikaci ransomware

Ransomware je aktuálně nejoblíbenější technika hackerů, jak si vcelku jednoduše vydělat slušné peníze. Jedná se o druh malware, který po svém spuštění uživateli zablokuje přístup ke všem datům (nejčastěji zašifrováním dat), a následně za jejich dešifrování požaduje peníze. Platby drtivá většina ransomware požaduje v relativně anonymní měně Bitcoin (BTC) či Monero (XMR).

Ransomware se do OS nejčastěji dostane lidskou chybou &ndash; příloha k mailu, zdánlivě bezpečná aplikace, odkliknutí bezpečnostního varování apod. Také se ovšem do OS může dostat chybou v děravém síťovém SW jako Flash nebo Java, dokonce někdy stačí pouze otevřít stránku se škodlivou reklamou.

Z těchto důvodů ransomware představuje obrovské riziko pro jednotlivce i společnosti. Infekce ransomware není neobvyklá a není to žádná ostuda &ndash; může se to stát komukoli (také už jsem si svojí chybou znehodnotil mnoho svých dat, nutno ovšem poznamenat, že vše neprodleně obnovil ze zálohy).

<span class="red">Je důrazně doporučeno nic neplatit</span>, jelikož tím autory podporujete k další činnosti. Bohužel, někdy to je jediná cesta, jak svá cenná data získat zpět. Veřejnost si často myslí, že ransomware není žádný problém, že stačí chvíli hledat na internetu a na daný druh ransomware najdete dekrypter (aplikace, která umožňuje soubory zadarmo rozšifrovat). Není to tak úplně pravda.

Níže si povíme, jak správně identifikovat rodinu ransomware, zjistit, zdali pro ni existuje dekrypter &ndash; pokud ano, jak obnovit data. Následně si řekneme, jak se ransomware zbavit.

Než začneme, měli bychom zmínit ještě jednu věc. Některé rodiny ransomware ve svém zobrazovacím okně zobrazují odpočítávání a hrozí postupným mazáním dat (zde [příklad](https://guide.mople71.cz/img/en/jigsaw.png)). V takovém případě je doporučeno v prvé řadě <span class="red">PC urychleně vypnout a již nezapínat!</span>

<br>

## Krok #1: Identifikace ransomware

Nejprve je logicky nutné ransomware identifikovat, abychom věděli, co dělat dál. Pro spolehlivou identifikaci ransomware můžeme použít vzorek samotného malware, nebo vzorek zašifrovaných souborů a soubor s instrukcemi zanechaný daným ransomware.

Váš úkol je tedy zajistit vzorek pro spolehlivou identifikaci za použití jedné z variant. Jednodušší a rychlejší je druhá varianta, ale pro zajímavost zde zmíníme i první, která je samozřejmě přesnější, ale nedoporučena pro běžné uživatele. Nutno zmínit, že ve většině případů druhá varianta postačí.

### Identifikace pomocí vzorku ransomware (nedoporučeno):

> Návod

Vzorek ransomware obvykle nalezete v lokacích <span class="blue">%appdata%</span>, <span class="blue">%localappdata%</span> a <span class="blue">%temp%</span>. Pokud nevíte, jak se do těchto lokací dostat, stiskněte kláv. zkratku ![win](https://mople71.cz/img/icons/wkey.png) <span class="ks">+ R</span>, do textového pole následně zadejte požadovanou cestu (např. %appdata%) a stiskněte **Enter**.

Také se můžete ve Správci úloh podívat na běžící procesy, identifikovat běžící ransomware, kliknout na něj pravým tlačítkem a otevřít lokaci procesu. V obou případech aplikaci zkopírujte **na Plochu**.

Po zajištění vzorku ransomware jej analyzujte webovou službou [VirusTotal](https://virustotal.com/).

- Navštivte [VirusTotal](https://virustotal.com/).
- Klikněte na tlačítko <span class="green">Nahrát a zkontrolovat soubor</span> a vyberte požadovaný vzorek ransomware.
- Uplynulo-li posledního skenu více než 24 hodin, kliknutím na tři tečky v horním pravém rohu rozbalte menu a zvolte možnost <span class="green">Analyzovat znovu</span>.
- Po dokončení analýzy se vám zobrazí výsledky.
- Zde můžete vidět, jak daný ransomware detekují různé AV. Důležité informace také můžete naleznout v komentářích.</li>

Nyní tedy snad víme, o co se jedná. Díky tomu můžeme snadno dohledat dekrypter &ndash; pokud existuje. Pokud ne, máme v tuto chvíli smůlu.

<br>

### Identifikace pomocí zašifrovaného souboru a instrukcí k odšifrování (doporučeno):
Jak již bylo zmíněno výše, díky analytikovi *Michael Gillespie* skupině *MalwareHunterTeam* je tato metoda velmi snadná, jelikož vytvořili a udržují online službu, jež je schopna určit, kterým druhem ransomware jste byli infikováni. K tomu je ovšem nutné zajistit vzorek zašifrovaného souboru a TXT soubor s instrukcemi.

Pokud OS můžete normálně používat a ransomware neukazuje odpočítávání, klidně můžete k PC připojit USB disk (samozřejmě prázdný, jinak riskujete zašifrování jeho obsahu) a jedoduše požadované soubory např. z Plochy na disk přetáhnout. Riziko přenosu infekce na flash disk a následné infikace jiného OS je mizivé.

Pokud OS nelze používat nebo ransomware ukazuje odpočítávání a hrozí postupným mazáním dat, případně pokud si jen chcete být jistí, je doporučeno v prvé řadě <span class="red">OS urychleně vypnout</span>. Následně stáhněte live linux ISO (např. [Fedora](https://getfedora.org/cs/workstation/)), vytvořte si bootovací USB disk a nabootujte z něj na infikovaném PC.

Pokud můžete, překopírujte veškerá svá zašifrovaná data na jiné úložiště. Tento krok byste s největší pravděpodobností stejně museli provést v pozdější fázi. Pokud u sebe aktuálně nemáte dostatečně velké médium, překopírujte pouze dva libovolné zašifrované soubory a soubor s instrukcemi (obvykle něco jako *HELP_DECRYPT.TXT*, bývá na Ploše, případně v Dokumentech). Následně soubory přesuňte na PC s přístupem k internetu a můžeme zjistit, jakým ransomware jsou data šifrována.

- Otevřete si dvě kopie (ve dvou panelech) stránky [ID Ransomware](https://id-ransomware.malwarehunterteam.com/index.php?lang=cs_CZ).
- Nejprve v prvním panelu nahrajte jeden ze zašifrovaných souborů a vyčkejte na výsledek.
<li style="list-style-type: none">![idrw](https://guide.mople71.cz/img/cs/idrw.png)</li>
- Přesuňte se do druhého panelu, ve kterém nahrajte soubor s instrukcemi k dešifrování a vyčkejte na výsledek.
<li style="list-style-type: none">![idrw1](https://guide.mople71.cz/img/cs/idrw1.png)</li>
- Výsledky v obou panelech porovnejte a měli byste dojít k jasnému výsledku. ID Ransomware vám také prozradí, zdali je možné daný ransomware možné zdarma dešifrovat.
<li style="list-style-type: none">![idrw2](https://guide.mople71.cz/img/cs/idrw2.png)</li>

> Možné výsledky ID Ransomware

- V případě snadné možnosti obnovy dat IDR zobrazí následující hlášku a obvykle vás pošle přímo k dekryptoru &ndash; stačí kliknout na <span class="red">Klikněte zde pro více informací o ****</span>.
<li style="list-style-type: none">![idrw2](https://guide.mople71.cz/img/cs/idrw2.png)</li>
- V případě složitější a problematičtější možnosti obnovy dat zobrazí IDR následující hlášku. V takovém případě to již chce použít Google a mít nadprůměrné znalosti IT. Nebo si zde založte téma, rádi vám pomůžeme.
<li style="list-style-type: none">![idrw3](https://guide.mople71.cz/img/cs/idrw3.png)</li>
- V případě kompletní absence dekrypteru zobrazí IDR následující hlášku. V tomto případě je opravdu jediná možnost data zálohovat a čekat na dekryptor.
<li style="list-style-type: none">![idrw4](https://guide.mople71.cz/img/cs/idrw4.png)</li>
- Pokud se jedná o čerstvou rodinu ransomware, která ještě není dostatečně zdokumentovaná a analyzovaná, zobrazí IDR následující hlášku. V tomto případě použijte Google, případně se zde zeptejte.
<li style="list-style-type: none">![idrw5](https://guide.mople71.cz/img/cs/idrw5.png)</li>
- Pokud IDR daný ransomware nezná, zobrazí následující hlášku. V tomto případě doporučuji založit si zde vlákno, může se totiž jednat o známý a dešifrovatelný ransomware, který služba jenom nezná. Pokud se opravdu jedná o čerstvý nezdokumentovaný kousek, poskytnutím svých vzorků a informací můžete pomoci dekryptor vytvořit.
<li style="list-style-type: none">![idrw6](https://guide.mople71.cz/img/cs/idrw6.png)</li>

<br><br><hr><br>

## Krok #2: Obnova dat
V předchozím kroku jste se dozvěděli, jakým typem ransomware jste byli infikováni a zdali je dešifrovatelný.

Pokud <span class="red">není</span> dešifrovatelný, máte následující možnosti:

- obnovit data ze zálohy
- zašifrovaná data odložit a doufat, že se v budoucnu objeví dekryptor (ne moc pravděpodobné)
- <span class="s">zaplatit výkupné autorům ransomware</span> (to prosím pokud možno nedělejte, podporujete tím autory ransomware a znehodnocujete tím práci všech malwarefighterů)

Pokud <span class="red">je</span> dešifrovatelný, data stačí přesunout na jiný PC a odtud je pomocí dekrypteru dešifrovat. K dekrypterům na jejich stránkách zpravidla naleznete podrobné instrukce. Obvykle je potřeba mít zašifrovanou i nezašifrovanou verzi souboru. Většinu dekrypterů má na svědomí [Emsisoft](https://decrypter.emsisoft.com/) a [Demonslay335](https://www.bleepingcomputer.com/download/publisher/michael-gillespie/), dále [Kaspersky, Trend Micro, AVG, Avast...](https://www.nomoreransom.org/cs/decryption-tools.html)

K dekrypteru vás je schopna nasměrovat služba ID Ransomware. Pokud selže, můžete použít Google nebo se zeptat zde.

<br><br><hr><br>

## Krok #3: Odstranění ransomware

Vzhledem k tomu, co jsou některé rodiny ransomware schopny provést s/v OS, nedoporučuji se pouštět do čištění. Naopak doporučuji přenést veškerá důležitá data z **celého fyzického disku** s infikovaným OS na externí médium. Následně celý disk vyčistit a nainstalovat čistou instalaci Windows.

Návody na čistou instalaci + vyčištění disku (DISKPART část v návodech) naleznete zde:

- [Čistá instalace Windows 10](https://guide.mople71.cz/cs/wnt/w10install.php)
- [Čistá instalace Windows 8.1](https://guide.mople71.cz/cs/wnt/w8install.php)
- [Čistá instalace Windows 7](https://guide.mople71.cz/cs/wnt/w7install.php)

<br><br><hr><br>

## Krok #4: Prevence
**Zálohovat, zálohovat, zálohovat.**

Chcete-li vědět, jak se účinně bránit před ransomware, vyhraďte si chvíli volného času a pročtěte si celé [FAQ Bezpečnosti](https://faq.mople71.cz/cs/).

<br><br><hr>

<h3 class="nocol">Hezký den. <img class="smile" src="https://mople71.cz/img/sm/smile.svg" alt="smile"></h3>
