
# Créer les données du tableau
data_seuils <- data.frame(
  Axes = c("Representativeness", "Stability", "Performance", "Complementary tests", "Complementary tests"),
  KRI = c("Stability Index (IS)", "Stability Index (IS)", "HHI", "Spearman Correlation", "Vcramer Correlation"),
  Critical = c(">0,25", ">0,25", ">0,7", ">0,5", ">0,5"),
  Average = c(">0,1 and <0,25", ">0,1 and <0,25", ">0,5 and <0,7", ">0,3 and <0,5", ">0,2 and <0,5"),
  Good = c("<0,1", "<0,1", "<0,5", "<0,3", "<0,2")
)

# Créer le tableau stylisé avec flextable
ft <- flextable(data_seuils)

# Appliquer les styles de base
ft <- theme_vanilla(ft)
ft <- set_table_properties(ft, width = 1, layout = "autofit")

# Style de l'entête
ft <- bg(ft, bg = "#002D4F", part = "header")
ft <- color(ft, color = "white", part = "header")
ft <- fontsize(ft, size = 10, part = "header")

# Style des cellules
ft <- bg(ft, j = "Critical", bg = ifelse(data_seuils$Critical == ">0,25", "#FF0000", "transparent"))
ft <- bg(ft, j = "Average", bg = ifelse(data_seuils$Average == ">0,1 and <0,25", "#FFA500", "transparent"))
ft <- bg(ft, j = "Good", bg = ifelse(data_seuils$Good == "<0,1", "#228B22", "transparent"))

# Appliquer les couleurs de texte
ft <- color(ft, j = "Critical", color = ifelse(data_seuils$Critical == ">0,25", "white", "black"))
ft <- color(ft, j = "Average", color = ifelse(data_seuils$Average == ">0,1 and <0,25", "white", "black"))
ft <- color(ft, j = "Good", color = ifelse(data_seuils$Good == "<0,1", "white", "black"))

# Ajuster la taille de la police pour les cellules
ft <- fontsize(ft, size = 10, part = "body")

# Ajuster l'espacement des colonnes
ft <- width(ft, j = 1, width = 1.5)
ft <- width(ft, j = 2, width = 1.5)
ft <- width(ft, j = 3, width = 1.0)
ft <- width(ft, j = 4, width = 1.5)
ft <- width(ft, j = 5, width = 1.0)

# Afficher le tableau
ft
