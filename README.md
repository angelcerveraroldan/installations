# Installations

- [Neovim](#neovim-installation-and-setup)
  - [Neovim Plugins](#neovim-plugins)

# Neovim installation and setup

Note: It is recommended to learn the [basics](https://www.youtube.com/watch?v=ggSyF1SVFr4) of vim before the insatllation, as we will be using vim along the way.

To install neovim in Ubuntu, run `sudo apt-get install neovim`. To install neovim in Arch Linux, run `sudo pacman -S neovim`.  Now, run `nvim` on the terminal to see if the installation worked out. If it did, the follwing will show:
![Screenshot from 2021-07-26 12-57-31](https://user-images.githubusercontent.com/48255007/126994756-fd7f51ce-94cd-4342-a797-4ac95a98c215.png)

To create the neovim setup file, run `cd`, this should take you to the home directory. Once here, go into the `.config` folder by running `cd .config`. Now go into the `nvim` folder using `cd nvim`. If any of this folders dont exist, create them.

When you're inside the nvim folder, make a `init.vim` file (if it doesn't already exist) by runnning `touch init.vim`. 

Open the file using neovim by running `nvim init.vim`. After the file has opened, press `a` to go into insert mode, and write one of the following:

1. `set number` -> This will show line numbers on the side.
2. `set relativenumber` -> This will show the line number relative to the cursor.
3. `set number relativenumber` -> This is a hybrid between the other two settings. It will show both the line number relative to the cursor and the absolute line number.

To save the file and exit, press the `esc` key, this will take you to the command mode. The command to save and quit is `:wq`, `:w` is the save command, and `:q` is the quit command. After you have saved and quit, open the file again using vim, you should now see line numbers.

The next step is to install [vim-plug](https://github.com/junegunn/vim-plug), this will allow us to install plugins for neovim. 

To do this, run the following command:

`sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'`

Now, we need to go back to the `init.vim` file we created later, and paste the following under the `set number` line. 

````
call plug#begin()

" You can add plugins here

call plug#end()
````

Now we can install plugins:

## Neovim Plugins
The first plugin to install is [NerdTree](https://github.com/preservim/nerdtree), this will add a file system explorer for neovim.  To install this plugin, we just need to paste

`Plug 'preservim/nerdtree'` between the plug#begin() and the plug#end(). It should look like this:

````
call plug#begin()

" NerdTree plugin          <--- This line is a comment
Plug 'preservim/nerdtree

call plug#end()
````

Now save the file by going into command mode and running the command `:wq` and open the file back up again. Now run the command `:PlugInstall`. This command will install all of the plugins in the `init.vim` file.

Once installed, we can remap the key that will toggle the tree on and off by adding the following command above the plug#begin(): 
`nnoremap <silent> <F5> :NERDTreeToggle<CR>`
This command will change the key that toggles the tree, in this case, `F5`.

Your `init.vim` file should now look something like this:
![Screenshot from 2021-07-26 14-11-31](https://user-images.githubusercontent.com/48255007/126994645-38824e49-a933-4351-90b4-32901805a4e1.png)

Now we can add more plugins, for example:
`Plug 'chun-yang/auto-pairs'`  <---  This will automatically close any brackets, quotation marks etc...

If youre using vim as an IDE, installing an autocompleter is very important. A plugin that does this is [coc autocomplete](https://github.com/neoclide/coc.nvim).
To install this, first you need to have nodejs installed, to check if you have nodejs istalled, run `node -v` in the terminal. If nodejs is installed, its version will be shown. If it isn't installed, you can [install](https://github.com/nodesource/distributions/blob/master/README.md#debinstall) it by running the following command:
````
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt-get install -y nodejs
````
Once nodejs is installed, add 

`Plug 'neoclide/coc.nvim', {'branch': 'release'}` to the `init.vim` file as we did with the NerdTree plugin, and after saving the file, run the command `:PlugInstall` to install the coc plugin.

Once coc is installed, paste the following in your `init.vim` file, just below the NerdTree key remap.

````
" Use tab for trigger completion with characters ahead and navigate.
" NOTE: Use command ':verbose imap <tab>' to make sure tab is not mapped by
" other plugin before putting this into your config.
inoremap <silent><expr> <TAB>
       \ pumvisible() ? "\<C-n>" :
       \ <SID>check_back_space() ? "\<TAB>" :
       \ coc#refresh()
 inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"
 
 function! s:check_back_space() abort
   let col = col('.') - 1
   return !col || getline('.')[col - 1]  =~# '\s'
 endfunction
````
As the comment indicates, this will let us use tab to navigate a pop up window that will autocomplete code.

To add support for python, we need to use [coc-pyright](https://github.com/fannheyward/coc-pyright). To install it, open the `init.vim`  file using neovim and run the command 

`:CocInstall coc-pyright`
And to add support for [rust](https://github.com/fannheyward/coc-rust-analyzer), run the command `:CocInstall coc-rust-analyzer`.

Once you have installed both of this, you now have autocmplete for rust and python when using neovim.

Other plugins you could install are:
1. `Plug 'alec-gibson/nvim-tetris'`  <--- Play [tetris](https://github.com/alec-gibson/nvim-tetris) by using the command `:Tetris`.
2. `Plug 'vim-airline/vim-airline'`  <--- Better looking [status bar](https://github.com/vim-airline/vim-airline).
