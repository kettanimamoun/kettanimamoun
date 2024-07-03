N <- length(combined)
  
  # Calculer les rangs critiques pour l'intervalle de confiance
  rank_diff <- qnorm(1 - alpha / 2) * sqrt(n1 * n2 * (n1 + n2 + 1) / 12)
  lower_rank <- ceiling((N + 1) / 2 - rank_diff)
  upper_rank <- floor((N + 1) / 2 + rank_diff)
  
  # S'assurer que les rangs sont dans les limites de l'ensemble combiné
  lower_rank <- max(1, lower_rank)
  upper_rank <- min(N, upper_rank)
  
  ci_lower <- combined_sorted[lower_rank]
  ci_upper <- combined_sorted[upper_rank]
  
