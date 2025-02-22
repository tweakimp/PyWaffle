# Icons

PyWaffle supports [Font Awesome icons](https://fontawesome.com/). Blocks could be icons instead of squares.

When using icons, the parameters for setting block size would be ignored, including `interval_ratio_x`, `interval_ratio_y` and `block_aspect_ratio`. Instead, use `icon_size` to set the size of icons. For availale sizes, visit [FontProperties.set_size](https://matplotlib.org/api/font_manager_api.html#matplotlib.font_manager.FontProperties.set_size).

```python
fig = plt.figure(
    FigureClass=Waffle,
    rows=5,
    columns=10,
    values=[48, 46, 3],
    colors=["#232066", "#983D3D", "#DCB732"],
    icons='star',
    icon_size=12,
)
```
    
<img class="img_middle" alt="Icons" src="https://raw.githubusercontent.com/gyli/PyWaffle/master/examples/docs/icons.svg?sanitize=true">

Categories could have different icon settings by passing parameter `icons` a list or tuple of icon names. The length must be the same as `values`.

In Font Awesome Icons, there are different icon sets in different styles, including Solid, Regular and Brands. It can be specified through parameter `icon_style`. By default it searches icon from `solid` style.

With `icon_legend`=`True`, the symbol in legend would be the icon. Otherwise, it would be a color bar.

```python
fig = plt.figure(
    FigureClass=Waffle,
    rows=5,
    values=[48, 46, 3],
    colors=["#FFA500", "#4384FF", "#C0C0C0"],
    icons=['sun', 'cloud-showers-heavy', 'snowflake'],
    icon_size=12,
    icon_style='solid',
    icon_legend=True,
    legend={
        'labels': ['sun', 'shower', 'snow'], 
        'loc': 'upper left', 
        'bbox_to_anchor': (1, 1)
    }
)
```

<img class="img_middle" alt="Icons per category" src="https://raw.githubusercontent.com/gyli/PyWaffle/master/examples/docs/icons_different_per_category.svg?sanitize=true">

Font Awesome Icons locates icons by style and icon name. Different styles contain different sets of icons. Thus icon_style might not be the same for all icons. In this case, `icon_style` could be a list or a tuple of styles. 

```python
fig = plt.figure(
    FigureClass=Waffle,
    rows=5,
    values=[48, 46, 3],
    colors=["#FFA500", "#4384FF", "#C0C0C0"],
    icons=['sun', 'cloud-showers-heavy', 'font-awesome-flag'],
    icon_size=12,
    icon_style=['regular', 'solid', 'brands'],
    icon_legend=False,
    legend={
        'labels': ['sun', 'shower', 'flag'], 
        'loc': 'upper left', 
        'bbox_to_anchor': (1, 1)
    }
)
```

<img class="img_middle" alt="Icons with different styles" src="https://raw.githubusercontent.com/gyli/PyWaffle/master/examples/docs/icons_different_style.svg?sanitize=true">
