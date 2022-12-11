softwares that I will install just after the installation of the linux system:

to enable `neovim`  to copy to system clipboard, install `wl-clipboard`

`zsh` and `oh-my-zsh`, with some plugins: `git`, `zsh-autosuggestion`, `zsh-syntax-highlighting`, and `zsh-vi-mode`

```bash
# install oh my zsh

git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
  
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/jeffreytse/zsh-vi-mode \
  $ZSH_CUSTOM/plugins/zsh-vi-mode
  
# replace the configuration file
```

```shell
plugins=(
	git
	zsh-autosuggestions
	fast-syntax-highlighting
	zsh-vi-mode
	)
```



`chrome` 离线扩展：medium解锁

`fcitx5` and `rime`