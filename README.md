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
yay -S ytm-desktop-bin whatsapp-for-linux-bin telegram-desktop-bin discord appimagelauncher okular
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
curl -L --create-dirs -o ~/.config/fish/completions/artisan.fish <https://github.com/adriaanzon/fish-artisan-completion/raw/master/completions/artisan.fish>
curl -L --create-dirs -o ~/.config/fish/completions/php.fish <https://github.com/adriaanzon/fish-artisan-completion/raw/master/completions/php.fish>
curl -L --create-dirs -o ~/.config/fish/functions/artisan.fish <https://github.com/adriaanzon/fish-artisan-completion/raw/master/functions/artisan.fish>
```

## Alternativas em rust para programas de linha de comando

```shellscript
cargo install ripgrep zoxide fd-find tealdeer procs git-delta bat exa du-dust tokei rmesg grex
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
yay -S --needed --no-confirm sway wl-clipboard wofi waybar swaylock-effects swayidle pavucontrol pamixer wlr-randr swaync swaybg ly neovim-git wezterm lazygit keychain podman podman-compose ttf-meslo-nerd btop veracrypt ytm-desktop-bin whatsapp-for-linux-bin telegram-desktop-bin discord appimagelauncher okular libzip oniguruma postgresql-libs re2c
```
