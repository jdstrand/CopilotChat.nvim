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
# or
$ sudo apt-get install python3-dotenv python3-requests python3-pynvim python3-prompt-toolkit
```
3. Open up Neovim and run `:UpdateRemotePlugins` (this updates
   `~/.local/share/nvim/rplugin.vim` to have (can we set PYTHONPATH in here?):
   ```
    " python3 plugins
    call remote#host#RegisterPlugin('python3', '/home/ubuntu/.config/nvim/rplugin/python3/plugin.py', [
          \ {'sync': v:false, 'name': 'CopilotChat', 'type': 'command', 'opts': {'nargs': '1'}},
         \ ])
   ```
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


## TODO

* use a named buffer instead of a scratch file
* be able to use :CopilotChat from any buffer
* add a marker at the end of the chat output (eg `--` or `## DONE` or ...)
