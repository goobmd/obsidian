2024-06-02 19:01

Tags: [[linux]], [[programming]], [[project]]

# riceman

### Overview
riceman is a project I am writing in order to provide a method to create & manage rices with support for Rofi. I hope to create a bash script to handle replacing dotfiles with saved files created in advance that will all be stored in a central directory that will likely be located in the home directory. 

### Namesake
Riceman is named after the package manager for arch-based distros & the parameters used will be based on parameters used by pacman.

### Usage
Parameters will include:
	-S: Switch rice
	-N: New rice
	-U: Upgrade rice
	-R: Remove rice
	-X: Extras
Example command:
	`sudo riceman -S persona`

Additionally, I'm hoping to provide compatibility with Rofi, as mentioned before. Menus will be assigned to choose a parameter & select a rice with wallpapers acting as the thumbnails.

The Rofi menu may be assigned to a keybinding through the config files of the WM of choice. For AwesomeWM as I personally use, the keybinding is assigned in the rc.lua config file.

Keybinding:
	`Super + Alt + Space`

Compatibility with dmenu and fzf may be added in the future.

### Compatibility
Common programs used in ricing will be compatible with riceman, including:
	dotfiles:
		GTK3 | `$HOME/.config/gtk-3.0/settings.ini`
		AwesomeWM | `$HOME/.config/awesome/rc.lua`
		NeoVim | `$HOME/.config/nvim/lua/N/theme.lua`
			Note: Move theme plugin to separate file; Require in N.lua
		Alacritty | `$HOME/.config/alacritty/alacritty.toml`
		Neofetch | `$HOME/.config/neofetch/config.conf`
	Nitrogen wallpaper, specified in rice file
	Firefox(?), stylesheets are a whole rabbit hole I don't want to get into
	Rofi, I have a custom plugin that I want to customize with riceman

### Technical
riceman will be implemented in the form of a bash script located in the bin directory. Each variation of dotfiles as well as a config file for riceman itself to read will be placed in the riceman directory in the home directory. Users will be able to set up which files to save when creating a rice and specify which files to apply with the extra parameter.

##### Pseudocode
riceman is called.
read parameter 1, 2, & possibly 3 & 4 (Extra).

-N
	enter into daemon.
		which files do you wish to save?
		specify thumbnail.
	exit.
	create config file in riceman/$2 directory.
	cp dotfiles into riceman/$2 directory.
	create thumbnail in riceman/$2 directory.

-S
	cp files into riceman/bak directory (backup just in case).
	exec riceman/$2/riceman.conf.
		apply wallpaper.
		array of dotfiles to apply.
	exit.
	cp riceman/$2 files into dotfiles.

-U 
	enter into deamon.
		which files do you wish to save?
		specify thumbnail.
	exit.
	update config file in riceman/$2 directory
	cp dotfiles into riceman/$2 directory
	update thumbnail in riceman/$2 directory

-X
	enter into deamon.
		read riceman/$2/riceman.conf
		use array specified.
		which files do you wish to apply?
	exit.
	exec riceman/$2/riceman.conf
		apply wallpaper.
		disregard array of dotfiles to apply.
	exit.
	cp riceman/$2 files into dotfiles.

-R
	confirmation text.
	rm -R riceman/$2.

### Roadmap
I'm hoping to start with switching rices before adding creation, upgrade, and deletion and finally extra. After that, I will add Rofi support and maybe upload to github as a public repository before adding dmenu, fzf, & more ricing tool support.

# References

### Bash scripting
	[[Bash Beginners Guide]]
	[[Bash Advanced Guide]]
	[[Bash Cheatsheet]]


# Similar Notes