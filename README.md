# Copilot Chat for Neovim

## Authentication

It will prompt you with instructions on your first start. If you already have `Copilot.vim` or `Copilot.lua`, it will work automatically.

## Installation

0. Requires python 3.10+
1. Put the files in the right place
```
$ git clone https://github.com/gptlang/CopilotChat.nvim
$ cd CopilotChat.nvim
$ cp -r --backup=nil rplugin ~/.config/nvim/
```
2. Install dependencies
```
$ pip install -r requirements.txt
```
3. `export PYTHONPATH="$HOME/.config/nvim/rplugin/python3"`
4. Open up Neovim and run `:UpdateRemotePlugins` (this updates
   `~/.local/share/nvim/rplugin.vim` to have (can we set PYTHONPATH in here?):
   ```
    " python3 plugins
    call remote#host#RegisterPlugin('python3', '/home/ubuntu/.config/nvim/rplugin/python3/plugin.py', [
          \ {'sync': v:false, 'name': 'CopilotChat', 'type': 'command', 'opts': {'nargs': '1'}},
         \ ])
   ```
5. Restart Neovim


## Usage

1. Yank some code into the unnamed register (`y`)
2. `:CopilotChat What does this code do?`
