# DSI_Notes
This is to track my notes for the Galvanize DSI.

# Tables of Contents:
* [CLI Scripting](#cli)
* [Python](#python)
    * [Pandas](#pandas)
    * [Numpy](#numpy)
    * [Scipy](#scipy)
    * [Matplotlib](#matplot)
* [Machine Learning Workflow](#mlw)

______________________________________________

# List of things to look into:

* MyPy (DropBox is currently working on MyPyC)

______________________________________________

# Links:

* [Color brewer](https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3)
* [Univariate distribution relationshipd](http://www.math.wm.edu/~leemis/chart/UDR/UDR.html)
* [Visualizing `scipy.stats` distributions](https://stackoverflow.com/questions/37559470/what-do-all-the-distributions-available-in-scipy-stats-look-like)
* [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)


______________________________________________

# <a name="cli">CLI Scripting</a>:
* bash profile location on OSX: `~/.bash_profile`
* for zsh use: `~/.zshrc`

#### how to make a bash / zsh function:

```zsh
function gitadder(){
    git pull
    git add .
    if [ "$1" != "" ] then
        git commit -m "$1: $(date '+%b %d, %Y %H:%M:%S')"
    else
        git commit -m "Auto Update: $(date '+%b %d, %Y %H:%M:%S')"
    fi
    git push
}
```

#### call this function using:

```zsh
gitadder "Enter update text"

# Or just...

gitadder
```

______________________________________________

# <a name="python">Python</a>

## <a name="pandas">Pandas</a>
* creating a DataFrame
    * from a dictionary (creating by columns)

        ```python
        df = pd.DataFrame({'k1': value_lst1,
                           'k2': value_lst2})
        ```

    * from list of lists (creating by rows)

        ```python
        df = pd.DataFrame([['a', 1],
                           ['b', 2],
                           ['c', 3]],
                           columns=['Letters','Numbers'])
        ```

    * from csv (use parameter `sep='\t'` for txt file)

        ```python
        df_csv = pd.read_csv('filename.csv')
        df_txt = pd.read_csv('filename.txt', sep='\t')
        ```

* Drop a column

    ```python
    df.drop('col_1', axis = 1)
    ```

* Rename columns

    ```python
    df.rename(columns={'old_name': 'new_name'})
    ```

* Value counts for a column (i.e. series)

    ```python
    s.value_counts(dropna=False)
    ```

* Fill NA with mean (mean can be replaced with other stat functions)

    ```python
    s.fillna(s.mean())
    ```

## <a name="numpy">Numpy</a>

## <a name="scipy">Scipy</a>

## <a name="matplot">matplotlib</a>

______________________________________________

# <a name="mlw">Machine Learning Workflow</a>