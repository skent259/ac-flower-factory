# R


## Tidyverse

### ggplot2

See the [ggplot2 book](https://ggplot2-book.org/) online for more information

#### List of extensions to GGplot

* [Website maintaining extensions](http://www.ggplot2-exts.org/gallery/) - makes it easier to find ggplot extensions for what you need
* [Flipbook to modify major parts of the graph](https://evamaerey.github.io/little_flipbooks_library/taming_themes_in_ggplot/taming_ggplot_themes.html#1) - flipbook for messing with parts of the graph. 
* [Blog version of modifying everything in ggplot2](https://cedricscherer.netlify.com/2019/08/05/a-ggplot2-tutorial-for-beautiful-plotting-in-r/#prep)
* [Another step by step ggplot violin plot](https://ggplot2tutor.com/powerlifting/squats/)

<!-- #### ggraph

* layouts `ggraph(g, layout = "linear")`
  * linear
  * igraph
  * dendrogram
  * manual (specify with x, y dataframe)
  * treemap
  * circlepack
  * partition
  * hive
  * See `?ggraph` for more information
* colors
  * everything seems to be replaced with  -->

#### Legend

```R
theme(legend.position = c(.8, .2)) # top, bottom, left, right
geom_point(aes(x,y), show.legend = FALSE) 
```

#### Scales/Palettes

Using RColorBrewer
```r
RColorBrewer::display.brewer.all() # see all palettes 

scale_color_brewer(palette = "RdPu") # distinct colors
scale_color_distiller(palette = "RdPu") # for continuous data
```

Using manual scales

![](http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/figure/unnamed-chunk-5-1.png)
![](http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/figure/unnamed-chunk-5-2.png)
```R
scale_linetype_manual(name = "Linetypes", labels=c(...), values = c("blank", "solid", "dashed", "dotted", "dotdash", "longdash", "twodash"))
# w/ grey
cbPalette <- c("#999999", "#E69F00", "#56B4E9", "#009E73", "#F0E442", "#0072B2", "#D55E00", "#CC79A7")
# w/ black
cbbPalette <- c("#000000", "#E69F00", "#56B4E9", "#009E73", "#F0E442", "#0072B2", "#D55E00", "#CC79A7")
scale_color_manual(name = "Colors", values=cbPalette)
scale_fill_manual(name = "Colors", values=cbPalette)
```


#### Labels

```R
labs(x="x",
     y="y",
     title="Title",
     subtitle="Subtitle")
```

#### Statistical Summaries
```r
ggplot(diamonds, aes(color, price)) + 
  geom_bar(stat = "summary_bin", fun.y = mean)
```

#### Themes

[Ch 15 of ggplot2 book](https://ggplot2-book.org/polishing.html) has comprehensive guide on themes.

#### Multiplots

```R
library(gridExtra)
plot1 <- qplot(1)
plot2 <- qplot(1)
grid.arrange(plot1, plot2, ncol=2)
```

#### Ggplotly

- [Example of customizing tooltip](https://stackoverflow.com/questions/36325154/how-to-choose-variable-to-display-in-tooltip-when-using-ggplotly)

#### Cool example of detailed visualizations in ggplot

- [Cocktails with UMAP](https://github.com/MNoichl/Cocktails/blob/master/Cocktails-Cleanup.ipynb)

#### Saving plots

- [Nice defaults for plots in slides](https://rdrr.io/github/bjeil/beTools/src/R/qSave.r)

###  Programming with dplyr

* `quo` - is used to mark the variable name as literal, kind of like quotes "
* `enquo` - is used to look INSIDE what the variable, and quote that! It uses "dark magic"

```r
my_summarise <- function(df, group_var) {
  df %>%
    group_by(!! group_var) %>%
    summarise(a = mean(a))
}

my_summarise(df, quo(g1))
```
In order to make the call `my_summarise(df, g1)`, we need to make the following change:

```r
my_summarise <- function(df, group_var) {
  group_var <- enquo(group_var)
  df %>%
    group_by(!! group_var) %>%
    summarise(a = mean(a))
}

my_summarise(df, g1)
```

- If you have a string that you want denoted, you should use `rlang::sym` as suggested [here](https://stackoverflow.com/questions/44121728/programming-with-dplyr-using-string-as-input).
- When you want a variable for the column name, you need to make use of the syntax `!! colname := function(x) ...`, otherwise it's not valid R code.
- You can filter with expressions using the `parse_expr` function in the `rlang` package as follows

```r
expr <- paste0("s",1:2, " == ", c(0,1), collapse = " & ") # s1 == 0 & s2 == 1
filter(df, !!parse_expr(expr)) 
```


#### Recipes

1. [Getting relative frequencies from dplyr](https://stackoverflow.com/questions/24576515/relative-frequencies-proportions-with-dplyrS) - note that summarize unwraps the last grouping, can check with `groups()`. useful for bar plots of the frequencies

```R
mtcars %>%
  group_by(am, gear) %>%
  summarise(n = n()) %>%
  mutate(freq = n / sum(n)) # Gets Rel Freq from WITHIN all counts of am
```

2. [Reordering x for bar graphs](https://stackoverflow.com/questions/5208679/order-bars-in-ggplot2-bar-graph)

```R
ggplot(theTable,
       aes(x=reorder(Position,Position,
                     function(x)-length(x)))) +
       geom_bar()
```

### Lubridate



### Tibble

* `as_tibble(...,)`
  * For forcing matrices, `as_tibble(mat, .name_repair = ~c("a", "b", "c"))` allows you to name the columns for matrices without column names in one line
* `bind_rows` or `bind_col` is more efficient for combining lots of dataframes

## Packages

### Creating them 
[R official reference](https://cran.r-project.org/doc/manuals/R-exts.pdf) - pretty complete version of creating the packages

### Spatial

[Source list for spatial with crowd sourced twitter](https://www.zevross.com/blog/2019/05/01/unscientific-list-of-popular-r-packages-for-spatial-analysis/)

<details>
<summary> List of packages </summary>

<ul>
  <li>sf</li>
  <li>raster</li>
  <li>sp</li>
  <li>leaflet</li>
  <li>tmap</li>
  <li>mapview</li>
  <li>rgdal</li>
  <li>cartography</li>
  <li>gstat</li>
  <li>tigris</li>
</ul>

</details>




## Useful Functions to remember

* `gl()` - Factor level generation
* `xtabs()` - Cross table generation
* `table()` - see table of distribution
* `search()` see all packages that have been loaded

## Cookbook


### Working with formula object in R

```r
formula(y~x1 + x2) # create the formula object
frame <- model.frame(formula, data, drop.unused.levels = TRUE) # Get the relevant columns in the data frame used in the formula
model.matrix(formula, frame) # create the `X` matrix for working with the levels in the frame above based on formula
```

`attr(rhs, "assign")` - attribute contains the index of variable that each column of model matrix comes from. If 3 levels, you would need intercept, and 2 columns of the model matrix.

### Row-wise workflows 

Examples in [this workshop](https://github.com/jennybc/row-oriented-workflows#readme)

### Working with factors

```r
as.numeric(levels(temp))[temp] # unfactor temp
factor(cheese$additive, levels(cheese$additive)[c(4,1:3)]) # Reorder the factors
reorder(cheese$additive, cheese$scores, FUN = mean) # Relevel additives factor, by their average score
```


## Data Cleaning

Use `library(tidyr)`, this is the new interface into reshape

* `gather()` - fat to narrow
* `spread()` - narrow to fat


```R
gather(key, value, columns)
```


[GGplot force legend with constant aes](https://aosmith.rbind.io/2018/07/19/legends-constants-for-aesthetics-in-ggplot2/)


## Shortcuts

`Option+ Shift + k` - show keyboard shortcuts

## Kable

```R
kable(TABLE, booktabs=T) %>% kable_styling(position = center) %>% row_spec(2, hline_after=T)
```

## Advanced R

### Data Structures

* 6 Atomic types: logical, integer, double, character, complex, raw
* 3 properties of vectors: typeof(), length(), attributes()
* Coercion is least to most flexible, atomic type
* Most important attributes: Names, Dimensions, Class

### Objects

Need `library(pryr)` to use the main functions.

* `typeof()` - base type
* `otype()` - object type
* `ftype()` - tells you if "generic" function or "method"
* `is.object(x)` - Checks if has "class" attribute

###  Generic Functions

In the S3 Object system, methods don't belong to a class, but belong to a generic function.

Generic are responsible for something called *method dispatch* in which they are supposed to find the right method to use for the call. This is a system for polymorphism that is used in the Lisp system, but not very common otherwise.



```R
ftype()
summary # the generic function
summary.lm # methods associated with generic function
summary.glm 

> ftype(summary)
[1] "s3"      "generic"
> ftype(summary.lm)
[1] "s3"     "method"
> methods(summary)
 [1] summary.aov                    summary.aovlist*              
 [3] summary.aspell*                summary.check_packages_in_dir*
 [5] summary.connection             summary.corAR1*               
 [7] summary.corARMA*               summary.corCAR1*   
```

Classes are very casual in S3, it's essentially treated as an attribute, and can even have multiple classes, eg. glm. `UseMethod` though will look for the appropriate method based on the class that you pass to the class. DO NOT USE `.` when naming methods! It will make it look like an S3 object

```R
foo <- c(1, 2, 3, 4)
class(foo) <- "something"
t(foo) # will look for the method t.something to run
```


### Environments

Environments are basically just like lists, with 4 special characteristics.
1. They have parents,
2. elements of the list are not numbered
3. Each element defined is unique
4. Must use `rm()` to remove from environment, rather than setting to null.

* Special Environments
  - `.GlobalEnv` (`globalenv()`) - the global environment
  - `baseenv()` environment of base, parent is emptyenv
  - `emptyenv()` # ancestor of all. Only environment without a parent.
* Packages have two associated environments,

`ls()` - examine the elements of an environment
`rm()` - to remove something from environment
`ls.str()` - looks at the environment with structure as well

`pryr::where("name")` - What environment is the name found in, with regular scoping rules

`do.call(what, args, envir)` - construct

### Environment things
```r 
version
sessionInfo()
.libPaths()
```

### Error checking

When debugging a detailed series of function calls, can use: 

```r
options(error = recover)
```



## Matrix Related

### Matrix Package

These are the dense matrices
* **`dgeMatrix`** - Real matrices in general storage mode
* `dsyMatrix` - Symmetric real matrices in non-packed storage
* **`dspMatrix`** - Symmetric real matrices in packed storage (one triangle only)
* `dtrMatrix` - Triangular real matrices in non-packed storage
* `dtpMatrix` - Triangular real matrices in packed storage (triangle only)
* `dpoMatrix` - Positive semi-definite symmetric real matrices in non-packed storage
* `dppMatrix` - ditto  in packed storage

sparse matrices
* `dgTMatrix` - general, numeric, sparse matrices in (a possibly redundant) triplet form. This can be a convenient form in which to construct sparse matrices.
* **`dgCMatrix`** - general, numeric, sparse matrices in the (sorted) compressed sparse column format.
* **`dsCMatrix`** - symmetric, real, sparse matrices in the (sorted) compressed sparse column format. Only the upper or the lower triangle is stored. Although there is provision for both forms, the lower triangle form works best with TAUCS.
* `dtCMatrix` - triangular, real, sparse matrices in the (sorted) compressed sparse column format.

```R
as(X, "dgCMatrix")               # Force into sparse Matrix
forceSymmetric(x, uplo = "U")    # take uplo = Upper (U) or Lower (L)
symmpart(x)                      # Average both upper and lower triangle
skewpart(x)                      # The difference between x and symmpart
```


### Matrix Decompositions

```r
qrX <- qr(X) # Gives QR object
qr.Q (qrX)   # Gives the Q part
qr.R(qrX)    # Gives the R part
qrX$rank     # Gives the rank
```

## Analysis

### ANOVA/LM

- [Helpful Twitter thread on ANOVA](https://threadreaderapp.com/thread/1223790298024726528.html)
- [Getting started with emmeans](https://aosmith.rbind.io/2019/03/25/getting-started-with-emmeans/)


### Nonlinear

* `nls` - seems to be the function to do so in R

```r
mod <- nls(..., start = list(a = 0, b =2)) # initialize parameters yourself to avoid fit issues
profile(mod, which = "parameter")
confint(profile(mod)) # seems to be the safer way of doing things.. as to not run into optimization issues
```

### Mixed Models
- `ranef(mod)` - get random effects from model
    - `dotplot.ranef.mer(randef(mod))` - dotplot of random effects, needs lattice
    - `attr(ranef(mod)$Subject, "postVar")` - There's also a "hidden" conditional variance associated with each of the random effects, these are accessed by the attribute "postVar" this is the vcov of each of the random effects I think?
        - `as.data.frame(ranef(mod))` gives a secret representation of conditional variances
- `getMF(mod, ["X", "Z"])` - get the fixed and random effect model matrices

Further Reading
* [Getting subject level standard errors](https://stackoverflow.com/questions/26198958/extracting-coefficients-and-their-standard-error-from-lme)
* [Ben Bolker FAQ](https://bbolker.github.io/mixedmodels-misc/glmmFAQ.html)
* [Estimated zero variance of estimate, Bates Email thread](https://stat.ethz.ch/pipermail/r-sig-mixed-models/2014q3/022509.html)


### GLMs

- `model.matrix(mod)` - gets the design matrix
- `mod$linear.predictors` - X\beta

### 2x2 contingencies

* `table(dat$tx, dat$survival)` - create contingency table
* `addmargins()` - add row and column sums to 2x2 table
* `cut(dat$w6minBl, quantile(dat$w6minBl,0:5/5,na.rm=T), include.lowest = TRUE))` - Create strata

```R
X <- table(dat$tx,dat$survival, dnn = c("TX", "Survival"))
X
d <- factor(c("treat","notreat"), levels=c("treat","notreat"))
modci <- glm(X~d, family=binomial)
summary(modci)
exp(confint(modci)[2,]) # Conf int
```

Residuals 

```R
plot(mod) # Pearson Residuals diagnostics
resid(mod, type="Deviance") # Deviance, Pearson, Working, Response, Partial
mod$residuals # Gives Working residuals
```

### Contrast Coding

* [Overview by UCLA](https://stats.idre.ucla.edu/r/library/r-library-contrast-coding-systems-for-categorical-variables/#DEVIATION)
* [Some more detailed investigation](https://rstudio-pubs-static.s3.amazonaws.com/65059_586f394d8eb84f84b1baaf56ffb6b47f.html)

* Crawley, 2002, is supposed to be a "transparent introduction" to contrast coding, according to `adonis` documentation

## Useful Links

* [R Style Guide](https://style.tidyverse.org/)
* [R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)
* [Collection of R Examples](http://dwoll.de/rexrepos/index.html)
