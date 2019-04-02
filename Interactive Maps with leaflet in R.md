## Interactive Maps with leaflet in R

### Creating an Interactive Web Map

Similar to the packages in the tidyverse, the leaflet package makes use of the pipe operator (i.e., %>%) from the magrittr package to chain function calls together. This means we can pipe the result of one function into another without having to store the intermediate output in an object. For example, one way to find every car in the mtcars data set with a mpg >= 25 is to pipe the data through a series of functions.

mtcars  %>% 
    mutate(car = rownames(.))  %>% 
    select(car, mpg)  %>% 
    filter(mpg >= 25)  
To create a web map in R, you will chain together a series of function calls using the %>% operator. Our first function leaflet() will initialize the htmlwidget then we will add a map tile using the addTiles() function.

Instructions
100 XP
Load the leaflet library.
Call the leaflet() function.
Pipe the output of leaflet() into addTiles().
Experiment with zooming and panning your first interactive web map.

```
# Load the leaflet library
library(leaflet)

# Create a leaflet map with default map tile using addTiles()
leaflet() %>%
    addTiles()

```



### Provider Tiles
In the previous exercise, addTiles() added the default OpenStreetMap (OSM) tile to your leaflet map. Map tiles weave multiple map images together. The map tiles presented adjust when a user zooms or pans the map enabling the interactive features you experimented with in exercise 2.

The leaflet package comes with more than 100 map tiles that you can use. These tiles are stored in a list called providers and can be added to your map using addProviderTiles() instead of addTiles().

The leaflet and tidyverse libraries have been loaded for you.

Instructions
100 XP
Instructions
100 XP
Print the list of 100+ provider tiles that are included in the leaflet package.
To make this output more readable, print just the names of the provider tiles using the names() function.
Use the str_detect() function from the stringr package to determine which provider tiles include the string "CartoDB".
Print the name of every provider map tile that includes the string "CartoDB".

```
# Print the providers list included in the leaflet library
providers

# Print only the names of the map tiles in the providers list 
names(providers)

# Use str_detect() to determine if the name of each provider tile contains the string "CartoDB"
str_detect(names(providers), "CartoDB")

# Use str_detect() to print only the provider tile names that include the string "CartoDB"
print(names(providers))[str_detect(names(providers), "CartoDB")]
```


### Adding a Custom Map Tile
Did any tile names look familiar? If you have worked with the mapping software you may recognize the name ESRI or CartoDB.

We create our first leaflet map using the default OSM map tile.

leaflet() %>% 
    addTiles()
We will primarily use CartoDB provider tiles, but feel free to try others, like Esri. To add a custom provider tile to our map we will use the addProviderTiles() function. The first argument to addProviderTiles() is your leaflet map, which allows us to pipe leaflet() output directly into addProviderTiles(). The second argument is provider, which accepts any of the map tiles included in the providers list.

Familiarize yourself with the SCRIPT.R and HTML VIEWER tabs. Click back and forth to type your code and view your maps.


Change addTiles() to addProviderTiles() and set the provider argument to "CartoDB".


```
# Change addTiles() to addProviderTiles() and set the provider argument to "CartoDB"
leaflet() %>% 
    addProviderTiles(provider = "CartoDB")
    
    
# Create a leaflet map that uses the CartoDB.PositronNoLabels provider tile
leaflet() %>% 
    addProviderTiles("CartoDB.PositronNoLabels" )

```


A Map with a View I
You may have noticed that, by default, maps are zoomed out to the farthest level. Rather than manually zooming and panning, we can load the map centered on a particular point using the setView() function.

leaflet()  %>% 
    addProviderTiles("CartoDB")  %>% 
    setView(lat = 40.7, lng = -74.0, zoom = 10)
Currently, DataCamp has offices at the following locations:

350 5th Ave, Floor 77, New York, NY 10118

Martelarenlaan 38, 3010 Kessel-Lo, Belgium

These addresses were converted to coordinates using the geocode() function in the ggmaps package.

NYC: (-73.98575, 40.74856)
Belgium: (4.717863, 50.881363)

Use the coordinates above to create a map with the "CartoDB" provider tile that is centered on DataCamp's New York office with a zoom of 6.


```
# Map with CartoDB tile centered on DataCamp's NYC office with zoom of 6
leaflet()  %>% 
    addProviderTiles("CartoDB")  %>% 
    setView(lng = -73.98575, lat = 40.74856, zoom = 6)
    
# Map with CartoDB.PositronNoLabels tile centered on DataCamp's Belgium office with zoom of 4
leaflet() %>% 
    addProviderTiles("CartoDB.PositronNoLabels" ) %>% 
    setView(lng = dc_hq$lon[2], lat = dc_hq$lat[2], zoom = 4)    
```    

### A Map with a Narrower View
We can limit users' ability to pan away from the map's focus using the options argument in the leaflet() function. By setting minZoom anddragging, we can create an interactive web map that will always be focused on a specific area.

leaflet(options = 
        leafletOptions(minZoom = 14, dragging = FALSE))  %>% 
  addProviderTiles("CartoDB")  %>% 
  setView(lng = -73.98575, lat = 40.74856, zoom = 14) 
Alternatively, if we want our users to be able to drag the map while ensuring that they do not stray too far, we can set the maps maximum boundaries by specifying two diagonal corners of a rectangle.

You'll use dc_hq to create a map with the "CartoDB" provider tile that is centered on DataCamp's Belgium office.

Instructions
100 XP
Instructions
100 XP
Use a minimum zoom level of 12.
Set the dragging option to TRUE.
Use maximum bounds of .05 decimal degrees from the headquarters.


```

leaflet(options = leafletOptions(
                    # Set minZoom and dragging 
                    minZoom = 12, dragging = TRUE))  %>% 
  addProviderTiles("CartoDB")  %>% 
  
  # Set default zoom level 
  setView(lng = dc_hq$lon[2], lat = dc_hq$lat[2], zoom = 14) %>% 
  
  # Set max bounds of map 
  setMaxBounds(lng1 = dc_hq$lon[2] + 0.05, 
               lat1 = dc_hq$lat[2] + .05, 
               lng2 = dc_hq$lon[2] - 0.05, 
               lat2 = dc_hq$lat[2] - .05) 
```



### Mark it
So far we have been creating maps with a single layer: a base map. We can add layers to this base map similar to how you add layers to a plot in ggplot2. One of the most common layers to add to a leaflet map is location markers, which you can add by piping the result of addTiles() or addProviderTiles() into the add markers function.

For example, if we plot DataCamp's NYC HQ by passing the coordinates to addMarkers() as numeric vectors with one element, our web map will place a blue drop pin at the coordinate. In chapters 2 and 3, we will review some options for customizing these markers.

leaflet()  %>% 
    addProviderTiles("CartoDB")  %>% 
    addMarkers(lng = -73.98575, lat = 40.74856)
The dc_hq tibble is available in your work space.

Plot DataCamp's NYC HQ using addMarkers().

```
# Plot DataCamp's NYC HQ
leaflet() %>% 
    addProviderTiles("CartoDB") %>% 
    addMarkers(lng = dc_hq$lon[1], lat = dc_hq$lat[1])


# Plot DataCamp's NYC HQ with zoom of 12    
leaflet() %>% 
    addProviderTiles("CartoDB") %>% 
    addMarkers(lng = -73.98575, lat = 40.74856)  %>% 
    setView(lng = -73.98575, lat = 40.74856, zoom = 12)    
    
    
# Plot both DataCamp's NYC and Belgium locations
leaflet() %>% 
    addProviderTiles("CartoDB") %>% 
    addMarkers(lng = dc_hq$lon, lat = dc_hq$lat)
```

### Adding Popups and Storing your Map
To make our map more informative we can add popups. To add popups that appear when a marker is clicked we need to specify the popup argument in the addMarkers() function. Once we have a map we would like to preserve, we can store it in an object. Then we can pipe this object into functions to add or edit the map's layers.

dc_nyc <- 
    leaflet() %>% 
        addTiles() %>% 
        addMarkers(lng = -73.98575, lat = 40.74856, 
                   popup = "DataCamp - NYC") 

dc_nyc %>% 
    setView(lng = -73.98575, lat = 40.74856, 
            zoom = 2)
Let's try adding popups to both DataCamp location markers and storing our map in an object.


Add the popup argument to addMarkers() to display the value in the hq column and store the leaflet map in an object called map.
Center the view of map on the Belgium HQ with a zoom of 5 and store it in map_zoom.
Print the map_zoom object.

```
# Store leaflet hq map in an object called map
map <- leaflet() %>%
          addProviderTiles("CartoDB") %>%
          # Use dc_hq to add the hq column as popups
          addMarkers(lng = dc_hq$lon, lat = dc_hq$lat,
                     popup = dc_hq$hq)

# Center the view of map on the Belgium HQ with a zoom of 5 
map_zoom <- map  %>%
      setView(lat = 50.881363, lng = 4.717863,
              zoom = 5)

# Print map_zoom
print(map_zoom)
```


### Cleaning up the Base Map
If you are storing leaflet maps in objects, there will come a time when you need to remove markers or reset the view. You can accomplish these tasks with the following functions.

clearMarkers()- Remove one or more features from a map
clearBounds()- Clear bounds and automatically determine bounds based on map elements
To remove the markers and to reset the bounds of our m map we would:

m <- m  %>% 
        addMarkers(lng = dc_hq$lon, lat = dc_hq$lat) %>% 
        setView(lat = 50.9, lng = 4.7, zoom = 5)

m  %>% 
    clearMarkers() %>% 
    clearBounds()
The leaflet map of DataCamp's headquarters has been printed for you.


Use clearMarkers() to remove markers and clearBounds() to restore the default view and store in the map_clear object.


```
# Remove markers, reset bounds, and store the updated map in the m object
map_clear <- map %>%
        clearMarkers() %>% 
        clearBounds()

# Print the cleared map
print(map_clear)

```

