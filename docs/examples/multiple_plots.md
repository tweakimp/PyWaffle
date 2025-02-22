# Multiple Plots

It is quite common that we would like to show multiple waffle charts in one plot. Multiple plots is supportted by
PyWaffle so that duplicated legends, titles and other components could be avoided.

Let's say we have sample data as shown below:

```python
import pandas as pd
data = pd.DataFrame(
    {
        'labels': ['Hillary Clinton', 'Donald Trump', 'Others'],
        'Virginia': [1981473, 1769443, 233715],
        'Maryland': [1677928, 943169, 160349],
        'West Virginia': [188794, 489371, 36258],
    },
).set_index('labels')

# A glance of the data:
#                  Maryland  Virginia  West Virginia
# labels
# Hillary Clinton   1677928   1981473         188794
# Donald Trump       943169   1769443         489371
# Others             160349    233715          36258
```

To convert the vote numbers into reasonable block numbers, we can simply passing in values like `data['Virginia'] / 30000`. Note that parameter `values` also accpet column data in pandas.Series type. For now, unlike values in dict, pandas.Series value does not support auto labeling yet.

To make multiple plots, move and merge the parameters for each plot to parameter `plots` as dict values. The keys are 3-digit integer describing the position of the subplot. Take a look of [matplotlib.pyplot.subplot](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplot.html) in Matplotlib document for detail.

Parameters could also be shared among plots, simply by keeping passing them to matplotlib.pyplot.figure like for single plot, instead of moving to `plots`.

> **_NOTE:_** Parameters specified in `plots` would overwrite the shared parameters.

```python
fig = plt.figure(
    FigureClass=Waffle,
    plots={
        '311': {
            'values': data['Virginia'] / 30000,
            'labels': ["{0} ({1})".format(n, v) for n, v in data['Virginia'].items()],
            'legend': {
                'loc': 'upper left',
                'bbox_to_anchor': (1.05, 1),
                'fontsize': 8
            },
            'title': {
                'label': '2016 Virginia Presidential Election Results',
                'loc': 'left'
            }
        },
        '312': {
            'values': data['Maryland'] / 30000,
            'labels': ["{0} ({1})".format(n, v) for n, v in data['Maryland'].items()],
            'legend': {
                'loc': 'upper left',
                'bbox_to_anchor': (1.2, 1),
                'fontsize': 8
            },
            'title': {
                'label': '2016 Maryland Presidential Election Results',
                'loc': 'left'
            }
        },
        '313': {
            'values': data['West Virginia'] / 30000,
            'labels': ["{0} ({1})".format(n, v) for n, v in data['West Virginia'].items()],
            'legend': {
                'loc': 'upper left',
                'bbox_to_anchor': (1.3, 1),
                'fontsize': 8
            },
            'title': {
                'label': '2016 West Virginia Presidential Election Results',
                'loc': 'left'
            }
        },
    },
    rows=5,
    colors=("#2196f3", "#ff5252", "#999999"),  # shared parameter among subplots
    figsize=(9, 5)  # figsize is a parameter of plt.figure
)
```

<img class="img_middle" alt="With dict values" src="https://raw.githubusercontent.com/gyli/PyWaffle/master/examples/readme/multiple_plots.svg?sanitize=true">

<sub>Data source: [https://en.wikipedia.org/wiki/United_States_presidential_election,_2016](https://en.wikipedia.org/wiki/United_States_presidential_election,_2016).</sub>
