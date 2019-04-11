Converting a ggplot2 scatterplot
The ggplotly() command makes it easy to create interactive versions of most static plots created using the ggplot2 package. In this exercise, your task is to create an interactive version of the below scatterplot, exploring the relationship between video game sales in North America (NA_sales) and aggregate critic score (Critic_Score) in 2016.

After creating the interactive graphic, be sure to explore what interactions are possible.

Note: loading plotly also loads ggplot2 and dplyr.

Instructions
100 XP
Instructions
100 XP
Load plotly.
Create a scatterplot with NA_Sales on the x-axis and Critic_Score on the y-axis for video games found in the vgsales dataset from 2016. Store this plot in the scatter object.
Use the ggplotly() command to convert scatter to a plotly interactive graphic.

```
library(plotly)

# Store the scatterplot of Critic_Score vs. NA_Sales sales in 2016
scatter <-vgsales %>%
			filter(Year == 2016) %>%
			ggplot(aes(x = NA_Sales, y = Critic_Score)) +
			geom_point(alpha = 0.3)

# Convert the scatterplot to a plotly graphic
ggplotly(scatter)
```


Histograms
In this exercise, you'll use plotly to create a histogram from scratch in order to explore the distribution of the critic scores of video games sold between 1980 and 2016. The data are contained in the Critic_Score variable in the vgsales data frame.

As you complete this exercise, think about how the bins influence what you see in the distribution of critic scores.

Note that plotly has already been loaded for you.


Create a histogram of the critic score (Critic_Score) using the default number of bins.




```

# Create a histogram of Critic_Score
vgsales %>%
	plot_ly(x = ~Critic_Score) %>%
	add_histogram()
  
  # Create a histogram of Critic_Score with at most 25 bins
vgsales %>%
	plot_ly(x = ~Critic_Score)  %>%
	add_histogram(nbinsx = 25)
 # Create a histogram with bins of width 10 between 0 and 100


# Create a histogram with bins of width 10 between 0 and 100
vgsales %>%
plot_ly(x = ~Critic_Score)  %>%
	add_histogram(xbins = list(start = 0, end = 100, size = 10))
 
  # Create a frequency for Genre
genre_table <- vgsales %>%
	count(Genre)

# Create a bar chart of Genre
genre_table %>%
	plot_ly(x = ~Genre, y = ~n) %>%
	add_bars()
  
  ```
  
  
  ```
  # Create a frequency for Genre
genre_table <- vgsales %>%
	count(Genre)

# Reorder the bars for Genre by n
genre_table %>%
	mutate(Genre = fct_reorder(Genre, n, .desc = TRUE)) %>%
	plot_ly(x = ~Genre, y = ~n) %>% 
	add_bars()                      
  
```
  
  A first scatterplot
Do video game players and critics rate games similarly? In this exercise, you will create a scatterplot in plotly to explore the relationship between the average player score (User_Score) and the average critic score (Critic_Score).

If you see anything unusual, be sure to utilize the interactive tools, such as hover info, to investigate.

Note that the data set, vgsales, and plotly have already been loaded for you.

Instructions
100 XP
Create a scatter plot with critic score (Critic_Score) on the x-axis and user score (User_Score) on the y-axis.


  ```
  # Create a scatter plot of User_Score against Critic_Score
vgsales %>% 
  plot_ly(x = ~Critic_Score, y = ~User_Score) %>% 
	add_markers()                      
  ```
  
  
  A first stacked bar chart
In this exercise, your task is to create a stacked bar chart to investigate whether there is an association between the Genre and Rating of video games.

Be sure to investigate what happens when you click on the color swatches in the legend.

Note that plotly has already been loaded for you.

Instructions
100 XP
Create a stacked bar chart of counts with Genre on the x-axis and Rating used to color in the bars.


```
# Filter out the 2016 video games
vg2016 <- vgsales %>%
	filter(Year == 2016)

# Create a stacked bar chart of Rating by Genre
vg2016 %>%
	count(Genre, Rating) %>%
	plot_ly(x = ~Genre , y = ~n, color = ~Rating) %>%
  	add_bars() %>%
  	layout(barmode = "stack")
 ```
 
 Boxplots
In this exercise, your task is to create a boxplot of global video game sales (the number of units sold) for each genre. Does genre appear to be related to sales?

Be sure to explore what hover information is given by default.

Note that plotly has already been loaded for you.

Instructions
100 XP
Create side-by-side boxplots with Global_Sales on the x-axis and Genre on the y-axis.


```
# Filter out the 2016 video games
vg2016 <- vgsales %>%
	filter(Year == 2016)

# Create boxplots of Global_Sales by Genre for above data
vg2016 %>% 
    plot_ly(x = ~Global_Sales , y = ~Genre) %>%
    add_boxplot()
  ```
  
  

