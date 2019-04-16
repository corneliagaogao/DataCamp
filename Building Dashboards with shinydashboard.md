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










