- [Around 95% of steam users are running windows 64-bit](https://store.steampowered.com/hwsurvey/Steam-Hardware-Software-Survey-Welcome-to-Steam). And so are a lot of other people who can't use your lisp software easily.
- With regular lisp-executable dumping, every change requires booting up windows and rebuilding the entire binary. What if you didn't have to touch windows at all? What if all you had to do was `copy`, `paste`, and `rename`?


### Example for shipping [sucle](https://github.com/pupcraft/sucle)
see [this release](https://github.com/pupcraft/trivial-ship/releases/tag/win64)

3 files:  
`launcher.exe`  
`launcher.lisp` -> example which runs sucle  
```
;;as if we were running sucle from the repl
(ql:quickload :sucle)  
(let ((application:*main-subthread-p* nil))   
   (sucle:start))
```
`glfw.dll` -> for sucle support  

click on `launcher.exe`  

to distribute your own project, modify `launcher.lisp`, [and throw in any `.dll` files]

### What End to End Distribution and Installation looks like:
1. I have an app that I want to name `game.exe`
2. I rename `launcher.exe`, found in the `bin` folder after building to `game.exe`
3. I create `game.lisp` file to load lisp code. This is the same as opening a lisp repl with quicklisp installed.
4. I put `game.exe` and `game.lisp` in a folder, lets call it `gamev1.0`
5. [optional] run `game.exe` to preload the quicklisp libraries
6. I zip up `gamev1.0` to `gamev1.0.zip`
7. I upload `gamev1.0.zip` to the internet
8. A user downloads `gamev1.0.zip`
9. The user unzips `gamev1.0.zip` to `gamev1.0` 
10. The user clicks the `gamev1.0` folder to enter it
11. The user clicks on `game.exe`
12. The libraries are downloaded if not already bundled with the download
13. The user uses the program

### More details
(After building)
Inside the `bin` folder is an executable that will, in the same directory as the executable, execute a lisp file of the same name and create a dedicated quicklisp and ASDF installation

lets go inside the `bin` folder (and for the correct arch and os)

`launcher.exe` is a standalone windows executable that can be placed anywhere

running `launcher.exe` will:
1. make sure a dedicated folder exists called `launcher_sys` in the same folder
2. load `launcher.lisp` in the same folder

if `launcher.exe` is renamed to `foobar.exe` then `foobar.exe` will:  
1. make sure a dedicated folder exists called `foobar_sys` in the same folder
2. load `foobar.lisp` in the same folder

etc...

### How to build

1. `(ql:quickload :trivial-ship)` [need this repo]
2. `(trivial-ship:build-launcher)`

### Benchmark

## [sucle](https://github.com/pupcraft/sucle)
- downloading and setting up: `3 minutes`  
- booting once compiled: `8 seconds`
