# Copilot Chat for Neovim

This is a fork of https://github.com/gptlang/CopilotChat.nvim that:
* adds python 3.8 support
* collapses all py files into `plugin.py` (so PYTHONPATH doesn't need to be
  set)
* updates the README.md for improved usage and installation instructions
* various other small updates

This fork is only going to be used until `copilot.vim` adds proper Copilot Chat
support. Please contribute to the upstream project for any issues or
improvements at https://github.com/gptlang/CopilotChat.nvim. This repo may pull
from it, or may not.


## Authentication

It will prompt you with instructions on your first start. If you already have `Copilot.vim` or `Copilot.lua`, it will work automatically.

## Installation

First install dependencies:
```
$ pip install -r requirements.txt
# or
$ sudo apt-get install python3-dotenv python3-requests python3-pynvim python3-prompt-toolkit
```

Then choose an installation method (below)


### Without plugin manager

1. Put the files in the right place
```
$ git clone https://github.com/gptlang/CopilotChat.nvim
$ cd CopilotChat.nvim
$ cp -r --backup=nil rplugin ~/.config/nvim/
```
2. Open up Neovim and run `:UpdateRemotePlugins` (this updates
   `~/.local/share/nvim/rplugin.vim` to have (can we set PYTHONPATH in here?):
   ```
    " python3 plugins
    call remote#host#RegisterPlugin('python3', '/home/ubuntu/.config/nvim/rplugin/python3/plugin.py', [
          \ {'sync': v:false, 'name': 'CopilotChat', 'type': 'command', 'opts': {'nargs': '1'}},
         \ ])
   ```
3. Restart Neovim


### With vim-plug

1. Update nvim configuration to use:
    ```
    call plug#begin()
    ...
    Plug 'jdstrand/CopilotChat.nvim', { 'branch': 'jdstrand/main', 'do': ':UpdateRemotePlugins' }
    call plug#end()
    ```
2. Run `nvim +PlugInstall` (installs to `~/.local/share/nvim/plugged`)
3. Run `nvim +UpdateRemotePlugins` (updates `~/.local/share/nvim/rplugin.vim`)
4. Restart Neovim


## Usage

1. Yank some code into the unnamed register (`y`)
2. `:CopilotChat What does this code do?`

Possible workflow:

1. open a file in nvim
2. do `:vsplit` followed by `:enew` followed by `:setlocal buftype=nofile bufhidden=hide noswapfile wrap linebreak nonu` to open a scratch file
3. (always) chat in this buffer. Eg: `:CopilotChat hi there!`
4. go to another buffer (eg, the file you opened with) and yank (y) a function into a buffer. Go back to the scratch file (a limitation of the CopilotChat.nvim is it will open a new scratch file if the current buffer is not one)
5. chat about the context in the unnamed buffer that was yanked:
  * `:CopilotChat explain this function`
  * `:CopilotChat write documentation for this function`
  * `:CopilotChat write unit tests for this function`
  * `:CopilotChat how can this function be made better?`
6. copy (yank) and paste from the scratch buffer into other buffers to incorporate the changes

Just the chat:
1. `nvim`
2. `:CopilotChat ...`


## TODO

* use a named buffer instead of a scratch file
* be able to use :CopilotChat from any buffer
* add a marker at the end of the chat output (eg `--` or `## DONE` or ...)
