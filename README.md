# <a name="top">DSI Notes</a>

# Tables of Contents:
* [CLI Scripting](#cli)
* [Unix](#unix)
* [Git](#git)
* [Statistics](#stats)
* [Python](#python)
    * [Pandas](#pandas)
    * [Numpy](#numpy)
    * [Scipy](#scipy)
    * [Matplotlib](#matplot)
* [AWS](#aws)
* [Docker](#docker)
* [Machine Learning Workflow](#mlw)

______________________________________________

# List of things to look into:

* MyPy (DropBox is currently working on MyPyC)
* Download p4merge
* look into internet extenders
* find out what map() is
* pyodbc
* crontab, luige, apache, or jams for automation
* dbeaver to get column names
* postman for interpretting apis
* toptal

______________________________________________

# Links:

* [DateTime](https://www.analyticsvidhya.com/blog/2020/05/datetime-variables-python-pandas/)
* [Git Reference](https://git-scm.com/docs)
* [Unix Cheat Sheet](http://www.mathcs.emory.edu/~valerie/courses/fall10/155/resources/unix_cheatsheet.html)
* [Markdown cheat sheet](https://www.markdownguide.org/cheat-sheet)
* [Python Tutor](http://www.pythontutor.com/visualize.html#mode=edit)
* [Color brewer](https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3)
* [Univariate distribution relationshipd](http://www.math.wm.edu/~leemis/chart/UDR/UDR.html)
* [Visualizing `scipy.stats` distributions](https://stackoverflow.com/questions/37559470/what-do-all-the-distributions-available-in-scipy-stats-look-like)
* [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)

______________________________________________

# <a name="cli">CLI Scripting</a>
* bash profile location on OSX: `~/.bash_profile`
* for zsh use: `~/.zshrc`

#### how to make a bash / zsh function

```zsh
function gitadder(){
    git pull
    git add -A
    if [ "$1" != "" ]; then
        git commit -m "$1: $(date '+%b %d, %Y %H:%M:%S')"
    else
        git commit -m "Auto Update: $(date '+%b %d, %Y %H:%M:%S')"
    fi
    git push
}
```

#### call this function using

```zsh
gitadder "Enter update text"

# Or just...

gitadder
```

[Back to top](#top)
______________________________________________

# <a name="unix">Unix</a>

* `echo "Hello World"` - prints message to screen
* `echo "Hello World" > hello.txt` - prints message to file (creates new file or overwrites existing)
* `echo "goodbye" >> hello.txt` - appends message to the end of file
* `cat hello.txt` - prints file to terminal
* `man ls` - print out a help menu for the command
* `history > history.txt` - saves command history in a file
* `grep <filter>` - looks at sheet of text and outputs only lines that have the keyword you are looking for
* `!<history number>` - runs command from a certain line in history
* `open https://google.com &` - opens google

[Back to top](#top)
______________________________________________

# <a name="git">Git</a>

* `git status` - Display the state of the working directory and the staging area and see which changes have been staged, which haven't, and which files aren't being tracked by Git
* `git log` - View version history of current branch (to exit this type `q`)
* `git reset [file]` - Unstages the file, but it preserves the file contents.
* `git reset [commit]` - Undoes all the commits after the specified commit and preserves the changes locally.
* `git add .` - Adds all files from the root directory to the staging area
* `git add -A` - Adds all files root and sub directories to the staging area
* `git add [filename1 filename2]` - Adds only listed files to the staging area
* `git commit -m "[Enter commit message]"` - Creates a new commit containing the current contents of the index
* `git pull` - Fetches and merges changes on the remote server to your working directory
* `git push` - Send your updates and new files in your commit from your local machine to the remote repository
* `git revert [commit]` - Undo the commit

#### Working on a team
* `git clone` the person's repo
* `git branch [branchname]`
* `git checkout [branchname]`
* `git add .`
* `git commit -m "adding new branch to remote repo"`
* `git push --set-upstream origin [branchname]`

* `git checkout master`


[Back to top](#top)
______________________________________________

# <a name="stats">Probability & Statistics</a>

#### Conditional probability
The probability of event A given B. When the two events are independent, the probabilty is simply P(A).

![Conditional Probability](images/ConditionalProb.png)

#### Bayes' theorem
Describes the probability of a posterior event, based on previous conditions related to the event. For example, given the probabilities P(B) and P(B | A), Bayes' theorem can be applied to calculate P(A | B).

Tip: it's a bayes problem if there's two different

![Bayes' Theorem](images/BayesTheorem.png)

#### Law of total probability

![Total Probability](images/TotalProb.png)

[Back to top](#top)
______________________________________________

# <a name="python">Python</a>
#### Generator expressions
Some simple generators can be coded succinctly as expressions using a syntax similar to list comprehensions but with parentheses instead of square brackets. These expressions are designed for situations where the generator is used right away by an enclosing function. Generator expressions are more compact but less versatile than full generator definitions and tend to be more memory friendly than equivalent list comprehensions.

```python
sum(i*i for i in range(10))         # sum of squares

# instead of...

sum([i*i for i in range(10)])       # needlessly allocates a list in memory
```

* `dir(var_name)` - shows all methods available for a variable
* `who` - list variable names

## <a name="pandas">Pandas</a>
#### Create a DataFrame
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

#### Summary statistics (numerical variables)

```python
df.describe()
```

#### Correlation -- Pearson and Spearman (numerical variables)

```python
df.corr(method='pearson').round(3)
```

#### Drop a column

```python
df.drop('col_1', axis = 1)
```

#### Rename columns

```python
df.rename(columns={'old_name': 'new_name'})
```

#### Value counts for a column (i.e. series)

```python
s.value_counts(dropna=False)
```

#### Fill NA with mean (mean can be replaced with other stat functions)

```python
s.fillna(s.mean())
```

#### Convert a series of str formatted dates into a datetime type

```python
norm_dates = pd.to_datetime(str_dates, format='%Y%m%d')
```

[Back to top](#top)
______________________________________________

## <a name="numpy">Numpy</a>

#### Create an array

```python
a = np.array([1,2,3,4,5,6])     # 1D
b = np.array([[1,2,3],          # 2D
              [4,5,6]])
c = np.array([[[1,2,3],         # 3D
               [4,5,6]],
              [[7,8,9],
               [10,11,12]]])
```

#### Reshape array

```python
a = np.array([1,2,3,4,5,6]).reshape(2,3)  # 2 rows, 3 cols
```

#### Create an array of evenly spaced values (by step)

```python
a = np.arange(1,10,2)
```

#### Create an array of evenly spaced values (by # of samples)

```python
a = np.linespace(1,10,101)   # odd numbers for 3rd parameter work best
```

#### `np.random.uniform` & `np.random.normal`
The np.random subpackage contains some functions for creating arrays of random numbers. These two are the most useful, but there are more!

```python
unif = np.random.normal(loc=0.0, scale=1.0, size=10**7)

fig, ax = plt.subplots(figsize=(10, 4))
_ = ax.hist(unif, bins=100, color="green")
```

```python
unif = np.random.normal(loc=0.0, scale=1.0, size=10**7)

fig, ax = plt.subplots(figsize=(10, 4))
_ = ax.hist(unif, bins=100, color="green")
```

#### Create a new array based on conditions

```python
arr = np.arange(10)
out = np.where(arr % 2 == 1, -1, arr)
print(arr)
out
#> [0 1 2 3 4 5 6 7 8 9]
# array([ 0, -1,  2, -1,  4, -1,  6, -1,  8, -1])
```

[Back to top](#top)
______________________________________________

## <a name="scipy">Scipy</a>


[Back to top](#top)
______________________________________________

## <a name="matplot">matplotlib</a>

#### The Object Oriented interface

```python
# this is a shorter way to create 
# a single blank figure & axes
fig, ax = plt.subplots()

ax.plot(x_data,y_data_1)

ax.set_title('some stuff')
ax.set_xlabel('horizontal axis')
ax.set_ylabel('vertical axis')

# let's add another plot on these axes
ax.scatter(x_data, y_data_2, color='b')
```

#### Subplots
* `plt.subplots(n,m)` specifies a grid with n rows and m columns, with an axes object in each grid square. These axes objects are returned in a numpy array.
* `figsize=(width, length)` parameter in suplots() controls the size
* `plt.tight_layout()` prevents ugly overlapping text
* ***Remember you can use `dir()` function on any object to see it's attributes and methods!!!***

```python
fig, axs = plt.subplots(2,4, figsize=(10,4))

axs[0,2].plot(x_data,y_data_2)
axs[0,2].set_title('cool')

plt.tight_layout()
```

#### Interating over subplots

```python
fig, axs = plt.subplots(2,4, figsize=(10,4))

for i, ax in enumerate(axs.flatten()):
    ax.scatter(x_data,y_data_3)
    ax.set_title(f'Plot number {i}')

plt.tight_layout()
```

#### You can also use list comprehension

```python
m, n = 5,7
xx = np.linspace(0,10,40)
yy = np.random.random(size = (len(xx), m*n))
fig, axs = plt.subplots(m,n, figsize = (10,4))

[ax.scatter(xx, yy[:,i]) for i, ax in enumerate(axs.flatten())];
```

#### Scatterplot

```python
plt.scatter(
    x,              # scalar or array
    y,              # scalar or array
    s=None,         # marker size
    c=None,         # color
    marker=None,    # marker shape (ex. 'o'(default),'x','*','v','^')
    cmap=None,      # A `.Colormap` instance or registered colormap name. *cmap* is
                    # only used if c is an array  of floats.
    norm=None,      # used to scale luminance data between 0 and 1 (only used when c is an array  of floats)
    vmin=None,      # only used with norm
    vmax=None,      # only used with norm
    alpha=None,     # The alpha blending value, between 0 (transparent) and 1 (opaque).
    linewidths=None,# border width
    edgecolors=None,# color of border
    *,
    plotnonfinite=False,
    data=None,
    **kwargs,
)
```

#### Plot draws a line between each point instead of just the point

```python
# Example
plt.plot(x, 
         y, 
         color='k', 
         linestyle='--',
         linewidth=2,
         marker='^', 
         markersize=8)
```

[Plot() Documentation](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html)


[Back to top](#top)

______________________________________________

# <a name="aws">AWS</a>

#### Doing this weird vm thing:

In `~/.ssh/config` add...

```bash
Host examplename    # name of host
 HostName 52.27.155.84  # replace with path from AWS
 User ubuntu
 IdentityFile ~/.ssh/rft5.pem
```

Call using `ssh examplename`

#### Making a bucket and adding files to it

```python
import boto3

s3 = boto3.client('s3')

remote_file_name = 'cancer_rates.png'
local_file_name = 'cancer_rates.png'
bucket_name = 'mdubatto1'

s3.create_bucket(Bucket=bucket_name)

s3.upload_file(Filename=local_file_name, 
               Bucket=bucket_name, 
               Key=remote_file_name)
```

#### Copying a .py file from a local environment to a aws machine

```bash
scp local_file.py examplename:/home/ubuntu/remote_file.py
```

[Back to top](#top)

______________________________________________

# <a name="docker">Docker</a>

#### Postgres container

```zsh
docker run --name pgserv -d -p 5432:5432 -v "$PWD":/home/data -e POSTGRES_PASSWORD='password' postgres
```

- the `-d` flag means "run this container in the background"
- `-p 5432:5432` means "connect port 5432 from this computer (localhost) to the container's port 5432". This will allow us to connect to the Postgres server (which is inside the container) from services running outside of the container (such as python, as we'll see later).
  - Most services expect to find Postgres running on port 5432. If you have any previous installations of Postgres installed you may want to change this to 5435. If you do you will have to remember to specify what port to connect to working from your system.    
- the `-v` flag connects the filesystem in the container to your computer's filesystem. See the documentation for [docker volumes](https://docs.docker.com/storage/volumes/). 
  - Here, the container's folder `/home/data` will be mapped to whichever folder you ran the `docker run` command from (`$PWD`). If you want to make your entire home folder visible to the docker container, navigate to `~` before running the above command. If you only want the container to see, say, a folder you cloned from github, navigate to `/path/to/repo_folder` first. **Any changes made to files in this folder are immediately visible to the container and your native file system. This is important for the step of loading data into the database** 
- the `-e` is setting up an enviroment variable which is the default password for postgres.  You most likely want to choose something better than the default `password` above.

#### PySpark container

```zsh
docker run --name sparkbook -p 8881:8888 -v "$PWD":/home/jovyan/work jupyter/pyspark-notebook start.sh jupyter lab --LabApp.token=''
```

- this will take a while to download the first time you run it
- here I've given this container the name `sparkbook`. You can call it whatever you like.
- the `-p` flag is exposing port `8881`, so as not to collide with any other notebooks you have running.
- the `-v` flag connects the filesystem in the container to your computer's filesystem. See the documentation for [docker volumes](https://docs.docker.com/storage/volumes/). 
  - Here, the container's folder `/home/jovyan/work` will be mapped to whichever folder you ran the `docker run` command from (`$PWD`). If you want to make your entire home folder visible to the docker container, navigate to `~` before running the above command. If you only want the container to see, say, a folder you cloned from github, navigate to `/path/to/repo_folder` first. Then you can **make changes from inside the container** and **run git commands outside the container**
</br></br>
#### Open a bash shell in a container

```zsh
docker exec -it <container name> bash
```

[Back to top](#top)

______________________________________________

# <a name="mlw">Machine Learning Workflow</a>



[Back to top](#top)