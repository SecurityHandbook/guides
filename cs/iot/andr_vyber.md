# Jak vybrat bezpečný telefon s OS Android
Výběr bezpečného chytrého telefonu není nijak snadný &ndash; zvláště pro člověka, který se v této problematice neorientuje. Mnoho lidí nebere počítačovou bezpečnost vážně, nezajímá se o ni a nedodržuje základní pravidla. V případě mobilního telefonu je zde ovšem jeden velký rozdíl &ndash; nosíme jej denně v kapse. Infikovaný telefon může odposlouchávat naše rozhovory s ostatními lidmi, zjišťovat naši aktuální polohu, fotit či natáčet nás, naši rodinu nebo domácnost. A tak dále. Nejhorší na tom je, že to pravděpodobně nikdy nezjistíme.

Proto je nezbytné zabývat se aspektem bezpečnosti již při výběru modelu.

## Kritéria výběru pro běžné uživatele:
### Výrobce:
Prvním kritériem výběru telefonu by měl být výrobce. Na trhu působí výrobci, jejichž pověst z pohledu bezpečnosti není příliš dobrá, a naopak výrobci, jejichž pověst je špičková.

Uživatelé by se měli obloukem vyhnout neznámým (obvykle čínským) výrobcům, jelikož telefony sice mohou být levné a dobře vybavené, často ovšem také obsahují předinstalovaný malware. Používat ověřené značky se známou minulostí na trhu je rozumnější volbou.

Ze známějších značek by se uživatelé měli vyvarovat výrobci **<span class="mi">Xiaomi</span>**, jehož modely prokazatelně obsahují *backdoor*, který v lepším případě odesílá telemetrická data bez uživatelova svolení/vědomí. Stejně tak by se uživatelé měli vyvarovat výrobci **<span class="le">Lenovo</span>**, jehož některé modely prokazatelně měly předinstalovaný malware v OS. Další nedůvěryhodné značky z hlediska bezpečnosti jsou **Aligator**, **Alcatel**, **Meizu**, **ZTE**, **Prestigio**, **Leagoo**, **Zopo**, **Doogee**, **Ulefone**, **BLU** a mnohé další.

<br>

### Verze OS Android:
Druhým kritériem výběru by měla být verze samotného OS. V době psaní tohoto článku je nejnovější verzí Android <span class="green">Oreo</span>, konkrétně <span class="green">8.1</span>.

> Proč záleží na verzi OS

Každá verze OS Android přináší mnohá bezpečnostní a jiná vylepšení. **Kitkat** (4.4) přinesl implementaci **SELinux**, která byla ve verzi **Lollipop** (5.0) výrazně zrobustněna. **Marshmallow** přinesl správu oprávnění pro aplikace, kdy si uživatel může zvolit, jaká aplikace má k čemu přístup.

**Nougat** přinesl přepsaný *MediaServer*, který likviduje celé rodiny exploitů a zabraňuje exploitaci na principu exploitu *Stagefright*. Je možné s klidným svědomím říci, že <span class="red">žádná verze OS Android před verzí *Nougat* není bezpečná a neměla by být používána.</span>

**Oreo** posunul sandboxing na mnohonásobně vyšší úroveň díky *Project Treble*, zároveň přinesl celoplošené využítí *seccomp* pro veškeré aplikace. Také výrazně zvýšil bezpečnost *WebView*, zrobustnil model oprávnění aplikací atd.

![Treble case study: media stack](https://guide.mople71.cz/img/en/mstreble.png)
<p class="imgsrcf">*Treble case study: media stack (upraveno).* Zdroj: [What's New in Android Security (Google I/O '17)](https://www.youtube.com/watch?v=C9_ytg6MUP0)</p>

Drobný příklad. Nainstalujete škodlivou aplikaci na *Android 5.0* &ndash; nemáte kontrolu nad oprávněními aplikace, aplikace si může dělat, co chce. Nainstalujete škodlivou aplikaci na *Android 8.1* &ndash; aplikaci můžete odebrat oprávnění, která nechcete. Už se tedy nestane, aby aplikace na svítilnu měla přístup k vašim datům, mikrofonu a videu.

<br>

Z výše uvedených důvodů je vždy nezbytné vybírat z modelů, které mají nejnovější verzi OS Android, v současné době **Oreo** (**8.1**). Starší modely se staršími verzemi OS Android jsou implicitně nebezpečné.

Zde je přehled procentuálního rozložení verzí OS Android na zařízeních v době psaní návodu:

| Verze               | Zastoupení  |
| ------------------- | ----------- |
| Gingerbread         | 0,3 %       |
| Ice Cream Sandwich  | 0,4 %       |
| Jelly Bean          | 5,0 %       |
| KitKat              | 12,0 %      |
| Lollipop            | 24,6 %      |
| Marshmallow         | 28,1 %      |
| Nougat (7.0)        | 22,3 %      |
| Nougat (7.1.x)      | 6,2 %       |
| Oreo                | 1,1 %       |

<br>

### Bezpečnostní aktualizace:
Nejnovější verze OS Android sama o sobě ovšem nic neznamená, jelikož nemusí obsahovat nezbytné bezpečnostní záplaty. Google každý měsíc vydává bezpečnostní bulletin, ve kterém popisuje desítky nově záplatovaných bezpečnostních zranitelností. Tyto bezpečnostní záplaty ovšem v drtivé většině případů nikdy nedorazí k majitelům telefonů, jelikož mnoho výrobců nemá prostředky/zájem (spíše zájem) udržovat své modely aktualizované. Modelů, které jsou opravdu aktuální a mají nejnovější záplaty, je pouze hrstka.

Nejspolehlivější jsou z hlediska bezpečnostních aktualizací telefony přímo od **<span class="go">Google</span>**, tedy řada <span class="green">Pixel</span> a starší řada <span class="green">Nexus</span>, které dostávají pravidelné měsíční bezpečnostní aktualizace. Garance bezpečnostních aktualizací je 3 roky od uvedení modelu. Bulletiny aktualizací naleznete [zde](https://source.android.com/security/bulletin/).

Příklad *Google* následuje výrobce **<span class="no">Nokia</span>**, který se zavázal pro veškeré své modely poskytovat měsíční bezpečnostní aktualizace a vydávání aktualizací garantuje po 2 roky od uvedení modelu. Stejně na tom je výrobce **Essential**.

Pravidelné měsíční bezpečnostní aktualizace dále dostávají vyšší modely značky **<span class="sam">Samsung</span>** (přehled aktualizací [zde](https://security.samsungmobile.com/workScope.smsb)) a vlajkové lodě značky **<span class="lg">LG</span>** (přehled aktualizací [zde](https://lgsecurity.lge.com/security_updates.html)). Tito výrobci ovšem nijak nedeklarovali délku podpory zařízení v podobě bezpečnostních aktualizací, v průměru se jedná o 2 roky.

Výrobce **SONY** odvádí velmi slušnou práci v podpoře svých modelů co se SW týče. Jako jeden z prvních nabízí aktualizace verze OS a pro své vyšší modely vydává časté bezpečnostní aktualizace, podpora jednotlivých modelů je v průměru 1,5 roku.

Výrobce **<span class="hu">Huawei</span>** vydává pravidelné bezpečnostní aktualizace pro své vlajkové lodě a garantuje je po dobu 2 let od vydání modelu. Aktualizace ovšem nemají shodnou dostupnost po celém světě a v ČR se nejedná o žádný zázrak. Čas od času vydá bezpečnostní aktualizace i pro své nižší modely. Stránky PSIRT výrobce Huawei naleznete [zde](http://www.huawei.com/en/psirt).

> Proč záleží na bezpečnostních aktualizacích

Uvedu příklad. Nainstalujete si škodlivou aplikaci na <span class="green">8.1</span> &ndash; máte kontrolu nad oprávněními aplikace a všechna nepotřebná oprávnění tedy můžete zakázat. Nemáte ovšem nejnovější bezpečnostní záplaty. Aplikace tedy může využít známou bezpečnostní díru a dostat se díky ní na úroveň OS, který následně infikuje a uživatel se o tom nikdy nedozví. Toto v praxi aplikuje každý slušný malware pro OS Android, jelikož se jedná o nejjednodušší cestu infekce &ndash; cca. **90% zařízení nemá základní bezpečnostní záplaty**. Z mediálně známých např. Kemoge, Godless,...

<br>

Pouze o výše uvedených modelech má smysl dále se bavit, jelikož modely obsahující známé nezáplatované bezpečnostní zranitelnosti, jsou implicitně nebezpečné.

<br><br><hr><br>

## Přijatelné modely dle kritérií pro běžné uživatele:
- **libovolný model** řady **<span class="go">Pixel</span>**
- **libovolný model** výrobce **<span class="no">Nokia</span>**
- *Essential Phone*
- vlajkové lodě výrobců **<span class="sam">Samsung</span>**, **<span class="lg">LG</span>**, **<span class="hu">Huawei</span>** a **SONY**
- vyšší modely výrobců **<span class="sam">Samsung</span>** a **SONY**

<br><br><hr><br>

## Kritéria výběru pro pokročilé:
### Architektura:
Zařízení by mělo být založeno na 64-bit architektuře (arm64) z mnoha bezpečnostních důvodů, např. už jenom ASLR. V dnešní době jsou všechna moderní zařízení 64-bit.

<br>

### Kernel:
Zařízení by mělo mít nejnovější kernel. Z důvodu obtíží s ovladači (nová verze Androidu ovšem v tomto ohledu přináší změny architektury &ndash; *Project Treble*) na nejnovějších verzích kernelu &ndash; **4.4** / **4.9** &ndash; běží pouze nejnovější zařízení. Novější zařízení běží na kernelu **3.18**, na který jsou zatím backportovány veškeré důležité bezpečnostní funkce. Zbytek zařízení je ovšem zaseknut na kernelu **3.10** nebo na starších &ndash; nepodporovaných &ndash; kernelech (*3.4*,...).

Vzhledem k robustnímu bezpečnostnímu modelu userspace se nyní hackeři soustředí na exploitaci kernelu. V roce 2016 bylo **44 %** ze všech objevených zranitelností v kernelu. V roce 2015 se jednalo pouze o **9 %**.

Mainline kernel (**4.4** / **4.9**) mají zpravidla zařízení od výrobců, kteří do svých modelů instalují své vlastní chipsety, jelikož mají plnou kontrolu nad ovladači &ndash; vyšší modely výrobce *<span class="hu">Huawei</span>* s chipsety **Kirin** (např. P10, Honor 8,...) a vyšší modely výrobce *<span class="sam">Samsung</span>* s chipsety **Exynos** (např. S8). Dále zařízení s nejnovějším chipsetem **Qualcomm** &ndash; např. *<span class="go">Google</span> Pixel 2*, *<span class="no">Nokia</span> 8* atd.

Na LTS kernelu (**3.18**) jsou zaseknutá novější zařízení s Qualcomm/MTK chipsety, např. *<span class="go">Google</span> Pixel*, *<span class="no">Nokia</span>*, *<span class="lg">LG</span> G6* atd. Google na něj kvůli modelu Pixel pracně backportuje veškeré nové mitigace proti exploitům a bezpečnostní fuknce. Zařízení s kernelem 3.18 jsou tedy aktuálně z tohoto pohledu bezpečná &ndash; samozřejmě, je-li kernel aktuální.

Starší zařízení s OS Android běží na EOL kernelech (**3.10** a starší), např. *<span class="go">Google</span> Nexus* atd. Toto již představuje problém, jelikož zatímco na LTS *3.18* kernel Google backportuje bezpečnostní funkce kvůli svému modelu Pixel, backport těchto funkcí na EOL verze kernelu již neprovádí. Zařízení s kernelem *3.10* tedy nemají důležité bezpečnostní funkce jako **PAN emulation**, **hardened-usercopy**. Např. **hardened-usercopy** likviduje cca. *45* % kernel exploitů a proto z tohoto pohledu zařízení běžící na *3.10* nemohou být považována za bezpečná. O starších zařízeních se nemá smysl ani bavit.

![Druhy zranitelností Android kernelu](https://guide.mople71.cz/img/en/kbugs.png)
<p class="imgsrcf">*What causes kernel bugs? (upraveno)* Zdroj: [What's New in Android Security (Google I/O '17)](https://www.youtube.com/watch?v=C9_ytg6MUP0)</p>

Výrobce **Blackberry** rád prohlašuje, že je nejbezpečnější na trhu a uvádí důvody jako &bdquo;**kernel hardening**&ldquo;. Všechny modely Blackberry kromě modelu *KEYone* běží na LTS **3.10** kernelu, takže o nějaké bezpečnosti se v tomto smyslu nedá bavit. A co se týče *&bdquo;kernel hardening&ldquo;*, v podání Blackberry se jedná o několik málo mitigací převzatých z prehistorických *grsecurity* patchů, jde tedy pouze o marketing, z určitého pohledu dokonce o klamavou reklamu. Nemluvě o přístupu výrobce k aktualizacím svých modelů, který je tristní.

Chcete-li vědět používanou verzi kernelu u určitého modelu, můžete zkusit prohledat internet, ale pravděpodobně budete muset nahlédnout přímo do zdrojového kódu. Máte-li model u sebe, stačí se jednoduše podívat do nastavení.

<br>

### Full verified boot:
Zařízení s Android **Nougat** a výše mohou podporovat striktní *verified boot*, kdy telefon nenastartuje v případě poškozeného/napadeného boot oddílu.

<br><br><hr>

<h3 class="nocol">To je vše. Stay safe! ![smile](https://mople71.cz/img/sm/smile.gif)</h3>
