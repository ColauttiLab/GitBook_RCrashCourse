# Quick Visualizations

## Overview

Visualizing data is a key step in any analysis. Whether you are just starting to understand the structure of your data or polishing off the perfect figure for publication in 'tabloid' journal like [Science](https://www.science.org/journal/science) or [Nature](https://www.nature.com/), R provides powerful and flexible graphing tools.

In this tutorial, you will learn how to make quick graphs with the `qplot` function, with the option of some basic formatting customization. In the [ggplot Tutorial](https://colauttilab.github.io/RCrashCourse/3_ggplot.html) you will learn some additional tricks and resources for developing your graphing skills even further

By the time you are finished these two self-tutorials, you will have all the resources you need to make **publication-ready graphics**! All you will really need to do is practice and apply what you have learned.

Both `qplot` and `ggplot` come from the [`ggplot2`](https://ggplot2.tidyverse.org/) package. Don't ask me what happened to ggplot1... Developed by Hadley Wickham and the same team as R Studio, `ggplot2` is part of the [Tidyverse](https://www.tidyverse.org/) group of helpful R packages. 

Once you have mastered these tutorials, you might want to continue to expand your `ggplot` repertoire by reading through additional examples in the `ggplot2` documentation http://docs.ggplot2.org/current/

> WARNING: There is a learning curve!

Learning visualizations in R can feel like a struggle at first, and you may ask yourself: *Is it worth my time?* If you already have experience making figures with graphics programs, you may ask youself: *Why deal with all these coding errors when I can just generate a quick figure in a different program?* There are a few good reasons to invest the time to get over the learning curve and use R for all your graphing needs.

  1. You will get much faster with practice
  2. You have much more control over every aspect of your figure
  3. Your visualization will be **reproducible**, meaning anyone with the data and the code can reproduce every aspect of your figure, from each individual data point down to the specific axis labels.

The third point is worth some extra thought. Everybody makes mistakes, whether you are graphing with R or a point-and-click graphics program. If you make an error in R you will either get an error message telling you, or you will have reproducible code that you can have somebody check. If you make a mistake in a point-and-click program, you may produce a graph that is incorrect and no way to check!

Now consider what happens if you add new data or find a mistake in your original data that needs to be corrected. With a point-and-click program you have to make the graph all over again. With R, you just rerun the code with new input and get the updated figure right away!

### Graphical Concepts

There are a few universal graphing concepts that are important to understand in order to create publication-ready graphics in R.

### Vector vs. Raster

The first concept is to understand that there are two main **file types** that you can use to save your graphs. Once saved, you can send these to graphics programs, printers, or journal websites. 

**Raster** files save graphs in a 2-dimensional grid of data corresponding to pixels. You are probably quite familiar with this format if you've ever worked with a digital photo or an 8-bit video game. Some popular Raster file types include *JPEG/JPG, PNG, TIFF, and BMP*. 

**Vector** files save information about points, lines and curves. If you've ever drawn a shape in a program like Microsoft Powerpoint or Adobe Illustrator, you might have some sense of how this works. Some popular vector formats include *SVG, PDF, EPS, AI, PS*.

> Why does this matter?

In most cases, you should save your visualizations as **vector** files. *SVG* is a good choice, because it can be interpreted by web browsers and it is not proprietary. *PDF* and *EPS* are commonly used by publishers. The reason for this is that *raster* files introduce artifacs when they are scaled. You may have seen some images that look 'pixelated' -- this happens when you try to expand the size of a lower-resolution figure.

In contrast, you can expand **vector** images to any size and the lines will always be clean and clear. This is why they are generally preferred for publication. There are a few important exceptions, however.

  1. **Photographs** -- Photographs captured by a camera are saved in the *Raster* format and cannot be converted to vector without significant loss of information
  2. **Grid Data** -- Raster data are convenient for plotting data that occurs in a grid. This may include spatial data that is broken up into a geographic grid. However, even in these cases, you may often want to use the vector format so that the overlapping geographical features (e.g. borders, lakes, rivers) are not pixellated.
  3. **Large Data** --   With some large data applications a graph may have many millions or billions of data points or lines. In these cases, the **vector** file would be too big to use in publication (e.g. several gigabytes). In this case you might opt for a high-resolution *Raster* file. On the other hand, you could graph your data using a density grid with colours corresponding to the density of points. In this case, you could use the *vector* format to maintain clean lines for the graph axes and labels.
  
The bottom line: you generally want to save your graphics as *SVG* or *PDF* files if you plan to publish them.

### Resolution vs Dimension

In cases where you do need to use raster images in a publication, pay careful attention to the image's **Pixel Dimension**. We are used to thinking about resolution -- for example a 2 megapixel camera is better than a 1 megapixel camera. Or 200 dpi (dots per inch) is better than 100 dpi. But it's not just the **resolution** that matters, the image **size** also determines the quality of the final image. The **size** and **resolution** of an image jointly determine its **Pixel Dimension**.

For example, an image with 200 dpi that is 1 x 3 inches will have the same pixel dimension of an image with 100 dpi that is 2 x 6 inches. These images will look exactly the same if they are printed at the same size. That's because the pixel dimension determines how an image looks on a page, and both of these have the same pixel dimension: 200 x 600 pixels.

### Screen vs Print

Another important consideration is whether your figures are intended for a computer screen or printed page (or both). Each pixel of your screen has tiny lights that determine the specific colour that is reproduced. The **emission** of different wavelengths from your screen produces the different colours. In contrast, printed images get their colour from combinatios of ink, which **absorb** different wavelengths of colour. As a result, some colours that look fine on your screen do not reproduce well in print. In print, the intensity of colours are limited by the intensity of the Cyan, Magenta and Yellow inks that are used to reproduce the images. This is called CMYK printing.

Some programs like Adobe Illustrator have options to limit the colours on your screen to only display colours that can be reproduced with CMYK printing.

### Accessibility

There are two other important considerations for colouring your figures. First, remember that a significant portion of the population is unable to see certain colours. In addition, many scientists and students may print out your paper in black-and-white. You should try to choose colours that can be discerned in these situations.

The `viridis` package is a good tool for this. See: https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html

### Slides

Some of the above information is covered and expanded in the [Introductory Slides](https://colauttilab.github.io/RCrashCourse/Graphics_small.pdf) for examples of graphical output from R, using `ggplot2` and other graphing functions. These slides cover: 

  1. Graphing examples
  2. Graphical concepts
  3. `ggplot` grammar
  4. anatomy of a `qplot`/`ggplot` graph
  

## Getting Started

Install the `ggplot2` package using `install.packages("ggplot2")`. Load it with the `library` function whenever you want to include a function from the `ggplot2` library in your code.. 


```r
library(ggplot2)
```

The `ggplot2` package includes two main functions, quickplot `qplot()` for fast graphs and the `ggplot()` function for more detailed, customizable graphs.

### Data setup

We will again be working with the `FallopiaData.csv` dataset, which can be downloaded here: https://colauttilab.github.io/RCrashCourse/FallopiaData.csv, and saved to your project folder, which you can identify with the `getwd()` function. You may want to save this to a folder called 'Data', and then open the file in R:


```r
MyData<-read.csv("./Data/FallopiaData.csv", header=T)
```

alternatively, you can load the file right from the internet:


```r
MyData<-read.csv("https://colauttilab.github.io/RCrashCourse/FallopiaData.csv", 
                 header=T)
```

This dataset comes from the research group of Dr. Oliver Bossdorf at the University of Tuebingen in Tuebingen, Germany -- a wonderful little town on the Neckar River. The data come from a plant competition experiment involving two invasive species from the genus *Fallopia*.  


```r
str(MyData)
```

```
## 'data.frame':	123 obs. of  13 variables:
##  $ PotNum      : int  1 2 3 5 6 7 8 9 10 11 ...
##  $ Scenario    : chr  "low" "low" "low" "low" ...
##  $ Nutrients   : chr  "low" "low" "low" "low" ...
##  $ Taxon       : chr  "japon" "japon" "japon" "japon" ...
##  $ Symphytum   : num  9.81 8.64 2.65 1.44 9.15 ...
##  $ Silene      : num  36.4 29.6 36 21.4 23.9 ...
##  $ Urtica      : num  16.08 5.59 17.09 12.39 5.19 ...
##  $ Geranium    : num  4.68 5.75 5.13 5.37 0 9.05 3.51 9.64 7.3 6.36 ...
##  $ Geum        : num  0.12 0.55 0.09 0.31 0.17 0.97 0.4 0.01 0.47 0.33 ...
##  $ All_Natives : num  67 50.2 61 40.9 38.4 ...
##  $ Fallopia    : num  0.01 0.04 0.09 0.77 3.4 0.54 2.05 0.26 0 0 ...
##  $ Total       : num  67.1 50.2 61.1 41.7 41.8 ...
##  $ Pct_Fallopia: num  0.01 0.08 0.15 1.85 8.13 1.12 3.7 0.61 0 0 ...
```

The first 4 columns give information about the pot and treatments. The rest give biomass measurements. 

<br>

***

<br>

## Basic Graphs

Think back to the [R Fundamentals Tutorial](https://colauttilab.github.io/RCrashCourse/1_fundamentals.html), and you will hopefully recall the different data types. For graphing purposes, there are two main types of data: **categorical** and **continuous** putting these together in different combinations with `plot` gives us different graphs. One nice thing is that we don't have to specify which graphs to make; `qplot` will decide which type of graph based on the type of data. Of course, we can also specify a plot type if we want something different.


### One continuous

If we input one continous variable, `qplot` will produce a frequency histogram by default.

##### Histogram


```r
qplot(x=Total, data=MyData)
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-5-1.png" width="672" />

### One categorical

If we input one categorical variable, `qplot` will produce a bar graph showing counts for each category.

##### Bar Graph


```r
qplot(x=Scenario, data=MyData)
```

<img src="02_qplot_files/figure-html/unnamed-chunk-6-1.png" width="672" />

### Two continuous

If we input two continuous variables, we get the classic bivariate plot a.k.a. scatterplot.

##### Bivariate plot


```r
qplot(x=Silene, y=Total, data=MyData)
```

<img src="02_qplot_files/figure-html/unnamed-chunk-7-1.png" width="672" />

### Two categorical

Plotting two categorical variables just plots overlapping dots, and it's not so useful except if you want to check for representation of particular variables.


```r
qplot(x=Nutrients, y=Scenario, data=MyData)
```

<img src="02_qplot_files/figure-html/unnamed-chunk-8-1.png" width="672" />

In this case we can see that there is only one type of "Low" Nutrient treatment, but 4 types of "High" treatments. In other words, all of the rows with "Low" nutrient treatment also have the "Low" scenario, and NONE of the rows with "Low" in the scenario column have "Low" in the Nutrients column.

### Categorical by continuous

If we input a combination of categorical and continuous variables, we see get a categorical scatterplot showing the spread of points along the Y or X axis.

##### Categorical scatter plots


```r
qplot(x=Nutrients, y=Total, data=MyData)
```

<img src="02_qplot_files/figure-html/unnamed-chunk-9-1.png" width="672" />

That's it! That's all you need to start exploring your data! Load your data frame, and plot different combinations of variables to look at the distribution of values or the relationship between your variables.

Of course, you might also want to make a few quick tweaks to the look of the graph.

<br>

***

<br>

## Basic customization

There are a number of parameters available with `qplot()` to quickly customize a few of the basic features of your graphs. Most of these will work with `ggplot()` as well, though the syntax or context is a bit different in some cases. Refer back to these when you work through the [ggplot Tutorial](https://colauttilab.github.io/RCrashCourse/3_ggplot.html).

### `binwidth`

Use this with the histogram graph to alter the size of the 'bins' along the x-axis.


```r
qplot(x=Total, data=MyData, binwidth=9)
```

<img src="02_qplot_files/figure-html/unnamed-chunk-10-1.png" width="672" />

```r
qplot(x=Total, data=MyData, binwidth=0.5)
```

<img src="02_qplot_files/figure-html/unnamed-chunk-10-2.png" width="672" />

### `size`

This controls the size of points (usually) or sometimes lines, depending on the context.


```r
qplot(x=Silene, y=Fallopia, data=MyData, size=Total) # Scale by a variable
```

<img src="02_qplot_files/figure-html/unnamed-chunk-11-1.png" width="672" />

```r
qplot(x=Silene, y=Total, data=MyData, size=I(5)) # Scale by a constant
```

<img src="02_qplot_files/figure-html/unnamed-chunk-11-2.png" width="672" />

**NOTE** the use of the identity function: `I()` for constant. What happens if you just put a 5 in there without the identity function? Do it and see if you can figure out the problem.

Try using different numbers for comparison (e.g., 2, 5 and 10). How does the size change when you include the `I()` function vs when you just put the number in?

The explanation is a bit tricky, but imagine if you added a column to your data frame and put in a number. Then for size you put the column name. R would treat this as a variable and scale the size of the symbol to the value in this column. However, since all the rows have the same value, then they all have the same scaled size. Now try using a different column for scaling:


```r
qplot(x=Silene, y=Total, data=MyData, size=Total) # Scale by column 'Total'
```

<img src="02_qplot_files/figure-html/unnamed-chunk-12-1.png" width="672" />

You can see in the legend how the point size scales with the column called *Total*

On the other hand, the identify function `I()` tells R: *I want to use this exact point size*.

### `colour` or `color`

Another nice feature of `qplot` and `ggplot` is that you can use different spelling. You can use colour or color to colour add colour to your graphs.

For example, you can colours points based on a factor


```r
qplot(x=Silene, y=Fallopia, data=MyData, colour=Nutrients) # Categorical colour
```

<img src="02_qplot_files/figure-html/unnamed-chunk-13-1.png" width="672" />

```r
qplot(x=Silene, y=Fallopia, data=MyData, colour=Total) # Continuous colour
```

<img src="02_qplot_files/figure-html/unnamed-chunk-13-2.png" width="672" />

Or use the identity function `I()` again to set a specific colour


```r
qplot(x=Silene, y=Total, data=MyData, colour=I("purple")) # basic colour
```

<img src="02_qplot_files/figure-html/unnamed-chunk-14-1.png" width="672" />

```r
qplot(x=Silene, y=Total, data=MyData, colour=I(rgb(1,0,0))) # rgb = red/green/blue
```

<img src="02_qplot_files/figure-html/unnamed-chunk-14-2.png" width="672" />

#### Histogram

Note what happens when we use the `colour` parameter for a histrogram


```r
qplot(x=Total, data=MyData, group=Nutrients, colour=Nutrients)
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-15-1.png" width="672" />

The coloured outlines might be useful but we usually will want the inside coloured.

### `fill`

This parameter is used for boxes and other shapes that have a separate outline (`colour=`) and interior (`fill=`). 


```r
qplot(x=Total, data=MyData, group=Nutrients, fill=Nutrients)
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-16-1.png" width="672" />

### `posit`

Use this to adjust the position, usually for histograms or bar graphs. For example, if we want to compare histograms on the same graph:


```r
qplot(x=Total, data=MyData, group=Nutrients, fill=Nutrients)
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-17-1.png" width="672" />

It's hard to interpret that graph, so we can shift the position using `"dodge"`.


```r
qplot(x=Total, data=MyData, group=Nutrients, fill=Nutrients, posit="dodge")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-18-1.png" width="672" />

### `alpha`

Think of `alpha` as a measure of opacity, ranging from 0 to 1 with 1 being the default, solid point or line and 0 being invisible.

This is particularly useful for visualizing overlapping points.


```r
qplot(x=Silene,y=Total,data=MyData,size=I(5),alpha=I(0.3))
```

<img src="02_qplot_files/figure-html/unnamed-chunk-19-1.png" width="672" />

### `shape`

You can also change the shape of your points, again using a column of data or the identity `I()` function.


```r
qplot(x=Silene,y=Total,data=MyData,size=I(5),shape=Nutrients)
```

<img src="02_qplot_files/figure-html/unnamed-chunk-20-1.png" width="672" />

```r
qplot(x=Silene,y=Total,data=MyData,size=I(5),shape=I(17))
```

<img src="02_qplot_files/figure-html/unnamed-chunk-20-2.png" width="672" />

There are a number of different shapes available, by specifying a number from 0 through 25.

<img src="02_qplot_files/figure-html/unnamed-chunk-21-1.png" width="672" />

Note that the shapes with grey in the above figure can be coloured with `fill=` paremeter, while all of the black parts (lines and fill) can be coloured with the `colour=` parameter.

You can use `fill` and `colour` to customize these separately.


```r
qplot(x=Silene,y=Total,data=MyData,size=I(5),shape=I(21),fill=I("yellow"),colour=I("red"))
```

<img src="02_qplot_files/figure-html/unnamed-chunk-22-1.png" width="672" />

### `lab`, `xlab`, and `ylab`

Use these to customize your axis labels.


```r
qplot(x=Silene, y=Total, data=MyData,
      xlab="Silene Biomass",ylab="Total Biomass")
```

<img src="02_qplot_files/figure-html/unnamed-chunk-23-1.png" width="672" />

### `main`

This will add a title to your plot. Usually you wouldn't use this for a figure intended for publication, but this can be useful for reports, websites, presentations, supplementary material, appendices, etc.


```r
qplot(x=Silene,y=Total,data=MyData,main="Biomass")
```

<img src="02_qplot_files/figure-html/unnamed-chunk-24-1.png" width="672" />

<br>

***

<br>

## Themes and Geoms

Themes determine the look and 'feel' of your graphs, while Geoms determine the geometry -- how your data are physically mapped to the graphing space. In both `qplot` and `ggplot`, themes are added with a separate function linked to the graph by using the plus sign `+`. Geoms are defined by the `geom=` paremeter inside the `qplot()` function or with a specific `geom_FUNCTION()` linked to the main `ggplot()` function by using the plus sign.

These are easy to understand with a few examples.

### `+ theme_NAME()`

There are a number of available themes, defined by changing the *NAME* part. 


```r
qplot(x=Silene,data=MyData) + theme_grey() # default
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-25-1.png" width="672" />

```r
qplot(x=Silene,data=MyData) + theme_bw() # cleaner, better contrast
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-25-2.png" width="672" />

```r
qplot(x=Silene,data=MyData) + theme_linedraw() # thicker grid lines
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-25-3.png" width="672" />

```r
qplot(x=Silene,data=MyData) + theme_light() # fainter border and axis values
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-25-4.png" width="672" />

```r
qplot(x=Silene,data=MyData) + theme_minimal() # no borders
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-25-5.png" width="672" />

```r
qplot(x=Silene,data=MyData) + theme_classic() # x and y lines only, no tick marks
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-25-6.png" width="672" />

These can be further customized. Or you can create a completely new theme. For example, here is a simplified and cleaner version of `theme_classic` but with bigger axis labels taht are more suitable for figures in presentation or publication:


```r
# Clean theme for presentations & publications used in the Colautti Lab
theme_pub <- function (base_size = 12, base_family = "") {
  theme_classic(base_size = base_size, base_family = base_family) %+replace% 
    theme(
      axis.text = element_text(colour = "black"),
      axis.title.x = element_text(size=18),
      axis.text.x = element_text(size=12),
      axis.title.y = element_text(size=18,angle=90),
      axis.text.y = element_text(size=12),
      axis.ticks = element_blank(), 
      panel.background = element_rect(fill="white"),
      panel.border = element_blank(),
      plot.title=element_text(face="bold", size=24),
      legend.position="none"
    ) 
}
```

To use this theme, you could just copy-and-paste the above function into your R code. 

Alternatively, you could save it as a separate `.R` file and thean load it with the `source()` function.

A third, even easier option, is to load the version of this code that is available online:


```r
source("http://bit.ly/theme_pub")
```

The theme is called `theme_pub` (pub = publication):


```r
qplot(x=Silene,data=MyData) + theme_pub() # A clean format with bigger axis labels for publication
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-28-1.png" width="672" />

```r
qplot(x=Pct_Fallopia,y=Silene,data=MyData) + theme_pub() # Bivariate plot
```

<img src="02_qplot_files/figure-html/unnamed-chunk-28-2.png" width="672" />

### `theme_set`

If you want to use the same theme throughout your code, you can use this funciton.


```r
theme_set(theme_pub())
qplot(x=Silene,data=MyData) 
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-29-1.png" width="672" />

### `geom`

In addition to the default genomes that `qplot` uses for different data types, there are some other options available.

For example, the scatterplot doesn't give a good sense of the spread of the data.


```r
qplot(x=Nutrients,y=Total,data=MyData) # Basic
```

<img src="02_qplot_files/figure-html/unnamed-chunk-30-1.png" width="672" />

But the `boxplot` geom shows the median (line), 1st and 3rd quartiles (boxes), range of most observations (whiskers), and potential outliers (dots)


```r
qplot(x=Nutrients,y=Total,data=MyData,geom="boxplot") # Geom
```

<img src="02_qplot_files/figure-html/unnamed-chunk-31-1.png" width="672" />

Another useful example is for histograms with many 'bins' which can be smoothed into a `density` curve rather than plotting bar graphs.

For example, the bar graph from above 


```r
qplot(Total,data=MyData) # Basic
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-32-1.png" width="672" />

reformatted as a `density` geom.


```r
qplot(Total,data=MyData,geom="density") # Geom
```

<img src="02_qplot_files/figure-html/unnamed-chunk-33-1.png" width="672" />

See the `ggplot2` website for a complete list of geoms with examples:

https://ggplot2.tidyverse.org/reference/

<br>

***

<br>

## Multiple graphs

It is often handy to plot separate graphs for different categories of a grouping variable. This can be done with `facets` in `qplot`.

### `facets`

Facets have the general form `VERTICAL ~ HORIZONTAL`. Use the period `.` to indicate 'all data' r 'do not separate my data'.


```r
qplot(x=Silene,data=MyData,facets=Nutrients~.) # Vertical stacking
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-34-1.png" width="672" />

```r
qplot(x=Silene,data=MyData,facets=.~Nutrients) # Horizontal stacking
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-34-2.png" width="672" />

```r
qplot(x=Silene,data=MyData,facets=Taxon~Nutrients) # Both (2 column stacking)
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="02_qplot_files/figure-html/unnamed-chunk-34-3.png" width="672" />

<br>

***

<br>

## Save output

Saving your graphs to an external file requires three important steps: 

  1. Open a file using a function like `pdf` or `svg` for the **vector** format, or `png` for the **raster** format.
  2. Run the code to produce the graph, just like above. However, instead of seeing a graph in your R interface, you will not see anything because the graph is being sent to the file.
  3. Close the file! Do this with the `dev.off()` function. 
    
> Important: If you don't close the file, it is unusable.

Failing to close the file is a common source of error when generating graphs. If you are having problems with graphing outputs, try running the `dev.off()` function a few times to make sure you close any files that are 'hanging' open.

Here's an example code for making a `pdf` output of a grpah.


```r
pdf("SileneHist.pdf") # 1. Create and open a file
  qplot(x=Silene,data=MyData,facets=Taxon~Nutrients) # 2. Write the graph info
dev.off() # 3. Close the file
```

Note how the qplot command does not open in the plots window when you run this. This is because the info is sent to *SileneHist.pdf* file instead of the graphing area in your R console (e.g. *plots* tab in R Studio)

## Practice

Graphing may seem slow and tedious at first, but the more you practice, the faster you will be able to produce meaningful visualizations. 

Don't be afraid to try new things. Try mixing up components and see what happens. At worst you will just get an error message. 

Once you have a good understanding of these basics, you can see how to build more advanced plots with `ggplot()`.



