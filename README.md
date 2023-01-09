# Telescope recent files extension

This is an extension for the [Telescope](https://github.com/nvim-telescope/telescope.nvim)
plugin which implements a picker for the recent files.

The picker presents all files from `:h v:oldfiles` + the files which have been opened
in the current session. There are also a couple of useful [options](#options).

How does it differ from:

- Telescope's native `:h builtin.oldfiles`. Old files in [Neo]vim are saved only
  when the program is closed. So if you open the file you haven't worked on before,
  the builtin picker will not show it, which is sometimes quite annoying. This
  plugin addresses this use case by taking into account all buffers you opened.

- [Frecency](https://github.com/nvim-telescope/telescope-frecency.nvim) extension.
  Frecency is a fancier extension with smart algorithms, and persisting the results
  to the local database. However, frecency is not recency. This extension is much
  simpler - the algorithm is as dumb as it can be (whatever opened last is shown last),
  and there is also no local database to maintain.

## Installation

With [packer.nvim](https://github.com/wbthomason/packer.nvim):

```lua
-- Required.
use {"nvim-telescope/telescope.nvim"}
-- This extension.
use {"smartpde/telescope-recent-files"}
```

## Usage

Once installed, the extension has to be loaded using standard Telescope's API:

```lua

-- Load extension.
require("telescope").load_extension("recent_files")
```

An example of the shortcut to open recent files:

```lua
-- Map a shortcut to open the picker.
vim.api.nvim_set_keymap("n", "<Leader><Leader>",
  [[<cmd>lua require('telescope').extensions.recent_files.pick()<CR>]],
  {noremap = true, silent = true})
```

## Options

Extension options can be configured in the Telescope's setup:

```lua
require("telescope").setup {
  defaults = {
    -- Your regular Telescope's options.
  },
  extensions = {
    recent_files = {
      -- Telescope options applied specifically to this plugin.
    }
  }
}
```
