# Telescope recent files extension

This is an extension for the
[Telescope](https://github.com/nvim-telescope/telescope.nvim) plugin which
implements a picker for the recent files.

The picker presents all files from `:h v:oldfiles` + the files which have been
opened in the current session. There are also a couple of useful
[options](#options).

How does it differ from:

- Telescope's native `:h builtin.oldfiles`. Old files in [Neo]vim are saved
  only when the program is closed. So if you open the file you haven't worked
  on before, the builtin picker will not show it, which is sometimes quite
  annoying. This plugin addresses this use case by taking into account all
  buffers you opened.

- [Frecency](https://github.com/nvim-telescope/telescope-frecency.nvim)
  extension. Frecency is a fancier extension with smart algorithms, and
  persisting the results to the local database. However, frecency is not
  recency. This extension is much simpler - the algorithm is as dumb as it can
  be (whatever opened last is shown last), and there is also no local database
  to maintain.

## Installation

With [vim-plug](https://github.com/junegunn/vim-plug):

```vim
" Required
Plug 'nvim-lua/plenary.nvim'
Plug 'nvim-telescope/telescope.nvim'

" This extension
Plug 'rsookram/telescope-recent-files'
```

## Usage

Once installed, the extension has to be loaded using standard Telescope's API:

```vim
-- Load extension
lua << EOF
require("telescope").load_extension("recent_files")
EOF
```

An example of the shortcut to open recent files:

```vim
-- Map a shortcut to open the picker
nnoremap <leader>e <CMD>Telescope recent_files theme=dropdown previewer=false pick<CR>
```

## Options

Extension options can be configured in the Telescope's setup:

```lua
require("telescope").setup {
  defaults = {
    -- Your regular Telescope's options
  },
  extensions = {
    recent_files = {
      -- Telescope options applied specifically to this plugin
    }
  }
}
```
