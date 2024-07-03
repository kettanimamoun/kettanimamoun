# Fonction pour le test de Wilcoxon avec conclusion et intervalle de confiance
wilcoxon_test_manual <- function(group1, group2, alpha = 0.05) {
  # Vérifier que les entrées sont des vecteurs numériques
  if (!is.numeric(group1) | !is.numeric(group2)) {
    stop("Les entrées doivent être des vecteurs numériques")
  }
  
  # Combiner les groupes
  combined <- c(group1, group2)
  
  # Calculer les rangs
  ranks <- rank(combined)
  
  # Séparer les rangs en fonction des groupes
  ranks1 <- ranks[1:length(group1)]
  ranks2 <- ranks[(length(group1) + 1):length(ranks)]
  
  # Calculer les sommes des rangs
  W1 <- sum(ranks1)
  W2 <- sum(ranks2)
  
  # Calculer les tailles des échantillons
  n1 <- length(group1)
  n2 <- length(group2)
  
  # Calculer la statistique U de Mann-Whitney
  U1 <- W1 - n1 * (n1 + 1) / 2
  U2 <- W2 - n2 * (n2 + 1) / 2
  
  # Utiliser la plus petite des deux statistiques U
  U <- min(U1, U2)
  
  # Calculer la moyenne et la variance de U sous l'hypothèse nulle
  mean_U <- n1 * n2 / 2
  sd_U <- sqrt(n1 * n2 * (n1 + n2 + 1) / 12)
  
  # Calculer la statistique z
  z <- (U - mean_U) / sd_U
  
  # Calculer la p-valeur
  p_value <- 2 * pnorm(-abs(z))
  
  # Conclusion basée sur le seuil alpha
  conclusion <- ifelse(p_value < alpha, "Rejet de H0", "Non rejet de H0")
  
  # Calculer l'intervalle de confiance pour la différence des médianes
  combined_sorted <- sort(combined)
  rank_diff <- qnorm(1 - alpha / 2) * sqrt(n1 * n2 * (n1 + n2 + 1) / 12)
  ci_lower <- combined_sorted[ceiling((n1 * n2 / 2 - rank_diff))]
  ci_upper <- combined_sorted[floor((n1 * n2 / 2 + rank_diff))]
  
  # Résultats
  return(list(
    U = U,
    z = z,
    p_value = p_value,
    conclusion = conclusion,
    ci_lower = ci_lower,
    ci_upper = ci_upper
  ))
}

# Exemple concret avec des données dans un data frame
# Création d'un data frame exemple
set.seed(123)
data <- data.frame(
  group = rep(c("A", "B"), each = 30),
  values = c(rnorm(30, mean = 5, sd = 1), rnorm(30, mean = 6, sd = 1.5))
)

# Séparation des groupes
group_A <- data$values[data$group == "A"]
group_B <- data$values[data$group == "B"]

# Application de la fonction wilcoxon_test_manual avec alpha = 0.05
result <- wilcoxon_test_manual(group_A, group_B, alpha = 0.05)

# Affichage des résultats
print(result)
