install.packages("R.utils")
install.packages("pryr")
library(R.utils)
library(pryr)

# Fonction pour vérifier la disponibilité des ressources
check_resources <- function(threshold_memory = 0.7, threshold_cpu = 0.7) {
  # Vérifier l'utilisation de la mémoire
  mem_used <- mem_used()
  mem_total <- mem_total()
  mem_available <- (mem_total - mem_used) / mem_total
  
  # Vérifier l'utilisation du CPU
  cpu_load <- system("top -bn1 | grep 'Cpu(s)' | sed 's/.*, *\\([0-9.]*\\)%* id.*/\\1/' | awk '{print 100 - $1}'", intern = TRUE)
  cpu_available <- as.numeric(cpu_load) / 100
  
  return(mem_available > threshold_memory && cpu_available < threshold_cpu)
}
  # Attendre que les ressources soient disponibles
  while (!check_resources()) {
    Sys.sleep(5)  # Vérifier toutes les 5 secondes
  }
