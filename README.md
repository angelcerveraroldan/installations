# Installations

- [Neovim](#neovim-installation-and-setup)
  - [Neovim PLugins](#neovim-plugins)

# Neovim installation and setup

To install neovim in Ubuntu, run `sudo apt-get install neovim`.  Now, run `nvim` on the terminal to see if the installation worked out. If it did, the follwing will show:
![Screenshot from 2021-07-26 12-57-31](https://user-images.githubusercontent.com/48255007/126988022-f2e8f337-8ae6-4be0-a269-0dd53273c1a4.png)

To create the neovim setup file, run `cd`, this should take you to the home directory. Once here, go into the `.config` folder by running `cd .config`. Now go into the `nvim` folder using `cd nvim`. If any of this folders dont exist, create them.

When you're inside the nvim folder, make a `init.vim` file by runnning `touch init.vim`. 

Open the file using neovim by running `nvim init.vim`. After the file has opened, press `a` to go into inser mode, and write one of the following:

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
