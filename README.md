

# Créer le tableau stylisé avec flextable
ft <- flextable(data_seuils)

# Appliquer les styles
ft <- theme_vanilla(ft)

# Style de l'entête
ft <- bg(ft, bg = "#002D4F", part = "header")
ft <- color(ft, color = "white", part = "header")

# Style des cellules
ft <- bg(ft, i = ~ Critical == ">0,25", j = "Critical", bg = "#FF0000")
ft <- bg(ft, i = ~ Critical == ">0,25", j = "Average", bg = "#FFA500")
ft <- bg(ft, i = ~ Critical == ">0,25", j = "Good", bg = "#228B22")

ft <- bg(ft, i = ~ Average == ">0,1 and <0,25", j = "Critical", bg = "#FFA500")
ft <- bg(ft, i = ~ Average == ">0,1 and <0,25", j = "Average", bg = "#FFA500")
ft <- bg(ft, i = ~ Average == ">0,1 and <0,25", j = "Good", bg = "#228B22")

ft <- bg(ft, i = ~ Good == "<0,1", j = "Good", bg = "#228B22")

# Appliquer les couleurs de texte
ft <- color(ft, i = ~ Critical == ">0,25", j = "Critical", color = "white")
ft <- color(ft, i = ~ Critical == ">0,25", j = "Average", color = "white")
ft <- color(ft, i = ~ Critical == ">0,25", j = "Good", color = "white")

ft <- color(ft, i = ~ Average == ">0,1 and <0,25", j = "Critical", color = "white")
ft <- color(ft, i = ~ Average == ">0,1 and <0,25", j = "Average", color = "white")
ft <- color(ft, i = ~ Average == ">0,1 and <0,25", j = "Good", color = "white")

ft <- color(ft, i = ~ Good == "<0,1", j = "Good", color = "white")

# Afficher le tableau
ft
