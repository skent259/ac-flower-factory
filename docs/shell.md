# Shell

## Tar


```bash
$ tar  -xvf archive.tar
```

or

```bash 
$ tar -xvzf file.tar.gz
```

- `-[x | c]` : extract | create archive

- `v`: The “v” stands for “verbose.” This option will list all of the files one by one in the archive.

- `z`: The z option is very important and tells the tar command to uncompress the file (gzip).

- `f`: This options tells tar that you are going to give it a file name to work with.


## Zsh functions

After `M-x` you can input zsh functions
`_expand_alias` - you can expand aliases...

## Dotfile Control

Using the bare repository method outlined [here](https://www.atlassian.com/git/tutorials/dotfiles)

For use, you can be in any directory and just use config as you normally would.

```bash
config add .FILENAME
```

## Shell Parameter Expansion

* [In Bash](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)
* [In Zsh](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Parameter-Expansion)


### Recipes
* `%` matches end
  - `%%*.` for file type, greedy till end
* `#` matches beginning

# wget

```bash
wget -r -np -l 1 -A zip http://example.com/download/

-r,  --recursive          specify recursive download.
-np, --no-parent          don't ascend to the parent directory.
-l,  --level=NUMBER       maximum recursion depth (inf or 0 for infinite).
-A,  --accept=LIST        comma-separated list of accepted extensions.
```
