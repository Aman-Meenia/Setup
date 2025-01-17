
# How to setup wezterm for macbook 

## Installation
```
brew install --cask wezterm
```

## Brew Installation 
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```


## Create config file to customize wezterm .wezterm.lua
```
-- Pull in the wezterm API
local wezterm = require("wezterm")

-- This will hold the configuration.
local config = wezterm.config_builder()

return config
```

## Theme setup 
```
-- Appearance
config.colors = {
	foreground = "#CDD6F4",
	background = "#1E1E2E",
	-- background = "#181825",
	cursor_bg = "#F5E0DC",
	cursor_border = "#F5E0DC",
	cursor_fg = "#1E1E2E",
	selection_bg = "#F5E0DC",
	selection_fg = "#1E1E2E",

	ansi = {
		"#45475A", -- black
		"#F38BA8", -- red
		"#A6E3A1", -- green
		"#F9E2AF", -- yellow
		"#89B4FA", -- blue
		"#F5C2E7", -- magenta
		"#94E2D5", -- cyan
		"#BAC2DE", -- white
	},
	brights = {
		"#585B70", -- bright black
		"#F38BA8", -- bright red
		"#A6E3A1", -- bright green
		"#F9E2AF", -- bright yellow
		"#89B4FA", -- bright blue
		"#F5C2E7", -- bright magenta
		"#94E2D5", -- bright cyan
		"#A6ADC8", -- bright white
	},
	indexed = {
		[16] = "#FAB387",
		[17] = "#F5E0DC",
	},
	tab_bar = {
		background = "#1E1E2E",
		active_tab = {
			bg_color = "#89B4FA",
			fg_color = "#1E1E2E",
		},
		inactive_tab = {
			bg_color = "#45475A",
			fg_color = "#BAC2DE",
		},
		inactive_tab_hover = {
			bg_color = "#585B70",
			fg_color = "#CDD6F4",
		},
		new_tab = {
			bg_color = "#1E1E2E",
			fg_color = "#A6ADC8",
		},
		new_tab_hover = {
			bg_color = "#A6E3A1",
			fg_color = "#1E1E2E",
		},
	},
}

```

## Window Padding
```
-- Set window padding
config.window_padding = {
	-- 	left = 20,
	right = 20,
	top = 10,
	bottom = 10,
}
```

## Border Color
```
-- // Border color
config.window_frame = {
	border_left_width = "0.5cell",
	border_right_width = "0.5cell",
	border_bottom_height = "0.25cell",
	border_top_height = "0.25cell",
	border_left_color = "purple",
	border_right_color = "purple",
	border_bottom_color = "purple",
	border_top_color = "purple",
}
```

## Font size
```
-- font size 
config.font_size = 19
```

## Font 
```
-- font 
config.font = wezterm.font("MesloLGS Nerd Font Mono")
                      or
config.font = wezterm.font("JetBrains Mono", {})
```

## Disable top bar 
```
-- disale mac default top bar
config.window_decorations = "RESIZE"
```

## Transparent and blur
```
-- MAKE TERMINAL TRANSPARENT
config.window_background_opacity = 0.75
config.macos_window_background_blur = 25
```

## Hide cursor when typing
```
-- make cursor hide whiel typing
config.hide_mouse_cursor_when_typing = true
```

## Keybinding to move between tabs
```
-- Key bindings for moving between tabs
config.keys = {
	-- Move to the next tab
	{ key = "l", mods = "CMD", action = wezterm.action({ ActivateTabRelative = 1 }) },
	-- Move to the previous tab
	{ key = "h", mods = "CMD", action = wezterm.action({ ActivateTabRelative = -1 }) },
}
```

## Iitial window size of wezterm 
```
-- Set the initial window size
config.initial_rows = 32
config.initial_cols = 117
```

## Enable Tab Bar
```
-- to enable the tab bar
config.enable_tab_bar = true --  true or false
```

## Tab Bar config
```
-- top bar config
wezterm.plugin.require("https://github.com/nekowinston/wezterm-bar").apply_to_config(config, {
	position = "top",
	max_width = 32,
	dividers = "slant_right", -- "slant_right" or "slant_left", "arrows", "rounded", false
	indicator = {
		leader = {
			enabled = true,
			off = " ",
			on = " ",
		},
		mode = {
			enabled = true,
			names = {
				resize_mode = "RESIZE",
				copy_mode = "VISUAL",
				search_mode = "SEARCH",
			},
		},
	},
	tabs = {
		numerals = "arabic", -- or "roman"
		pane_count = "superscript", -- or "subscript", false
		brackets = {
			active = { "", ":" },
			inactive = { "", ":" },
		},
	},
	clock = { -- note that this overrides the whole set_right_status
		enabled = false,
		-- format = "%H:%M:%S", -- use https://wezfurlong.org/wezterm/config/lua/wezterm.time/Time/format.html
	},
})

```

## Make link clickable 
```
config.hyperlink_rules = wezterm.default_hyperlink_rules()
config.hyperlink_rules = wezterm.default_hyperlink_rules()
```

## To open tmux session automatically when open wezterm

```
-- Define the tmux session name
local tmux_session_name = "Aman"  

--  command to start or attach to the tmux session
local tmux_command = {
	"/bin/bash",
	"-c",
	string.format(
		[[
    if tmux has-session -t %s 2>/dev/null; then
      tmux attach-session -t %s
    else
      tmux new-session -s %s
    fi
    exec $SHELL
  ]],
		tmux_session_name,
		tmux_session_name,
		tmux_session_name
	),
}
config.default_prog = tmux_command
```


## Starship download

```
brew install starship
// write in .zshrc
# eval "$(starship init zsh)"

starship preset gruvbox-rainbow -o ~/.config/starship.toml
```


## Neofetch Download
```
brew install neofetch
```

## Neofetch to work everytime when we open wezterm
```
.zshrc File 
# neofetch
neofetch
```
