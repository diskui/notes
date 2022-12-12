things i will do after the installation of the linux system:

install some packages:

```shell
sudo pacman -S wl-clipboard bitwarden clash-for-windows-bin telegram-desktop firefox ranger	zathura zathura-pdf-mupdf foliate gnome ibus ibus-libpinyin spotify flameshot xdg-desktop-portal-gnome xdg-desktop-portal
```

some aur packages:

```shell
paru -S google-chrome visual-sdudio-code-bin jetbrains-toolbox typora 
```



`zsh` and `oh-my-zsh`, with some plugins: `git`, `zsh-autosuggestion`, `zsh-syntax-highlighting`, and `zsh-vi-mode`

```bash
# install oh my zsh

git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
  
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/jeffreytse/zsh-vi-mode \
  $ZSH_CUSTOM/plugins/zsh-vi-mode
  
# replace the configuration file

plugins=(
	git
	zsh-autosuggestions
	fast-syntax-highlighting
	zsh-vi-mode
	)
```



`chrome` 离线扩展：medium解锁

config git:
```shell
git config --global user.name "linux"
git config --global user.email kaxiford@gmail.com
```

generate an ssh key:
```shell
ssh-keygen -t ed25519 -C "kaxiford@gmail.com"

#add to github
```
