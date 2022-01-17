# First Post about Getting Started with Plotting with Python/Matplotlib

Here's the table of contents:

1. TOC
{:toc}

## Why I am posting this

Obviously, visualization is one of the best tools to make data understandable and support your arguments to listeners, readers, etc. - thus, in order to get your point through to me, to anyone, visualize your data well!
I structured the way I use matplotlib/python and all these great further libraries so far, so that you get an easy way (hopefully) into plotting in python as well.
I am using the so called `"oo" - method` (**o**bject-**o**riented), which I also recommend to anyone as it is the method where you can actually adjust the plots in all possible ways you want your data to be visualized.

### Further information to grab

One of the main places I look for information regarding the plots with matplotlib is its [documentation](https://matplotlib.org/) (obviously).
But in particular, I find the [gallery](https://matplotlib.org/stable/gallery/index.html) useful to get inspiration on how to visualize data and look at example codes that have already been created.

## Creating your first easy figure

By the way... all the code I will present in the following lines, is available in my ipynb uploaded in github: [here](https://github.com/sarisabell/Shared_JPNBs/blob/main/Graphs_first_plots.ipynb) - so if you just want to look at the code in its finished version - look it up there.

### The presteps to do before you can start

First, I will import the libraries/functions that I need for plotting:
```python
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker
```

Then, I set up the font to be used for the graph labels.
```python
# define font and colors for graph descriptions and labels etc.
font = {'family': 'sans-serif',
        'color':  'black',
        'weight': 'normal',
        'size': 12,
        }
```
What is very important in a lot of projects, and (probably also yours) is the given templates/styles and colours. In my project, which I am currently working on I can use the following colours, which my students should also be using:
- dark blue: `'#00599F'` 
- green: `'#BDCD00'` 
- medium blue: `'#8EBAE5'`
- light blue: `'#C7DDF2'`
- dark grey: `'#595959'`
- light grey: `'#bfbfbf'`

Obviously, you need some data, which you want to plot - I will usually read my data from `.csv`-files:

```python
Data=pd.read_csv("Data/Example.csv", delimiter=';'); #depending on how you have saved your csv file, you might have different delimiters!
```
After importing the data as a pd dataframe, I usually check the types of the data by using the function `.dtypes` (more info [here](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dtypes.html)) on the now imported dataframe `Data`.
This way, I make sure that I have integers or floats that I am working with. If you have objects within your dataframe, these will not be plotted, so check your csv file up front!
Maybe you have some spaces or some data in between which does not have the type `int` or `float`.

### Finally - working on the actual figure

Following, I will finally set up the *"framework"* for the figure to come (basically the box in which the graph will eventually unfold):
```python
cm = 1/2.54  # centimeters in inches
fig, ax1 = plt.subplots(figsize=(16*cm,9*cm))
fig.set_dpi(100)
```
Then I plot the line within the box and give a certain color to it:
```python
ax1.plot(Example["Date"], Example["Parameter [mg/L]"], "-", color="#00599F") #the "-" here means that I will get a line plot, if you want dots, use e.g. "."
```
I also make a grid for better readibility (also in the given colours):
```python
ax1.xaxis.grid(color="#bfbfbf")
ax1.yaxis.grid(color="#bfbfbf")
```
Now, I will do the settings for x and y axis:

```python
# set, color and label y axis 
ax1.yaxis.set_major_locator(ticker.LinearLocator(5)) #5 ticks only, always ;)
ax1.set_ylim([0,40]) #limit of y axis' range
ax1.set_ylabel("Parameter [mg/L]", fontdict=font, color="#00599F") #give name and color

# set color and label x axis
ax1.set_xticks(("01.01.2020", "01.03.2020", "01.05.2020", "01.07.2020", "01.09.2020")) # set specific ticks, again max. 5
ax1.set_xlim(["01.01.2020","01.09.2020"]) # limit x axis' range
plt.xlabel("Date", fontdict=font) # give the x axis a name and its characteristics (font, as was described earlier)
```
Last, I usually rotate the x labels, because oftentimes I have dates as labels - the rotation also works with other data than "date" though!

```python
from datetime import datetime, timedelta #import specific function that is required for an "easy" rotation
fig.autofmt_xdate(rotation=45)
```

And **finally** I will let the plot show:
```python
plt.show()
```
The output here will look like this:

![](/images/first_plot.png "Your first easy plot")



## Create your figure with another dataset, which uses a secondary y-axis

For this, if I start within a new file/notebook, I will do all the work which I have commented on previously again (basically `copy`-`paste`;)), except for the rotation of the x axis' labels (and I will add colour to the y axis label `Parameter 1 [mg/L]`:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker
font = {'family': 'sans-serif',
        'color':  'black',
        'weight': 'normal',
        'size': 12,
        }
# setup figure and its size
cm = 1/2.54  # centimeters in inches
fig, ax1 = plt.subplots(figsize=(16*cm,9*cm))
fig.set_dpi(100)

# plot line on axis and give color to it
ax1.plot(Example["Date"], Example["Parameter [mg/L]"], color="#00599F")

# make grid in plot for better visibility
ax1.xaxis.grid(color="#bfbfbf")
ax1.yaxis.grid(color="#bfbfbf")

# set, color and label y axis 
ax1.yaxis.set_major_locator(ticker.LinearLocator(5)) #5 ticks only, always ;)
ax1.set_ylim([0,40]) #limit of range of y axis
ax1.set_ylabel("Parameter 1 [mg/L]", fontdict=font, color="#00599F") #give name and color (here I further added a 

# set color and label x axis
ax1.set_xticks(("01.01.2020", "01.03.2020", "01.05.2020", "01.07.2020", "01.09.2020")) # set specific ticks
ax1.set_xlim(["01.01.2020","01.09.2020"]) # limit x axis range
plt.xlabel("Date", fontdict=font) # give the x axis a name and its characteristics (font)
```
And **NOW** I add the second axis `ax2`:
```python
# create another y-axis sharing a common x-axis
ax2 = ax1.twinx()

# plot line on axis and give color to it
ax2.plot(Example["Date"], Example["Water [m³/h]"], "#BDCD00")

# label, color and set 2nd y axis 
ax2.yaxis.set_major_locator(ticker.LinearLocator(5)) #5 ticks only, always ;)
ax2.set_ylim([500,1500]) # limit range of y axis
ax2.set_ylabel("Water [m³/h]", color="#BDCD00", fontdict=font) # give name and color

# label, color and set x axis of ax2 (same as ax1)
ax2.set_xlabel("Date", fontdict=font)
ax2.set_xlim(["01.01.2020","01.09.2020"])
ax2.set_xticks(("01.01.2020", "01.03.2020", "01.05.2020", "01.07.2020", "01.09.2020"))

# rotate the x labels in that particular way
from datetime import datetime, timedelta
fig.autofmt_xdate(rotation=45)

plt.show()
```

The output will then look like:

![](/images/second_y_axis_plot.png "Your second plot with second y axis")






