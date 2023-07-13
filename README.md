monokai-tasty.nvim
==================

A Lua implementation of the very tasty vim-monokay-tasty with my personal
stylish touch.


![Showcase](./docs/monokai.png)

## 🔌 Installation

Just add the repo to your packer manager:

```lua
local plugins = {
    "polirritmico/monokai.nvim",
    ...
}

```

## 🐺 Config

Default config:

```lua
require("monokai").setup({})
```

### Customization:

```lua
require("monokai").setup({
    disable_italics = true,
    transparent_background = false,
    -- theme = custom_theme,
})
```
### Extras:

To use the [lualine.nvim](https://github.com/nvim-lualine/lualine.nvim) theme:
```lua
-- Lualine setup
monokai = require("monokai.extras").lualine
require("lualine").setup({
    options = {
        theme = monokai,
    }
})
```

## 📺 Screenshots

![screenshot](./docs/python.png)
![screenshot](./docs/cpp)
![screenshot](./docs/lua)


## 🎨 Colour palette

| Colour name      |Colour Code | Colour
|------------------|------------|------------------------------------------------------------
| Yellow           | `#ffff87`  |![#ffff87](https://place-hold.it/100x40/ffff87/111111?text=+)
| Purple           | `#af87ff`  |![#af87ff](https://place-hold.it/100x40/af87ff/000000?text=+)
| Light Green      | `#A4E400`  |![#A4E400](https://place-hold.it/100x40/A4E400/000000?text=+)
| Light Blue       | `#62D8F1`  |![#62D8F1](https://place-hold.it/100x40/62D8F1/000000?text=+)
| Magenta          | `#FC1A70`  |![#FC1A70](https://place-hold.it/100x40/FC1A70/000000?text=+)
| Orange           | `#FF9700`  |![#FF9700](https://place-hold.it/100x40/FF9700/000000?text=+)

