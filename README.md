# Data Visualization

###  Understanding the grammar, part 2


```
# 1 - The dia_plot object has been created for you
dia_plot <- ggplot(diamonds, aes(x = carat, y = price))

# 2 - Expand dia_plot by adding geom_point() with alpha set to 0.2
dia_plot <- dia_plot + geom_point(alpha = 0.2)

# 3 - Plot dia_plot with additional geom_smooth() with se set to FALSE
dia_plot + geom_smooth(se = FALSE)

# 4 - Copy the command from above and add aes() with the correct mapping to geom_smooth()
dia_plot + geom_smooth(aes(color =clarity), se = FALSE)

```

### base package and ggplot2, part 3

Plot 1: add geom_point() in order to make a scatter plot.

Plot 2: copy and paste Plot 1.

Add a linear model for each subset according to cyl by adding a geom_smooth() layer.

Inside this geom_smooth(), set method to "lm" and se to FALSE.

Note: geom_smooth() will automatically draw a line per cyl subset. It recognizes the groups you want to identify by color in the aes() call within the ggplot() command.

Plot 3: copy and paste Plot 2.

Plot a linear model for the entire dataset, do this by adding another geom_smooth() layer.

Set the group aesthetic inside this geom_smooth() layer to 1. This has to be set within the aes() function.

Set method to "lm", se to FALSE and linetype to 2. These have to be set outside aes() of the geom_smooth().

Note: the group aesthetic will tell ggplot() to draw a single linear model through all the points.


```
# Convert cyl to factor (don't need to change)
mtcars$cyl <- as.factor(mtcars$cyl)

# Example from base R (don't need to change)
plot(mtcars$wt, mtcars$mpg, col = mtcars$cyl)
abline(lm(mpg ~ wt, data = mtcars), lty = 2)
lapply(mtcars$cyl, function(x) {
  abline(lm(mpg ~ wt, mtcars, subset = (cyl == x)), col = x)
  })
legend(x = 5, y = 33, legend = levels(mtcars$cyl),
       col = 1:3, pch = 1, bty = "n")

# Plot 1: add geom_point() to this command to create a scatter plot
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
geom_point()  # Fill in using instructions Plot 1

# Plot 2: include the lines of the linear models, per cyl
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
geom_point() + # Copy from Plot 1
geom_smooth(method = "lm", se = FALSE)   # Fill in using instructions Plot 2

# Plot 3: include a lm for the entire dataset in its whole
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
geom_point() + # Copy from Plot 1
geom_smooth(method = "lm", se = FALSE) +  # Fill in using 
geom_smooth(aes(group= 1), method = "lm", se = FALSE, linetype =2) # Fill in using instructions Plot 3

```


### Variables to visuals, part 1b

You'll use two functions from the tidyr package:

gather() rearranges the data frame by specifying the columns that are categorical variables with a - notation. Complete the command. Notice that only one variable is categorical in iris.
separate() splits up the new key column, which contains the former headers, according to .. The new column names "Part" and "Measure" are given in a character vector. Don't forget the quotes.
```
# Load the tidyr package
library(tidyr)

# Fill in the ___ to produce to the correct iris.tidy dataset
iris.tidy <- iris %>%
  gather(key, Value, -Species) %>%
  separate(key, c("Part", "Measure"), "\\.")
```



### Variables to visuals, part 2
Look at the heads of iris, iris.wide and iris.tidy using head().
Fill in the ggplot function with the appropriate data frame and variable names. The names of the aesthetics of the plot will match with variable names in your dataset. The previous instruction will help you match variable names in datasets with the ones in the plot.


```
# The 3 data frames (iris, iris.wide and iris.tidy) are available in your environment
# Execute head() on iris, iris.wide and iris.tidy (in that order)
head(iris)
head(iris.wide)
head(iris.tidy)



# Think about which dataset you would use to get the plot shown right
# Fill in the ___ to produce the plot given to the right
ggplot(iris.wide, aes(x = Length, y = Width, color = Part)) +
  geom_jitter() +
  facet_grid(. ~ Species)

```
  
Before you begin, you need to add a new column called Flower that contains a unique identifier for each row in the data frame. This is because you'll rearrange the data frame afterwards and you need to keep track of which row, or which specific flower, each value came from. It's done for you, no need to add anything yourself.
gather() rearranges the data frame by specifying the columns that are categorical variables with a - notation. In this case, Species and Flower are categorical. Complete the command.
separate() splits up the new key column, which contains the former headers, according to .. The new column names "Part" and "Measure" are given in a character vector.
The last step is to use spread() to distribute the new Measure column and associated value column into two columns.


```
# Load the tidyr package
library(tidyr)

# Add column with unique ids (don't need to change)
iris$Flower <- 1:nrow(iris)

# Fill in the ___ to produce to the correct iris.wide dataset
iris.wide <- iris %>%
  gather(key, value, -Species, -Flower) %>%
  separate(key, c("Part", "Measure"), "\\.") %>%
  spread(Measure, value)

```
  
  
  
### All about aesthetics, part 1


The mtcars data frame is available in your workspace. For each of the following four plots, use geom_point():

1 - Map mpg onto the x aesthetic, and cyl onto the y.
2 - Reverse the mappings of the first plot.
3 - Map wt onto x, mpg onto y, and cyl onto color.
Modify the previous plot by changing the shape argument of the geom to 1 and increase the size to 4. These are attributes that you should specify inside geom_point().


```
# 1 - Map mpg to x and cyl to y
ggplot(mtcars, aes(mpg, cyl)) +
  geom_point()
  
# 2 - Reverse: Map cyl to x and mpg to y
ggplot(mtcars, aes(cyl, mpg)) +
  geom_point()

# 3 - Map wt to x, mpg to y and cyl to col
ggplot(mtcars, aes(wt, mpg, col = cyl)) +
  geom_point()

# 4 - Change shape and size of the points in the above plot
ggplot(mtcars, aes(wt, mpg, col = cyl)) +
  geom_point(shape = 1, size = 4)



```


Note: In the mtcars dataset, cyl and am have been converted to factor for you.

1 - Copy & paste the first plot's code. Change the aesthetics so that cyl maps to fill rather than col.
2 - Copy & paste the second plot's code. In geom_point() change the shape argument to 21 and add an alpha argument set to 0.6.
3 - Copy & paste the third plot's code. In the ggplot() aesthetics, map am to col.



```
# am and cyl are factors, wt is numeric
class(mtcars$am)
class(mtcars$cyl)
class(mtcars$wt)

# From the previous exercise
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
  geom_point(shape = 1, size = 4)

# 1 - Map cyl to fill
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl)) +
  geom_point(shape = 1, size = 4)



# 2 - Change shape and alpha of the points in the above plot
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl)) +
  geom_point(shape = 21, size = 4, alpha = 0.6)


# 3 - Map am to col in the above plot
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl, col = am)) +
  geom_point(shape = 21, size = 4, alpha = 0.6)


```


Use ggplot() to create a basic scatter plot. Inside aes(), map wt onto x and mpg onto y. Typically, you would say "mpg described by wt" or "mpg vs wt", but in aes(), it's x first, y second. Use geom_point() to make three scatter plots:

cyl on size
cyl on alpha
cyl on shape
Try this last variant:

cyl on label. In order to correctly show the text (i.e. label), use geom_text().


```
# Map cyl to size
ggplot(mtcars, aes(wt, mpg, size = cyl)) +
 geom_point()


# Map cyl to alpha
ggplot(mtcars, aes(wt, mpg, alpha = cyl)) +
geom_point()



# Map cyl to shape 
ggplot(mtcars, aes(wt, mpg, shape = cyl)) +
geom_point()



# Map cyl to label
ggplot(mtcars, aes(wt, mpg, label = cyl)) +
geom_text()
```

1 - You will continue to work with mtcars. Use ggplot() to create a basic scatter plot: map wt onto x, mpg onto y and cyl onto color.
2 - Overwrite the color of the points inside geom_point() to my_color. Notice how this cancels out the colors given to the points by the number of cylinders!
3 - Starting with plot 2, map cyl to fill instead of col and set the attributes size to 10, shape to 23 and color to my_color inside geom_point().

```
# Define a hexadecimal color
my_color <- "#4ABEFF"

# Draw a scatter plot with color *aesthetic*

ggplot(mtcars, aes(wt, mpg, col = cyl)) +
geom_point()
# Same, but set color *attribute* in geom layer 
ggplot(mtcars, aes(wt, mpg, col = cyl)) +
geom_point(col = my_color)



# Set the fill aesthetic; color, size and shape attributes
ggplot(mtcars, aes(wt, mpg, fill = cyl)) +
geom_point(col = my_color, size = 10, shape = 23)

```


Add to the first command: draw points with alpha set to 0.5.
Add to the second command: draw points of shape 24 in the color yellow.
Add to the third command: draw text with label rownames(mtcars) in the color red. Don't use geom_point() here! You should get a scatter plot with the names of the cars instead of points.
Note: Remember to specify characters with quotation marks ("yellow", not yellow).


```
# Expand to draw points with alpha 0.5
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl)) +
geom_point(alpha = 0.5)
  
# Expand to draw points with shape 24 and color yellow
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl)) +
geom_point(shape = 24, col = "yellow")

  
# Expand to draw text with label rownames(mtcars) and color red
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl, label = rownames(mtcars))) +
geom_text( col = "red")
```

Variables in a data frame are mapped to aesthetics in aes(). (e.g. aes(col = cyl)) within ggplot(). Visual elements are set by attributes in specific geom layers (geom_point(col = "red")). Don't confuse these two things - here you're focusing on aesthetic mappings.

Draw a scatter plot of mtcars with mpg on the x-axis, qsec on the y-axis and factor(cyl) as colors.
Copy the previous plot and expand to include factor(am) as the shape of the points.
Copy the previous plot and expand to include the ratio of horsepower to weight (i.e. (hp/wt)) as the size of the points.

```

# Map mpg onto x, qsec onto y and factor(cyl) onto col
ggplot(mtcars, aes(mpg, qsec, col = factor(cyl))) +
geom_point()


# Add mapping: factor(am) onto shape
ggplot(mtcars, aes(mpg, qsec, col = factor(cyl), shape = factor(am))) +
geom_point()


# Add mapping: (hp/wt) onto size
ggplot(mtcars, aes(mpg, qsec, col = factor(cyl), shape = factor(am), size =(hp/wt))) +
geom_point(  )


```











