 ## Install NeoVim

### Linux

#### apt (Neon KDE (me))

```bash
apt install neovim
```

#### pacman

```bash
pacman -S neovim python-pynvim
```

#### yum

```bash
yum install neovim python36-neovim
```

### 'universal'

```bash
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
chmod x nvim.appimage
./nvim.appimage
```

### MacOS

#### HomeBrew

```bash
brew install neovim
```

### Windows

#### [Chocolatey](https://chocolatey.org/)

```bash
choco install neovim
```

## Install 'vim-plug'

### linux & macos

```bash
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

> you could find it in ~/home/you/.local/share/nvim/autoload/plug.vim

### windows

```powershell
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni "$(@($env:XDG_DATA_HOME, $env:LOCALAPPDATA)[$null -eq $env:XDG_DATA_HOME])/nvim-data/site/autoload/plug.vim" -Force
```

>you could find it in C:/Users/you/AppData/Local/nvim-data/site/autoload/plug.vim

## Install neovim's plugins

### some dependencies of plugins

#### [ctags](http://ctags.sourceforge.net/) for [tagbar](https://github.com/majutsushi/tagbar)

```bash
apt install ctags
```

### init.vim

```bash
touch ~/.config/nvim/init.vim
```

#### [see init.vim](./init.vim)

### use vim-plug

```bash
nvim test.cpp
# command mode
:PlugInstall # install plugins in `init.vim`
```

### coc-vim

```bash
# use [coc.nvim](https://github.com/neoclide/coc.nvim) in command mode
:CocInstall some-plugins-you-need
```

#### requirement

npm, nodejs

#### coc-extensions I used (see [this](https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions))

```bash
# you may need install clang+llvm manually(see below `install clang+llvm`)
coc-clangd
coc-clang-format-style-options
coc-git
coc-highlight
coc-syntax
coc-snippets
coc-pairs
coc-sh
coc-cmake
coc-jedi
coc-vimlsp
coc-yaml
coc-json
```

#### coc-ccls

```bash
#command mod
:CocConfig
```

or

```bash
touch ~/.config/nvim/coc-settings.json
```

```json
{
    "languageserver": {
        "ccls": {
            "command": "ccls",
            "filetypes": ["c", "cc", "cpp", "c++", "objc", "objcpp"],
            "rootPatterns": [".ccls", "compile_commands.json", ".git/", ".hg/"],
            "initializationOptions": {
                "cache": {
                    "directory": "/tmp/ccls"
                }
            }
        }
    }
    # the line below is not exist now(see below `install clang+llvm`)
    # "clangd.path": "/home/you/.config/coc/extensions/coc-clangd-data/install/12.0.0/clangd_12.0.0/bin/clangd"
}
```

### [ccls](https://github.com/MaskRay/ccls)

#### build(see [this](https://github.com/MaskRay/ccls/wiki/Build) for detail)

```bash
git clone --depth=1 --recursive https://github.com/MaskRay/ccls
cd ccls

wget -c https://github.com/llvm/llvm-project/releases/tag/llvmorg-which-version-you-need/clang+llvm-Version-Architecture-OS.tar.xz
tar xf clang+llvm-xxxxx.tar.xz

cmake -H. -BRelease -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH=where-clang+llvm+is
cmake --build Release
cd Release
sudo make install
```

```bash
# you may need something below
libclang-10-dev
zlib1g-dev 
libncurses-dev
clang 
libclang-dev
```

### install clang+llvm

### I was install clang manually, but you can

```bash
# command mode
:CocCommand clangd.install
```

#### not sure it will work

### addition

#### you may also need [this](https://sarcasm.github.io/notes/dev/compilation-database.html)

#### [CMake](https://sarcasm.github.io/notes/dev/compilation-database.html#id54)

To generate a JSON compilation database with [CMake](https://cmake.org/), enable the [CMAKE_EXPORT_COMPILE_COMMANDS](https://cmake.org/cmake/help/latest/variable/CMAKE_EXPORT_COMPILE_COMMANDS.html) option (requires `CMake >= 2.8.5`).

For example, in an existing build directory, type:

```
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON .
```

This will create a file name `compile_commands.json` in the build directory.