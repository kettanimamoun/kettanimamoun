library(rAmCharts)

# Exemple de données
set.seed(123)
tab <- rnorm(1000)  # Remplacez par vos données réelles

# Créer l'histogramme avec amHist
histogram <- amHist(x = tab, control_hist = list(breaks = c(0, 0.001, 0.0015, 0.002, 0.005, 0.01, 0.05, 1)),
                    col = "red", border = "red", theme = "patterns",
                    xlab = "Default Rate", ylab = "Density", main = "Default Rate Distribution")

# Calculer la densité empirique
empirical_density <- density(tab)

# Ajouter la courbe de densité empirique (rouge)
histogram <- amLines(histogram, y = empirical_density$y, col = "red", lwd = 2, lty = "solid")

# Calculer la densité normale
x_values <- seq(min(tab), max(tab), length.out = 100)
normal_density <- dnorm(x_values, mean = mean(tab), sd = sd(tab))

# Ajouter la courbe de densité normale (verte)
histogram <- amLines(histogram, y = normal_density, col = "green", lwd = 2, lty = "solid")

# Ajouter une légende
legend_labels <- list(
  list(text = "Empirical Density", lineColor = "red"),
  list(text = "Normal Density", lineColor = "green")
)
histogram <- addLegend(histogram, legend_labels)

# Afficher le graphique
print(histogram)


