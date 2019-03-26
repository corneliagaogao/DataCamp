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

Add a geom_bar() call to cyl.am. By default, the position will be set to "stack".
Fill in the second ggplot command. Explicitly set position to "fill" inside geom_bar().
Fill in the third ggplot command. Set position to "dodge".
The position = "dodge" version seems most appropriate. Finish off the fourth ggplot command by completing the three scale_ functions:
scale_x_discrete() takes as its only argument the x-axis label: "Cylinders".
scale_y_continuous() takes as its only argument the y-axis label: "Number".
scale_fill_manual() fixes the legend. The first argument is the title of the legend: "Transmission". Next, values and labels are set to predefined values for you. These are the colors and the labels in the legend.

```
# The base layer, cyl.am, is available for you
# Add geom (position = "stack" by default)
cyl.am + 
geom_bar()

# Fill - show proportion
cyl.am + 
  geom_bar(position = "fill")  

# Dodging - principles of similarity and proximity
cyl.am +
  geom_bar(position = "dodge") 

# Clean up the axes with scale_ functions
val = c("#E41A1C", "#377EB8")
lab = c("Manual", "Automatic")
cyl.am +
  geom_bar(position = "dodge") +
  scale_x_discrete("Cylinders") + 
  scale_y_continuous("Number") +
  scale_fill_manual("Transmission", 
                    values = val,
                    labels = lab) 
                    
```

Try to run ggplot(mtcars, aes(x = mpg)) + geom_point() in the console. x is only one of the two essential aesthetics for geom_point(), which is why you get an error message.
1 - To fix this, map a value, e.g. 0, instead of a variable, onto y. Use geom_jitter() to avoid having all the points on a horizontal line.
2 - To make everything look nicer, copy & paste the code for plot 1 and change the limits of the y axis using the appropriate scale_y_...() function. Set the limits argument to c(-2, 2).


```
# 1 - Create jittered plot of mtcars, mpg onto x, 0 onto y
ggplot(mtcars, aes(x = mpg, y =0)) +
  geom_jitter()

# 2 - Add function to change y axis limits
ggplot(mtcars, aes(x = mpg, y =0)) +
  geom_jitter() +
  scale_y_continuous(limits = c(-2,2))

```


Overplotting 1 - Point shape and transparency
In the previous section you saw that there are lots of ways to use aesthetics. Perhaps too many, because although they are possible, they are not all recommended. Let's take a look at what works and what doesn't.

So far you've focused on scatter plots since they are intuitive, easily understood and very common. A major consideration in any scatter plot is dealing with overplotting. You'll encounter this topic again in the geometries layer, but you can already make some adjustments here.

You'll have to deal with overplotting when you have:

Large datasets,
Imprecise data and so points are not clearly separated on your plot (you saw this in the video with the iris dataset),
Interval data (i.e. data appears at fixed values), or
Aligned data values on a single axis.
One very common technique that I'd recommend to always use when you have solid shapes it to use alpha blending (i.e. adding transparency). An alternative is to use hollow shapes. These are adjustments to make before even worrying about positioning. This addresses the first point as above, which you'll see again in the next exercise.

Instructions
100 XP
Instructions
100 XP
Begin by making a basic scatter plot of mpg (y) vs. wt (x), map cyl to color and make the size = 4. cyl has already been converted to a factor variable for you.
Modify the above plot to set shape to 1. This allows for hollow circles.
Modify the first plot to set alpha to 0.6.


```
# Basic scatter plot: wt on x-axis and mpg on y-axis; map cyl to col
ggplot(mtcars, aes(x= wt, y = mpg, col =cyl))+
geom_point(size = 4)


# Hollow circles - an improvement
ggplot(mtcars, aes(x= wt, y = mpg, col =cyl))+
geom_point(size = 4, shape = 1)


# Add transparency - very nice
ggplot(mtcars, aes(x= wt, y = mpg, col =cyl, alpha = 0.6))+
geom_point(size = 4, shape = 1, alpha = 0.6)

```


Overplotting 2 - alpha with large datasets
In a previous exercise we defined four situations in which you'd have to adjust for overplotting. You'll consider the last two here with the diamonds dataset:

Large datasets.
Aligned data values on a single axis
Instructions
100 XP
Instructions
100 XP
The diamonds data frame is available in the ggplot2 package. Begin by making a basic scatter plot of price (y) vs. carat (x) and map clarity onto color.
Copy the above functions and set the alpha to 0.5. This is a good start to dealing with the large dataset.
Align all the diamonds within a clarity class, by plotting carat (y) vs. clarity (x). Map price onto color. alpha should still be 0.5.
In the previous plot, all the individual values line up on a single axis within each clarity category, so you have not overcome overplotting. Modify the above plot to use the position = "jitter" inside geom_point().


```
# Scatter plot: carat (x), price (y), clarity (color)
ggplot(diamonds, aes(carat, price, col = clarity)) +
geom_point()


# Adjust for overplotting
ggplot(diamonds, aes(carat, price, col = clarity)) +
geom_point(alpha = 0.5)


# Scatter plot: clarity (x), carat (y), price (color)
ggplot(diamonds, aes(clarity, carat, col = price)) +
geom_point(alpha = 0.5)


# Dot plot with jittering
ggplot(diamonds, aes(clarity, carat, col = price)) +
geom_point(alpha = 0.5, position = "jitter")


```

Scatter plots and jittering (1)
You already saw a few examples using geom_point() where the result was not a scatter plot. For example, in the plot shown in the viewer a continuous variable, wt, is mapped to the y aesthetic, and a categorical variable, cyl, is mapped to the x aesthetic. This also leads to over-plotting, since the points are arranged on a single x position. You previously dealt with overplotting by setting the position = jitter inside geom_point(). Let's look at some other solutions here.

Instructions
100 XP
Instructions
100 XP
Beginning with the code for the plot in the viewer (given), make these modifications

1 - Use a shortcut geom, geom_jitter(), instead of geom_point().
2 - Unfortunately, the width of the jitter is a bit too wide to be useful. Adjust this by setting the argument width = 0.1 inside geom_jitter().
3 - Finally, return to geom_point() and set the position argument here to position_jitter(0.1), which will set the jittering width directly inside a points layer.
Note: For convenience, you could have saved the data and aesthetic layers as a ggplot2 object and re-used it in all solutions. We've made each plot explicit so that you can see all plotting instructions.



```


# Shown in the viewer:
ggplot(mtcars, aes(x = cyl, y = wt)) +
  geom_point()

# Solutions:
# 1 - With geom_jitter()
ggplot(mtcars, aes(x = cyl, y = wt)) +
  geom_jitter()

# 2 - Set width in geom_jitter()
ggplot(mtcars, aes(x = cyl, y = wt)) +
  geom_jitter(width = 0.1)

# 3 - Set position = position_jitter() in geom_point() ()
ggplot(mtcars, aes(x = cyl, y = wt)) +
  geom_point(position = position_jitter(0.1))
```


Scatter plots and jittering (2)
In the chapter on aesthetics you saw different ways in which you will have to compensate for overplotting. In the video you saw a dataset that suffered from overplotting because of the precision of the dataset.

Another example you saw is when you have integer data. This can be continuous data measured on an integer (i.e. 1 ,2, 3 ...), as opposed to numeric (i.e. 1.1, 1.4, 1.5, ...), scale, or two categorical (e.g. factor) variables, which are just type integer under-the-hood.

In such a case you'll have a small, defined number of intersections between the two variables.

You will be using the Vocab dataset. The Vocab dataset contains information about the years of education and integer score on a vocabulary test for over 21,000 individuals based on US General Social Surveys from 1972-2004.

Instructions
100 XP
Instructions
100 XP
The Vocab data frame has been loaded for you. Both the education and vocabulary variables are classified as integers. You can imagine these as factor variables, but here, integers are more convenient to work with. First, get familiar with the dataset by looking at its structure with str().
Make a basic scatter plot of vocabulary (y) vs. education (x). Here it becomes apparent that you have issues with overplotting because of the integer scales.
Use geom_jitter() instead of geom_point().
Using the jittered plot, set alpha to 0.2 (very low).
Using the jittered plot, set shape to 1.

```

# Examine the structure of Vocab
str(Vocab)

# Basic scatter plot of vocabulary (y) against education (x). Use geom_point()
ggplot(Vocab, aes(education, vocabulary) )+
geom_point()


# Use geom_jitter() instead of geom_point()
ggplot(Vocab, aes(education, vocabulary) )+
geom_jitter()


# Using the above plotting command, set alpha to a very low 0.2
ggplot(Vocab, aes(education, vocabulary) )+
geom_jitter(alpha = 0.2)


# Using the above plotting command, set the shape to 1
ggplot(Vocab, aes(education, vocabulary) )+
geom_jitter(alpha = 0.2, shape = 1)
```












