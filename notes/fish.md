# Fish shell

## Files & directories

| Task | Command |
|---|---|
| Create directory | `mkdir name` |
| Create nested directories | `mkdir -p a/b/c` |
| Create file | `touch file.txt` |
| Rename file | `mv old.txt new.txt` |
| Move file/directory | `mv thing path/to/dest/` |
| Copy file | `cp file.txt copy.txt` |
| Copy directory | `cp -r dir/ dest/` |
| Remove file | `rm file.txt` |
| Remove directory | `rm -r dir/` |
| Remove empty directory | `rmdir dir/` |
| List files (incl. hidden) | `ls -la` |
| Print current directory | `pwd` |
| Go home / back | `cd` / `cd -` |
| Previous / next directory | `prevd` / `nextd` (or `Alt+←` / `Alt+→`) |

## Viewing & finding

```fish
cat file.txt                 # print file
less file.txt                # scroll file (q to quit)
head -n 20 file.txt          # first 20 lines
tail -f log.txt              # follow a file as it grows
grep -rn "text" .            # search for text in files
find . -name "*.md"          # find files by name
du -sh *                     # size of each item here
df -h                        # disk space
```

## Variables

Fish uses `set` instead of `export` / `VAR=value`.

```fish
set name Tom                 # local variable
echo $name
set -gx EDITOR vim           # global + exported (like `export`)
set -Ux EDITOR vim           # universal: saved permanently across sessions
set -e name                  # erase a variable
fish_add_path ~/.local/bin   # add to PATH permanently
```

## Command substitution & logic

```fish
set files (ls)               # use () instead of $( ) or backticks
cmd1; and cmd2               # run cmd2 only if cmd1 succeeds (&& also works)
cmd1; or cmd2                # run cmd2 only if cmd1 fails (|| also works)
echo $status                 # exit code of last command (not $?)
```

## Loops & if

```fish
for f in *.txt
    echo $f
end

if test -f file.txt
    echo "exists"
else
    echo "missing"
end
```

## Abbreviations & functions

```fish
abbr -a gs git status        # type `gs` + space -> expands to `git status`
abbr -a gp git push

function mkcd
    mkdir -p $argv[1]; and cd $argv[1]
end
funcsave mkcd                # save the function permanently
functions                    # list functions
```

## Config & handy keys

- Config file: `~/.config/fish/config.fish`
- Web settings UI: `fish_config`
- Reload config: `source ~/.config/fish/config.fish`

| Key | Action |
|---|---|
| `→` or `Ctrl+F` | Accept autosuggestion |
| `Alt+→` | Accept one word of the suggestion |
| `↑` (after typing) | Search history for commands starting with that text |
| `Ctrl+R` | Search history |
| `Tab` | Complete (press again to cycle) |
| `Alt+S` | Prepend `sudo` to the current command |
| `Ctrl+C` | Cancel current line |
| `Ctrl+L` | Clear screen |
