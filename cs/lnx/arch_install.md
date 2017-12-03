# Instalace Arch Linux
Jelikož informace o distribuci *Arch Linux* nejsou vždy v českém jazyce dostupné/aktuální, popíšu zde korektní postup její instalace. Jedná se v základě o velmi jednoduchý proces, stačí trocha praxe a přehledného postupu.

<br>

## Instalační médium
Návod na vytvoření instalačního média je určen pro **OS Linux**. Pokud vytváříte instalační médium z **OS Windows**, jednoduše použijte <a href="http://rufus.akeo.ie/">Rufus</a>.

- Otevřete si <a href="https://mirror.vpsfree.cz/archlinux/iso/">následující stránku</a>.
- Nalezněte složku s nejnovějším obrazem a otevřete ji. Stáhněte si *ISO* a jeho *SIG* podpis.
- Zkontrolujte podpis ISO souboru pomocí následujícího příkazu:
<li style="list-style-type: none"><pre><code>gpg --keyserver-options auto-key-retrieve --verify archlinux-<verze>-x86_64.iso.sig</code></pre></li>
- Vložte USB disk do PC.
- Zjistěte jeho identifikátor:
<li style="list-style-type: none"><pre><code>lsblk</code></pre></li>
- Následně jej odpojte &ndash; s největší pravděpodobností byl automaticky připojen. (<span class="red">x</span> vždy nahraďte příslušným písmenem)
<li style="list-style-type: none"><pre><code>sudo umount /dev/sdx</code></pre></li>
- Vybalte na něj instalační soubory *Arch Linux*.
<li style="list-style-type: none"><pre><code>sudo dd bs=4M if=/cesta/k/archlinux-<verze>-x86_64.iso of=/dev/sdx status=progress && sync</code></pre></li>

<br><br><hr><br>

## Příprava na instalaci
- Nabootujte live OS. V průběhu instalace budete používat americké rozložení klávesnice, máte jej popsané na levé straně kláves vaší fyzické klávesnice.
- Ověřte připojení k internetu:
<li style="list-style-type: none"><pre><code>ping -c3 8.8.8.8</code></pre></li>
- Pokud používáte WiFi připojení, musíte se nejprve připojit k vaší síti:
<li style="list-style-type: none"><pre><code>wifi-menu -o</code></pre></li>
- Aktualizujte datum a čas:
<li style="list-style-type: none"><pre><code>timedatectl set-ntp true</code></pre></li>

<br>

### Rozdělení disku:
- Nyní přichází k nejpracnější část návodu. Nejprve zjistěte název požadovaného disku:
<li style="list-style-type: none"><pre><code>lsblk</code></pre></li>
- Jakmile identifikujete váš disk, otevřete jej v aplikaci <span class="green">parted</span>. (<span class="red">x</span> vždy nahraďte příslušným písmenem)
<li style="list-style-type: none"><pre><code>parted /dev/sdx</code></pre></li>
- Otevře se správa disku. Nejprve korektně nastavte výchozí jednotku a následně vypište aktuální stav disku.
<li style="list-style-type: none"><pre><code>unit GiB
print</code></pre></li>

> Přepsání celého disku a vymezení určité části pro Arch (1 disk GPT)

- Odstraňte předchozí záznamy o diskových oddílech.
<li style="list-style-type: none"><pre><code>mklabel gpt</code></pre></li>
- Vytvořte ESP oddíl:
<li style="list-style-type: none"><pre><code>mkpart ESP fat32 1MiB 513MiB
set 1 boot on</code></pre></li>
- Vytvořte systémový oddíl o velikosti 50 GB:
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 513MiB 50.5</code></pre></li>
- Vytvořte datový oddíl libovolné velikosti (např. 500 GB &ndash; upravte):
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 50.5 550.5</code></pre></li>
- Vytvořte oddíl na dočasné soubory o velikosti 2 GB:
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 550.5 552.5</code></pre></li>
- Vytvořte swap oddíl o velikosti 2 GB:
<li style="list-style-type: none"><pre><code>mkpart primary linux-swap 552.5 554.5</code></pre></li>
- Oddíly zkontrolujte a editor ukončete:
<li style="list-style-type: none"><pre><code>print
quit</code></pre></li>

<br>

### Vytvoření souborových systémů:
- Vypište a identifikujte jednotlivé diskové oddíly:
<li style="list-style-type: none"><pre><code>lsblk</code></pre></li>
- Vytvořte *FAT32* pro **ESP oddíl**:
<li style="list-style-type: none"><pre><code>mkdosfs -F32 /dev/sdx1</code></pre></li>
- Vytvořte *swap*:
<li style="list-style-type: none"><pre><code>mkswap /dev/sdx5
swapon /dev/sdx5</code></pre></li>
- Vytvořte *BTRFS* pro zbylé oddíly:
<li style="list-style-type: none"><pre><code>mkfs.btrfs -f /dev/sdx2
mkfs.btrfs -f /dev/sdx3
mkfs.btrfs -f /dev/sdx4</code></pre></li>

<br>

### Připojení vytvořených oddílů:
- Připojte systémový oddíl.
<li style="list-style-type: none"><pre><code>mount /dev/sdx2 /mnt</code></pre></li>
- Připojte **ESP** oddíl jako */boot/efi*:
<li style="list-style-type: none"><pre><code>mkdir -p /mnt/boot/efi
mount /dev/sdx1 /mnt/boot/efi</code></pre></li>
- Připojte datový oddíl jako */home* a oddíl pro dočasné soubory jako */tmp*:
<li style="list-style-type: none"><pre><code>mkdir -p /mnt/home
mkdir -p /mnt/tmp
mount /dev/sdx3 /mnt/home
mount /dev/sdx4 /mnt/tmp</code></pre></li>

<br><br><hr><br>

## Instalace
- Upravte seznam zrcadel pro stahování balíčků. Řádky mažete klávesovou zkratkou **Ctrl** + **K**. Změny zavřete a uložíte **Ctrl** + **X** a klávesou <span class="red">Y</span>.
<li style="list-style-type: none"><pre><code>nano /etc/pacman.d/mirrorlist</code></pre></li>
- Můj *mirrorlist* vypadá nějak takto:
<li style="list-style-type: none"><pre><code>##
## Arch Linux repository mirrorlist
## Filtered by mirror score from mirror status page
## Generated on 2017-07-01
##

## Czech Republic
Server = http://mirrors.nic.cz/archlinux/$repo/os/$arch
## Germany
Server = http://ftp.uni-bayreuth.de/linux/archlinux/$repo/os/$arch
## Czech Republic
Server = http://mirror.vpsfree.cz/archlinux/$repo/os/$arch
## Czech Republic
Server = http://ftp.fi.muni.cz/pub/linux/arch/$repo/os/$arch
## Germany
Server = http://ftp.uni-kl.de/pub/linux/archlinux/$repo/os/$arch
## Czech Republic
Server = http://mirror.dkm.cz/archlinux/$repo/os/$arch
## Slovakia
Server = http://tux.rainside.sk/archlinux/$repo/os/$arch
## Germany
Server = http://mirror.de.leaseweb.net/archlinux/$repo/os/$arch</code></pre></li>
- Vytvořte OS:
<li style="list-style-type: none"><pre><code>pacstrap /mnt base base-devel</code></pre></li>
- Po dokončení vytvořte *fstab* a zkopírujte jej do nového OS.
<li style="list-style-type: none"><pre><code>genfstab -U /mnt >> /mnt/etc/fstab</code></pre></li>

<br><br><hr><br>

## Konfigurace
Gratuluji, prošli jste nejtěžší částí návodu. ![smile](https://mople71.cz/img/sm/smile.gif)

- Přepněte se do nového OS.
<li style="list-style-type: none"><pre><code>arch-chroot /mnt</code></pre></li>
- Nastavte čas:
<li style="list-style-type: none"><pre><code>ln -sf /usr/share/zoneinfo/Europe/Prague /etc/localtime
hwclock --systohc</code></pre></li>
- Nastavte lokalizaci (jazyk) OS. V seznamu nalezněte řádek <span class="red">#cs_CZ.UTF-8</span> a odstraňte mřížku na jeho začátku.
<li style="list-style-type: none"><pre><code>nano /etc/locale.gen</code></pre></li>
- Vytvořte lokalizaci a určete jako výchozí:
<li style="list-style-type: none"><pre><code>locale-gen
echo LANG=cs_CZ.UTF-8 > /etc/locale.conf</code></pre></li>
- Nastavte název svého OS v síti (např. *arch*):
<li style="list-style-type: none"><pre><code>echo arch > /etc/hostname</code></pre></li>
- Nainstalujte potřebné aplikace pro připojení k WiFi a nástroje pro *btrfs* a *NTFS*:
<li style="list-style-type: none"><pre><code>pacman -Sy iw wpa_supplicant dialog btrfs-progs ntfs-3g</code></pre></li>
- Máte-li CPU od **Intel**, nainstalujte microcode:
<li style="list-style-type: none"><pre><code>pacman -S intel-ucode</code></pre></li>
- Nainstalujte **GRUB**:
<li style="list-style-type: none"><pre><code>pacman -S grub efibootmgr dosfstools
grub-install /dev/sdx
grub-mkconfig -o /boot/grub/grub.cfg</code></pre></li>

<br>

### Vytvoření uživatele:
- Vytvořte svého uživatele jako správce.
<li style="list-style-type: none"><pre><code>useradd -m -G wheel -s /bin/bash uživatelské_jméno</code></pre></li>
- Změňte heslo uživatele, zatím může být pouze ve stylu *ahojahoj*.
<li style="list-style-type: none"><pre><code>passwd uživatelské_jméno</code></pre></li>
- Nastavte **sudo**:
<li style="list-style-type: none"><pre><code>EDITOR=nano visudo</code></pre></li>
- Sjeďte na konec souboru, nalezněte řádek <span class="red">#%wheel ALL=(ALL) ALL</span> a odstraňte mřížku na jeho začátku:
<li style="list-style-type: none"><pre><code>## Uncomment to allow members of group wheel to execute any command
%wheel ALL=(ALL) ALL</code></pre></li>

<br>

### Ovladače GPU:
- Zjistěte, jakou máte grafickou kartu. Pokud si nejste jistí, můžete ověřit následujícím příkazem:
<li style="list-style-type: none"><pre><code>lspci | grep -e VGA -e 3D</code></pre></li>
- Následně dle tabulky vyberte vhodný ovladač.

| Výrobce  | Typ           | Ovladač               | OpenGL        |
| -------- | ------------- | --------------------- | ------------- |
| AMD      | open-source   | xf86-video-amdgpu     | mesa          |
| Intel    | open-source   | xf86-video-intel      | mesa          |
| nVidia   | proprietární  | nvidia                | nvidia-utils  |
| nVidia   | open-source   | xf86-video-nouveau    | mesa          |

![idea](https://mople71.cz/img/sm/idea.gif) S *open-source* ovladačem pro karty **nVidia** si moc nezahrajete, spíš vůbec. Plánujete-li hrát hry či provádět jinak náročné činnosti na GPU, použijte proprietární ovladač.

- Potřebné balíčky nainstalujte. Předpokládejme např. nVidia GTX 960:
<li style="list-style-type: none"><pre><code>pacman -S nvidia nvidia-utils</code></pre></li>

<br>

### Grafické rozhraní:
- Nyní nainstalujte **GNOME** jako nejbezpečnější desktopové prostředí.
<li style="list-style-type: none"><pre><code>pacman -S gdm
pacman -S gnome network-manager-applet</code></pre></li>
- Pokud nevíte, co která aplikace dělá, a nedokážete to zjistit, prostě nainstalujte všechny (**Enter**).
- Nastavte spuštění *GNOME* při startu.
<li style="list-style-type: none"><pre><code>systemctl enable gdm
systemctl enable NetworkManager</code></pre></li>
- Stiskněte klávesovou zkratku **Ctrl** + **D**.
- Odpojte oddíly nového OS.
<li style="list-style-type: none"><pre><code>umount -R /mnt</code></pre></li>
- Restartujte PC.
<li style="list-style-type: none"><pre><code>reboot</code></pre></li>

<br>

### První přihlášení:
- Pokud jste vše udělali správně, za chvíli se zobrazí přihlašovací obrazovka *GNOME* s vaším vytvořeným účtem. Přihlaste se.
- Otevřete si <span class="green">Nastavení</span> a změňte klávesnici na českou/dle vaší preference.
- Přihlaste se na WiFi.
- Otevřete si <span class="green">Terminál</span>.
- Zakažte přihlášení uživatele **root** a zároveň ověřte korektní konfiguraci *sudo*:
<li style="list-style-type: none"><pre><code>sudo passwd -l root</code></pre></li>
- Nainstalujte důležité knihovny a aplikace:
<li style="list-style-type: none"><pre><code>sudo pacman -S gnome-tweak-tool asp gnupg chromium mpv libmtp flatpak gedit file-roller gnome-calendar git gimp transmission-gtk acpi tlp youtube-dl unzip libmatroska flac libmad libx264 x265 ffmpeg2.8
sudo systemctl enable tlp</code></pre></li>
- Odstraňte nepotřebné aplikace jako GNOME přehrávač:
<li style="list-style-type: none"><pre><code>sudo pacman -R totem</code></pre></li>
- Restartujte OS.

<br><br><hr><br>

## Doporučení:
- V prvé řadě si nastudujte <a href="https://faq.mople71.cz/cs/lnx/index.php#lin">FAQ Bezpečnosti</a>. Až se pořádně seznámíte s OS, můžete poté již být bráni jako pokročilí, v takovém případě je zde <a href="https://faq.mople71.cz/cs/lnx/adv.php#lin">FAQ Bezpečnosti pro pokročilé</a>.
- Preferujte Flatpak verze aplikací, např. **Steam** ve flatpaku je jediná rozumná varianta, jak jej rozchodit na *Arch Linux*.
- ...

<br><br><hr>

<h3 class="nocol">To je vše. Stay safe! ![smile](https://mople71.cz/img/sm/smile.gif)</h3>
