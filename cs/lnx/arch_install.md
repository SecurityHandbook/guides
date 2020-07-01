# Instalace Arch Linux
## Instalační médium
Návod na vytvoření instalačního média je určen pro **OS Linux**. Pokud vytváříte instalační médium z **OS Windows**, jednoduše použijte [Rufus](https://guides.securityhandbook.cz/cs/wnt/rufus.php).

- Otevřete si [následující stránku](https://pkg.adfinis-sygroup.ch/archlinux/iso/latest/).
- Stáhněte si nejnovější *ISO* a jeho *SIG* podpis.
- Zkontrolujte podpis ISO souboru pomocí následujícího příkazu:
<li style="list-style-type: none"><pre><code>gpg --keyserver-options auto-key-retrieve --verify archlinux-\*.iso.sig</code></pre></li>
- Vložte USB disk do PC.
- Zjistěte jeho identifikátor.
<li style="list-style-type: none"><pre><code>lsblk</code></pre></li>
- Následně jej odpojte – pokud byl automaticky připojen. (místo <span class="red">x</span> vždy dosaďte příslušné písmeno)
<li style="list-style-type: none"><pre><code>sudo umount /dev/sdx</code></pre></li>
- Rozbalte na něj instalační soubory *Arch Linux*.
<li style="list-style-type: none"><pre><code>sudo dd bs=4M if=./archlinux-\*.iso of=/dev/sdx status=progress && sync</code></pre></li>

<br><br><hr><br>

## Příprava na instalaci
- Nabootujte live OS. V průběhu instalace budete používat americké rozložení klávesnice, máte jej popsané na levé straně kláves vaší fyzické klávesnice.
- Používáte-li WiFi připojení, nejprve se připojte k vaší síti:
<li style="list-style-type: none"><pre><code>wifi-menu</code></pre></li>
- Ověřte připojení k internetu:
<li style="list-style-type: none"><pre><code>ping -c3 8.8.8.8</code></pre></li>
- Aktualizujte datum a čas:
<li style="list-style-type: none"><pre><code>timedatectl set-ntp true</code></pre></li>

<br>

### Rozdělení disku:
- Zjistěte název a aktuální rozložení požadovaného disku:
<li style="list-style-type: none"><pre><code>lsblk</code></pre></li>
- Jakmile identifikujete váš disk, otevřete jej v aplikaci <span class="green">parted</span>.
<li style="list-style-type: none"><pre><code>parted /dev/sdx</code></pre></li>
- Otevře se správa disku. Nastavte *GiB* jako výchozí jednotku a následně vypište aktuální stav disku.
<li style="list-style-type: none"><pre><code>unit GiB
print</code></pre></li>
- Před vytvořením nové tabulky oddílů určtete požadovaný typ rozdělení disku (**GPT** či **MBR**).

<div class="alert info"><p><em class="icon-info-circled"></em>**Info**<br>
Pro stroje z roku 2014 a novější pravděpodobně bude jednat o GPT. U starších přístrojů a většiny virtuálních prostředí ve výchozím nastavení se bude jednat o MBR. **Kroky níže jsou optimalizovány pro GPT schéma.**</p></div>

> Přepsání celého disku a vymezení určité části pro Arch (1 disk GPT)

- Odstraňte předchozí záznamy o diskových oddílech.
<li style="list-style-type: none"><pre><code>mklabel gpt</code></pre></li>
- Vytvořte ESP oddíl:
<li style="list-style-type: none"><pre><code>mkpart ESP fat32 1MiB 513MiB
set 1 boot on</code></pre></li>
- Vytvořte systémový oddíl o velikosti 50 GiB:
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 513MiB 50.5</code></pre></li>
- Vytvořte datový oddíl libovolné velikosti (v příkladu níže 500 GiB):
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 50.5 550.5</code></pre></li>
- Vytvořte oddíl na dočasné soubory o velikosti 2 GiB:
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 550.5 552.5</code></pre></li>
- Vytvořte swap oddíl o velikosti 2 GiB:
<li style="list-style-type: none"><pre><code>mkpart primary linux-swap 552.5 554.5</code></pre></li>
- Oddíly zkontrolujte a editor ukončete:
<li style="list-style-type: none"><pre><code>print
quit</code></pre></li>

> Přepsání celého disku a vymezení určité části pro Arch (1 disk MBR)

- Odstraňte předchozí záznamy o diskových oddílech.
<li style="list-style-type: none"><pre><code>mklabel msdos</code></pre></li>
- Vytvořte systémový oddíl o velikosti 50 GiB:
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 1MiB 50
set 1 boot on</code></pre></li>
- Vytvořte datový oddíl libovolné velikosti (v příkladu níže 500 GiB):
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 50 550</code></pre></li>
- Vytvořte oddíl na dočasné soubory o velikosti 2 GiB:
<li style="list-style-type: none"><pre><code>mkpart primary btrfs 550 552</code></pre></li>
- Vytvořte swap oddíl o velikosti 2 GiB:
<li style="list-style-type: none"><pre><code>mkpart primary linux-swap 552 554</code></pre></li>
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
- Upravte seznam zrcadel pro stahování balíčků. Řádky mažete klávesovou zkratkou **Ctrl** + **K**. Následně zbylé servery upravíte pro přístup přes https. Změny zavřete a uložíte **Ctrl** + **X** a klávesou <span class="red">Y</span>.
<li style="list-style-type: none"><pre><code>nano /etc/pacman.d/mirrorlist</code></pre></li>
<li style="list-style-type: none"><pre><code>## Iceland
Server = https://mirror.system.is/arch/$repo/os/$arch
## Switzerland
Server = https://pkg.adfinis-sygroup.ch/archlinux/$repo/os/$arch
## Czechia
Server = https://ftp.sh.cvut.cz/arch/$repo/os/$arch
## Switzerland
Server = https://mirror.puzzle.ch/archlinux/$repo/os/$arch
</code></pre></li>
- Vytvořte OS:
<li style="list-style-type: none"><pre><code>pacstrap /mnt base base-devel linux nano</code></pre></li>
- Po dokončení vytvořte *fstab* pro nový OS. Následně jej zkontrolujte.
<li style="list-style-type: none"><pre><code>genfstab -U /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab</code></pre></li>

<br><br><hr><br>

## Konfigurace
- Přepněte se do nového OS.
<li style="list-style-type: none"><pre><code>arch-chroot /mnt</code></pre></li>
- Nastavte čas:
<li style="list-style-type: none"><pre><code>ln -s /usr/share/zoneinfo/Europe/Prague /etc/localtime
hwclock --systohc</code></pre></li>
- Nastavte lokalizaci (jazyk) OS. Chcete-li češtinu, v seznamu nalezněte řádek <span class="red">#cs_CZ.UTF-8</span> a odstraňte mřížku na jeho začátku. Změny uložte.
<li style="list-style-type: none"><pre><code>nano /etc/locale.gen</code></pre></li>
- Vytvořte požadovanou lokalizaci a určete ji jako výchozí:
<li style="list-style-type: none"><pre><code>locale-gen
echo LANG=cs_CZ.UTF-8 > /etc/locale.conf</code></pre></li>
- Nastavte název svého OS v síti (např. *arch*):
<li style="list-style-type: none"><pre><code>echo arch > /etc/hostname</code></pre></li>
- Nainstalujte potřebné aplikace pro připojení k WiFi a nástroje k souborovým systémům:
<li style="list-style-type: none"><pre><code>pacman -Sy iw wpa_supplicant dialog btrfs-progs dosfstools</code></pre></li>
- Máte-li novější CPU (Sandy Bridge a výše) od **Intel**, nainstalujte microcode:
<li style="list-style-type: none"><pre><code>pacman -S intel-ucode</code></pre></li>
- Nainstalujte **GRUB**:
<li style="list-style-type: none"><pre><code>pacman -S grub efibootmgr
grub-install /dev/sdx
grub-mkconfig -o /boot/grub/grub.cfg</code></pre></li>

<br>

### Vytvoření uživatele:
- Vytvořte účet správce.
<li style="list-style-type: none"><pre><code>useradd -m -G wheel uživatelské_jméno</code></pre></li>
- Změňte heslo správce.
<li style="list-style-type: none"><pre><code>passwd uživatelské_jméno</code></pre></li>
- Povolte **sudo** pro účet správce.
<li style="list-style-type: none"><pre><code>echo "uživatelské_jméno ALL=(ALL) ALL" > /etc/sudoers.d/uživatelské_jméno</code></pre></li>

<br>

### Ovladače GPU:
- Zjistěte výrobce a model své grafické karty. Pokud si nejste jistí, můžete ověřit následujícím příkazem:
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

- Potřebné balíčky nainstalujte. Pár příkladů níže:
<li style="list-style-type: none"><pre><code>## NVIDIA open-source:
pacman -S xf86-video-nouveau mesa mesa-vdpau libva-vdpau-driver

## NVIDIA proprietární:
pacman -S nvidia nvidia-utils libva-vdpau-driver

## Intel open-source:
pacman -S xf86-video-intel mesa libva-intel-driver</code></pre></li>

<br>

### HW-specific konfigurace:
> (pra)Staré ThinkPad NTBs

- Nainstalujte si **tp-smapi**.
<li style="list-style-type: none"><pre><code>pacman -S tp_smapi</code></pre></li>
- Následně neinstalujte balíček **acpi** v sekci *Konfigurace*.

> Novější ThinkPad NTBs (Sandy Bridge a výše)

- Nainstalujte si **acpi-call**.
<li style="list-style-type: none"><pre><code>pacman -S acpi_call</code></pre></li>
- Následně neinstalujte balíček **acpi** v sekci *Konfigurace*.

> Virtuální OS přes GNOME Boxes

- Nainstalujte si grafický ovladač **qxl** a **spice-vdagent**.
<li style="list-style-type: none"><pre><code>pacman -S xf86-video-qxl spice-vdagent</code></pre></li>

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
- Nainstalujte desktopové prostředí **GNOME**.
<li style="list-style-type: none"><pre><code>pacman -S gdm
pacman -S gnome network-manager-applet gnome-tweaks</code></pre></li>
- Z výběru balíčků zvolte následující:
<li style="list-style-type: none"><pre><code>epiphany, file-roller, gedit, gnome-backgrounds, gnome-calculator, gnome-characters,
gnome-clocks, gnome-color-manager, gnome-control-center, gnome-font-viewer, gnome-keyring, gnome-menus, gnome-screenshot, gnome-shell-extensions,
gnome-system-monitor, gnome-terminal,
gnome-video-effects, gvfs, gvfs-goa, gvfs-google,
gvfs-mtp, mousetweaks, mutter, nautilus, networkmanager,
xdg-user-dirs-gtk, gnome-boxes, gnome-software</code></pre></li>
- Čísla výše zmíněných balíčků (v čase se mění) zadejte následujícím způsobem a stiskněte **Enter**.
<li style="list-style-type: none"><pre><code>4,6,8,9,11,12,...,63</code></pre></li>
- Ponechte výchozí zdroj pro *libjack*.
- Nastavte spuštění *GNOME* při startu:
<li style="list-style-type: none"><pre><code>systemctl enable gdm
systemctl enable NetworkManager</code></pre></li>
- Stiskněte klávesovou zkratku **Ctrl** + **D**.
- Odpojte oddíly nového OS.
<li style="list-style-type: none"><pre><code>umount -R /mnt</code></pre></li>
- Restartujte PC.
<li style="list-style-type: none"><pre><code>reboot</code></pre></li>

<br>

### Nastavení po prvním přihlášení:
- Po chvíli se zobrazí přihlašovací obrazovka *GNOME* s vytvořeným účtem správce. Přihlaste se.
- Připojte se k internetu.
- Otevřete si <span class="green">Terminál</span>.
- Deaktivujte uživatele **root** a zároveň ověřte korektní konfiguraci *sudo*:
<li style="list-style-type: none"><pre><code>sudo passwd -l root</code></pre></li>
- Doinstalujte důležité balíčky:
<li style="list-style-type: none"><pre><code>sudo pacman -S acpi asp flatpak git gnu-free-fonts gstreamer-vaapi libmatroska nftables ninja noto-fonts noto-fonts-emoji tlp ttf-dejavu ttf-droid ttf-liberation ttf-roboto vi
sudo systemctl enable tlp
sudo systemctl enable tlp-sleep
sudo systemctl mask systemd-rfkill
sudo systemctl mask systemd-rfkill.socket</code></pre></li>
- Nainstalujte si **Paper Icon Theme**:
<li style="list-style-type: none"><pre><code>git clone https://aur.archlinux.org/paper-icon-theme-git.git
cd paper-icon-theme-git
makepkg -sri</code></pre></li>
- Otevřete si <span class="green">Vylepšení</span> a zvolte **Paper** jako motiv pro ikony.
- Vytvořte v nastavení běžného uživatele pro denní provoz (podrobnější návod [zde](https://securityhandbook.cz/cs/lnx/index.php#lnx2.2).
- Restartujte OS a přihlaste se na vytvořeného uživatele.

<br>

### Aplikace:
- Otevřete si <span class="green">Terminál</span>. Nainstalujte aplikace / flatpak verze aplikací.
<li style="list-style-type: none"><pre><code>sudo pacman -S mpv youtube-dl chromium
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install flathub org.gnome.Evince
flatpak install flathub org.gnome.eog
flatpak install flathub org.libreoffice.LibreOffice
flatpak install flathub org.gimp.GIMP
flatpak install flathub io.atom.Atom
flatpak install flathub io.atom.electron.BaseApp
flatpak install flathub com.transmissionbt.Transmission
flatpak install flathub com.valvesoftware.Steam</code></pre></li>

<br>

### Zabezpečení:
- Nastavte */tmp* oddíl jako **noexec**. Nápověda [zde](https://securityhandbook.cz/cs/lnx/index.php#lnx2.1), je třeba upravit syntax.
- Nepoužíváte-li *IPv6*, zakažte jej. Nápověda [zde](https://securityhandbook.cz/cs/lnx/index.php#lnx2.3), je třeba upravit syntax.
- Nastavte CZ.NIC *DNSSEC* – 193.17.47.1,185.43.135.1 – návod [zde](https://securityhandbook.cz/cs/lnx/index.php#lnx2.3).
- Nastavte **firewall** (podrobnější návod [zde](https://securityhandbook.cz/cs/lnx/adv.php#lnx2.1)):
<li style="list-style-type: none"><pre><code>sudo su -
nano /etc/nftables.conf
---------------------
table inet filter {
    chain input {
        type filter hook input priority 0; policy drop;
        ct state invalid drop
        ct state established,related accept
        iif "lo" accept
    }

    chain forward {
        type filter hook forward priority 0; policy drop;
    }

    chain output {
        type filter hook output priority 0; policy accept;
    }
}
---------------------
systemctl enable nftables
systemctl start nftables
nft list ruleset</code></pre></li>
- Bezpečně nastavte prohlížeč(e). Návod [zde](https://securityhandbook.cz/cs/lnx/index.php#lnx4).
- Restartujte OS.

<div class="alert success"><p><em class="icon-ok-circled"></em>**Úspěch**<br>
Tímto jste nainstalovali Arch Linux a provedli jeho základní konfiguraci.</p></div>

<br><br><hr>

<h3 class="nocol">Hezký den. <img class="smile" src="https://securityhandbook.cz/img/sm/smile.svg" alt="smile"></h3>
