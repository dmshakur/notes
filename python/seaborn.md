
# Seaborn tutorials
[Seaborn tutorial site](https://seaborn.pydata.org/tutorial.html)

## Visualizing statistical relationships
The most important things gleamed from this tutorial can be quickly assimilated into memory,
the scatter plot and line plot, which are essentialy integrated and as one.

### Scatter/line plot
The default setting for kind is `scatter`, if nothing is specified. Only `x`, `y`, and `data` are necessary for displaying a scatter plot, while the line plot requires `kind` as well to be set to, `line`.
```python
sns.relplot(
    x = 'x_data',
    y = 'y_data',
    hue = 'hue',
    style = 'style',
    size = 'size',
    sizes = (start, end),
    palette = 'palette',
    estimator = 'estimator',
    markers = 'markers',
    dashes = 'dashes',
    hue_norm = 'hue_norm',
    ci = 'ci',
    sort = 'sort',
    data = 'data'
)
```

#### `X`
Here is where the data for the x axis goes.
The string for `x` should be the name of the column you want to include.
#### `Y`
This is where the data for the y axis goes.
The string for `y` should be the name of the column you want to include.
#### `Hue`
This setting enables another dimension, which will be displayed as a differentiation in color. 
Both discrete and continuous variables are allowed.
The string for `hue` should be the column you wish to include.
#### `Style`
This will alter the appearence of the line or point, allowing another dimension to be displayed.
The string for `style` should be the column you wish to include.
#### `Size`
Size also can add another dimension to your data, be changing the size of any point/line.
The string for `style` should be the column you wish to include.
#### `Sizes`
This is related to the `size` parameter. It sets a range for the size of the point/line.
#### `Palette`
This sets the color palette for the 
#### `Estimator`
Method for aggregating across multiple observations of the `y` variable at the same `x` level. If `None`, all observations will be drawn.
#### `Markers`
Object determining how to draw the markers for different levels of the style variable. Setting to True will use default markers, or you can pass a list of markers or a dictionary mapping levels of the style variable to markers. Setting to False will draw marker-less lines. Markers are specified as in matplotlib.
#### `Dashes`
An object determining how to draw the lines at different levels of the style variable.
#### `Ci`
Size of the confidence interval to draw when aggregating the estimator. `sd` will set it to be the standard deviation.
#### `Data`
This is where the dataset goes.
The data must be in pandas dataframe format.

### Plotting with date data
You can plot with date data by saving the plot to a variable and calling the `.fig.autofmt_xdate()` method as follows.
```python
g = sns.relplot(x = 'time', y = 'value', kind = 'line', data = df)
g.fig.autofmt_xdate()
```

### Showing multiple relationships with facets
Use the `col` parameter to indicate which variable you wish to plot over multiple plots.
When using the `col` parameter, a plot will be created for every unique value in that pandas column. Everything about each plot will be the same except for the `col` parameter.

The `col_wrap` parameter specifies how many plots will be displayed on the horizontal axis at a maximum. The same goes for `height` except that it indicates the maximum displayed plots for the vertical axis.
```python
sns.relplot(
    x = 'hori',
    y = 'vert', 
    col = 'z', 
    col_wrap = x_axis,
    height = y_axis,
    linewidth = linewidth,
    data = df
)
```

## Plotting with categorical data
Categorical scatter plots can be displayed as follows.
```python
sns.catplot(
    x = 'x',
    y = 'y',
    jitter = jitter,
    kind = 'kind',
    data = 'data'
)
```

By switching `x` and `y` you can make it so it displays horizontally instead of veritcally.

This plot is very similar to the line/scatter plot.
The key difference is that it can shown multiple `x`s at once.

#### `Jitter`
This sets the amount of deviation form a standard line, for human readability purposes of being able to see more data, without overlap.

#### `Kind`
Different settings:
* **Box**: This will represent the data as a candlestick plot.
* **Violin**: Displays categorical data that has a violin body shape.
* **Point**: Displays a line that shows a confidence interval for each measure of `y`.
* **Count**: Basically a bar chart. `x` and `y` must be none for count plots.
* **Bar**: A bar chart that displays additional data, other than the amount.
