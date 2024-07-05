# Installer et charger ggplot2 si ce n'est pas déjà fait
if (!requireNamespace("ggplot2", quietly = TRUE)) {
  install.packages("ggplot2")
}

library(ggplot2)

# Exemple de données pour tab_plot_1
tab_plot_1 <- data.frame(
  description = c("0-4 years", "5-9 years", "10-14 years", "15-19 years", "20-24 years"),
  value = c(500, 450, 400, 350, 300)
)

# Calculer le pourcentage
total <- sum(tab_plot_1$value)
tab_plot_1$percentage <- (tab_plot_1$value / total) * 100

# Arrondir les pourcentages pour une meilleure lisibilité
tab_plot_1$percentage <- round(tab_plot_1$percentage, 2)

# Créer le graphique en entonnoir
ggplot(tab_plot_1, aes(x = reorder(description, -value), y = value, fill = description)) +
  geom_bar(stat = "identity", width = 0.6) +
  coord_flip() +
  geom_text(aes(label = paste0(percentage, "%")), hjust = -0.1) +
  labs(title = "Population Pyramid Example", x = "Age Group", y = "Value") +
  theme_minimal() +
  theme(legend.position = "none")

  
