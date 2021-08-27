# First post about plotting for better visualization

Here's the table of contents:

1. TOC
{:toc}

## Why I am posting this

Obviously, visualization is one of the best tools to make data understandable and support your arguments to listeners, readers, etc. - thus, in order to get your point thorugh to me, to anyone, I structured the way I use matplotlib/python and all these great further libraries, so that you get an easy way (hopefully) into plotting in python as well.

## Create your first easy figure

Python code and output:

```python
# define font and colors for graph descriptions and labels etc.
font = {'family': 'sans-serif',
        'color':  'black',
        'weight': 'normal',
        'size': 12,
        }
# colors that can be used for lines acc. to AquaSPICE project: 
#              'AquaSPICE_1': '#00599F', 'AquaSPICE_2': '#BDCD00', 
#              'AquaSPICE_3': '#8EBAE5','AquaSPICE_4': 'C7DDF2', 
#              'AquaSPICE_5': '595959', 'AquaSPICE_6': '#bfbfbf'

# setup figure and its size
cm = 1/2.54  # centimeters in inches
fig, ax1 = plt.subplots(figsize=(16*cm,9*cm))
fig.set_dpi(100)

# plot line on axis and give color to it
ax1.plot(EBSM_2020["Date"], EBSM_2020["COD[mg/L]"], color="#00599F")

# make grid in plot for better visibility
ax1.xaxis.grid(color="#bfbfbf")
ax1.yaxis.grid(color="#bfbfbf")

# set, color and label y axis 
ax1.yaxis.set_major_locator(ticker.LinearLocator(5)) #5 ticks only, always ;)
ax1.set_ylim([0,40]) #limit of range of y axis
ax1.set_ylabel("COD [mg/L]", fontdict=font, color="#00599F") #give name and color

# set color and label x axis
ax1.set_xticks(("01.01.2020", "01.03.2020", "01.05.2020", "01.07.2020", "01.09.2020")) # set specific ticks
ax1.set_xlim(["01.01.2020","01.09.2020"]) # limit x axis range
plt.xlabel("Date", fontdict=font) # give the x axis a name and its characteristics (font)


# rotate the x labels in a particular way (if there are questions, please let me know here - the rotation also works on data which is not in "date" format)
from datetime import datetime, timedelta
fig.autofmt_xdate(rotation=45)


plt.show()
```

## Create your figure with secondary y-axis

```python
# define font and colors for graph descriptions and labels etc.
font = {'family': 'sans-serif',
        'color':  'black',
        'weight': 'normal',
        'size': 12,
        }
# colors that can be used for lines acc. to AquaSPICE project: 
#              'AquaSPICE_1': '#00599F', 'AquaSPICE_2': '#BDCD00', 
#              'AquaSPICE_3': '#8EBAE5','AquaSPICE_4': 'C7DDF2', 
#              'AquaSPICE_5': '595959', 'AquaSPICE_6': '#bfbfbf'

# setup figure and its size
cm = 1/2.54  # centimeters in inches
fig, ax1 = plt.subplots(figsize=(16*cm,9*cm))
fig.set_dpi(100)

# plot line on axis and give color to it
ax1.plot(EBSM_2020["Date"], EBSM_2020["COD[mg/L]"], color="#00599F")

# make grid in plot for better visibility
ax1.xaxis.grid(color="#bfbfbf")
ax1.yaxis.grid(color="#bfbfbf")

# set, color and label y axis 
ax1.yaxis.set_major_locator(ticker.LinearLocator(5)) #5 ticks only, always ;)
ax1.set_ylim([0,40]) #limit of range of y axis
ax1.set_ylabel("COD [mg/L]", fontdict=font, color="#00599F") #give name and color

# set color and label x axis
ax1.set_xticks(("01.01.2020", "01.03.2020", "01.05.2020", "01.07.2020", "01.09.2020")) # set specific ticks
ax1.set_xlim(["01.01.2020","01.09.2020"]) # limit x axis range
plt.xlabel("Date", fontdict=font) # give the x axis a name and its characteristics (font)

## NOW --> second axis (ax2)
# create another y-axis sharing a common x-axis
ax2 = ax1.twinx()

# plot line on axis and give color to it
ax2.plot(WaterIntake_2020["Date"], WaterIntake_2020["Total Water [m³/h]"], "#BDCD00")

# label, color and set 2nd y axis 
ax2.yaxis.set_major_locator(ticker.LinearLocator(5)) #5 ticks only, always ;)
ax2.set_ylim([500,1500]) # limit range of y axis
ax2.set_ylabel("Total Water Intake [m³/h]", color="#BDCD00", fontdict=font) # give name and color


# label, color and set x axis of ax2 (same as ax1)
ax2.set_xlabel("Date", fontdict=font)
ax2.set_xlim(["01.01.2020","01.09.2020"])
ax2.set_xticks(("01.01.2020", "01.03.2020", "01.05.2020", "01.07.2020", "01.09.2020"))


# rotate the x labels in a particular way (if there are questions, please let me know here - the rotation also works on data which is not in "date" format)
from datetime import datetime, timedelta
fig.autofmt_xdate(rotation=45)


plt.show()
```
## Annotate your figure to avoid ugly legends



## Further information to grab

One of the main places I look for information regarding the plots with matplotlib is its [documentation](https://matplotlib.org/) (obviously).
But in particular, I find the [gallery](https://matplotlib.org/stable/gallery/index.html) useful to get inspiration on how to visualize my data and look at example codes that have been created.

## Footnotes

[^1]: This is the footnote.


