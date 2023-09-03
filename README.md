# 🫖 Monokai NighTasty

<!-- panvimdoc-ignore-start -->

![Pull Requests](https://img.shields.io/badge/Pull_Requests-Welcome-a4e400?style=flat-square)
![GitHub last commit](https://img.shields.io/github/last-commit/polirritmico/monokai-nightasty.nvim/main?style=flat-square&color=62d8f1)
![GitHub issues](https://img.shields.io/github/issues/polirritmico/monokai-nightasty.nvim?style=flat-square&color=fc1a70)

<!-- panvimdoc-ignore-end -->

## 🐧 Description

A dark/light theme for Neovim based on the Monokai color palette. This theme is
born from a mix between the code of the great
[tokyonight.nvim](https://github.com/folke/tokyonight.nvim) and the palette of
the flavorful
[vim-monokai-tasty](https://github.com/patstockwell/vim-monokai-tasty).

<!-- panvimdoc-ignore-start -->

![Monokai-NighTasty](https://github.com/polirritmico/monokai-nightasty.nvim/assets/24460484/be1b74e6-8614-482d-8591-ac8a59793620)

<!-- panvimdoc-ignore-end -->

## 🌆 Features

- Infused with the Monokai palette for a vibrant, distraction-free coding
  experience.
- Avoid eye strain by seamlessly toggling between clear and dark styles at
  your fingertips, whether you're at your station or out in the wild.
- Highly customizable for your coding needs.

<!-- panvimdoc-ignore-start -->

## 📷 Screenshots

### 🌙 Dark Theme

![Dark Theme](https://github.com/polirritmico/monokai-nightasty.nvim/assets/24460484/763caac7-f18a-428c-b8e7-14eeceed9108)

### 💨 Dark Theme with transparent background:

![Transparent Dark Theme](https://github.com/polirritmico/monokai-nightasty.nvim/assets/24460484/94703fdc-fc82-48a0-9241-c58fca3f0f62)

### ☀️ Light Theme

![Light Theme](https://github.com/polirritmico/monokai-nightasty.nvim/assets/24460484/f2b3f522-6f27-410a-92d7-f0adf2a65788)

<!-- panvimdoc-ignore-end -->

## 📋 Requirements

- [Neovim](https://neovim.io/) >= 0.9.0


## 📦 Installation

Install with your package manager.

- folke/lazy.nvim:

```lua
{
    "polirritmico/monokai-nightasty.nvim",
    lazy = false,
    priority = 1000,
    opts = {},
}
```

## 🛠️ Configuration

**Base configuration**

No need to use the `setup()` function:

```lua
vim.opt.background = "dark" -- default to dark or light
vim.cmd([[colorscheme monokai-nightasty]])
```

**💡 Toggle function**

The Dark/light styles could be toggled by calling the provided function:

```vim
:MonokaiToggleLight
```

### 🧩 Extra Themes

Currently the theme generate this extras:

<!-- extras:start -->
- [Monokai Nightasty Palettes](https://github.com/polirritmico/monokai-nightasty.nvim/tree/main/extras/palettes) ([palettes](extras/palettes))
- [Tmux](https://github.com/tmux/tmux/wiki) ([tmux](extras/tmux))
- [Zathura](https://pwmt.org/projects/zathura/) ([zathura](extras/zathura))
<!-- extras:end -->

#### Lualine

```lua
require("lualine").setup({
    options = { theme = "monokai-nightasty" },
})
```

### ⚙️ Advanced configuration

> ⚠️ Set the configuration **BEFORE** calling `colorscheme monokai`.

#### Full config example:

```lua
vim.opt.background = "dark" -- The theme has `dark` and `light` styles

require("monokai-nightasty").setup({
    dark_style_background = "transparent", -- default, dark, transparent, #color
    light_style_background = "default", -- default, dark, transparent, #color
    terminal_colors = true, -- Set the colors used when opening a `:terminal`
    color_headers = true, -- Enable header colors for each header level (h1, h2, etc.)
    hl_styles = {
        -- Style to be applied to different syntax groups. See `:help nvim_set_hl`
        comments = { italic = true },
        keywords = { italic = false },
        functions = {},
        variables = {},
        -- Background styles for sidebars (panels) and floating windows:
        floats = "default", -- default, dark, transparent
        sidebars = "default", -- default, dark, transparent
    },
    sidebars = { "qf", "help" }, -- Set a darker background on sidebar-like windows. For example: `["qf", "vista_kind", "terminal", "packer"]`

    hide_inactive_statusline = false, -- Hide inactive statuslines and replace them with a thin border instead. Should work with the standard **StatusLine** and **LuaLine**.
    dim_inactive = false, -- dims inactive windows
    lualine_bold = true, -- Lualine headers will be bold or regular.
    lualine_style = "default", -- "dark", "light" or "default" (Follows dark/light style)

    --- You can override specific color/highlights. Current values in `extras/palettes`

    ---@param colors ColorScheme
    on_colors = function(colors)
        colors.border = colors.grey
        colors.comment = "#2d7e79"
    end,

    ---@param highlights Highlights
    ---@param colors ColorScheme
    on_highlights = function(highlights, colors)
        highlights.TelescopeNormal = { fg = colors.magenta, bg = colors.charcoal }
        highlights.WinSeparator = { fg = colors.grey }
    end,
})

-- Toggle Dark/Light styles
vim.keymap.set(
    {"n", "v"}, "<leader>tl", "<CMD>MonokaiToggleLight<CR>",
    {silent = true, desc = "Monokai-NighTasty: Toggle light/dark theme"}
)

```
---

## 🔍 Colors and Highlights

How the plugin setup the highlights and colors under the hood:

1. `colors` are loaded from the base palette and adjusted based on your
   configuration settings. For example, in the dark style the `bg` color is set
   to `#2b2b2b` if `dark_style_background` is set to `default`. If
   `dark_style_background` is set to `transparent`, then the `bg` value will be
   changed from the default value `#2b2b2b` to `none`.

2. The colors of the **light style** are set in `colors.light_palette`. If
   `vim.o.background == "light"` is detected, then the `default` palette is
   overriden with the light palette values.

3. Finally, `config.on_colors(colors)` is called, overriden any matching color.
   Currently, any change with `config.on_colors(colors)` affects both light and
   dark styles. I plan to correct this behaviour in future versions, but be
   warned that this will most likely introduce some breaking changes on your
   config.

4. These `colors` are utilized to generate the highlight groups.

5. `config.on_highlights(highlights, colors)` can be used to override highlight
   groups.

If you want to get the name or the colors of a highlight group here are some
alternatives:

1. Use `:Inspect` to get info of the highlight group at the current position.
2. Use `:TSHighlightCapturesUnderCursor` from the
   [playground]("https://github.com/nvim-treesitter/playground") plugin.
3. Check the generated palettes in the [extras](###🧩-Extra-Themes).
4. For the theme with the color names instead of the colors code, you could
   check directly the `theme.lua` or `colors.lua` files inside the
   `lua/monokai-nightasty/` directory.

---

## 🔮 Extras

Check the `extras` folder . Copy, link or reference the file in each setting.
Refer to their respective documentation.

### Tmux

#### Fix `undercurls` in [Tmux](https://github.com/tmux/tmux)

If the undercurls or colors are not being properly displayed within
[Tmux](https://github.com/tmux/tmux), add the following to your config file:

```sh
# Undercurl
set -as terminal-features ",xterm-256color:RGB" # or: set -g default-terminal "${TERM}"
set -as terminal-overrides ',*:Smulx=\E[4::%p1%dm'  # undercurl support
set -as terminal-overrides ',*:Setulc=\E[58::2::%p1%{65536}%/%d::%p1%{256}%/%{255}%&%d::%p1%{255}%&%d%;m'  # underscore colours - needs tmux-3.0
```


### 🚀 Using with other plugins

You could import the color palette to use with other plugins:

```lua
local colors = require("monokai-nightasty.colors").setup()

some_plugin_config.background = colors.bg_dark
some_plugin_config.default_color = colors.fg
some_plugin_config.title = colors.blue_light
```

Some color utilily functions are avaliable for your use:

```lua
local colors = require("monokai-nightasty.colors").setup()
local util = require("monokai-nightasty.util")

some_plugin_config.highlight_match = util.lighten(colors.bg, 0.5)
some_plugin_config.unfocus_bg = util.darken(colors.bg, 0.3)
```


## 🎨 Color Palettes

### 🌃 Dark Style

<!-- panvimdoc-ignore-start -->

| Color name  | Hex code  | Render                                                        |
|-------------|-----------|---------------------------------------------------------------|
| Yellow      | `#ffff87` | ![#ffff87](https://place-hold.it/100x40/ffff87/111111?text=+) |
| Purple      | `#af87ff` | ![#af87ff](https://place-hold.it/100x40/af87ff/000000?text=+) |
| Green Light | `#a4e400` | ![#a4e400](https://place-hold.it/100x40/a4e400/000000?text=+) |
| Blue Light  | `#62d8f1` | ![#62d8f1](https://place-hold.it/100x40/62d8f1/000000?text=+) |
| Magenta     | `#fc1a70` | ![#fc1a70](https://place-hold.it/100x40/fc1a70/000000?text=+) |
| Orange      | `#ff9700` | ![#ff9700](https://place-hold.it/100x40/ff9700/000000?text=+) |

<!-- panvimdoc-ignore-end -->

<!-- panvimdoc-include-comment

| Color name  | Hex code  |
|-------------|-----------|
| Yellow      | `#ffff87` |
| Purple      | `#af87ff` |
| Green Light | `#a4e400` |
| Blue Light  | `#62d8f1` |
| Magenta     | `#fc1a70` |
| Orange      | `#ff9700` |

-->

### 🏙️ Light Style

<!-- panvimdoc-ignore-start -->

| Color name  | Hex code  | Render                                                        |
|-------------|-----------|---------------------------------------------------------------|
| Yellow      | `#ff8f00` | ![#ff8f00](https://place-hold.it/100x40/ff8f00/000000?text=+) |
| Purple      | `#6054d0` | ![#6054d0](https://place-hold.it/100x40/6054d0/000000?text=+) |
| Green Light | `#4fb000` | ![#4fb000](https://place-hold.it/100x40/4fb000/000000?text=+) |
| Blue Light  | `#00b3e3` | ![#00b3e3](https://place-hold.it/100x40/00b3e3/000000?text=+) |
| Magenta     | `#ff004b` | ![#ff004b](https://place-hold.it/100x40/ff004b/000000?text=+) |
| Orange      | `#ff4d00` | ![#ff4d00](https://place-hold.it/100x40/ff4d00/000000?text=+) |

<!-- panvimdoc-ignore-end -->

<!-- panvimdoc-include-comment

| Color name  | Hex code  |
|-------------|-----------|
| Yellow      | `#ff8f00` |
| Purple      | `#6054d0` |
| Green Light | `#4fb000` |
| Blue Light  | `#00b3e3` |
| Magenta     | `#ff004b` |
| Orange      | `#ff4d00` |

-->

## 🌱 Contributions

This plugin is made mainly for my personal use, but suggestions, issues, or pull
requests are very welcome.

Enjoy
