<h1 id="intro">Meu pós instalação do manjaro gnome padrão</h1>

## Confira meus dotfiles para usar minhas configurações

[My-dotfiles](https://github.com/JohnWick92/my-dotfiles)

## Atualizar e instalar os pacotes necessários para usar o arch (fish é meu shell favorito)

```shellscript
sudo pacman -Syyu base-devel git curl fish
chsh -s /usr/bin/fish
fish
```

## Eu altero o /etc/pacman.conf, permitindo downloads paralelos (12), ativo a colorização e o ILoveCandy

## Instalando o yay como aur helper

```shellscript
cd /tmp
git clone https://aur.archlinux.org/yay-bin
cd yay-bin
makepkg -si
```

## Se você quiser tudo em [um comando](#all-in-one)

## Sway e utilitários

```shellscript
yay -S sway wl-clipboard wofi waybar swaylock-effects swayidle pavucontrol pamixer wlr-randr swaync swaybg ly
```

## Eu uso nvidia e os drivers proprietários por causa do som no displayport

```shellscript
yay -S nvidia sway-nvidia
```

## Antes de reiniciar alterer o /etc/default/grub e adicione na linha GRUB_CMDLINE_LINUX_DEFAULT

```shellscript
nvidia_drm.modeset=1 nvidia_drm.fbdev=1
```

## E gere novamente o grub com

```shellscript
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## Remova o kms dos HOOKS em /etc/mkinitcpio.conf e adicione em modules

```shellscript
nvidia nvidia_uvm nvidia_drm nvidia_modeset
```

## Crie um hook para que sempre que houver atualização nos drivers ele regenere o initramfs

```shellscript
sudo mkdir -p /etc/pacman.d/hooks
sudo echo "[Trigger]
Operation=Install
Operation=Upgrade
Operation=Remove
Type=Package
# Uncomment the installed NVIDIA package
Target=nvidia
#Target=nvidia-open
#Target=nvidia-lts
# If running a different kernel, modify below to match
Target=linux

[Action]
Description=Updating NVIDIA module in initcpio
Depends=mkinitcpio
When=PostTransaction
NeedsTargets
Exec=/bin/sh -c 'while read -r trg; do case $trg in linux*) exit 0; esac; done; /usr/bin/mkinitcpio -P'" | sudo tee /etc/pacman.d/hooks/nvidia.hook > /dev/null
```

## Gere o initramfs

```shellscript
sudo mkinitcpio -P
```

## Eu uso o ly em vez do gdm e ativo o cronie para fazer snapshots periódicos do timeshift

```shellscript
sudo systemctl disable gdm
sudo systemctl enable ly
sudo systemctl enable --now cronie
```

## Meu editor é a distro neovim lazyvim, se você copiou [My-dotfiles](https://github.com/JohnWick92/my-dotfiles) você já terá minha configuração personalizada

```shellscript
yay -S neovim-git wezterm lazygit keychain podman podman-compose ttf-meslo-nerd btop veracrypt
```

## Apps mais avulsos pro dia a dia

```shellscript
yay -S ytmdesktop-bin whatsapp-for-linux-bin telegram-desktop-bin discord appimagelauncher okular
```

## Como appimage eu uso o [bitwarden](https://bitwarden.com/download/), [beekeeper-community](https://www.beekeeperstudio.io/get-community) e o [insomnium](https://github.com/ArchGPT/insomnium/releases)

## Dependências para o php

```shellscript
yay -S libzip oniguruma postgresql-libs re2c
```

## Asdf como gerenciador de linguagens, o melhor na minha opinião :)

```shellscript
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0
source ~/.asdf/asdf.fish
```

## Autocomplete para podman e asdf

```shellscript
mkdir -p ~/.config/fish/completions; and ln -s ~/.asdf/completions/asdf.fish ~/.config/fish/completions
podman completion -f ~/.config/fish/completions/podman.fish fish
```

## Meus plugins do asdf

```shellscript
asdf plugin-add nodejs
asdf plugin-add java
asdf plugin-add zig
asdf plugin-add php
asdf plugin-add rust
asdf plugin-add golang
```

## Nem todas as linguagens eu uso a versão mais recente, tenha atenção o_O

```shellscript
asdf install nodejs latest && asdf global nodejs latest
asdf install golang latest && asdf global golang latest
asdf install rust latest && asdf global rust latest
asdf install java openjdk-21 && asdf global java openjdk-21
asdf install php 8.3.9 && asdf global php 8.3.9
asdf install zig 0.13.0 && asdf global zig 0.13.0
npm i -g yarn && asdf reshim
```

## Autocomplete para o php artisan

```shellscript
curl -L --create-dirs -o ~/.config/fish/completions/artisan.fish https://github.com/adriaanzon/fish-artisan-completion/raw/master/completions/artisan.fish
curl -L --create-dirs -o ~/.config/fish/completions/php.fish https://github.com/adriaanzon/fish-artisan-completion/raw/master/completions/php.fish
curl -L --create-dirs -o ~/.config/fish/functions/artisan.fish https://github.com/adriaanzon/fish-artisan-completion/raw/master/functions/artisan.fish
```

## Alternativas em rust para programas de linha de comando

```shellscript
cargo install ripgrep zoxide fd-find tealdeer procs git-delta bat exa du-dust tokei rmesg grex
asdf reshim
```

## Alguns aliases que eu me acostumei

```shellscript
alias --save ls="exa --icons"
alias --save pa="php artisan"
alias --save zz="zig build"
alias --save ip="ip -c -br a"
```

<h2 id="all-in-one">Um comando para todos reger, um comando para a encontrá-los...</h2>

## Ele irá apenas instalar os pacotes do sistema... Linguagens, alias etc tem que ser manualmente o_O

## Aviso: Recomendo usar este comando nas seguintes circustâncias

- Você já usou esse guia mais de uma vez
- Você já leu e quer tudo nele
- Caso não se encaixe em uma das alternativas acima confira tudo do [início](#intro)

```shellscript
yay -S --needed --no-confirm sway wl-clipboard wofi waybar swaylock-effects swayidle pavucontrol pamixer wlr-randr swaync swaybg ly neovim-git wezterm lazygit keychain podman podman-compose ttf-meslo-nerd btop veracrypt ytmdesktop-bin whatsapp-for-linux-bin telegram-desktop-bin discord appimagelauncher okular libzip oniguruma postgresql-libs re2c
```
