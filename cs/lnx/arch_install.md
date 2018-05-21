# Instalace Arch Linux
Aktualizovaný postup ke korektní instalaci distribuce *Arch Linux* není vždy v českém jazyce dostupný. Jedná se v zásadě o jednoduchý proces, každý krok je logický a srozumitelný, navíc při dostatečné praxi zabere pouze cca. 30 minut. Tento návod slouží (zatím) spíše pro osobní použití.

<br>

## Instalační médium
Návod na vytvoření instalačního média je určen pro **OS Linux**. Pokud vytváříte instalační médium z **OS Windows**, jednoduše použijte <a href="http://rufus.akeo.ie/">Rufus</a>.

- Otevřete si [následující stránku](https://pkg.adfinis-sygroup.ch/archlinux/iso/latest/).
- Stáhněte si nejnovější *ISO* a jeho *SIG* podpis.
- Zkontrolujte podpis ISO souboru pomocí následujícího příkazu:
<li style="list-style-type: none"><pre><code>gpg --keyserver-options auto-key-retrieve --verify archlinux-<verze>-x86_64.iso.sig</code></pre></li>
- Vložte USB disk do PC.
- Zjistěte jeho identifikátor:
<li style="list-style-type: none"><pre><code>lsblk</code></pre></li>
- Následně jej odpojte &ndash; s největší pravděpodobností byl automaticky připojen. (<span class="red">x</span> vždy nahraďte příslušným písmenem)
<li style="list-style-type: none"><pre><code>sudo umount /dev/sdx</code></pre></li>
- Rozbalte na něj instalační soubory *Arch Linux*.
<li style="list-style-type: none"><pre><code>sudo dd bs=4M if=/cesta/k/archlinux-<verze>-x86_64.iso of=/dev/sdx status=progress && sync</code></pre></li>

<br><br><hr><br>

## Příprava na instalaci
- Nabootujte live OS. V průběhu instalace budete používat americké rozložení klávesnice, máte jej popsané na levé straně kláves vaší fyzické klávesnice.
- Ověřte připojení k internetu:
<li style="list-style-type: none"><pre><code>ping -c3 8.8.8.8</code></pre></li>
- Pokud používáte WiFi připojení, musíte se nejprve připojit k vaší síti:
<li style="list-style-type: none"><pre><code>wifi-menu</code></pre></li>
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
- Vytvořte datový oddíl libovolné velikosti (v příkladu níže 500 GB):
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
- Vytvořte *fat32* pro **ESP oddíl** a *&bdquo;přepište&ldquo;* ostatní oddíly:
<li style="list-style-type: none"><pre><code>mkdosfs -F32 /dev/sdx1
mkdosfs -F32 /dev/sdx2
mkdosfs -F32 /dev/sdx3
mkdosfs -F32 /dev/sdx4</code></pre></li>
- Vytvořte *swap*:
<li style="list-style-type: none"><pre><code>mkswap /dev/sdx5
swapon /dev/sdx5</code></pre></li>
- Vytvořte *btrfs* pro zbylé oddíly:
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
<li style="list-style-type: none"><pre><code>mkdir /mnt/home
mkdir /mnt/tmp
mount /dev/sdx3 /mnt/home
mount /dev/sdx4 /mnt/tmp</code></pre></li>

<br><br><hr><br>

## Instalace
- Upravte seznam zrcadel pro stahování balíčků. Řádky mažete klávesovou zkratkou **Ctrl** + **K**. Změny zavřete a uložíte **Ctrl** + **X** a klávesou <span class="red">Y</span>.
<li style="list-style-type: none"><pre><code>nano /etc/pacman.d/mirrorlist</code></pre></li>
<li style="list-style-type: none"><pre><code>##
## Arch Linux repository mirrorlist
## Filtered by mirror score from mirror status page
## Generated on 2018-03-01
##

## Switzerland
Server = https://pkg.adfinis-sygroup.ch/archlinux/$repo/os/$arch
## Switzerland
Server = https://mirror.puzzle.ch/archlinux/$repo/os/$arch</code></pre></li>
- Vytvořte OS:
<li style="list-style-type: none"><pre><code>pacstrap /mnt base base-devel</code></pre></li>
- Po dokončení vytvořte *fstab* pro nový OS. Následně jej zkontrolujte.
<li style="list-style-type: none"><pre><code>genfstab -U /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab</code></pre></li>

<br><br><hr><br>

## Konfigurace
Gratuluji, to nejhorší již máte za sebou. ![smile](https://mople71.cz/img/sm/smile.gif)

- Přepněte se do nového OS.
<li style="list-style-type: none"><pre><code>arch-chroot /mnt</code></pre></li>
- Nastavte čas:
<li style="list-style-type: none"><pre><code>ln -sf /usr/share/zoneinfo/Europe/Prague /etc/localtime
hwclock --systohc</code></pre></li>
- Nastavte lokalizaci (jazyk) OS. Chcete-li češtinu, v seznamu nalezněte řádek <span class="red">#cs_CZ.UTF-8</span> a odstraňte mřížku na jeho začátku.
<li style="list-style-type: none"><pre><code>nano /etc/locale.gen</code></pre></li>
- Vytvořte lokalizaci a určete ji jako výchozí:
<li style="list-style-type: none"><pre><code>locale-gen
echo LANG=cs_CZ.UTF-8 > /etc/locale.conf</code></pre></li>
- Nastavte název svého OS v síti (např. *arch*):
<li style="list-style-type: none"><pre><code>echo arch > /etc/hostname</code></pre></li>
- Nainstalujte potřebné aplikace pro připojení k WiFi a nástroje k souborovým systémům:
<li style="list-style-type: none"><pre><code>pacman -Sy iw wpa_supplicant dialog btrfs-progs ntfs-3g dosfstools</code></pre></li>
- Máte-li novější CPU od **Intel**, nainstalujte microcode:
<li style="list-style-type: none"><pre><code>pacman -S intel-ucode</code></pre></li>
- Nainstalujte **GRUB**:
<li style="list-style-type: none"><pre><code>pacman -S grub efibootmgr
grub-install /dev/sdx
grub-mkconfig -o /boot/grub/grub.cfg</code></pre></li>

<br>

### Vytvoření uživatele:
- Vytvořte svého uživatele jako správce.
<li style="list-style-type: none"><pre><code>useradd -m -G wheel -s /bin/bash uživatelské_jméno</code></pre></li>
- Změňte heslo uživatele.
<li style="list-style-type: none"><pre><code>passwd uživatelské_jméno</code></pre></li>
- Nastavte **sudo**:
<li style="list-style-type: none"><pre><code>EDITOR=nano visudo</code></pre></li>
- Sjeďte na konec souboru, nalezněte řádek <span class="red">#%wheel ALL=(ALL) ALL</span> a odstraňte mřížku na jeho začátku:
<li style="list-style-type: none"><pre><code>## Uncomment to allow members of group wheel to execute any command
%wheel ALL=(ALL) ALL
...</code></pre></li>

<br>

### Ovladače GPU:
- Zjistěte, jakou máte grafickou kartu. Pokud si nejste jistí, můžete ověřit následujícím příkazem:
<li style="list-style-type: none"><pre><code>lspci | grep -e VGA -e 3D</code></pre></li>
- Následně dle tabulky vyberte vhodný ovladač.

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
S *open-source* ovladačem pro karty **nVidia** si moc dobře náročné hry nezahrajete. V případě herního zaměření možná bude nezbytné použít proprietární ovladače.</p></div>

| Výrobce            | Typ          | Ovladač            | OpenGL       | HW akcelerace                      |
| ------------------ | ------------ | ------------------ | ------------ | ---------------------------------- |
| AMD<br>(GCN 3 a výše) | open-source  | xf86-video-amdgpu  | mesa         | mesa-vdpau,<br>libva-vdpau-driver     |
| AMD<br>(GCN 2 a níže) | open-source  | xf86-video-ati     | mesa         | mesa-vdpau,<br>libva-vdpau-driver     |
| Intel              | open-source  | xf86-video-intel   | mesa         | libva-intel-driver,<br>libvdpau-va-gl |
| nVidia             | open-source  | xf86-video-nouveau | mesa         | mesa-vdpau,<br>libva-vdpau-driver     |
| nVidia             | proprietární | nvidia             | nvidia-utils | nvidia-utils,<br>libva-vdpau-driver   |

- Potřebné balíčky nainstalujte. Předpokládejme např. nVidia GTX 960:
<li style="list-style-type: none"><pre><code>## Open-source:
pacman -S xf86-video-nouveau mesa mesa-vdpau libva-vdpau-driver

## Proprietární:
pacman -S nvidia nvidia-utils libva-vdpau-driver</code></pre></li>

<br>

### HW-specific konfigurace:
> Staré ThinkPad NTBs:

- Nainstalujte si **tp-smapi**.
<li style="list-style-type: none"><pre><code>pacman -S tp_smapi</code></pre></li>

> Novější ThinkPad NTBs (SandyBridge a výše):

- Nainstalujte si **acpi-call**.
<li style="list-style-type: none"><pre><code>pacman -S acpi_call</code></pre></li>

> Broadcom WiFi adaptér:

- Nainstalujte si **broadcom-wl**.
<li style="list-style-type: none"><pre><code>pacman -S dkms broadcom-wl-dkms</code></pre></li>
- Otevřete nastavení *GRUB*:
<li style="list-style-type: none"><pre><code>nano /etc/default/grub</code></pre></li>
- Zakažte ostatní ovladače.
<li style="list-style-type: none"><pre><code>GRUB_CMDLINE_LINUX_DEFAULT="quiet modprobe.blacklist=b43,b43legacy,ssb,brcmfmac,brcmsmac"</code></pre></li>
- Uložte a aktualizujte konfiguraci *GRUB*.
<li style="list-style-type: none"><pre><code>grub-mkconfig -o /boot/grub/grub.cfg</code></pre></li>

<br>

### Grafické rozhraní:
- Nyní nainstalujte **GNOME** jako nejbezpečnější desktopové prostředí.
<li style="list-style-type: none"><pre><code>pacman -S gdm
pacman -S gnome network-manager-applet</code></pre></li>
- Z výběru balíčků zvolte následující:
<li style="list-style-type: none"><pre><code>evince, file-roller, gedit, gnome-backgrounds, gnome-calculator, gnome-characters,
gnome-clocks, gnome-color-manager, gnome-control-center, gnome-font-viewer,
gnome-getting-started-docs, gnome-keyring, gnome-menus, gnome-screenshot,
gnome-session, gnome-settings-daemon, gnome-shell, gnome-shell-extensions,
gnome-system-monitor, gnome-terminal, gnome-themes-extra, gnome-user-docs,
gnome-video-effects, gvfs, gvfs-afc, gvfs-goa, gvfs-google, gvfs-gphoto2,
gvfs-mtp, gvfs-nfs, mousetweaks, mutter, nautilus, networkmanager, sushi,
xdg-user-dirs-gtk, yelp, gnome-boxes, simple-scan</code></pre></li>
- Čísla výše zmíněných balíčků (mohou se měnit) zadejte následujícím způsobem a stiskněte **Enter**.
<li style="list-style-type: none"><pre><code>5,6,8,9,10,12,...,64</code></pre></li>
- Nastavte spuštění *GNOME* při startu:
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
<li style="list-style-type: none"><pre><code>sudo pacman -S gnome-tweaks asp gnupg mpv libmtp flatpak git acpi tlp youtube-dl unzip libmatroska flac libmad libx264 x265 gstreamer-vaapi pinentry
sudo systemctl enable tlp
sudo systemctl enable tlp-sleep
sudo systemctl mask systemd-rfkill
sudo systemctl mask systemd-rfkill.socket</code></pre></li>
- Restartujte OS.

<br>

### Aplikace:
- Otevřete si <span class="green">Terminál</span>. Nainstalujte flatpak verze aplikací. Preferujte *gnome* repo při dotazu.
<li style="list-style-type: none"><pre><code>flatpak remote-add --if-not-exists gnome https://sdk.gnome.org/gnome.flatpakrepo
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install flathub org.gnome.Evince
sudo chmod 600 /usr/share/applications/evince.desktop
flatpak install flathub org.gnome.eog
flatpak install flathub org.gnome.Epiphany
flatpak install flathub org.gnome.Calendar
flatpak install flathub org.gnome.Weather
flatpak install flathub org.libreoffice.LibreOffice
flatpak install flathub com.transmissionbt.Transmission
flatpak install flathub org.gimp.GIMP
flatpak install flathub org.audacityteam.Audacity
flatpak install flathub io.atom.Atom
flatpak install flathub io.atom.electron.BaseApp
flatpak install flathub com.valvesoftware.Steam
flatpak install flathub org.signal.Signal</code></pre></li>
- Nainstalujte si **Paper Icon Theme**:
<li style="list-style-type: none"><pre><code>git clone https://aur.archlinux.org/paper-icon-theme-git.git
cd paper-icon-theme-git
makepkg -sri</code></pre></li>
- Otevřete si <span class="green">Vylepšení</span> a zvolte **Paper** jako motiv pro ikony.

<br>

### Zabezpečení:
- Nastavte */tmp* oddíl jako **noexec**. Nápověda [zde](https://faq.mople71.cz/cs/lnx/index.php#lnx2), je třeba upravit syntax.
- Nepoužíváte-li *IPv6*, zakažte jej. Nápověda [zde](https://faq.mople71.cz/cs/lnx/index.php#lnx2), je třeba upravit syntax.
- Nastavte *DNSSEC* &ndash; 217.31.204.130,193.29.206.206 &ndash; návod [zde](https://faq.mople71.cz/cs/lnx/index.php#lnx2).
- Nastavte **firewall**:
<li style="list-style-type: none"><pre><code>sudo -i
iptables -P INPUT   DROP
iptables -A INPUT -p tcp -m tcp ! --tcp-flags SYN,RST,ACK SYN -m state --state NEW -j DROP
iptables -N drop_invalid
iptables -A OUTPUT   -m state --state INVALID  -j drop_invalid
iptables -A INPUT    -m state --state INVALID  -j drop_invalid
iptables -A INPUT -p tcp -m tcp --sport 1:65535 --tcp-flags FIN,SYN,RST,PSH,ACK,URG NONE -j drop_invalid
iptables -A drop_invalid -j LOG --log-level debug --log-prefix "INVALID state -- DENY "
iptables -A drop_invalid -j DROP
iptables -A INPUT  -m state --state ESTABLISHED,RELATED  -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT
iptables -N In_RULE_1
iptables -A INPUT -p udp -m udp  -j In_RULE_1
iptables -A In_RULE_1  -j LOG  --log-level info --log-prefix "UDP -- DENY "
iptables -A In_RULE_1  -j DROP
iptables -N In_RULE_2
iptables -A INPUT -p tcp -m tcp  -j In_RULE_2
iptables -A In_RULE_2  -j LOG  --log-level info --log-prefix "TCP -- DENY "
iptables -A In_RULE_2  -j DROP
iptables -N In_RULE_3
iptables -A INPUT  -j In_RULE_3
iptables -A In_RULE_3  -j LOG  --log-level info --log-prefix "XXX -- DENY "
iptables -A In_RULE_3  -j DROP
iptables-save > /etc/iptables/iptables.rules
systemctl enable iptables</code></pre></li>
- Na citlivé záležitosti jako bankovnictví používejte prohlížeč **GNOME Web**. Chcete-li na internetu provádět i jiné činnosti, nainstalujte si **Chromium**.
- Bezpečně nastavte prohlížeč(e). Návod [zde](https://faq.mople71.cz/cs/lnx/index.php#lnx4).
- Restartujte OS.

<div class="alert success"><p><em class="icon-ok-circled"></em>**Úspěch**<br>
Tímto jste nainstalovali a bezpečně nakonfigurovali Arch Linux.</p></div>

<br><br><hr><br>

## Doporučení:
- V prvé řadě si prostudujte <a href="https://faq.mople71.cz/cs/lnx/index.php#lin">FAQ Bezpečnosti</a>. Až se pořádně seznámíte s OS a rozšíříte své znalosti, prostudujte si i <a href="https://faq.mople71.cz/cs/lnx/adv.php#lin">FAQ Bezpečnosti pro pokročilé</a>.
- Preferujte Flatpak verze aplikací.
- ...

<br><br><hr>

<h3 class="nocol">Hezký den. <img class="smile" src="https://mople71.cz/img/sm/smile.svg" alt="smile"></h3>
