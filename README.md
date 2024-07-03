
# Créer l'histogramme
hist(tab, breaks = c(0, 0.001, 0.0015, 0.002, 0.005, 0.01, 0.05, 1), probability = TRUE,
     col = "gray", border = "white", xlab = "Default Rate", ylab = "Density",
     main = "Default Rate Distribution")

# Ajouter la courbe de densité empirique (rouge)
lines(density(tab), col = "red", lwd = 2)

# Ajouter la courbe de densité normale (verte)
curve(dnorm(x, mean = mean(tab), sd = sd(tab)), col = "green", lwd = 2, add = TRUE)

# Ajouter une légende
legend("topright", legend = c("Empirical Density", "Normal Density"),
       col = c("red", "green"), lwd = 2)
