library(shiny)
library(semantic.dashboard)
library(shiny.semantic)
library(leaflet)

ui <- dashboardPage(
  dashboardHeader(
    color = "blue", inverted = TRUE, center = ("LOKASI KAMPUS TERDEKAT DARI ESA UNGGUL KJ")
    
  ),
  dashboardSidebar(
    size = "wide",
    sidebarMenu(
      menuItem(tabName = "map", text = "Map", icon = icon("map")),
      menuItem(tabName = "table", text = "Table", icon = icon("table"))
    )
  ),
  dashboardBody(
    tabItems(
      selected = 1,
      tabItem(
        tabName = "map",
        leafletOutput("map")
      ),
      tabItem(
        tabName = "table",
        fluidRow(
          h1("Tes Table"),
          semantic_DTOutput("tesTable")
        )
      )
    )
  )
)
server <- function(input, output) {
  output$map <- renderLeaflet({leaflet() %>%
      setView(lng = 106.778922, lat = -6.185679, zoom = 10.5) %>%
      addProviderTiles("Esri.NatGeoWorldMap") %>%
      addCircles(
        data = df,
        radius = 500,
        color = "#000000",
        fillColor = "#ffffff",
        fillOpacity = 0.5,
        popup = paste0(
          "Id Kampus  : ", df$idkampus," ",
          "Nama Kampus  : ", df$nama," ",
          "Kapasitas (%) : ", df$kapasitas," ",
          "Jarak (km) : ", df$jarak, " "
        )
      )
  })
  output$tesTable <- DT::renderDataTable(
    semantic_DT(df)
  )
}

shinyApp(ui, server)