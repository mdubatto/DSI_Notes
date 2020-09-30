# DSI_Notes
This is to track my notes for the Galvanize DSI.

# Tables of Contents:
* [Links](#links)
* [CLI](#cli)
______________________________________________

## List of things to look into:

* MyPy (DropBox is currently working on MyPyC)

______________________________________________

## <a name="links">Links</a>:

* [Color brewer](https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3)
* [Univariate distribution relationshipd](http://www.math.wm.edu/~leemis/chart/UDR/UDR.html)
* [Visualizing `scipy.stats` distributions](https://stackoverflow.com/questions/37559470/what-do-all-the-distributions-available-in-scipy-stats-look-like)
* [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)


______________________________________________

## <a name="cli">Bash / zsh Scripting</a>:
* bash profile location on OSX: `~/.bash_profile`
* for zsh use: `~/.zshrc`

#### how to make a bash function:

```bash
function gitadder(){
    git pull
    git add .
    if [ "$1" != "" ]
        then
            git commit -m "$1: $(date '+%b %d, %Y %H:%M:%S')"
        else
            git commit -m "Auto Update: $(date '+%b %d, %Y %H:%M:%S')"
        fi
    git push
}
```

### call this function using:

```bash
gitadder "Enter update text"

# Or just...

gitadder
```
