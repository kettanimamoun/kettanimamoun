
# Créer le tableau stylisé avec flextable
ft <- flextable(data)

# Appliquer les styles
ft <- set_header_df(ft, mapping = data.frame(keys = colnames(data), labels = colnames(data)))
ft <- theme_vanilla(ft)

ft <- bg(ft, bg = "#002D4F", part = "header")
ft <- color(ft, color = "white", part = "header")

ft <- bg(ft, i = ~ Critical == ">0,25", j = 3, bg = "#FF0000")
ft <- bg(ft, i = ~ Critical == ">0,25", j = 4, bg = "#FFA500")
ft <- bg(ft, i = ~ Critical == ">0,25", j = 5, bg = "#228B22")

ft <- bg(ft, i = ~ Average == ">0,1 and <0,25", j = 4, bg = "#FFA500")
ft <- bg(ft, i = ~ Average == ">0,1 and <0,25", j = 5, bg = "#228B22")

ft <- bg(ft, i = ~ Good == "<0,1", j = 5, bg = "#228B22")

# Appliquer les couleurs de texte
ft <- color(ft, i = ~ Critical == ">0,25", j = 3, color = "white")
ft <- color(ft, i = ~ Average == ">0,1 and <0,25", j = 4, color = "white")
ft <- color(ft, i = ~ Good == "<0,1", j = 5, color = "white")

# Afficher le tableau
ft
