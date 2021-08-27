# First post about plotting for better visualization

Here's the table of contents:

1. TOC
{:toc}

## Why I am posting this

Obviously, visualization is one of the best tools to make data understandable and support your arguments to listeners, readers, etc. - thus, in order to get your point thorugh to me, to anyone, I structured the way I use matplotlib/python and all these great further libraries, so that you get an easy way (hopefully) into plotting in python as well.

## Create your first easy figure

## Code

Python code and output:

```python
# define font and colors for graph descriptions and labels etc.
font = {'family': 'sans-serif',
        'color':  'black',
        'weight': 'normal',
        'size': 12,
        }
# colors that can be used for lines acc. to the AquaSPICE project: 'AquaSPICE_1': '#00599F', 'AquaSPICE_2': '#BDCD00', 
#              'AquaSPICE_3': '#8EBAE5','AquaSPICE_4': 'C7DDF2', 
#              'AquaSPICE_5': '595959', 'AquaSPICE_6': '#bfbfbf'


fig, ax1 = plt.subplots()

# plot line on axis and give color to it
ax1.plot(EBSM_2020["Date"], EBSM_2020["COD[mg/L]"], color="#00599F")

# make grid for better visibility
ax1.xaxis.grid()
ax1.yaxis.grid()

# set size of figure
fig.set_size_inches(5, 4.5)
fig.set_dpi(100)

# set ticks
ax1.xaxis.set_major_locator(ticker.LinearLocator(5))
ax1.yaxis.set_major_locator(ticker.LinearLocator(5))

#rotate y axis labels
plt.xticks(rotation=45)

# set axes ranges
plt.xlim(["01.01.2020","31.06.2020"])
plt.ylim([0,50])

# label x and y axis
plt.xlabel("Date", fontdict=font)
plt.ylabel("COD [mg/L]", fontdict=font)

plt.show()
```

## Further information to grab

One of the favorite places I look for inspiration and information regarding the plots with matplotlib is its documentation





## Footnotes

[^1]: This is the footnote.


