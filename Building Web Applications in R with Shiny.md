### First peek under the hood
On the right you can see the complete code to reproduce the app we demoed in the previous video. Don't be intimidated by how much code there is! Soon you'll be able to make this app yourself. Now you get to interact with the app on your own, and make small adjustments to it.

Instructions
100 XP
Instructions
100 XP
Hit Run Code to run the code and generate the app.
Play with the input selectors and observe how the output changes.
Change the selected argument in the selectInput() call for the y input to imdb_rating and for the x input to imdb_num_votes and rerun the app by submitting your answer.


```
library(shiny)
library(ggplot2)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_4850/datasets/movies.Rdata"))

# Define UI for application that plots features of movies 
ui <- fluidPage(
  
  # Sidebar layout with a input and output definitions 
  sidebarLayout(
    
    # Inputs
    sidebarPanel(
      
      # Select variable for y-axis
      selectInput(inputId = "y", 
                  label = "Y-axis:",
                  choices = c("imdb_rating", "imdb_num_votes", "critics_score", "audience_score", "runtime"), 
                  selected = "imdb_rating"),
      # Select variable for x-axis
      selectInput(inputId = "x", 
                  label = "X-axis:",
                  choices = c("imdb_rating", "imdb_num_votes", "critics_score", "audience_score", "runtime"), 
                  selected = "imdb_num_votes")
    ),
    
    # Outputs
    mainPanel(
      plotOutput(outputId = "scatterplot")
    )
  )
)

# Define server function required to create the scatterplot
server <- function(input, output) {

  # Create scatterplot object the plotOutput function is expecting
  output$scatterplot <- renderPlot({
    ggplot(data = movies, aes_string(x = input$x, y = input$y)) +
      geom_point()
  })
}

# Create a Shiny app object
shinyApp(ui = ui, server = server)

```



### Extend the UI
We'll start our learning with a simplified version of the app you saw in the previous exercise. In this app a selectInput widget is used to allow the user to select which variables should be plotted on the x and y axes of the scatterplot.

The selectInput function has four arguments: an inputId that is used to refer to the input parameter when building the scatterplot, a label that is displayed in the app, a list of choices to pick from, and a selected choice for when the app first launches. Note that choices takes a named vector, and the name rather than the value (which must match variable names in the data frame) is displayed to the user.

Instructions
100 XP
Instructions
100 XP
Add a new selectInput widget at line 27 to color the points by a choice of the following variables: "title_type", "genre", "mpaa_rating", "critics_rating", "audience_rating". Set the inputId = "z" and the label = "Color by:".
Make the default selection "mpaa_rating".


```
library(shiny)
library(ggplot2)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_4850/datasets/movies.Rdata"))

# Define UI for application that plots features of movies
ui <- fluidPage(
  
  # Sidebar layout with a input and output definitions
  sidebarLayout(
    
    # Inputs
    sidebarPanel(
      
      # Select variable for y-axis
      selectInput(inputId = "y", 
                  label = "Y-axis:",
                  choices = c("imdb_rating", "imdb_num_votes", "critics_score", "audience_score", "runtime"), 
                  selected = "audience_score"),
      
      # Select variable for x-axis
      selectInput(inputId = "x", 
                  label = "X-axis:",
                  choices = c("imdb_rating", "imdb_num_votes", "critics_score", "audience_score", "runtime"), 
                  selected = "critics_score"),
      
      # Select variable for color
      selectInput(inputId = "z", 
                  label = "Color by:",
                  choices = c("title_type", "genre", "mpaa_rating", "critics_rating", "audience_rating"),
                  selected = "mpaa_rating")
    ),
    
    # Outputs
    mainPanel(
      plotOutput(outputId = "scatterplot")
    )
  )
)

# Define server function required to create the scatterplot
server <- function(input, output) {
  
  # Create the scatterplot object the plotOutput function is expecting
  output$scatterplot <- renderPlot({
    ggplot(data = movies, aes_string(x = input$x, y = input$y,
                                     color = input$z)) +
      geom_point()
  })
}

# Create a Shiny app object
shinyApp(ui = ui, server = server)

```


### xtend the UI further
The potential variables the user can select for the x and y axes and color currently appear in the UI of the app the same way that they are spelled in the data frame header. However we might want to label them in a way that is more human readable. We can achieve this using named vectors for the choices argument, in the format of "Human readable label" = "variable_name". As you're going through this exercise, watch out for typos!

Instructions
100 XP
Instructions
100 XP
Fill in the blanks starting at line 17 with human readable labels for x and y inputs.
Use the labels "IMDB rating", "IMDB number of votes", "Critics score", "Audience score", and "Runtime".
Re-create the selectInput widget for color, z, with options "title_type", "genre", "mpaa_rating", "critics_rating", and "audience_rating". Use the same input ID "z" and the label "Color by:"
Use the human readable labels "Title type", "Genre", "MPAA rating", "Critics rating", and "Audience rating".
Make the default selection "mpaa_rating" just like in the previous exercise.


```
library(shiny)
library(ggplot2)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_4850/datasets/movies.Rdata"))

# Define UI for application that plots features of movies
ui <- fluidPage(
  
  # Sidebar layout with a input and output definitions
  sidebarLayout(
    
    # Inputs
    sidebarPanel(
      
      # Select variable for y-axis
      selectInput(inputId = "y", 
                  label = "Y-axis:",
                  choices = c("IMDB rating" = "imdb_rating", 
                    "IMDB number of votes" = "imdb_num_votes",
                  "Critics score" = "critics_score", 
                       "Audience score" = "audience_score", 
                         "Runtime" = "runtime"), 
                  selected = "audience_score"),
      
      # Select variable for x-axis
      selectInput(inputId = "x", 
                  label = "X-axis:",
                  choices = c("IMDB rating" = "imdb_rating", 
                    "IMDB number of votes" = "imdb_num_votes",
                  "Critics score" = "critics_score", 
                       "Audience score" = "audience_score", 
                         "Runtime" = "runtime"),  
                  selected = "critics_score"),
      
      # Select variable for color
      selectInput(inputId = "z",
     label = "Color by:",
                  choices = c("Title type" = "title_type", "Genre" = "genre","MPAA rating" = "mpaa_rating", "Critics rating" = "critics_rating","Audience rating" = "audience_rating"),
                  selected = "mpaa_rating")
    ),
    
    # Output
    mainPanel(
      plotOutput(outputId = "scatterplot")
    )
  )
)

# Define server function required to create the scatterplot
server <- function(input, output) {
  
  # Create the scatterplot object the plotOutput function is expecting
  output$scatterplot <- renderPlot({
    ggplot(data = movies, aes_string(x = input$x, y = input$y,
                                     color = input$z)) +
      geom_point()
  })
}

# Create a Shiny app object
shinyApp(ui = ui, server = server)
```



### Fix it up
On the right is the code for the Shiny app we built earlier, however currently the code is broken. Specifically there are errors in the definition of the server function as well as in the mainPanel of the UI.

Instructions
100 XP
Review the app and identify errors in the code.
Fix the errors and test out the app.


```
library(shiny)
library(ggplot2)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_4850/datasets/movies.Rdata"))

# Define UI for application that plots features of movies
ui <- fluidPage(
  
  # Sidebar layout with a input and output definitions
  sidebarLayout(
    
    # Inputs
    sidebarPanel(
      
      # Select variable for y-axis
      selectInput(inputId = "y", 
                  label = "Y-axis:",
                  choices = c("IMDB rating"          = "imdb_rating", 
                              "IMDB number of votes" = "imdb_num_votes", 
                              "Critics score"        = "critics_score", 
                              "Audience score"       = "audience_score", 
                              "Runtime"              = "runtime"), 
                  selected = "audience_score"),
      
      # Select variable for x-axis
      selectInput(inputId = "x", 
                  label = "X-axis:",
                  choices = c("IMDB rating"          = "imdb_rating", 
                              "IMDB number of votes" = "imdb_num_votes", 
                              "Critics score"        = "critics_score", 
                              "Audience score"       = "audience_score", 
                              "Runtime"              = "runtime"), 
                  selected = "critics_score"),
      
      # Select variable for color
      selectInput(inputId = "z", 
                  label = "Color by:",
                  choices = c("Title type" = "title_type", 
                              "Genre" = "genre", 
                              "MPAA rating" = "mpaa_rating", 
                              "Critics rating" = "critics_rating", 
                              "Audience rating" = "audience_rating"),
                  selected = "mpaa_rating")
    ),
    
    # Outputs
    mainPanel(
      plotOutput(outputId = "scatterplot")
    )
  )
)

# Define server function required to create the scatterplot
server <- function(input, output) {
  
  # Create the scatterplot object the plotOutput function is expecting
  output$scatterplot <- renderPlot({
    ggplot(data = movies, aes_string(x = input$x, y = input$y,
                                     color = input$z)) +
      geom_point()
  })
}

# Create a Shiny app object
shinyApp(ui = ui, server = server)


```
