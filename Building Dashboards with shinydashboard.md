Create empty Header, Sidebar, and Body
Using the functions discussed, create an "empty" header, sidebar, and body.

```
library(shinydashboard)

# Create an empty header
header <- dashboardHeader()

# Create an empty sidebar
sidebar <- dashboardSidebar()

# Create an empty body
body <- dashboardBody()

```
Using the header, sidebar, and body created in the previous exercise, create an "empty" dashboard with a header, sidebar, and body.

```
header <- dashboardHeader()
sidebar <- dashboardSidebar()
body <- dashboardBody()

# Create the UI using the header, sidebar, and body
ui <- dashboardPage(header, sidebar, body)

server <- function(input, output) {}

shinyApp(ui, server)


```


Create message menus
Let's update your empty dashboard. You can add menus to your header using the dropdownMenu() function. One type of menu is the message menu, which can be created by adding type = "messages".

header <- dashboardHeader(
  dropdownMenu(type = "messages")
)
You are building a NASA themed app. So far, the application includes a message in the header drop down menu pointing viewers to where they can find out when the International Space Station can be seen overhead.

header <- dashboardHeader(
  dropdownMenu(
    type = "messages",
    messageItem(
        from = "Lucy",
        message = "You can view the International Space Station!",
        href = "https://spotthestation.nasa.gov/sightings/"
        )
    )
)
Add a second message using the messageItem() function to link viewers to the frequently asked questions: https://spotthestation.nasa.gov/faq.cfm

We've already defined an empty server function for you.

Instructions
100 XP
Instructions
100 XP
Add a second message to the dropdownMenu() using the messageItem() function.
Include the following message text "Learn more about the International Space Station" and link to the International Space Station FAQ: https://spotthestation.nasa.gov/faq.cfm.
Set the new header in the dashboardPage().
Rerun the shiny app with these updates.


```
header <- dashboardHeader(
  dropdownMenu(
    type = "messages",
    messageItem(
        from = "Lucy",
        message = "You can view the International Space Station!",
        href = "https://spotthestation.nasa.gov/sightings/"
        ),
    # Add a second messageItem() 
    messageItem(
        from = "Lucy",
        message = "Learn more about the International Space Station",
        href = "https://spotthestation.nasa.gov/faq.cfm"
        )
    )
)

ui <- dashboardPage(header = header,
                    sidebar = dashboardSidebar(),
                    body = dashboardBody()
                    )
shinyApp(ui, server)

```


Create notification menus
You can also create a notification drop down menu on your header. This allows you to notify your user of something. Add a notification that the International Space Station is overhead.

Instructions
100 XP
Create a drop down menu of type notifications and create a notification item.
Add text to your notification item letting the viewer know "The International Space Station is overhead!".
Set the new header in the dashboardPage().
Rerun the shiny app with these updates.


```

header <- dashboardHeader(
  # Create a notification drop down menu
  dropdownMenu(
    type = 'notifications',
    notificationItem(
    text = "The International Space Station is overhead!",
    )
  )
)

# Use the new header
ui <- dashboardPage(header = header,
                    sidebar = dashboardSidebar(),
                    body = dashboardBody()
                    )
shinyApp(ui, server)

```


Create task menus
A third type of drop down menu is the tasks menu. In addition to providing text, these items show progress on a task using the value parameter. For example, if you wanted to indicate that the task "Alert users to the International Space Station" was 80% complete, you would indicate it in a taskItem() in the following manner.

taskItem(
  text = "Alert users to the International Space Station",
  value = 80
    )
Add a tasks drop down menu to the header that indicates the task "Mission Learn Shiny Dashboard" is 10% complete.

We've already defined an empty server function for you.

Instructions
100 XP
Instructions
100 XP
Create a drop down menu of type tasks and create a task item.
Add text to your task item: "Mission Learn Shiny Dashboard" and indicate that the task item is 10% complete.
Set the new header in the dashboardPage().
Rerun the shiny app with these updates.


```

header <- dashboardHeader(
  # Create a tasks drop down menu
  dropdownMenu(
    type = "tasks",
    taskItem(value = 10, color = "aqua",
    "Mission Learn Shiny Dashboard"
  )
    )
    
)

# Use the new header
ui <- dashboardPage(header = header,
                    sidebar = dashboardSidebar(),
                    body = dashboardBody()
                    )
shinyApp(ui, server)

```

Create Sidebar tabs
You can create tabs for you dashboard. First, create tabs on the sidebar using the sidebarMenu() function. You will create two tabs, one for the "Dashboard" and one for the "Inputs".

Instructions
100 XP
Instructions
100 XP
Use the sidebarMenu() to create a tab with text = "Dashboard" and tabName = "dashboard".
Create tab with text = "Inputs" and tabName = "inputs".
Use the new sidebar in the dashboardPage().
Rerun the shiny app with these updates.

```
sidebar <- dashboardSidebar(
  sidebarMenu(
  # Create two `menuItem()`s, "Dashboard" and "Inputs"
    menuItem("Dashboard", tabName = "dashboard"),
    menuItem("Inputs", tabName = "inputs")
  )
)

# Use the new sidebar
ui <- dashboardPage(header = dashboardHeader(),
                    sidebar = sidebar,
                    body = dashboardBody()
                    )
shinyApp(ui, server)
```

Create Body tabs
Now that you have created tabs on the sidebar, link them to tabs in the body using the tabItems() function in the dashboardBody().

Instructions
100 XP
Create a tabItem() in the body named dashboard.
Create a tabItem() in the body named inputs.
Rerun the shiny app with these updates.

```
body <- dashboardBody(
  tabItems(
  # Add two tab items, one with tabName "dashboard" and one with tabName "inputs"
      tabItem(tabName = "dashboard"),

    tabItem(tabName = "inputs")
  )
)

# Use the new body
ui <- dashboardPage(header = dashboardHeader(),
                    sidebar = sidebar,
                    body = body
                    )
shinyApp(ui, server)

```

Create tab boxes
Now that you have created tabs on the sidebar, and tabs in the body, we can add boxes within each of the body's tabs (and there can be tabs within the boxes!) You can add a tabBox() directly to the dashboardBody() or place it within a tabItem(). Here is an example of a tabBox() directly in the dashboardBody(). The tabPanel() function is from the shiny package and will add tabs within the box.

body <-  dashboardBody(
    tabBox(
      title = "Tracking the International Space Station",
      tabPanel("Tab1", "Content for the first tab"),
      tabPanel("Tab2", "Content for the second tab")
    )
  )
Add a tabBox() to the dashboard body you have been working on in the previous exercises.

Instructions
100 XP
Instructions
100 XP
Add a tabBox() to the dashboard tabItem().
Add a title to the tabBox() "International Space Station Fun Facts".
Add two tabPanel()s to the tabBox() named "Fun Fact 1" and "Fun Fact 2".
Rerun the shiny app with these updates.


```
library("shiny")
body <- dashboardBody(
  # Create a tabBox
  tabItems(
    tabItem(
      tabName = "dashboard",
      tabBox(
      title = "International Space Station Fun Facts",
      # The id lets us use input$tabset1 on the server to find the current tab
      
      tabPanel("Fun Fact 1"),
      tabPanel("Fun Fact 2")
    )
    ),
    tabItem(tabName = "inputs")
  )
)

ui <- dashboardPage(header = dashboardHeader(),
                    sidebar = sidebar,
                    body = body
                    )
shinyApp(ui, server)
```

Review selectInput and sliderInput
As a quick refresher, using the dashboardSidebar() function along with selectInput() and sliderInput() from the shiny package, you can create select lists and sliders. For example, to create a select list in the sidebar, you can do the following:

sidebar <- dashboardSidebar(
  selectInput(inputId = "numbers",
              label = "Numbers",
              choices = 1:3)
  )
For this chapter, we are working with the dplyr starwars dataset, a data set pulled from the Star Wars API containing information about characters from Star Wars. We are interested in creating a subset of the data set of characters between specified height parameters. For this exercise, create a slider to indicate the maximum height you'd like in your subset.

Instructions
100 XP
Create a slider in the sidebar with the following parameters:
inputId: "height", label: "Height", min: 66, max: 264, value: 264.
Rerun the shiny app with these updates.

```
sidebar <- dashboardSidebar(
  # Add a slider
  sliderInput("height", "Height", 66, 264, 264)
)

ui <- dashboardPage(header = dashboardHeader(),
                    sidebar = sidebar,
                    body = dashboardBody()
                    )
shinyApp(ui, server) 
```

Reactive expression practice
Using the dplyr starwars dataset, create a shiny app that allows the user to select a character by name and output the selected name in the body. The data frame is already loaded as starwars.

Instructions
100 XP
Instructions
100 XP
Create a select list in the Sidebar where the choices are the characters' name with:
inputId: "name", label: "Name", choices: starwars$name.
Output the name selected in the body using the renderText() and textOutput() functions. Use the output ID "name".
Rerun the shiny app with these updates.

```
library(shiny)
sidebar <- dashboardSidebar(
  # Create a select list
  selectInput(inputId = "name", label ="Name",choices = starwars$name)
)

body <- dashboardBody(
  textOutput("name")
)

ui <- dashboardPage(header = dashboardHeader(),
                    sidebar = sidebar,
                    body = body
                    )

server <- function(input, output) {
  output$name <- renderText({
      input$name
    })
}

shinyApp(ui, server)
```


Read in real-time data
One benefit of a dashboard is the ability to examine real-time data. In shiny, this can be done using the reactiveFileReader() or reactivePoll() functions from the shiny package. For example, if we had our data saved as a .csv, we could read it in using reactiveFileReader() along with the readFunc set to read.csv.

filepath <- "data.csv"

server <- function(input, output, session) {
  reactive_data <- reactiveFileReader(
    intervalMillis = 1000,
    session = session, 
    filePath = filepath,
    readFunc = read.csv
  )
}
We have our data saved as a .csv located at a url called starwars_url; this object is already loaded for your convenience. In order to read this in, we can set our own readFunc like this:

readFunc = function(filePath) { 
  read.csv(url(filePath))
  }
If this .csv were updated live, we would see the changes! Read in this real-time data using reactiveFileReader().

Instructions
100 XP
Instructions
100 XP
Read in starwars_url using reactiveFileReader().
Set your intervalMillis to 1000.
Rerun the shiny app with these updates.

```
library("shiny")

server <- function(input, output, session) {
  reactive_starwars_data <- reactiveFileReader(
         1000,
         session = session, 
    filePath =starwars_url,
        
         readFunc = function(filePath) { 
           read.csv(url(filePath))
         }
  )
}

ui <- dashboardPage(header = dashboardHeader(),
                    sidebar = dashboardSidebar(),
                    body = dashboardBody()
                    )
shinyApp(ui, server)

```

View real-time data
Now that you've read in the real-time data as reactive_starwars_data(), you can examine it as it updates using renderTable(). If you save this reactive table, you can then render it using the tableOutput() function. For example, if we had a reactive data frame called my_reactive_data() we could save this as output$my_table and render it using tableOutput() with the following code:

server <- function(input, output, session) {
  output$my_table <- renderTable({
    my_reactive_data()
  })
}

body <- dashboardBody(
  tableOutput("my_table")
)
Instructions
100 XP
Using the reactive dataset you just read in, create a reactive table called output$table.
Render this table in the body.
Rerun the shiny app with these updates.

```
library(shiny)

server <- function(input, output, session) {
  reactive_starwars_data <- reactiveFileReader(
        intervalMillis = 1000,
        session = session,
        filePath = starwars_url,
        readFunc = function(filePath) { 
           read.csv(url(filePath))
         }
         )
   
  output$table <- renderTable({
    reactive_starwars_data()
})
}

body <- dashboardBody(
  tableOutput("table")
)

ui <- dashboardPage(header = dashboardHeader(),
                    sidebar = dashboardSidebar(),
                    body = body
                    )
shinyApp(ui, server)
```


Optimize this
You have a file that is static that you want your users to have access to. Optimize the code below for this circumstance. The name of the file path for the file you'd like to read in is saved and loaded in the object starwars_filepath.

Instructions
100 XP
Examine the code below -- think about how many times the data will be read in.
Update the sample code to be more efficient.

```
starwars <- read.csv(starwars_filepath)
server <- function(input, output) { 
}
```

Create reactive menu items
We have added dynamic content via subsetting a data frame based on using input and reading in real-time data. Now we are going to allow the user to input task_data to determine task items. Recall that we can use an apply() function to iterate over a data frame, applying the taskItem() function to each row.

tasks <- apply(task_data, 1, function(row) { 
  taskItem(text = row[["text"]],
           value = row[["value"]])
})
dropdownMenu(type = "tasks", .list = tasks)
You have a data frame (already loaded) called task_data with columns text and value. Use this to create a task drop down menu.

Instructions
0 XP
Create a list of tasks called tasks from the task_data data frame, like in the code chunk provided.
Create the task drop down menu from your tasks list.
Output a reactive task menu to output$task_menu and render the newly created reactive task menu in the dashboardHeader().
Rerun the shiny app with these updates.



```
server <- function(input, output) {
  output$task_menu <- renderMenu({
      tasks <- apply(task_data, 1, function(row) {
        taskItem(text = row[["text"]],
                 value = row[["value"]])
                 })
    
      dropdownMenu(type = "tasks", .list = tasks)
  })
}

header <- dashboardHeader(dropdownMenuOutput("task_menu"))

ui <- dashboardPage(header = header,
                    sidebar = dashboardSidebar(),
                    body = dashboardBody()
                    )
shinyApp(ui, server)

```


Create reactive boxes
In addition to updating the task drop down menus reactively, it is possible to create reactive boxes in the body. Here, you have a clickable action button in your sidebar. You want to update a value box each time the user clicks the action button. The valueBox() function will create a value box in the body. This takes the following form:

valueBox(value = 10,
        subtitle = "There are ten things here!"
        )
Instructions
70 XP
Create a reactive value box called click_box that increases in value each time the user clicks the action button.
Set the subtitle of the reactive value box to "Click Box".
Render the reactive value box in the body.
Rerun the shiny app with these updates.

```
library("shiny")
sidebar <- dashboardSidebar(
  actionButton("click", "Update click box")
) 

server <- function(input, output) {
  output$click_box <- renderValueBox({
    valueBox(
      value = input$click,
      subtitle = "Click Box"
    )
  })
}

body <- dashboardBody(
      valueBoxOutput("click_box")
 )


ui <- dashboardPage(header = dashboardHeader(),
                    sidebar = sidebar,
                    body = body
                    )
shinyApp(ui, server)

```












