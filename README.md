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


# Histograms
Histograms are one of the most common and intuitive ways of showing distributions. In this exercise you'll use the mtcars data frame to explore typical variations of simple histograms. But first, some background:

The x axis/aesthetic: The documentation for geom_histogram() states the argument stat = "bin" as a default. Recall that histograms cut up a continuous variable into discrete bins - that's what the stat "bin" is doing. You always get 30 evenly-sized bins by default, which is specified with the default argument binwidth = range/30. This is a pretty good starting point if you don't know anything about the variable being ploted and want to start exploring.

The y axis/aesthetic: geom_histogram() only requires one aesthetic: x. But there is clearly a y axis on your plot, so where does it come from? Actually, there is a variable mapped to the y aesthetic, it's called ..count... When geom_histogram() executed the binning statistic (see above), it not only cut up the data into discrete bins, but it also counted how many values are in each bin. So there is an internal data frame where this information is stored. The .. calls the variable count from this internal data frame. This is what appears on the y aesthetic. But it gets better! The density has also been calculated. This is the proportional frequency of this bin in relation to the whole data set. You use ..density.. to access this information.

Instructions
100 XP
Instructions
100 XP
1 - Use the mtcars data frame and make a univariate histogram by mapping mpg onto the x aesthetic. Use geom_histogram() for the geom layer.
2 - Take plot 1 and manually create 1-unit wide bins with the binwidth = 1 argument in geom_histogram().
3 - Take plot 2, and map ..density.. onto the y aesthetic (i.e. inside an aes()) inside geom_histogram(). You'll have two aes() functions: one inside ggplot() and another inside geom_histogram(). (See the intro text for a discussion of ..density..).
4 - Take plot 3 and set the attribute fill, the inside of the bars, to the value "#377EB8" in geom_histogram(). This should not appear in aes(), since it's an attribute, not an aesthetic mapping.


```
# 1 - Make a univariate histogram
ggplot(mtcars, aes(x = mpg)) +
  geom_histogram()

# 2 - Plot 1, plus set binwidth to 1 in the geom layer
ggplot(mtcars, aes(x = mpg)) +
  geom_histogram(binwidth = 1)


# 3 - Plot 2, plus MAP ..density.. to the y aesthetic (i.e. in a second aes() function)
ggplot(mtcars, aes(x = mpg)) +
  geom_histogram(binwidth = 1, aes(y = ..density..))



# 4 - plot 3, plus SET the fill attribute to "#377EB8"
ggplot(mtcars, aes(x = mpg )) +
  geom_histogram(binwidth = 1, aes(y = ..density..), fill = "#377EB8")



```

Position
In the previous chapter you saw that there are lots of ways to position scatter plots. Likewise, the geom_bar() and geom_histogram() geoms also have a position argument, which you can use to specify how to draw the bars of the plot.

Three position arguments will be introduced here:

stack: place the bars on top of each other. Counts are used. This is the default position.
fill: place the bars on top of each other, but this time use proportions.
dodge: place the bars next to each other. Counts are used.
In this exercise you'll draw the total count of cars having a given number of cylinders (cyl), according to manual or automatic transmission type (am) - as shown in the viewer.

Since, in the built-in mtcars data set, cyl and am are integers, they have already been converted to factor variables for you.

Instructions
100 XP
Instructions
100 XP
1 - Using mtcars, map cyl onto the x aesthetic and am onto fill. Use geom_bar() to make a bar plot.
2 - Take plot 1 and explicitly set position = "stack" in geom_bar(). This doesn't change anything, does it? It was mentioned above that "stack" is the default.
3 - Take plot 2 and set position = "fill" in geom_bar().
4 - Take plot 3 and set position = "dodge" in geom_bar().

```
# Draw a bar plot of cyl, filled according to am
ggplot(mtcars, aes(x =cyl, fill = am)) +
  geom_bar()

# Change the position argument to stack
ggplot(mtcars, aes(x =cyl, fill = am) )+
  geom_bar(position = "stack")


# Change the position argument to fill
ggplot(mtcars, aes(x =cyl, fill = am)) +
  geom_bar(position = "fill")


# Change the position argument to dodge
ggplot(mtcars, aes(x =cyl, fill = am)) +
  geom_bar(position = "dodge")
```

Overlapping bar plots
So far you've seen three different positions for bar plots: stack (the default), dodge (preferred), and fill (to show proportions).

However, you can go one step further by adjusting the dodging, so that your bars partially overlap each other. For this example you'll again use the mtcars dataset. Like last time cyl and am are already available as factors inside mtcars.

Instead of using position = "dodge" you're going to use position_dodge(), like you did with position_jitter() in the Scatter plots and jittering (1) exercise. Here, you'll save this as an object, posn_d, so that you can easily reuse it.

Remember, the reason you want to use position_dodge() (and position_jitter()) is to specify how much dodging (or jittering) you want.

Instructions
100 XP
Instructions
100 XP
1 - The last plot from the last exercise has been provided for you.
2 - Define a new object called posn_d by calling position_dodge() with the argument width = 0.2.
3 - Take plot 1 and make slightly overlapping bars by using the position = posn_d argument.
4 - Take plot 3 and set alpha = 0.6 to see the overlap in bars.




```
# 1 - The last plot form the previous exercise
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position = "dodge")

# 2 - Define posn_d with position_dodge()
posn_d <- position_dodge(width = 0.2)

# 3 - Change the position argument to posn_d
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position = posn_d)


# 4 - Use posn_d as position and adjust alpha to 0.6
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position = posn_d,alpha = 0.6)


```

Overlapping histograms
Overlapping histograms pose similar problems to overlapping bar plots, but there is a unique solution here: a frequency polygon.

This is a geom specific to binned data that draws a line connecting the value of each bin. Like geom_histogram(), it takes a binwidth argument and by default stat = "bin" and position = "identity".

Instructions
100 XP
Instructions
100 XP
The code for a basic histogram of mpg, which you've already seen, is provided. Extend the code to map cyl onto fill inside aes().
The default position for histograms is "stack". Copy your solution to the first exercise and set the position for the histogram bars to "identity".
Using the same data and base layers as in the previous two plots, create a plot with a geom_freqpoly(). Because you're no longer working with bars, change the aes() function: cyl should be mapped onto color, not onto fill. This will correctly color the geom.

```
# A basic histogram, add coloring defined by cyl
ggplot(mtcars, aes(mpg, fill = cyl)) +
  geom_histogram(binwidth = 1)

# Change position to identity
ggplot(mtcars, aes(mpg,  fill = cyl)) +
  geom_histogram(binwidth = 1,position = "identity")



# Change geom to freqpoly (position is identity by default)
ggplot(mtcars, aes(mpg,  col = cyl)) +
  geom_freqpoly(binwidth =1)



```

Bar plots with color ramp, part 1
In this example of a bar plot, you'll fill each segment according to an ordinal variable. The best way to do that is with a sequential color series.

You'll be using the Vocab dataset from earlier. Since this is a much larger dataset with more categories, you'll also compare it to a simpler dataset, mtcars. Both datasets are ordinal.

Instructions
100 XP
Instructions
100 XP
The bar plot from the previous exercise is provided - cyl is on the x-axis and filled according to transmission type, am. Notice how you can set the color palette used to fill the bars with scale_fill_brewer(). For a full list of possible color sets, have a look at ?brewer.pal.
Explore Vocab with str(). Notice that the education and vocabulary variables have already been converted to factor variables for you.
Make a filled bar chart with the Vocab dataset.
Map education to x and vocabulary to fill.
Inside geom_bar(), make sure to set position = "fill".
Allow color brewer to choose a default color palette by using the appropriate scale function, without arguments. Notice how this generates a warning message and an incomplete plot.

```

# Example of how to use a brewed color palette
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar() +
  scale_fill_brewer(palette = "Set1")

# Use str() on Vocab to check out the structure

str(Vocab)
# Plot education on x and vocabulary on fill
# Use the default brewed color palette

ggplot(Vocab, aes(x = education, fill = vocabulary)) +
  geom_bar(position = "fill") +
  scale_fill_brewer(palette = "Set1")


```

Bar plots with color ramp, part 2
In the previous exercise, you ended up with an incomplete bar plot. This was because for continuous data, the default RColorBrewer palette that scale_fill_brewer() calls is "Blues". There are only 9 colours in the palette, and since you have 11 categories, your plot looked strange.

In this exercise, you'll manually create a color palette that can generate all the colours you need. To do this you'll use a function called colorRampPalette().

The input is a character vector of 2 or more colour values, e.g. "#FFFFFF" (white) and "#0000FF" (pure blue). (See this exercise for a discussion on hexadecimal codes).

The output is itself a function! So when you assign it to an object, that object should be used as a function. To see what we mean, execute the following three lines in the console:

new_col <- colorRampPalette(c("#FFFFFF", "#0000FF"))
new_col(4) # the newly extrapolated colours
munsell::plot_hex(new_col(4)) # Quick and dirty plot
new_col() is a function that takes one argument: the number of colours you want to extrapolate. You want to use nicer colours, so we've assigned the entire "Blues" colour palette from the RColorBrewer package to the character vector blues.

Instructions
100 XP
Instructions
100 XP
1 - Like in the example code above, create a new function called blue_range that uses colorRampPalette() to extrapolate over all 9 values of the blues character vector.
2 - Take the plot code from the last exercise (provided), and change scale_fill_brewer() to be scale_fill_manual(). Set the argument values = blue_range(11) inside scale_fill_manual().


```

# Final plot of last exercise
ggplot(Vocab, aes(x = education, fill = vocabulary)) +
  geom_bar(position = "fill") +
  scale_fill_brewer()

# Definition of a set of blue colors
blues <- brewer.pal(9, "Blues") # from the RColorBrewer package

# 1 - Make a color range using colorRampPalette() and the set of blues
blue_range <- colorRampPalette(blues)

# 2 - Use blue_range to adjust the color of the bars, use scale_fill_manual()
ggplot(Vocab, aes(x = education, fill = vocabulary)) +
  geom_bar(position = "fill") +
  scale_fill_manual(values = blue_range(11))


```

Overlapping histograms (2)
As a last example of bar plots, you'll return to histograms (which you now see are just a special type of bar plot). You saw a nice trick in a previous exercise of how to slightly overlap bars, but now you'll see how to overlap them completely. This would be nice for multiple histograms, as long as there are not too many different overlaps!

You'll make a histogram using the mpg variable in the mtcars data frame.

Instructions
100 XP
Instructions
100 XP
1 - A basic histogram plot is provided.
2 - Take plot 1 and map am onto fill within the aes() function. The default position is "stack".
3 - Take plot 2 and add the position argument within geom_histogram(). Set it to "dodge".
4 - Take plot 3 and change the position argument to "fill". In this case, none of these positions really work well, because it's difficult to compare the distributions directly.
5 - Take plot 4 and change the position argument to "identity" and set alpha = 0.4. This produces overlapping bars.
6 - Take plot 5 and change the aesthetic mapping. Map cyl onto fill.


```
# 1 - Basic histogram plot command
ggplot(mtcars, aes(mpg)) +
  geom_histogram(binwidth = 1)

# 2 - Plot 1, Expand aesthetics: am onto fill

ggplot(mtcars, aes(mpg, fill = am)) +
  geom_histogram(binwidth = 1)

# 3 - Plot 2, change position = "dodge"
ggplot(mtcars, aes(mpg, fill = am)) +
  geom_histogram(binwidth = 1, position = "dodge")


# 4 - Plot 3, change position = "fill"
ggplot(mtcars, aes(mpg, fill = am)) +
  geom_histogram(binwidth = 1, position = "fill")


# 5 - Plot 4, plus change position = "identity" and alpha = 0.4
ggplot(mtcars, aes(mpg, fill = am)) +
  geom_histogram(binwidth = 1, position = "identity", alpha = 0.4)

# 6 - Plot 5, plus change mapping: cyl onto fill
ggplot(mtcars, aes(mpg, fill = cyl)) +
  geom_histogram(binwidth = 1, position = "identity", alpha = 0.4)

```

Line plots
In the video you saw how to make line plots using time series data. To explore this topic, you'll use the economics data frame, which contains time series for unemployment and population statistics from the Federal Reserve Bank of St. Louis in the US. The data is contained in the ggplot2 package.

To begin with, you can look at how the median unemployment time and the unemployment rate (the number of unemployed people as a proportion of the population) change over time.

In the next exercises, you'll explore to how add embellishments to the line plots, such as recession periods.

Instructions
100 XP
Instructions
100 XP
Print out the head() of the economics data frame.
Use the economics data frame to plot date on the x axis and unemploy on the y-axis. Use geom_line().
Copy, paste and adjust the code for the previous instruction: instead of unemploy, plot unemploy/pop to represent the fraction of the total population that is unemployed.


```
# Print out head of economics
head(economics)

# Plot unemploy as a function of date using a line plot
ggplot(economics, aes(x = date, y = unemploy)) +
geom_line()


# Adjust plot to represent the fraction of total population that is unemployed
ggplot(economics, aes(x = date, y = unemploy/pop)) +
geom_line()

```
Periods of recession
By themselves, time series often contain enough valuable information, but you always want to maximize the number of variables you can show in a plot. This allows you (and your viewers) to begin making comparisons between those variables that would otherwise be difficult or impossible.

Here, you'll add shaded regions to the background to indicate recession periods. How do unemployment rate and recession period interact with each other?

In addition to the economics dataset from before, you'll also use the recess dataset for the periods of recession. The recess data frame contains 2 variables: the begin period of the recession and the end. It's already available in your workspace.

Instructions
100 XP
Instructions
100 XP
Expand the command from the previous exercise with geom_rect(). You will use this geom layer to draw rectangles across the recession periods. There are a few pitfalls here:

geom_rect() uses the recess dataset, so pass this directly as data = recess inside geom_rect().
The geom_rect() command shouldn't inherit aesthetics from the base ggplot() command it belongs to. It would result in an error, since you're using a different dataset and it doesn't contain unemploy or pop. That's why you should specify inherit.aes = FALSE in geom_rect().
geom_rect() needs four aesthetics: xmin, xmax, ymin and ymax. These should be set to begin, end and -Inf, +Inf, respectively. Define them within aes().
The rectangles you add will be black and opaque by default. Set fill to "red" and alpha to 0.2 to improve this. Define them outside aes().


```
# Basic line plot
ggplot(economics, aes(x = date, y = unemploy/pop)) +
  geom_line()

# Expand the following command with geom_rect() to draw the recess periods
ggplot(economics, aes(x = date, y = unemploy/pop)) +
  geom_rect(data = recess,
         aes(xmin = begin, xmax = end, ymin = -Inf, ymax = +Inf),
         inherit.aes = FALSE, fill = "red", alpha = 0.2) +
  geom_line()
```

Multiple time series, part 1
In the data chapter we discussed how the form of your data affects how you can plot it. Here, you'll explore that topic in the context of multiple time series.

The dataset you'll use contains the global capture rates of seven salmon species from 1950 - 2010.

In your workspace, the following dataset is available:

fish.species: Each variable (column) is a Salmon Species and each observation (row) is one Year.
To get a multiple time series plot, however, both Year and Species should be in their own column. You need tidy data: one variable per column. Once you have that you can get the plot shown in the viewer by mapping Year to the x aesthetic and Species to the color aesthetic.

You'll use the gather() function of the tidyr package, which is already loaded for you.

Instructions
100 XP
Instructions
100 XP
Use gather() to move from fish.species to a tidy data frame, fish.tidy. This data frame should have three columns: Year (int), Species (factor) and Capture (int).
gather() takes four arguments: the original data frame (fish.species), the name of the key column (Species), the name of the value column (Capture) and the name of the grouping variable, with a minus in front (-Year). They can all be specified as object names (i.e. no "").


```
# Check the structure as a starting point
str(fish.species)

# Use gather to go from fish.species to fish.tidy
fish.tidy <- gather(fish.species, Species, Capture, -Year)
```


Using qplot
For simple exploratory plots, there are a variety of functions available. ggplot2 offers a powerful and diverse array of functions, but qplot() allows for quick and dirty plots. Plus, you should also be familiar with basic plotting notation.

Instructions
100 XP
Have a look at the base R plotting function. It plots mpg on the y-axis against wt on the x-axis. Create the same plot using ggplot().
Create the same plot using qplot().

```
# The old way (shown)
plot(mpg ~ wt, data = mtcars) # formula notation
with(mtcars, plot(wt, mpg)) # x, y notation

# Using ggplot:
ggplot(mtcars, aes(wt, mpg)) +
  geom_point()

# Using qplot:
qplot(wt, mpg, data =mtcars)
```

Choosing geoms, part 1
qplot automatically takes care of assigning a geom to our plot given the type of data, but you can specify the geom yourselves.

Instructions
100 XP
Instructions
100 XP
Make a quick plot using qplot(). Use the mtcars dataset and plot only factor(cyl) onto x. Which geom does qplot() choose?
Extend the previous qplot() command so that it maps factor(vs) onto y. Which geom does qplot() use now?
The previous plot had overlapping points. For the last instruction, copy the previous qplot(), but manually set geom to "jitter" in qplot().

```
# qplot() with x only
qplot(factor(cyl), data = mtcars)

# qplot() with x and y
qplot(factor(cyl),factor(vs), data = mtcars)

# qplot() with geom set to jitter manually
qplot(factor(cyl),factor(vs), data = mtcars, geom = "jitter")



```


Choosing geoms, part 2 - dotplot
Some naming conventions:

Scatter plots:
Continuous x, continuous y.
Dot plots:
Categorical x, continuous y.
You use geom_point() for both plot types. Jittering position is set in the geom_point() layer.

However, to make a "true" dot plot, you can use geom_dotplot(). The difference is that unlike geom_point(), geom_dotplot() uses a binning statistic. Binning means to cut up a continuous variable (the y in this case) into discrete "bins". You already saw binning with geom_histogram() (see this exercise for a refresher).

One thing to notice is that geom_dotplot() uses a different plotting symbol to geom_point(). For these symbols, the color aesthetic changes the color of its border, and the fill aesthetic changes the color of its interior.

Let's take a look at how the two geoms compare.

Instructions
100 XP
Instructions
100 XP
A "basic" dot plot is shown in the viewer (see the code in the editor). Here, cyl (categorical) is mapped onto the x and wt (continuous) is mapped onto the y aesthetic. For this exercise we've already converted am to a factor variable for you.

1 - Re-draw that plot in the viewer as a "true" dot plot.
Add a dotplot geom by calling geom_dotplot().
Set the arguments stackdir = "center" and binaxis = "y". These are our standard settings, but take a look at the help pages and try different settings to get familiar with these arguments.
2 - Convert the previous ggplot() command to a qplot() command.

```
# cyl and am are factors, wt is numeric
class(mtcars$cyl)
class(mtcars$am)
class(mtcars$wt)

# "Basic" dot plot, with geom_point():
ggplot(mtcars, aes(cyl, wt, col = am)) +
  geom_point(position = position_jitter(0.2, 0))

# 1 - "True" dot plot, with geom_dotplot():
ggplot(mtcars, aes(cyl, wt, fill = am)) +
  geom_dotplot(binaxis = "y", stackdir = "center")

# 2 - qplot with geom "dotplot", binaxis = "y" and stackdir = "center"
qplot(
  cyl, wt,
  data = mtcars,
  fill = am,
  geom = "dotplot",
  binaxis = "y",
  stackdir = "center"
)

```



Titanic
You've watched the movie Titanic by James Cameron (1997) again and after a good portion of sobbing you decide to investigate whether you'd have a chance of surviving this disaster.

To start your investigation, you decide to do some exploratory visualization with ggplot(). You have information on who survived the sinking given their age, sex and passenger class.

Instructions
100 XP
Instructions
100 XP
1 - Have a look at the str() of the titanic dataset, which has been loaded into your workspace. Looks like the data is pretty tidy!
2 - Plot the distribution of sexes within the classes of the ship.
Use ggplot() with the data layer set to titanic.
Map Pclass onto the x axis, Sex onto fill and draw a dodged bar plot using geom_bar(), i.e. set the geom position to "dodge".
3 - These bar plots won't help you estimate your chances of survival. Copy the previous bar plot, but this time add a facet_grid() layer: . ~ Survived.
4 - We've defined a position object for you.
5 - Include Age, the final variable.
Take plot 3 and add a mapping of Age onto the y aesthetic.
Change geom_bar() to geom_point() and set its attributes size = 3, alpha = 0.5 and position = posn.jd.
Make sure that Sex is mapped onto color instead of fill to correctly color the scatter plots. (This was discussed in detail here and here).


```


# titanic is avaliable in your workspace
# 1 - Check the structure of titanic
str(titanic)

# 2 - Use ggplot() for the first instruction
ggplot(titanic, aes(x = Pclass, fill = Sex)) +
  geom_bar(position = "dodge")

# 3 - Plot 2, add facet_grid() layer
ggplot(titanic, aes(x = Pclass, fill = Sex)) +
  geom_bar(position = "dodge") +
  facet_grid(. ~ Survived)


# 4 - Define an object for position jitterdodge, to use below
posn.jd <- position_jitterdodge(0.5, 0, 0.6)

# 5 - Plot 3, but use the position object from instruction 4
ggplot(titanic, aes(x = Pclass, y = Age, col = Sex)) +
  geom_point(size =3, alpha = 0.5, position = posn.jd) +
  facet_grid(. ~ Survived)



```







