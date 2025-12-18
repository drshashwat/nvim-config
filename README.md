# 💤 Neovim Configuration

A modern Neovim configuration built on [LazyVim](https://github.com/LazyVim/LazyVim), a distribution that comes with sensible defaults and a curated set of plugins.

## Quick Start

### Prerequisites

- Neovim (>= 0.8)
- Git
- A nerd font (recommended for proper icon rendering)

### Installation

This configuration is located at `~/.config/nvim`. If you don't have Neovim installed:

```bash
# macOS
brew install neovim

# Or build from source
git clone https://github.com/neovim/neovim
cd neovim && make CMAKE_BUILD_TYPE=Release && sudo make install
```

### First Launch

Simply start Neovim:

```bash
nvim
```

On first launch, LazyVim will automatically:
- Clone the `lazy.nvim` plugin manager
- Install all configured plugins
- Set up the default colorscheme (TokyoNight)

## Configuration Structure

```
~/.config/nvim/
├── init.lua                 # Main entry point - bootstraps LazyVim
├── lua/
│   └── config/
│       ├── options.lua      # Neovim settings and preferences
│       ├── keymaps.lua      # Custom key bindings
│       ├── autocmds.lua     # Automatic commands and event handlers
│       └── lazy.lua         # Plugin manager configuration
└── lua/
    └── plugins/
        └── example.lua      # Directory for custom plugins
```

## Features

### Out of the Box

LazyVim includes a carefully selected set of plugins:

- **Code Navigation**: LSP support, Telescope fuzzy finder
- **Git Integration**: Gitsigns, Lazygit integration
- **Editing**: Enhanced motions, surround operations, comment toggling
- **UI Enhancements**: Statusline, bufferline, better notifications
- **Themes**: Built-in colorscheme support (TokyoNight default)
- **Treesitter**: Advanced syntax highlighting and parsing

### Lazy Loading

All plugins use `lazy.nvim` for smart lazy loading, ensuring fast startup times while keeping all functionality available.

## Configuration

### Adding Options

Edit [lua/config/options.lua](lua/config/options.lua) to customize Neovim settings:

```lua
-- Example: Set tab width to 2 spaces
vim.opt.tabstop = 2
vim.opt.shiftwidth = 2
```

### Custom Keymaps

Edit [lua/config/keymaps.lua](lua/config/keymaps.lua) to add your keybindings:

```lua
-- Example: Map <leader>ex to a command
vim.keymap.set("n", "<leader>ex", "<cmd>SomeCommand<cr>", { noremap = true })
```

### Adding Plugins

Create or edit files in [lua/plugins/](lua/plugins/) to add custom plugins. Each file should return a plugin spec:

```lua
-- lua/plugins/my-plugin.lua
return {
  "user/plugin-name",
  version = "*",
  config = function()
    require("plugin-name").setup({
      -- your options
    })
  end,
}
```

### Automatic Commands

Edit [lua/config/autocmds.lua](lua/config/autocmds.lua) to add custom autocmds:

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  group = vim.api.nvim_create_augroup("CustomGroup", { clear = true }),
  callback = function()
    -- Your autocommand logic
  end,
})
```

## Key Bindings

This configuration uses LazyVim's default keymaps plus any custom ones you add. Some common ones:

- `<leader>ff` - Find files
- `<leader>fg` - Find grep
- `<leader>fb` - Find buffers
- `<leader>ca` - Code actions
- `<leader>cf` - Format code
- `<leader>e` - Toggle file explorer

(For a full list, check LazyVim's [documentation](https://lazyvim.github.io/keymaps))

## Updates

Plugins are checked for updates periodically. You can manually update plugins:

```
:Lazy
```

Then navigate to the update option and apply updates.

## Customization Tips

1. **Override LazyVim Defaults**: You can customize any LazyVim plugin by creating a plugin spec that disables or modifies it
2. **Check LazyVim Docs**: The [LazyVim documentation](https://lazyvim.github.io/) is comprehensive and helpful
3. **Keep It Lean**: Don't add too many plugins; focus on tools that improve your workflow
4. **Test Changes**: Always reload your configuration or restart Neovim after making changes

## Troubleshooting

### Plugins not loading

Run `:Lazy` to check the plugin manager status. Ensure all plugins installed correctly.

### Issues with LSP

Some language servers require additional setup. Check the LazyVim documentation for your specific language.

### Performance Issues

Profile your config using:

```
:Lazy profile
```

## Resources

- [LazyVim Documentation](https://lazyvim.github.io/)
- [Neovim Documentation](https://neovim.io/doc/user/)
- [Telescope](https://github.com/nvim-telescope/telescope.nvim)
- [LSP Configuration](https://github.com/neovim/nvim-lspconfig)

## License

This configuration template uses LazyVim, which is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for more details.
