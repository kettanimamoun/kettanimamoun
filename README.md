# Exemple de données
set.seed(123)
tab <- c(rnorm(10000, mean = 0.001, sd = 0.0005), rnorm(500, mean = 0.01, sd = 0.005))  # Remplacez par vos données réelles

# Définir les breaks personnalisés
breaks <- c(seq(0, 0.0015, by = 0.0001), seq(0.002, 0.01, by = 0.001), seq(0.02, 1, by = 0.1))

# Créer l'histogramme avec les breaks personnalisés
hist(tab, breaks = breaks, col = "gray", border = "white", prob = TRUE,
     xlab = "Default Rate", ylab = "Density", main = "Default Rate Distribution",
     xlim = c(0, 1))

# Calculer la densité empirique
empirical_density <- density(tab)

# Ajouter la courbe de densité empirique (rouge)
lines(empirical_density, col = "red", lwd = 2)

# Calculer la densité normale
x_values <- seq(min(tab), max(tab), length.out = 100)
normal_density <- dnorm(x_values, mean = mean(tab), sd = sd(tab))

# Ajouter la courbe de densité normale (verte)
lines(x_values, normal_density, col = "green", lwd = 2)

# Ajouter une légende
legend("topright", legend = c("Empirical Density", "Normal Density"), col = c("red", "green"), lwd = 2)
