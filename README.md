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

* [DateTime](https://www.analyticsvidhya.com/blog/2020/05/datetime-variables-python-pandas/)
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
* Create a DataFrame
    * from a dictionary (creating by columns)

        ```python
        df = pd.DataFrame({'Letters': ['a','b','c'],
                           'Numbers': [1,2,3]})
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

* Convert a series of str formatted dates into a datetime type

    ```python
    norm_dates = pd.to_datetime(str_dates, format='%Y%m%d')
    ```

## <a name="numpy">Numpy</a>

* Create an array

    ```python
    a = np.array([1,2,3,4,5,6])     # 1D
    b = np.array([[1,2,3],          # 2D
                  [4,5,6]])
    c = np.array([[[1,2,3],         # 3D
                   [4,5,6]],
                  [[7,8,9],
                   [10,11,12]]])
    ```

* Reshape array

    ```python
    a = np.array([1,2,3,4,5,6]).reshape(2,3)  # 2 rows, 3 cols
    ```

## <a name="scipy">Scipy</a>
* Create an array of evenly spaced values (by step)

    ```python
    a = np.arange(1,10,2)
    ```

* Create an array of evenly spaced values (by # of samples)

    ```python
    a = np.linespace(1,10,100)
    ```

## <a name="matplot">matplotlib</a>

______________________________________________

# <a name="mlw">Machine Learning Workflow</a>