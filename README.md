# Installer et charger le package rAmCharts si ce n'est pas déjà fait
if (!requireNamespace("rAmCharts", quietly = TRUE)) {
  install.packages("rAmCharts")
}

library(rAmCharts)

# Exemple de données
data <- data.frame(
  description = c("0-4 years", "5-9 years", "10-14 years", "15-19 years", "20-24 years"),
  value = c(500, 450, 400, 350, 300)
)

# Calculer le pourcentage
total <- sum(data$value)
data$percentage <- (data$value / total) * 100

# Arrondir les pourcentages pour une meilleure lisibilité
data$percentage <- round(data$percentage, 2)

# Créer un nouveau champ combinant description et pourcentage
data$label <- paste0(data$description, ": ", data$percentage, "%")

# Créer le graphique en entonnoir
funnelChart <- amFunnel(
  dataProvider = data,
  title = "Population Pyramid Example",
  depth3D = 15,
  angle = 30
)

# Ajouter les descriptions et pourcentages aux labels
funnelChart <- funnelChart %>%
  setChartTitle(text = "Population Pyramid Example") %>%
  setDepth3D(15) %>%
  setAngle(30) %>%
  addGraph(
    balloonText = "[[description]]: [[value]] ([[percentage]]%)", 
    titleField = "description", 
    valueField = "value"
  )

# Personnaliser les couleurs et labels avec pourcentage
funnelChart <- funnelChart %>%
  setGraphColors(c("#FF0F00", "#FF6600", "#FF9E01", "#FCD202", "#F8FF01")) %>%
  setLabelRadius(10) %>%
  setLabelText("[[label]]")

# Afficher le graphique personnalisé
print(funnelChart)

  
